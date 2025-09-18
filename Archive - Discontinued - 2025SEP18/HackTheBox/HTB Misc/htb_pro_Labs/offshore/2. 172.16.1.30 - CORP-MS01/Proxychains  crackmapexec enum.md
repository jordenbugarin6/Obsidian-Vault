ssh
```bash
[root💀~] [10.10.14.39] [2023-10-13 19:33:26] 
 └─╼ # proxychains crackmapexec ssh 172.16.1.0/24
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
SSH         172.16.1.23     22     172.16.1.23      [*] SSH-2.0-OpenSSH_7.2p2 Ubuntu-4ubuntu2.10
SSH         172.16.1.30     22     172.16.1.30      [*] SSH-2.0-Network ConfigManager SCP Server
```
smb
```bash
[root💀~] [10.10.14.39] [2023-10-13 19:36:31] 
 └─╼ # proxychains crackmapexec smb 172.16.1.0/24
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
SMB         172.16.1.15     445    SQL01            [*] Windows Server 2016 Standard 14393 x64 (name:SQL01) (domain:corp.local) (signing:False) (SMBv1:True)
SMB         172.16.1.30     445    MS01             [*] Windows Server 2016 Standard 14393 x64 (name:MS01) (domain:corp.local) (signing:False) (SMBv1:True)
SMB         172.16.1.5      445    DC01             [*] Windows Server 2016 Standard 14393 x64 (name:DC01) (domain:corp.local) (signing:True) (SMBv1:True)
SMB         172.16.1.26     445    FS01             [*] Windows Server 2016 Standard 14393 x64 (name:FS01) (domain:corp.local) (signing:False) (SMBv1:True)
SMB         172.16.1.36     445    WSADM            [*] Windows 10.0 Build 17134 x64 (name:WSADM) (domain:corp.local) (signing:False) (SMBv1:False)
SMB         172.16.1.24     445    WEB-WIN01        [*] Windows 10.0 Build 14393 x64 (name:WEB-WIN01) (domain:corp.local) (signing:False) (SMBv1:False)
SMB         172.16.1.200    445    DC0              [*] Windows 10.0 Build 17763 x64 (name:DC0) (domain:LAB.OFFSHORE.LOCAL) (signing:True) (SMBv1:False)
SMB         172.16.1.201    445    JOE-LPTP         [*] Windows 10.0 Build 19041 x64 (name:JOE-LPTP) (domain:JOE-LPTP) (signing:False) (SMBv1:False)
SMB         172.16.1.220    445    SRV01            [*] Windows Server 2016 Standard 14393 x64 (name:SRV01) (domain:LAB.OFFSHORE.LOCAL) (signing:True) (SMBv1:True)
```
winrm
```bash
[root💀~] [10.10.14.39] [2023-10-13 19:37:17] 
 └─╼ # proxychains crackmapexec winrm 172.16.1.0/24
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
SMB         172.16.1.24     5985   WEB-WIN01        [*] Windows 10.0 Build 14393 (name:WEB-WIN01) (domain:corp.local)
HTTP        172.16.1.24     5985   WEB-WIN01        [*] http://172.16.1.24:5985/wsman
SMB         172.16.1.15     5985   SQL01            [*] Windows 10.0 Build 14393 (name:SQL01) (domain:corp.local)
SMB         172.16.1.30     5985   MS01             [*] Windows 10.0 Build 14393 (name:MS01) (domain:corp.local)
HTTP        172.16.1.30     5985   MS01             [*] http://172.16.1.30:5985/wsman
HTTP        172.16.1.15     5985   SQL01            [*] http://172.16.1.15:5985/wsman
SMB         172.16.1.26     5985   FS01             [*] Windows 10.0 Build 14393 (name:FS01) (domain:corp.local)
HTTP        172.16.1.26     5985   FS01             [*] http://172.16.1.26:5985/wsman
SMB         172.16.1.5      5985   DC01             [*] Windows 10.0 Build 14393 (name:DC01) (domain:corp.local)
SMB         172.16.1.36     5985   WSADM            [*] Windows 10.0 Build 17134 (name:WSADM) (domain:corp.local)
HTTP        172.16.1.5      5985   DC01             [*] http://172.16.1.5:5985/wsman
HTTP        172.16.1.36     5985   WSADM            [*] http://172.16.1.36:5985/wsman
SMB         172.16.1.200    5985   DC0              [*] Windows 10.0 Build 17763 (name:DC0) (domain:LAB.OFFSHORE.LOCAL)
HTTP        172.16.1.200    5985   DC0              [*] http://172.16.1.200:5985/wsman
SMB         172.16.1.201    5985   JOE-LPTP         [*] Windows 10.0 Build 19041 (name:JOE-LPTP) (domain:JOE-LPTP)
HTTP        172.16.1.201    5985   JOE-LPTP         [*] http://172.16.1.201:5985/wsman
SMB         172.16.1.220    5985   SRV01            [*] Windows 10.0 Build 14393 (name:SRV01) (domain:LAB.OFFSHORE.LOCAL)
HTTP        172.16.1.220    5985   SRV01            [*] http://172.16.1.220:5985/wsman
```
rdp
```bash
[root💀~] [10.10.14.39] [2023-10-13 19:39:09] 
 └─╼ # proxychains crackmapexec rdp 172.16.1.0/24
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
RDP         172.16.1.24     3389   WEB-WIN01        [*] Windows 10 or Windows Server 2016 Build 14393 (name:WEB-WIN01) (domain:corp.local) (nla:True)
RDP         172.16.1.36     3389   WSADM            [*] Windows 10 or Windows Server 2016 Build 17134 (name:WSADM) (domain:corp.local) (nla:True)
RDP         172.16.1.30     3389   MS01             [*] Windows 10 or Windows Server 2016 Build 14393 (name:MS01) (domain:corp.local) (nla:True)
RDP         172.16.1.15     3389   SQL01            [*] Windows 10 or Windows Server 2016 Build 14393 (name:SQL01) (domain:corp.local) (nla:True)
RDP         172.16.1.5      3389   DC01             [*] Windows 10 or Windows Server 2016 Build 14393 (name:DC01) (domain:corp.local) (nla:True)
RDP         172.16.1.26     3389   FS01             [*] Windows 10 or Windows Server 2016 Build 14393 (name:FS01) (domain:corp.local) (nla:True)
RDP         172.16.1.200    3389   DC0              [*] Windows 10 or Windows Server 2016 Build 17763 (name:DC0) (domain:LAB.OFFSHORE.LOCAL) (nla:True)

```
smb with credentials
```bash
SMB         172.16.1.5      445    DC01             [+] corp.local\ned.flanders_adm:Lefthandedyeah! 
SMB         172.16.1.30     445    MS01             [+] corp.local\ned.flanders_adm:Lefthandedyeah! 
SMB         172.16.1.24     445    WEB-WIN01        [-] Connection Error: Error while reading from remote
SMB         172.16.1.24     445    WEB-WIN01        [-] corp.local\ned.flanders_adm:Lefty1974! STATUS_LOGON_FAILURE 
SMB         172.16.1.24     445    WEB-WIN01        [-] corp.local\ned.flanders@offshore.com:Lefthandedyeah! STATUS_LOGON_FAILURE 
SMB         172.16.1.24     445    WEB-WIN01        [-] corp.local\ned.flanders@offshore.com:Lefty1974! STATUS_LOGON_FAILURE 
SMB         172.16.1.26     445    FS01             [+] corp.local\ned.flanders_adm:Lefthandedyeah! 
SMB         172.16.1.36     445    WSADM            [+] corp.local\ned.flanders_adm:Lefthandedyeah! 
SMB         172.16.1.101    445    WS02             [+] corp.local\ned.flanders_adm:Lefthandedyeah! 
SMB         172.16.1.15     445    SQL01            [+] corp.local\ned.flanders_adm:Lefthandedyeah! 

```