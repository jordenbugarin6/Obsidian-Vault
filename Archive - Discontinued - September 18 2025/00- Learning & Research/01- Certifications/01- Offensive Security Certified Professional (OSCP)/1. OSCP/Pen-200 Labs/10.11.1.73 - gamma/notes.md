###  Machine Information

```shell
IP ADDRESS: 10..1.1.73
HN: Gamma
OS: Windows Machine 
- possible Windows 7 Professional 7601 Service Pack 1 (Windows 7 Professional 6.1)
EXPLOIT/PORT:
PRIVESC:
USERS MENTIONED:
CREDENTIALS:
```

### 1. Initial Scanning:  

#ping 
```shell
┌──(root㉿kali)-[/home/kali]
└─# ping 10.11.1.73          
PING 10.11.1.73 (10.11.1.73) 56(84) bytes of data.
64 bytes from 10.11.1.73: icmp_seq=1 ttl=127 time=56.2 ms
64 bytes from 10.11.1.73: icmp_seq=2 ttl=127 time=56.5 ms

```

#rustscan 
```c
┌──(root㉿kali)-[/home/kali]
└─# rustscan -a 10.11.1.73  
PORT      STATE SERVICE      REASON
135/tcp   open  msrpc        syn-ack ttl 127
139/tcp   open  netbios-ssn  syn-ack ttl 127
445/tcp   open  microsoft-ds syn-ack ttl 127
554/tcp   open  rtsp         syn-ack ttl 127
1100/tcp  open  mctp         syn-ack ttl 127
2869/tcp  open  icslap       syn-ack ttl 127
3306/tcp  open  mysql        syn-ack ttl 127
5357/tcp  open  wsdapi       syn-ack ttl 127
5800/tcp  open  vnc-http     syn-ack ttl 127
5900/tcp  open  vnc          syn-ack ttl 127
8014/tcp  open  unknown      syn-ack ttl 127
8080/tcp  open  http-proxy   syn-ack ttl 127
10243/tcp open  unknown      syn-ack ttl 127
49152/tcp open  unknown      syn-ack ttl 127
49153/tcp open  unknown      syn-ack ttl 127
49154/tcp open  unknown      syn-ack ttl 127
49155/tcp open  unknown      syn-ack ttl 127
49156/tcp open  unknown      syn-ack ttl 127
49157/tcp open  unknown      syn-ack ttl 127

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 2.36 seconds
           Raw packets sent: 27 (1.140KB) | Rcvd: 20 (876B)


```
#nmapfulltcp
```shell

┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV -p- -Pn 10.11.1.73
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-30 19:35 EDT
Stats: 0:02:37 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 42.46% done; ETC: 19:41 (0:03:33 remaining)
Stats: 0:06:38 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 95.00% done; ETC: 19:42 (0:00:08 remaining)
Stats: 0:06:43 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 95.00% done; ETC: 19:42 (0:00:08 remaining)
Stats: 0:07:39 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 99.89% done; ETC: 19:43 (0:00:00 remaining)
Nmap scan report for 10.11.1.73
Host is up (0.061s latency).
Not shown: 65515 filtered tcp ports (no-response)
PORT      STATE SERVICE      VERSION
135/tcp   open  msrpc        Microsoft Windows RPC
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds Windows 7 Professional 7601 Service Pack 1 microsoft-ds (workgroup: WORKGROUP)
554/tcp   open  rtsp?
1100/tcp  open  java-rmi     Java RMI
| rmi-dumpregistry: 
|   creamtec/ajaxswing/JVMFactory
|     com.creamtec.ajaxswing.core.JVMFactory_Stub
|     @127.0.0.1:49157
|     extends
|       java.rmi.server.RemoteStub
|       extends
|_        java.rmi.server.RemoteObject
2869/tcp  open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
3306/tcp  open  mysql?
5357/tcp  open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Service Unavailable
5800/tcp  open  vnc-http     TightVNC (user: gamma; VNC TCP port: 5900)
|_http-title: TightVNC desktop [gamma]
5900/tcp  open  vnc          VNC (protocol 3.8)
| vnc-info: 
|   Protocol version: 3.8
|   Security types: 
|     VNC Authentication (2)
|     Tight (16)
|   Tight auth subtypes: 
|_    STDV VNCAUTH_ (2)
8014/tcp  open  http         Apache httpd
|_http-server-header: Apache
|_http-title: 404 Not Found
8080/tcp  open  http         Apache httpd 2.4.9 ((Win32) PHP/5.5.12)
|_http-title: Site doesn't have a title (text/html).
|_http-open-proxy: Proxy might be redirecting requests
| http-robots.txt: 1 disallowed entry 
|_/testmysql.php
|_http-server-header: Apache/2.4.9 (Win32) PHP/5.5.12
10243/tcp open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
49152/tcp open  msrpc        Microsoft Windows RPC
49153/tcp open  msrpc        Microsoft Windows RPC
49154/tcp open  msrpc        Microsoft Windows RPC
49155/tcp open  msrpc        Microsoft Windows RPC
49156/tcp open  msrpc        Microsoft Windows RPC
49157/tcp open  java-rmi     Java RMI
49647/tcp open  java-rmi     Java RMI
Service Info: Host: GAMMA; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb-os-discovery: 
|   OS: Windows 7 Professional 7601 Service Pack 1 (Windows 7 Professional 6.1)
|   OS CPE: cpe:/o:microsoft:windows_7::sp1:professional
|   Computer name: gamma
|   NetBIOS computer name: GAMMA\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2023-03-30T23:42:25+00:00
|_clock-skew: mean: -5s, deviation: 3s, median: -7s
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-time: 
|   date: 2023-03-30T23:42:24
|_  start_date: 2022-08-04T00:12:28
| smb2-security-mode: 
|   210: 
|_    Message signing enabled but not required

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 497.54 seconds

```

#nmapudp
```shell
┌──(root㉿kali)-[/home/kali]
└─# nmap -sU 10.11.1.73            
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-30 19:47 EDT
Nmap scan report for 10.11.1.73
Host is up (0.058s latency).
All 1000 scanned ports on 10.11.1.73 are in ignored states.
Not shown: 1000 open|filtered udp ports (no-response)

Nmap done: 1 IP address (1 host up) scanned in 59.61 seconds

```
### 2. Searchsploit:
#searchsploit

```shell
```

### 3. Web Fuzzing : Dirsearch & GoBuster
#webfuzzing 
```shell
┌──(root㉿kali)-[/home/kali]
└─# gobuster dir -u http://10.11.1.73:8080 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.11.1.73:8080
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              asp,aspx,php,txt,html
[+] Timeout:                 10s
===============================================================
2023/03/30 20:09:40 Starting gobuster in directory enumeration mode
===============================================================
/.html                (Status: 403) [Size: 294]
/.hta                 (Status: 403) [Size: 293]
/.hta.php             (Status: 403) [Size: 297]
/.hta.html            (Status: 403) [Size: 298]
/.hta.txt             (Status: 403) [Size: 297]
/.hta.asp             (Status: 403) [Size: 297]
/.hta.aspx            (Status: 403) [Size: 298]
/.htaccess            (Status: 403) [Size: 298]
/.htaccess.txt        (Status: 403) [Size: 302]
/.htaccess.html       (Status: 403) [Size: 303]
/.htaccess.asp        (Status: 403) [Size: 302]
/.htaccess.aspx       (Status: 403) [Size: 303]
/.htaccess.php        (Status: 403) [Size: 302]
/.htpasswd.php        (Status: 403) [Size: 302]
/.htpasswd            (Status: 403) [Size: 298]
/.htpasswd.txt        (Status: 403) [Size: 302]
/.htpasswd.html       (Status: 403) [Size: 303]
/.htpasswd.aspx       (Status: 403) [Size: 303]
/.htpasswd.asp        (Status: 403) [Size: 302]
/aux                  (Status: 403) [Size: 292]
/aux.html             (Status: 403) [Size: 297]
/aux.asp              (Status: 403) [Size: 296]
/aux.aspx             (Status: 403) [Size: 297]
/aux.php              (Status: 403) [Size: 296]
/aux.txt              (Status: 403) [Size: 296]
/cgi-bin/             (Status: 403) [Size: 297]
/cgi-bin/.html        (Status: 403) [Size: 302]
/com1                 (Status: 403) [Size: 293]
/com1.txt             (Status: 403) [Size: 297]
/com1.html            (Status: 403) [Size: 298]
/com1.asp             (Status: 403) [Size: 297]
/com1.aspx            (Status: 403) [Size: 298]
/com1.php             (Status: 403) [Size: 297]
/com2.txt             (Status: 403) [Size: 297]
/com2                 (Status: 403) [Size: 293]
/com2.php             (Status: 403) [Size: 297]
/com2.html            (Status: 403) [Size: 298]
/com2.asp             (Status: 403) [Size: 297]
/com2.aspx            (Status: 403) [Size: 298]
/com3                 (Status: 403) [Size: 293]
/com3.asp             (Status: 403) [Size: 297]
/com3.aspx            (Status: 403) [Size: 298]
/com3.php             (Status: 403) [Size: 297]
/com3.txt             (Status: 403) [Size: 297]
/com3.html            (Status: 403) [Size: 298]
/con.php              (Status: 403) [Size: 296]
/con                  (Status: 403) [Size: 292]
/con.txt              (Status: 403) [Size: 296]
/con.html             (Status: 403) [Size: 297]
/con.asp              (Status: 403) [Size: 296]
/con.aspx             (Status: 403) [Size: 297]
/favicon.ico          (Status: 200) [Size: 202575]                            /filemanager          (Status: 301) [Size: 330] [--> http://10.11.1.73:8080/filemanager/]
/index.php            (Status: 200) [Size: 41]
/Index.php            (Status: 200) [Size: 41]
/index.php            (Status: 200) [Size: 41]
/index.php.txt        (Status: 200) [Size: 23895]
/lpt1                 (Status: 403) [Size: 293]
/lpt1.aspx            (Status: 403) [Size: 298]
/lpt1.php             (Status: 403) [Size: 297]
/lpt1.txt             (Status: 403) [Size: 297]
/lpt1.html            (Status: 403) [Size: 298]
/lpt2                 (Status: 403) [Size: 293]
/lpt2.php             (Status: 403) [Size: 297]
/lpt1.asp             (Status: 403) [Size: 297]
/lpt2.txt             (Status: 403) [Size: 297]
/lpt2.html            (Status: 403) [Size: 298]
/lpt2.asp             (Status: 403) [Size: 297]
/lpt2.aspx            (Status: 403) [Size: 298]
/nul                  (Status: 403) [Size: 292]
/nul.aspx             (Status: 403) [Size: 297]
/nul.asp              (Status: 403) [Size: 296]
/nul.html             (Status: 403) [Size: 297]
/nul.txt              (Status: 403) [Size: 296]
/nul.php              (Status: 403) [Size: 296]
/php                  (Status: 301) [Size: 322] [--> http://10.11.1.73:8080/php/]
/PHP                  (Status: 301) [Size: 322] [--> http://10.11.1.73:8080/PHP/]
/phpmyadmin           (Status: 403) [Size: 299]
/prn                  (Status: 403) [Size: 292]
/prn.aspx             (Status: 403) [Size: 297]
/prn.asp              (Status: 403) [Size: 296]
/prn.txt              (Status: 403) [Size: 296]
/prn.html             (Status: 403) [Size: 297]
/prn.php              (Status: 403) [Size: 296]
/robots.txt           (Status: 200) [Size: 72]
/robots.txt           (Status: 200) [Size: 72]
Progress: 27649 / 27690 (99.85%)
===============================================================
2023/03/30 20:12:58 Finished
===============================================================
                                                                                                                     
┌──(root㉿kali)-[/home/kali]
└─# 



```

```shell
#dirsearch medium.txt
[20:08:26] Starting: 
[20:08:28] 301 -  322B  - /php  ->  http://10.11.1.73:8080/php/
[20:08:36] 301 -  322B  - /PHP  ->  http://10.11.1.73:8080/PHP/
[20:08:37] 403 -  290B  - /%20
[20:08:45] 403 -  299B  - /*checkout*
[20:08:55] 403 -  299B  - /phpmyadmin
[20:09:07] 403 -  298B  - /*docroot*
[20:09:10] 403 -  290B  - /*
[20:09:14] 403 -  292B  - /con
[20:09:48] 403 -  294B  - /http%3A
[20:10:02] 403 -  296B  - /**http%3a
[20:10:12] 403 -  295B  - /*http%3A
[20:10:33] 403 -  292B  - /aux
[####                ] 22% 49399/220545[####                ] 22% 49400/220545[####                ] 22% 49401/220545[####                ] 22% 49402/220545[####                ] 22% 49403/220545[####                ] 22% 49404/220545[####                ] 22% 49405/220545[####                ] 22% 49406/220545[####                ] 22% 49407/220545[####                ] 22% 49408/220545[####                ] 22% 49409/220545[20:10:55] 403 -  296B  - /**http%3A
[20:11:17] 403 -  290B  - /%C0
[######              ] 30% 68172/220545[######              ] 30% 68173/220545[######              ] 30% 68174/220545[######              ] 30% 68175/220545[######              ] 30% 68176/220545[######              ] 30% 68177/220545[######              ] 30% 68178/220545[######              ] 30% 68179/220545[######              ] 30% 68180/220545[20:12:22] 403 -  299B  - /phpsysinfo
[20:12:22] 301 -  330B  - /filemanager  ->  http://10.11.1.73:8080/filemanager/
[20:13:24] 403 -  298B  - /%3FRID%3D2671
[20:13:36] 403 -  300B  - /devinmoore*
[20:17:02] 403 -  296B  - /200109*
[20:17:09] 403 -  293B  - /*sa_
[20:17:09] 403 -  293B  - /*dc_
[20:19:27] 403 -  290B  - /%D8
[20:19:27] 403 -  290B  - /%CD
[20:19:27] 403 -  290B  - /%CF
[20:19:27] 403 -  290B  - /%CE
[20:19:27] 403 -  290B  - /%CA
[20:19:27] 403 -  290B  - /%D0
[20:19:27] 403 -  290B  - /%D1
[20:19:27] 403 -  290B  - /%D5
[20:19:27] 403 -  290B  - /%D7
[20:19:27] 403 -  290B  - /%D6
[20:19:27] 403 -  290B  - /%D4
[20:19:27] 403 -  290B  - /%D3
[20:19:27] 403 -  290B  - /%D2
[20:19:27] 403 -  290B  - /%C9
[20:19:27] 403 -  290B  - /%CB
[20:19:27] 403 -  290B  - /%C8
[20:19:27] 403 -  290B  - /%CC
[20:19:27] 403 -  290B  - /%C7
[20:19:27] 403 -  290B  - /%C2
[20:19:27] 403 -  290B  - /%C6
[20:19:27] 403 -  290B  - /%C5
[20:19:27] 403 -  290B  - /%C4
[20:19:27] 403 -  290B  - /%C1
[20:19:27] 403 -  290B  - /%C3
[20:19:27] 403 -  290B  - /%D9
[20:19:27] 403 -  290B  - /%DF
[20:19:27] 403 -  290B  - /%DE
[20:19:27] 403 -  290B  - /%DD
[20:19:27] 403 -  290B  - /%DB
[20:19:38] 403 -  295B  - /login%3f
[20:20:04] 403 -  310B  - /%22james%20kim%22
[20:20:04] 403 -  312B  - /%22julie%20roehm%22
[20:20:04] 403 -  315B  - /%22britney%20spears%22

```

```shell
gobuster dir -u http://10.11.1.234:10443 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx

```

```shell
┌──(root㉿kali)-[/home/kali]
└─# nikto -host 10.11.1.73:8080
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          10.11.1.73
+ Target Hostname:    10.11.1.73
+ Target Port:        8080
+ Start Time:         2023-03-30 20:09:45 (GMT-4)
---------------------------------------------------------------------------
+ Server: Apache/2.4.9 (Win32) PHP/5.5.12
+ Retrieved x-powered-by header: PHP/5.5.12
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ Entry '/testmysql.php' in robots.txt returned a non-forbidden or redirect HTTP code (200)
+ Cookie OV4260859958 created without the httponly flag
+ Entry '/PHP/' in robots.txt returned a non-forbidden or redirect HTTP code (200)
+ "robots.txt" contains 2 entries which should be manually viewed.
+ PHP/5.5.12 appears to be outdated (current is at least 7.2.12). PHP 5.6.33, 7.0.27, 7.1.13, 7.2.1 may also current release for each branch.
+ Apache/2.4.9 appears to be outdated (current is at least Apache/2.4.37). Apache 2.2.34 is the EOL for the 2.x branch.
+ Web Server returns a valid response with junk HTTP methods, this may cause false positives.
+ OSVDB-877: HTTP TRACE method is active, suggesting the host is vulnerable to XST
+ Cookie OV4027342154 created without the httponly flag
+ OSVDB-3092: /php/: This might be interesting...
+ OSVDB-3233: /php/index.php: Monkey Http Daemon default PHP file found.
+ 8728 requests: 0 error(s) and 15 item(s) reported on remote host
+ End Time:           2023-03-30 20:21:10 (GMT-4) (685 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested

```
### 4. Web Browsing & WPscan

#wpscan 
```powershell
```

#wpscan #bruteforce #admin/princess #credentials

```shell
```

#wpscan #bruteforce
```shell
```


#wordpress #plugin #reverse #shell 
```shell
```

### 5. Reverse Shell : Word Press Add Plugin

```shell
```

### 6. Foothold Enumeration

```SHELL
```

### 7. Privilege Escalation : DirtyCow
```shell
```

### 8. Flag

```powershell
```




# Post Flag Notes








