###  Machine Information

```shell
IP ADDRESS: 10.11.1.39
HN: UNK
OS: NIX 
EXPLOIT/PORT: WEB
PRIVESC: writeable /etc/passwd
USERS MENTIONED:
CREDENTIALS: user5:pass123
```

#nmap 
```shell
┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV -p- -Pn 10.11.1.39
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-22 17:48 EDT
Nmap scan report for 10.11.1.39
Host is up (0.088s latency).
Not shown: 65097 filtered tcp ports (no-response), 435 filtered tcp ports (host-prohibited)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 6.6.1 (protocol 2.0)
| ssh-hostkey: 
|   2048 5ec17ed2f920f911ea4b0268073f54f2 (RSA)
|   256 36ef2731a2fd4ae3d24e12581f7a0358 (ECDSA)
|_  256 2c709cc94c5061d25143d567d1d039de (ED25519)
80/tcp   open  http    nginx 1.6.3
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-title: Apache HTTP Server Test Page powered by CentOS
|_http-server-header: nginx/1.6.3
3306/tcp open  mysql   MariaDB (unauthorized)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 472.54 seconds

```

#gobuster #dirsearch
```shell
#gobuster syntax
┌──(root㉿kali)-[/home/kali]
└─# gobuster dir -u http://10.11.1.39 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx          
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.11.1.39
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              php,txt,html,asp,aspx
[+] Timeout:                 10s
===============================================================
2023/03/22 18:00:26 Starting gobuster in directory enumeration mode
===============================================================
/.html                (Status: 403) [Size: 207]
/.hta                 (Status: 403) [Size: 206]
/.hta.php             (Status: 403) [Size: 210]
/.hta.txt             (Status: 403) [Size: 210]
/.hta.html            (Status: 403) [Size: 211]
/.hta.asp             (Status: 403) [Size: 210]
/.hta.aspx            (Status: 403) [Size: 211]
/.htaccess.txt        (Status: 403) [Size: 215]
/.htaccess            (Status: 403) [Size: 211]
/.htaccess.html       (Status: 403) [Size: 216]
/.htaccess.php        (Status: 403) [Size: 215]
/.htaccess.asp        (Status: 403) [Size: 215]
/.htaccess.aspx       (Status: 403) [Size: 216]
/.htpasswd            (Status: 403) [Size: 211]
/.htpasswd.asp        (Status: 403) [Size: 215]
/.htpasswd.aspx       (Status: 403) [Size: 216]
/.htpasswd.php        (Status: 403) [Size: 215]
/.htpasswd.txt        (Status: 403) [Size: 215]
/.htpasswd.html       (Status: 403) [Size: 216]
/cgi-bin/             (Status: 403) [Size: 210]                               /cgi-bin/.html        (Status: 403) [Size: 215]
/robots.txt           (Status: 301) [Size: 184] [--> http://10.11.1.39/bad.txt]
/robots.txt           (Status: 301) [Size: 184] [--> http://10.11.1.39/bad.txt]
/robots.txt.aspx      (Status: 301) [Size: 184] [--> http://10.11.1.39/bad.txt]
/robots.txt.txt       (Status: 301) [Size: 184] [--> http://10.11.1.39/bad.txt]
/robots.txt.php       (Status: 301) [Size: 184] [--> http://10.11.1.39/bad.txt]
/robots.txt.html      (Status: 301) [Size: 184] [--> http://10.11.1.39/bad.txt]
/robots.txt.asp       (Status: 301) [Size: 184] [--> http://10.11.1.39/bad.txt]
Progress: 27666 / 27690 (99.91%)
===============================================================
2023/03/22 18:03:39 Finished
===============================================================

#nothing
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.31]
└─# gobuster dir -u http://10.11.1.31/cgi-bin/ -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.11.1.31/cgi-bin/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              php,txt,html,asp,aspx
[+] Timeout:                 10s
===============================================================
2023/03/22 18:11:01 Starting gobuster in directory enumeration mode
===============================================================
Progress: 27657 / 27690 (99.88%)
===============================================================
2023/03/22 18:14:26 Finished
===============================================================




#dirsearch syntax
┌──(root㉿kali)-[/home/kali]
└─# 
                                                                                                                     
┌──(root㉿kali)-[/home/kali]
└─# dirsearch -e php,html,js,asp,aspx -u http://10.11.1.39:80 -x 400,401,403 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, html, js, asp, aspx | HTTP method: GET | Threads: 30 | Wordlist size: 220545

Output File: /root/.dirsearch/reports/10.11.1.39-80/_23-03-22_18-04-00.txt

Error Log: /root/.dirsearch/logs/errors-23-03-22_18-04-00.log

Target: http://10.11.1.39:80/

[18:04:00] Starting: 
[                    ] 0%   201/220545 [                    ] 0%   202/220545 [                    ] 0%   203/220545 [                    ] 0%   204/220545 [                    ] 0%   205/220545 [                    ] 0%   206/220545 [                    ] 0%   207/220545 [                    ] 0%   208/220545 [                    ] 0%   209/220545 [                    ] 0%   210/220545 [                    ] 0%   211/220545 [                    ] 0%   212/220545 [#                   ] 6% 14359/220545 [#                   ] 6% 14360/220545 [#                   ] 6% 14361/220545 [#                   ] 7% 16246/220545 [#                   ] 7% 16247/220545 [#                   ] 7% 16248/220545 [#                   ] 7% 16249/220545 [#                   ] 7% 16251/220545 [#                   ] 7% 16252/220545 [#                   ] 7% 16253/220545 [#                   ] 7% 16254/220545 [#                   ] 7% 16250/220545 [#                   ] 7% 16255/220545 [#                   ] 7% 16256/220545 [#                   ] 7% 16257/220545 [############        ] 62% 137875/22054[############        ] 62% 137876/22054[############        ] 62% 137877/22054[##############      ] 74% 163970/22054[##############      ] 74% 163971/22054[##############      ] 74% 163972/22054[##############      ] 74% 163973/22054[##############      ] 74% 163974/22054[##############      ] 74% 163975/22054[##############      ] 74% 163976/22054[##############      ] 74% 163977/22054[##############      ] 74% 163978/22054[#################   ] 85% 188651/22054[#################   ] 85% 188652/22054[#################   ] 85% 188653/22054[#################   ] 85% 188654/22054[#################   ] 85% 188655/22054[#################   ] 85% 188656/22054[#################   ] 85% 188657/22054[#################   ] 85% 188658/22054[#################   ] 85% 188659/22054[#################   ] 85% 188660/22054[#################   ] 85% 188661/22054[#################   ] 85% 188662/22054
Task Completed


#nikto got directory /otrs/index.pl which is a login screen
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.31]
└─# nikto -host http://10.11.1.39  
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          10.11.1.39
+ Target Hostname:    10.11.1.39
+ Target Port:        80
+ Start Time:         2023-03-22 18:16:28 (GMT-4)
---------------------------------------------------------------------------
+ Server: nginx/1.6.3
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ Cookie OTRSBrowserHasCookie created without the httponly flag
+ Retrieved x-powered-by header: OTRS 5.0.2 - Open Ticket Request System (http://www.otrs.com/)
+ Uncommon header 'x-otrs-login' found, with contents: /otrs/index.pl?
+ Entry '/otrs/index.pl' in robots.txt returned a non-forbidden or redirect HTTP code (200)
+ "robots.txt" contains 1 entry which should be manually viewed.


```
#searchsploit
```shell
#MariaDB searchsploit
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.31]
└─# searchsploit MariaDB             
---------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                      |  Path
---------------------------------------------------------------------------------------------------- ---------------------------------
MariaDB 10.2 - 'wsrep_provider' OS Command Execution                                                | linux/local/49765.txt
MariaDB Client 10.1.26 - Denial of Service (PoC)                                                    | linux/dos/45901.txt
MySQL / MariaDB - Geometry Query Denial of Service                                                  | linux/dos/38392.txt
MySQL / MariaDB / PerconaDB 5.5.51/5.6.32/5.7.14 - Code Execution / Privilege Escalation            | linux/local/40360.py
MySQL / MariaDB / PerconaDB 5.5.x/5.6.x/5.7.x - 'mysql' System User Privilege Escalation / Race Con | linux/local/40678.c

```
#webbrowsing
```shell
#nginx 1.6.3
http://10.11.1.39:80

```

![[Penetration Testing v2/oscp/Pen-200 Labs/10.11.1.39- linux/screenshots/1. webpage.png]]

![[2. bad.txt.png]]

#otrs5

![[3. OTRS loginpage.png]]

![[4. credential login.png]]

```shell
root@localhost:otrs
```







![[proof.txt & ip a.png]]