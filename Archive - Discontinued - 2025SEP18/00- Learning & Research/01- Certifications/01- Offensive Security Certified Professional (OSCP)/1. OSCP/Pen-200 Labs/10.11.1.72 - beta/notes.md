###  Machine Information

```shell
IP ADDRESS: 
HN: JAMES?
OS: Ubuntu 11.10
EXPLOIT/PORT: 110 / 25
PRIVESC:
USERS MENTIONED:
username: ryuu
password: QUHqhUPRKXMo4m7k
CREDENTIALS:
```

### 1. SCANNING:  

#rustscan 
```c

┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200]
└─# rustscan -a 10.11.1.72
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: https://discord.gg/GFrQsGy           :
: https://github.com/RustScan/RustScan :
 --------------------------------------
Please contribute more quotes to our GitHub https://github.com/rustscan/rustscan

[~] The config file is expected to be at "/root/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 10.11.1.72:22
Open 10.11.1.72:25
Open 10.11.1.72:80
Open 10.11.1.72:111
Open 10.11.1.72:110
Open 10.11.1.72:119
Open 10.11.1.72:2049
Open 10.11.1.72:4555
Open 10.11.1.72:33467
Open 10.11.1.72:34078
Open 10.11.1.72:39084
Open 10.11.1.72:53877
Open 10.11.1.72:60799
[~] Starting Script(s)
[>] Script to be run Some("nmap -vvv -p {{port}} {{ip}}")

[~] Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-29 20:20 EDT
Initiating Ping Scan at 20:20
Scanning 10.11.1.72 [4 ports]
Completed Ping Scan at 20:20, 0.09s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 20:20
Completed Parallel DNS resolution of 1 host. at 20:20, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 20:20
Scanning 10.11.1.72 [13 ports]
Discovered open port 110/tcp on 10.11.1.72
Discovered open port 25/tcp on 10.11.1.72
Discovered open port 22/tcp on 10.11.1.72
Discovered open port 111/tcp on 10.11.1.72
Discovered open port 80/tcp on 10.11.1.72
Discovered open port 33467/tcp on 10.11.1.72
Discovered open port 53877/tcp on 10.11.1.72
Discovered open port 4555/tcp on 10.11.1.72
Discovered open port 34078/tcp on 10.11.1.72
Discovered open port 2049/tcp on 10.11.1.72
Discovered open port 39084/tcp on 10.11.1.72
Discovered open port 60799/tcp on 10.11.1.72
Discovered open port 119/tcp on 10.11.1.72
Completed SYN Stealth Scan at 20:20, 0.18s elapsed (13 total ports)
Nmap scan report for 10.11.1.72
Host is up, received echo-reply ttl 63 (0.063s latency).
Scanned at 2023-03-29 20:20:47 EDT for 0s

PORT      STATE SERVICE REASON
22/tcp    open  ssh     syn-ack ttl 63
25/tcp    open  smtp    syn-ack ttl 63
80/tcp    open  http    syn-ack ttl 63
110/tcp   open  pop3    syn-ack ttl 63
111/tcp   open  rpcbind syn-ack ttl 63
119/tcp   open  nntp    syn-ack ttl 63
2049/tcp  open  nfs     syn-ack ttl 63
4555/tcp  open  rsip    syn-ack ttl 63
33467/tcp open  unknown syn-ack ttl 63
34078/tcp open  unknown syn-ack ttl 63
39084/tcp open  unknown syn-ack ttl 63
53877/tcp open  unknown syn-ack ttl 63
60799/tcp open  unknown syn-ack ttl 63

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.37 seconds
           Raw packets sent: 17 (724B) | Rcvd: 14 (600B)


# nmap scan
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.72]
└─# nmap -sC -sV -p 22,25,80,110,111,119,2049,4555,33467,34078,39084,53877,60799 -Pn 10.11.1.72 
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-29 20:23 EDT
Stats: 0:01:48 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 99.55% done; ETC: 20:25 (0:00:00 remaining)
Stats: 0:01:56 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 99.89% done; ETC: 20:25 (0:00:00 remaining)
Nmap scan report for 10.11.1.72
Host is up (0.059s latency).

PORT      STATE SERVICE     VERSION
22/tcp    open  ssh         OpenSSH 5.8p1 Debian 7ubuntu1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   1024 d32e100d4890ce9a33fb663fa0a69448 (DSA)
|   2048 ef0a3b8e3f92a45ef0abe77d75f0de0e (RSA)
|_  256 153a653b97ede0fc85bc4b53482261b1 (ECDSA)
25/tcp    open  smtp        JAMES smtpd 2.3.2
|_smtp-commands: beta Hello nmap.scanme.org (192.168.119.157 [192.168.119.157])
80/tcp    open  http        Apache httpd 2.2.20 ((Ubuntu))
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: Apache/2.2.20 (Ubuntu)
110/tcp   open  pop3        JAMES pop3d 2.3.2
111/tcp   open  rpcbind     2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100003  2,3,4       2049/tcp   nfs
|   100003  2,3,4       2049/tcp6  nfs
|   100003  2,3,4       2049/udp   nfs
|   100003  2,3,4       2049/udp6  nfs
|   100005  1,2,3      34078/tcp   mountd
|   100005  1,2,3      40458/udp   mountd
|   100005  1,2,3      40977/udp6  mountd
|   100005  1,2,3      60043/tcp6  mountd
|   100021  1,3,4      36807/udp6  nlockmgr
|   100021  1,3,4      39084/tcp   nlockmgr
|   100021  1,3,4      49366/udp   nlockmgr
|   100021  1,3,4      50518/tcp6  nlockmgr
|   100024  1          33467/tcp   status
|   100024  1          40485/udp   status
|   100024  1          45564/tcp6  status
|   100024  1          51358/udp6  status
|   100227  2,3         2049/tcp   nfs_acl
|   100227  2,3         2049/tcp6  nfs_acl
|   100227  2,3         2049/udp   nfs_acl
|_  100227  2,3         2049/udp6  nfs_acl
119/tcp   open  nntp        JAMES nntpd (posting ok)
2049/tcp  open  nfs_acl     2-3 (RPC #100227)
4555/tcp  open  james-admin JAMES Remote Admin 2.3.2
33467/tcp open  status      1 (RPC #100024)
34078/tcp open  mountd      1-3 (RPC #100005)
39084/tcp open  nlockmgr    1-4 (RPC #100021)
53877/tcp open  mountd      1-3 (RPC #100005)
60799/tcp open  mountd      1-3 (RPC #100005)
Service Info: Host: beta; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 169.55 seconds

```

#nikto
```c
──(root㉿kali)-[/home/kali]
└─# nikto -host 10.11.1.72        
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          10.11.1.72
+ Target Hostname:    10.11.1.72
+ Target Port:        80
+ Start Time:         2023-03-29 20:25:58 (GMT-4)
---------------------------------------------------------------------------
+ Server: Apache/2.2.20 (Ubuntu)
+ Server may leak inodes via ETags, header found with file /, inode: 310131, size: 177, mtime: Wed Jan  7 15:37:16 2015
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ Uncommon header 'tcn' found, with contents: list
+ Apache mod_negotiation is enabled with MultiViews, which allows attackers to easily brute force file names. See http://www.wisec.it/sectou.php?id=4698ebdc59d15. The following alternatives for 'index' were found: index.html
+ Apache/2.2.20 appears to be outdated (current is at least Apache/2.4.37). Apache 2.2.34 is the EOL for the 2.x branch.
+ Allowed HTTP Methods: GET, HEAD, POST, OPTIONS 
+ OSVDB-3268: /icons/: Directory indexing found.
+ OSVDB-3233: /icons/README: Apache default file found.
 - STATUS: Completed 5420 requests (~79% complete, 1.6 minutes left): currently in plugin 'Nikto Tests'
- STATUS: Running average: 100 requests: 0.06424 sec, 10 requests: 0.0647 sec.
+ 8725 requests: 0 error(s) and 10 item(s) reported on remote host
+ End Time:           2023-03-29 20:35:32 (GMT-4) (574 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested

```
#nmapfulltcp
```shell
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
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.72]
└─# gobuster dir -u http://10.11.1.72 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.11.1.72
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              php,txt,html,asp,aspx
[+] Timeout:                 10s
===============================================================
2023/03/29 20:31:38 Starting gobuster in directory enumeration mode
===============================================================
/.html                (Status: 403) [Size: 283]
/.hta                 (Status: 403) [Size: 282]
/.hta.php             (Status: 403) [Size: 286]
/.hta.asp             (Status: 403) [Size: 286]
/.hta.txt             (Status: 403) [Size: 286]
/.htaccess.html       (Status: 403) [Size: 292]
/.htaccess.php        (Status: 403) [Size: 291]
/.htaccess            (Status: 403) [Size: 287]
/.hta.html            (Status: 403) [Size: 287]
/.hta.aspx            (Status: 403) [Size: 287]
/.htaccess.aspx       (Status: 403) [Size: 292]
/.htaccess.asp        (Status: 403) [Size: 291]
/.htaccess.txt        (Status: 403) [Size: 291]
/.htpasswd.txt        (Status: 403) [Size: 291]
/.htpasswd.asp        (Status: 403) [Size: 291]
/.htpasswd.html       (Status: 403) [Size: 292]
/.htpasswd            (Status: 403) [Size: 287]
/.htpasswd.php        (Status: 403) [Size: 291]
/.htpasswd.aspx       (Status: 403) [Size: 292]
/cgi-bin/             (Status: 403) [Size: 286]
/cgi-bin/.html        (Status: 403) [Size: 291]
/index                (Status: 200) [Size: 177]
/index.html           (Status: 200) [Size: 177]
/index.html           (Status: 200) [Size: 177]
/server-status        (Status: 403) [Size: 291]
Progress: 27669 / 27690 (99.92%)


```

```shell
#dirsearch medium.txt
dirsearch -e php,html,js,asp,aspx -u http://10.11.1.234:80 -x 400,401,403 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

```shell
gobuster dir -u http://10.11.1.234:10443 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx

```

```shell
dirsearch -e php,html,js,asp,aspx -u http://10.11.1.234:10443 -x 400,401,403 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
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








