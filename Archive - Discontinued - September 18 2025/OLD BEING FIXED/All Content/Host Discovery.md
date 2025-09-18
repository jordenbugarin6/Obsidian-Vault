
Host Discovery

> $ nmap -sn 10.11.1.1-254 -vv -oA hosts  
> $ netdiscover -r 10.11.1.0/24  
> $ crackmapexec 192.168.10.0/24  
> $ arp-scan --interface=eth0 192.168.0.0/24

DNS server discovery

> $ nmap -p 53 10.11.1.1-254 -vv -oA dcs