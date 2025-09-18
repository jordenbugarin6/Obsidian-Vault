`whoami /groups`
- shows user groyps
```bash
[10/23 13:27:21] beacon> shell whoami /groups
[10/23 13:27:21] [*] Tasked beacon to run: whoami /groups
[10/23 13:27:22] [+] host called home, sent: 45 bytes
[10/23 13:27:23] [+] received output:


GROUP INFORMATION

-----------------



Group Name                                 Type             SID          Attributes                                        

========================================== ================ ============ ==================================================

Everyone                                   Well-known group S-1-1-0      Mandatory group, Enabled by default, Enabled group

BUILTIN\Remote Desktop Users               Alias            S-1-5-32-555 Mandatory group, Enabled by default, Enabled group

BUILTIN\Users                              Alias            S-1-5-32-545 Mandatory group, Enabled by default, Enabled group

NT AUTHORITY\REMOTE INTERACTIVE LOGON      Well-known group S-1-5-14     Mandatory group, Enabled by default, Enabled group

NT AUTHORITY\INTERACTIVE                   Well-known group S-1-5-4      Mandatory group, Enabled by default, Enabled group

NT AUTHORITY\Authenticated Users           Well-known group S-1-5-11     Mandatory group, Enabled by default, Enabled group

NT AUTHORITY\This Organization             Well-known group S-1-5-15     Mandatory group, Enabled by default, Enabled group

LOCAL                                      Well-known group S-1-2-0      Mandatory group, Enabled by default, Enabled group

Authentication authority asserted identity Well-known group S-1-18-1     Mandatory group, Enabled by default, Enabled group

Mandatory Label\Medium Mandatory Level     Label            S-1-16-8192  
```
`whoami /priv`
- shows user privileges
```bash
[10/23 13:29:03] beacon> shell whoami /priv
[10/23 13:29:03] [*] Tasked beacon to run: whoami /priv
[10/23 13:29:03] [+] host called home, sent: 43 bytes
[10/23 13:29:03] [+] received output:


PRIVILEGES INFORMATION

----------------------



Privilege Name                Description                          State   

============================= ==================================== ========

SeShutdownPrivilege           Shut down the system                 Disabled

SeChangeNotifyPrivilege       Bypass traverse checking             Enabled 

SeUndockPrivilege             Remove computer from docking station Disabled

SeIncreaseWorkingSetPrivilege Increase a process working set       Disabled

SeTimeZonePrivilege           Change the time zone                 Disabled

```
`whoami /all`
```bash
[10/23 13:52:35] beacon> shell whoami /all
[10/23 13:52:35] [*] Tasked beacon to run: whoami /all
[10/23 13:52:35] [+] host called home, sent: 42 bytes
[10/23 13:52:35] [+] received output:


USER INFORMATION

----------------



User Name             SID                                           

===================== ==============================================

corp\ned.flanders_adm S-1-5-21-2291914956-3290296217-2402366952-3604





GROUP INFORMATION

-----------------



Group Name                                 Type             SID          Attributes                                        

========================================== ================ ============ ==================================================

Everyone                                   Well-known group S-1-1-0      Mandatory group, Enabled by default, Enabled group

BUILTIN\Remote Desktop Users               Alias            S-1-5-32-555 Mandatory group, Enabled by default, Enabled group

BUILTIN\Users                              Alias            S-1-5-32-545 Mandatory group, Enabled by default, Enabled group

NT AUTHORITY\REMOTE INTERACTIVE LOGON      Well-known group S-1-5-14     Mandatory group, Enabled by default, Enabled group

NT AUTHORITY\INTERACTIVE                   Well-known group S-1-5-4      Mandatory group, Enabled by default, Enabled group

NT AUTHORITY\Authenticated Users           Well-known group S-1-5-11     Mandatory group, Enabled by default, Enabled group

NT AUTHORITY\This Organization             Well-known group S-1-5-15     Mandatory group, Enabled by default, Enabled group

LOCAL                                      Well-known group S-1-2-0      Mandatory group, Enabled by default, Enabled group

Authentication authority asserted identity Well-known group S-1-18-1     Mandatory group, Enabled by default, Enabled group

Mandatory Label\Medium Mandatory Level     Label            S-1-16-8192                                                    





PRIVILEGES INFORMATION

----------------------



Privilege Name                Description                          State   

============================= ==================================== ========

SeShutdownPrivilege           Shut down the system                 Disabled

SeChangeNotifyPrivilege       Bypass traverse checking             Enabled 

SeUndockPrivilege             Remove computer from docking station Disabled

SeIncreaseWorkingSetPrivilege Increase a process working set       Disabled

SeTimeZonePrivilege           Change the time zone                 Disabled





USER CLAIMS INFORMATION

-----------------------



User claims unknown.



Kerberos support for Dynamic Access Control on this device has been disabled.

```