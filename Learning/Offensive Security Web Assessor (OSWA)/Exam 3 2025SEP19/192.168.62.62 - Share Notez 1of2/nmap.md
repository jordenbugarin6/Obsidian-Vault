```bash
┌──(kali㉿gobots)-[20Sep2025 03:50:26]-[~]
└─$ nmap -Pn -sV 192.168.62.62 -p- 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-09-20 03:50 UTC
Stats: 0:00:14 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 72.60% done; ETC: 03:50 (0:00:06 remaining)
Stats: 0:00:18 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 96.48% done; ETC: 03:50 (0:00:01 remaining)
Stats: 0:00:25 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 33.33% done; ETC: 03:51 (0:00:12 remaining)
Nmap scan report for 192.168.62.62
Host is up (0.016s latency).
Not shown: 65532 closed tcp ports (reset)
PORT     STATE SERVICE  VERSION
22/tcp   open  ssh      OpenSSH 8.9p1 Ubuntu 3 (Ubuntu Linux; protocol 2.0)
80/tcp   open  http     Apache httpd 2.4.52 ((Ubuntu))
8443/tcp open  ssl/http Apache Tomcat (language: en)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 37.82 seconds
```