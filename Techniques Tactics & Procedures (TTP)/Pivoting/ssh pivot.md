##### /etc/proxychains config
```bash
socks5  127.0.0.1 1080
```
##### ssh command
```bash
ssh -i /root/.ssh/id_rsa -D 1080:localhost:22 root@10.10.110.21
```
##### proxychains nmap testing
```bash
┌──(root💀gobots)-[20Jun2024 13:32:37]-[/home/kali/SUT/Alchemy/172.16.0.20]
└─# proxychains nmap -sT -p 80 172.16.0.20 -Pn                                                         
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.17
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-06-20 13:34 UTC
Nmap scan report for 172.16.0.20
Host is up (0.031s latency).

PORT   STATE SERVICE
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 0.19 seconds

```