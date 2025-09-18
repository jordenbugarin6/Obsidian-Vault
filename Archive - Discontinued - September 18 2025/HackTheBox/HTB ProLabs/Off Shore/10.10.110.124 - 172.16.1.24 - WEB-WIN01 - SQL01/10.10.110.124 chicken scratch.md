#nmap
```bash
# only port 80, need to web fuzz
Nmap scan report for 10.10.110.124
Host is up (0.027s latency).
Not shown: 999 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
80/tcp open  http    Microsoft IIS httpd 10.0
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
|_http-title: Offshore Dev
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
```
#ping
```bash
# 126, windows box
[root💀~/bugs_] [10.10.14.39] [2023-08-07 13:46:05] 
 └─╼ # ping 10.10.110.124
PING 10.10.110.124 (10.10.110.124) 56(84) bytes of data.
64 bytes from 10.10.110.124: icmp_seq=1 ttl=126 time=21.3 ms
64 bytes from 10.10.110.124: icmp_seq=2 ttl=126 time=22.3 ms
```
### Web Fuzzing

#gobuster  #dirsearch #nikto
```bash
# flag.txt found here.
[root💀~/bugs_] [10.10.14.39] [2023-08-07 13:51:18] 
 └─╼ # gobuster dir -u http://10.10.110.124 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.110.124
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              txt,html,asp,aspx,php
[+] Timeout:                 10s
===============================================================
2023/08/07 13:56:04 Starting gobuster in directory enumeration mode
===============================================================
/About.aspx           (Status: 500) [Size: 3420]
/about                (Status: 500) [Size: 3420]
/About                (Status: 500) [Size: 3420]
/about.aspx           (Status: 500) [Size: 3420]
/aspnet_client        (Status: 301) [Size: 158] [--> http://10.10.110.124/aspnet_client/]
/contact              (Status: 500) [Size: 3420]
/contact.aspx         (Status: 500) [Size: 3420]
/Contact              (Status: 500) [Size: 3420]
/Contact.aspx         (Status: 500) [Size: 3420]
/Content              (Status: 301) [Size: 152] [--> http://10.10.110.124/Content/]
/content              (Status: 301) [Size: 152] [--> http://10.10.110.124/content/]
/dashboard            (Status: 302) [Size: 123] [--> /Login]
/dashboard.aspx       (Status: 301) [Size: 127] [--> /dashboard]
/default              (Status: 500) [Size: 3420]
/default.aspx         (Status: 500) [Size: 3420]
/Default              (Status: 500) [Size: 3420]
/Default.aspx         (Status: 500) [Size: 3420]
/favicon.ico          (Status: 200) [Size: 552]
/flag.txt             (Status: 200) [Size: 35]
/fonts                (Status: 301) [Size: 150] [--> http://10.10.110.124/fonts/]
/index.html           (Status: 200) [Size: 3079]
/Index.html           (Status: 200) [Size: 3079]
/index.html           (Status: 200) [Size: 3079]
/license.txt          (Status: 200) [Size: 1096]
/LICENSE.txt          (Status: 200) [Size: 1096]
/login                (Status: 401) [Size: 1293]
/login.aspx           (Status: 401) [Size: 1293]
/Login                (Status: 401) [Size: 1293]
/Login.aspx           (Status: 401) [Size: 1293]
/scripts              (Status: 301) [Size: 152] [--> http://10.10.110.124/scripts/]
/Scripts              (Status: 301) [Size: 152] [--> http://10.10.110.124/Scripts/]
Progress: 27647 / 27690 (99.84%)
===============================================================
2023/08/07 13:57:29 Finished
===============================================================


dirsearch -e php,html,js,asp,aspx -u http://10.10.110.124:80 -x 400,401,403 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

![[OFFSHORE{d0nt_l3av3_f1l3s_ar0und}.png]]
FLAG 1
OFFSHORE{d0nt_l3av3_f1l3s_ar0und}