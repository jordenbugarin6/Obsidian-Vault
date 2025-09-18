---
created_date: 25 September 2023
updated_date: 26 September 2023
type: windows/linux
PC NAME: Warcraft-DC
---
`existing users`
```
Administrator | Password1
Sylvanas Windrunner (swindrunner) | Password1
Anduin Wrynn (awrynn) | Password1
SQL Service (SQLService) | MYpassword123#
```

-----------------

`2023-09-25
```
- IE Enhanced Security Configuration turned off
- 7zip Downloaded
- Microsoft Defender Turned off
- Downloaded regshot
- Procmon Downloaded
	- https://live.sysinternals.com/
- Visual Studio 2019
```

-----------------

`2023-09-26
```
- Putty
- Python 3.11.5
	- path: C:\Users\Administrator\AppData\Local\Programs\Python\Python311
- SharpView.exe
	- https://github.com/tevora-threat/SharpView
```

--------------

`2023-09-27
```
- SharpDPAPI
	- https://github.com/GhostPack/SharpDPAPI
```

-----------

`2023-09-29
`Creating SPN for SQL Service
```shell
C:\Users\Administrator>setspn -a WARCRAFT-DC/SQLService.BLIZZARD.local:60111 BLIZZARD\SQLSERVICE
Checking domain DC=BLIZZARD,DC=local

Registering ServicePrincipalNames for CN=SQL Service,CN=Users,DC=BLIZZARD,DC=local
        WARCRAFT-DC/SQLService.BLIZZARD.local:60111
Updated object
```
`Checking to make sure SPN was actually created`
```shell
# this allows kerberoast to occur in our environment
C:\Users\Administrator>setspn -T BLIZZARD.local -Q */*
Checking domain DC=BLIZZARD,DC=local
CN=WARCRAFT-DC,OU=Domain Controllers,DC=BLIZZARD,DC=local
        Dfsr-12F9A27C-BF97-4787-9364-D31B6C55EB04/Warcraft-DC.BLIZZARD.local
        ldap/Warcraft-DC.BLIZZARD.local/ForestDnsZones.BLIZZARD.local
        ldap/Warcraft-DC.BLIZZARD.local/DomainDnsZones.BLIZZARD.local
        DNS/Warcraft-DC.BLIZZARD.local
        GC/Warcraft-DC.BLIZZARD.local/BLIZZARD.local
        RestrictedKrbHost/Warcraft-DC.BLIZZARD.local
        RestrictedKrbHost/WARCRAFT-DC
        RPC/065d332d-b3b3-4e16-8066-cd141feba337._msdcs.BLIZZARD.local
        HOST/WARCRAFT-DC/BLIZZARD
        HOST/Warcraft-DC.BLIZZARD.local/BLIZZARD
        HOST/WARCRAFT-DC
        HOST/Warcraft-DC.BLIZZARD.local
        HOST/Warcraft-DC.BLIZZARD.local/BLIZZARD.local
        E3514235-4B06-11D1-AB04-00C04FC2DCD2/065d332d-b3b3-4e16-8066-cd141feba337/BLIZZARD.local
        ldap/WARCRAFT-DC/BLIZZARD
        ldap/065d332d-b3b3-4e16-8066-cd141feba337._msdcs.BLIZZARD.local
        ldap/Warcraft-DC.BLIZZARD.local/BLIZZARD
        ldap/WARCRAFT-DC
        ldap/Warcraft-DC.BLIZZARD.local
        ldap/Warcraft-DC.BLIZZARD.local/BLIZZARD.local
CN=krbtgt,CN=Users,DC=BLIZZARD,DC=local
        kadmin/changepw
CN=SQL Service,CN=Users,DC=BLIZZARD,DC=local
        WARCRAFT-DC/SQLService.BLIZZARD.local:60111

Existing SPN found!
```

```
# created directory and enabling 139/445 smb
C:\hackme
```

----------
`2023-10-02`
```powershell
- Disabled SMB Signing to allow for SMB Relaying Attacks.
	- http://mctexpert.blogspot.com/2011/02/disable-smb-signing.html   #dont think this actually worked
- PS C:\Users\Administrator> Set-SmbServerConfiguration -EnableSMB2Protocol $false 
	- This command actually did disable SMB2 signing
```
-----------

`2023-10-15`
```
- enabled rdp
	- **Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -value 0**
- enabled smb
	- Enable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol
```



