 ```shell

 ┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV -Pn 10.11.1.44  
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-24 18:01 EDT
Nmap scan report for 10.11.1.44
Host is up (0.063s latency).
Not shown: 998 closed tcp ports (reset)
PORT     STATE SERVICE  VERSION
22/tcp   open  ssh      OpenSSH 5.3p1 Debian 3ubuntu7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   1024 656369c98b96b1fbbed55cf81e7bde8f (DSA)
|_  2048 2899c051209b31e1a4fb9a174652cffc (RSA)
8000/tcp open  ssl/http Rocket httpd 1.2.6 (Python 2.6.5)
|_http-generator: Web2py Web Framework
|_http-title: CSC438 - Issue Tracker Project
| ssl-cert: Subject: commonName=Tricia Admin/organizationName=Thinc/stateOrProvinceName=NY/countryName=US
| Not valid before: 2013-08-17T11:55:25
|_Not valid after:  2014-08-17T11:55:25
| sslv2: 
|   SSLv2 supported
|   ciphers: 
|     SSL2_RC4_128_WITH_MD5
|     SSL2_RC4_128_EXPORT40_WITH_MD5
|     SSL2_RC2_128_CBC_WITH_MD5
|     SSL2_RC2_128_CBC_EXPORT40_WITH_MD5
|     SSL2_DES_192_EDE3_CBC_WITH_MD5
|_    SSL2_DES_64_CBC_WITH_MD5
|_ssl-date: 2023-03-24T22:01:47+00:00; -1s from scanner time.
|_http-server-header: Rocket 1.2.6 Python/2.6.5
| http-robots.txt: 1 disallowed entry 
|_/welcome/default/user
| http-cookie-flags: 
|   /: 
|     session_id_issue_tracker: 
|_      httponly flag not set
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: -1s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 35.23 seconds
```

```