```bash
**[06/14 12:47:59] beacon> portscan 172.16.0.0/24
[06/14 12:47:59] [*] Tasked beacon to scan ports 1-1024,3389,5900-6000 on 172.16.0.0/24
[06/14 12:47:59] [+] host called home, sent: 95030 bytes
[06/14 12:48:01] [+] received output:
(ICMP) Target '172.16.0.2' is alive. [read 8 bytes]
(ICMP) Target '172.16.0.1' is alive. [read 8 bytes]
(ICMP) Target '172.16.0.3' is alive. [read 8 bytes]
(ICMP) Target '172.16.0.21' is alive. [read 8 bytes]
(ICMP) Target '172.16.0.20' is alive. [read 8 bytes]
(ICMP) Target '172.16.0.32' is alive. [read 8 bytes]
(ICMP) Target '172.16.0.33' is alive. [read 8 bytes]

[06/14 12:48:17] [+] received output:
172.16.0.33:5985

[06/14 12:48:19] [+] received output:
172.16.0.33:3389

[06/14 12:48:23] [+] received output:
172.16.0.33:139
172.16.0.33:135

[06/14 12:48:27] [+] received output:
172.16.0.32:5985

[06/14 12:48:37] [+] received output:
172.16.0.32:139
172.16.0.32:135

[06/14 12:48:43] [+] received output:
172.16.0.21:80
172.16.0.21:22 (SSH-2.0-OpenSSH_7.6p1 Ubuntu-4ubuntu0.5)

[06/14 12:48:45] [+] received output:
172.16.0.20:80
172.16.0.20:22 (SSH-2.0-OpenSSH_7.6p1 Ubuntu-4ubuntu0.7)

[06/14 12:48:47] [+] received output:
172.16.0.2:5985
172.16.0.3:22 (SSH-2.0-OpenSSH_8.4p1 Debian-5+deb11u3)

[06/14 12:48:48] [+] received output:
172.16.0.2:3389
172.16.0.2:636

[06/14 12:48:50] [+] received output:
172.16.0.2:593
172.16.0.2:464
172.16.0.2:389
172.16.0.2:139
172.16.0.2:135
172.16.0.2:88

[06/14 12:48:51] [+] received output:
172.16.0.2:53

[06/14 12:49:06] [+] received output:
172.16.0.1:443

[06/14 12:49:21] [+] received output:
172.16.0.1:80
172.16.0.1:53

[06/14 12:49:22] [+] received output:
172.16.0.1:22 (SSH-2.0-OpenSSH_9.4)

[06/14 12:49:31] [+] received output:
172.16.0.2:445 (platform: 500 version: 6.3 name: DC domain: ALCHEMY)
172.16.0.32:445
172.16.0.33:445
Scanner module is complete
**
```