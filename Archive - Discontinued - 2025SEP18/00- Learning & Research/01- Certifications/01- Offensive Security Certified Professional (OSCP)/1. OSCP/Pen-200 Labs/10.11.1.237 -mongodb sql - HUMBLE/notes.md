###  Machine Information

```shell
IP ADDRESS: 10.11.1.71
HN: ALPHA
OS: Linux alpha 3.13.0-141-generic #190-Ubuntu SMP Fri Jan 19 12:52:38 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
EXPLOIT/PORT: shellshock - port 80 - directory:
Sending Payload to http://10.11.1.71/cgi-bin/admin.cgi
PRIVESC:
USERS MENTIONED:
CREDENTIALS:
```

### 1. Initial Scanning:  
```

┌──(root㉿kali)-[/home/kali]
└─# ping 10.11.1.71 
PING 10.11.1.71 (10.11.1.71) 56(84) bytes of data.
64 bytes from 10.11.1.71: icmp_seq=2 ttl=63 time=1017 ms
64 bytes from 10.11.1.71: icmp_seq=3 ttl=63 time=57.4 ms
64 bytes from 10.11.1.71: icmp_seq=4 ttl=63 time=66.1 ms
```


#nmapfulltcp #rustscan
```c
# rustscan & nmap

─(root㉿kali)-[/home/kali]
└─# rustscan -a 10.11.1.71 
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: https://discord.gg/GFrQsGy           :
: https://github.com/RustScan/RustScan :
 --------------------------------------
Real hackers hack time ⌛

[~] The config file is expected to be at "/root/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 10.11.1.71:22
Open 10.11.1.71:80
[~] Starting Script(s)
[>] Script to be run Some("nmap -vvv -p {{port}} {{ip}}")

[~] Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-29 17:05 EDT
Initiating Ping Scan at 17:05
Scanning 10.11.1.71 [4 ports]
Completed Ping Scan at 17:05, 0.09s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 17:05
Completed Parallel DNS resolution of 1 host. at 17:05, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 17:05
Scanning 10.11.1.71 [2 ports]
Discovered open port 22/tcp on 10.11.1.71
Discovered open port 80/tcp on 10.11.1.71
Completed SYN Stealth Scan at 17:05, 0.09s elapsed (2 total ports)
Nmap scan report for 10.11.1.71
Host is up, received reset ttl 63 (0.057s latency).
Scanned at 2023-03-29 17:05:46 EDT for 0s

PORT   STATE SERVICE REASON
22/tcp open  ssh     syn-ack ttl 63
80/tcp open  http    syn-ack ttl 63

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.28 seconds
           Raw packets sent: 6 (240B) | Rcvd: 3 (128B)

                                                                                
┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV -p 22,80 -Pn 10.11.1.71 
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-29 17:06 EDT
Stats: 0:01:20 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 50.00% done; ETC: 17:08 (0:01:20 remaining)
Nmap scan report for 10.11.1.71
Host is up (0.062s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh?
|_ssh-hostkey: ERROR: Script execution failed (use -d to debug)
80/tcp open  http    Apache httpd 2.4.7 ((Ubuntu))
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
| http-title: Trees of Large Sizes
|_Requested resource was site/index.php/
|_http-server-header: Apache/2.4.7 (Ubuntu)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 171.84 seconds
```

#nmapudp
```shell
```
### 2. Searchsploit:
#searchsploit

```shell
```

### 3. Web Fuzzing : Dirsearch & GoBuster
#webfuzzing 
```c
┌──(root㉿kali)-[/home/kali]
└─# gobuster dir -u http://10.11.1.71:80 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx 
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.11.1.71:80
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              aspx,php,txt,html,asp
[+] Timeout:                 10s
===============================================================
2023/03/29 17:08:21 Starting gobuster in directory enumeration mode
===============================================================
/.html                (Status: 403) [Size: 282]
/.php                 (Status: 403) [Size: 281]
/.hta.html            (Status: 403) [Size: 286]
/.hta.txt             (Status: 403) [Size: 285]
/.hta.php             (Status: 403) [Size: 285]
/.hta                 (Status: 403) [Size: 281]
/.hta.asp             (Status: 403) [Size: 285]
/.htaccess            (Status: 403) [Size: 286]
/.hta.aspx            (Status: 403) [Size: 286]
/.htaccess.php        (Status: 403) [Size: 290]
/.htaccess.txt        (Status: 403) [Size: 290]
/.htaccess.asp        (Status: 403) [Size: 290]
/.htaccess.html       (Status: 403) [Size: 291]
/.htpasswd.php        (Status: 403) [Size: 290]
/.htaccess.aspx       (Status: 403) [Size: 291]
/.htpasswd            (Status: 403) [Size: 286]
/.htpasswd.txt        (Status: 403) [Size: 290]
/.htpasswd.asp        (Status: 403) [Size: 290]
/.htpasswd.html       (Status: 403) [Size: 291]
/.htpasswd.aspx       (Status: 403) [Size: 291]
/cache                (Status: 301) [Size: 307] [--> http://10.11.1.71/cache/]/cgi-bin/             (Status: 403) [Size: 285]
/cgi-bin/.html        (Status: 403) [Size: 290]
/cgi-bin/.php         (Status: 403) [Size: 289]
/core                 (Status: 301) [Size: 306] [--> http://10.11.1.71/core/]
/custom               (Status: 301) [Size: 308] [--> http://10.11.1.71/custom/]
/index.php            (Status: 302) [Size: 0] [--> site/index.php/]
/index.php            (Status: 302) [Size: 0] [--> site/index.php/]
/javascript           (Status: 301) [Size: 312] [--> http://10.11.1.71/javascript/]
/license.txt          (Status: 200) [Size: 42436]
/phpmyadmin           (Status: 301) [Size: 312] [--> http://10.11.1.71/phpmyadmin/]
/server-status        (Status: 403) [Size: 290]
/site                 (Status: 301) [Size: 306] [--> http://10.11.1.71/site/]
/templates            (Status: 301) [Size: 311] [--> http://10.11.1.71/templates/]
Progress: 27684 / 27690 (99.98%)
===============================================================
2023/03/29 17:12:03 Finished
===============================================================
```

```shell
#dirsearch medium.txt
┌──(root㉿kali)-[/home/kali]
└─# dirsearch -u http://10.11.1.71:80 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt   

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 30 | Wordlist size: 220545

Output File: /root/.dirsearch/reports/10.11.1.71-80/_23-03-29_17-08-02.txt

Error Log: /root/.dirsearch/logs/errors-23-03-29_17-08-02.log

Target: http://10.11.1.71:80/

[17:08:02] Starting: 
[17:08:03] 301 -  311B  - /templates  ->  http://10.11.1.71/templates/
[17:08:03] 301 -  306B  - /site  ->  http://10.11.1.71/site/
[17:08:06] 301 -  306B  - /core  ->  http://10.11.1.71/core/
[17:08:07] 301 -  308B  - /custom  ->  http://10.11.1.71/custom/
[17:08:07] 301 -  312B  - /javascript  ->  http://10.11.1.71/javascript/
[17:08:07] 301 -  307B  - /cache  ->  http://10.11.1.71/cache/
[17:08:35] 301 -  312B  - /phpmyadmin  ->  http://10.11.1.71/phpmyadmin/
[17:13:01] 403 -  290B  - /server-status

Task Completed

```

```shell
# ran ffuf but didnt come back with anything
┌──(root㉿kali)-[/home/kali]
└─# ffuf -w /usr/share/dirbuster/wordlists/directory-list-lowercase-2.3-medium.txt -u http://10.11.1.71/FUZZ

```

```shell
# nikto
┌──(root㉿kali)-[/home/kali]
└─# nikto -host 10.11.1.71        
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          10.11.1.71
+ Target Hostname:    10.11.1.71
+ Target Port:        80
+ Start Time:         2023-03-29 17:26:15 (GMT-4)
---------------------------------------------------------------------------
+ Server: Apache/2.4.7 (Ubuntu)
+ Retrieved x-powered-by header: PHP/5.5.9-1ubuntu4.4
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ Root page / redirects to: site/index.php/
+ Apache/2.4.7 appears to be outdated (current is at least Apache/2.4.37). Apache 2.2.34 is the EOL for the 2.x branch.
+ OSVDB-112004: /cgi-bin/admin.cgi: Site appears vulnerable to the 'shellshock' vulnerability (http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-6271).
+ OSVDB-112004: /cgi-bin/admin.cgi: Site appears vulnerable to the 'shellshock' vulnerability (http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-6278).
+ Uncommon header 'x-ob_mode' found, with contents: 0
+ OSVDB-3092: /cgi-bin/admin.cgi: This might be interesting...
+ OSVDB-3092: /cgi-bin/test.cgi: This might be interesting...
 - STATUS: Completed 3990 requests (~58% complete, 4.0 minutes left): currently in plugin 'Nikto Tests'
- STATUS: Running average: 100 requests: 0.06316 sec, 10 requests: 0.0634 sec.
+ OSVDB-3233: /icons/README: Apache default file found.
 - STATUS: Completed 6220 requests (~90% complete, 54 seconds left): currently in plugin 'Nikto Tests'
- STATUS: Running average: 100 requests: 0.15331 sec, 10 requests: 0.1622 sec.
+ OSVDB-3092: /license.txt: License file found may identify site software.
+ /phpmyadmin/: phpMyAdmin directory found
 - STATUS: Completed 8580 requests: currently in plugin 'Nikto Tests'
- STATUS: Running average: 100 requests: 0.11282 sec, 10 requests: 0.1178 sec.
+ 8883 requests: 0 error(s) and 13 item(s) reported on remote host
+ End Time:           2023-03-29 17:38:14 (GMT-4) (719 seconds)
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








