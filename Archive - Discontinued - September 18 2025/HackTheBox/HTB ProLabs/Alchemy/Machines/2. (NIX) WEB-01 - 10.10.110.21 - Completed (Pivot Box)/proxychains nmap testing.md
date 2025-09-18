```bash
                   
proxychains -T4 --min-rate=1000 -sC -sV -p- 10.0.3.1/24 -Pn                                                                                                                                             
proxychains nmap -T4 --min-rate=1000 -sC -sV -p- 10.0.3.1/24 -Pn                                                                                                                                        
proxychains nmap -T4 --min-rate=1000 -sC -sV -p- 10.0.3.1/24 -Pn -vv

```

-sS shows host up but filtered
```bash
Nmap scan report for 10.0.3.254
Host is up.
All 1000 scanned ports on 10.0.3.254 are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)

Nmap scan report for 10.0.3.255
Host is up.
All 1000 scanned ports on 10.0.3.255 are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)

Read data files from: /usr/bin/../share/nmap
Nmap done: 256 IP addresses (256 hosts up) scanned in 520.72 seconds
           Raw packets sent: 512000 (22.528MB) | Rcvd: 0 (0B)
                                                                                                                                                                                                            
┌──(root💀gobots)-[13Jun2024 18:21:19]-[/home/kali/SUT/Alchemy/WEB-01_10.10.110.21]
└─# proxychains nmap -T4 --min-rate=1000 -sS 10.0.3.1/24 -Pn -v

```


```bash

proxychains nmap -sT -p 21,80,135,137,443,445,338 10.0.3.1/24 -Pn -v
21,80,135,137,443,445,3389
```