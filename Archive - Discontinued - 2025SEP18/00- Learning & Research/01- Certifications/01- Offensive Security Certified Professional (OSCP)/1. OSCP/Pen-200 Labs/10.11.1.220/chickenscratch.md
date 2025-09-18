```shell

┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV -p- -Pn -vv 10.11.1.220
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-28 18:46 EDT
NSE: Loaded 155 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 18:46
Completed NSE at 18:46, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 18:46
Completed NSE at 18:46, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 18:46
Completed NSE at 18:46, 0.00s elapsed
Initiating Parallel DNS resolution of 1 host. at 18:46
Completed Parallel DNS resolution of 1 host. at 18:46, 0.00s elapsed
Initiating SYN Stealth Scan at 18:46
Scanning 10.11.1.220 [65535 ports]
Discovered open port 53/tcp on 10.11.1.220
Discovered open port 21/tcp on 10.11.1.220
Discovered open port 139/tcp on 10.11.1.220
Discovered open port 135/tcp on 10.11.1.220
Discovered open port 3389/tcp on 10.11.1.220
Discovered open port 445/tcp on 10.11.1.220
Discovered open port 49175/tcp on 10.11.1.220
Discovered open port 49169/tcp on 10.11.1.220
SYN Stealth Scan Timing: About 24.87% done; ETC: 18:48 (0:01:34 remaining)
SYN Stealth Scan Timing: About 28.36% done; ETC: 18:50 (0:02:34 remaining)
Discovered open port 389/tcp on 10.11.1.220
Discovered open port 47001/tcp on 10.11.1.220
Discovered open port 464/tcp on 10.11.1.220
Discovered open port 593/tcp on 10.11.1.220
Increasing send delay for 10.11.1.220 from 0 to 5 due to max_successful_tryno increase to 4
Discovered open port 9389/tcp on 10.11.1.220
SYN Stealth Scan Timing: About 47.92% done; ETC: 18:49 (0:01:39 remaining)
Discovered open port 49155/tcp on 10.11.1.220
Discovered open port 3268/tcp on 10.11.1.220
Discovered open port 49158/tcp on 10.11.1.220
Discovered open port 49173/tcp on 10.11.1.220
Discovered open port 49152/tcp on 10.11.1.220
Discovered open port 49154/tcp on 10.11.1.220
Discovered open port 5722/tcp on 10.11.1.220
Discovered open port 49157/tcp on 10.11.1.220
```

#ftp
```shell
#ftp 1st

anonymous login not allowed, discovered server info

220-FileZilla Server version 0.9.34 beta
```