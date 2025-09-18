###  Machine Information

```shell
IP ADDRESS: 
HN: 
OS: 
EXPLOIT/PORT:
PRIVESC:
USERS MENTIONED:
CREDENTIALS:
```

### 1. Nmap:  

#nmapfulltcp
```shell
oot㉿kali)-[/home/kali]
└─# nmap -sC -sV -p- -Pn 10.11.1.116
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-27 13:31 EDT
Nmap scan report for 10.11.1.116
Host is up (0.063s latency).
Not shown: 65530 closed tcp ports (reset)
PORT    STATE SERVICE    VERSION
21/tcp  open  ftp        vsftpd 3.0.3
22/tcp  open  ssh        OpenSSH 7.2p2 Ubuntu 4ubuntu2.4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 86887a3f919526ff1ad1644439ea8c1a (RSA)
|   256 076218a5a3892f3e91d906c2ea37cc23 (ECDSA)
|_  256 c2bea44f01a171fbb20c3a3ea4c85651 (ED25519)
80/tcp  open  http       Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Dotty
|_http-server-header: Apache/2.4.18 (Ubuntu)
110/tcp open  tcpwrapped
143/tcp open  tcpwrapped
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 105.09 seconds


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
```shell
┌──(root㉿kali)-[/home/kali]
└─# gobuster dir -u http://10.11.1.116 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.11.1.116
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              asp,aspx,php,txt,html
[+] Timeout:                 10s
===============================================================
2023/03/27 14:15:09 Starting gobuster in directory enumeration mode
===============================================================
/.php                 (Status: 403) [Size: 276]
/.html                (Status: 403) [Size: 276]
/.hta                 (Status: 403) [Size: 276]
/.hta.asp             (Status: 403) [Size: 276]
/.htaccess.html       (Status: 403) [Size: 276]
/.htaccess.asp        (Status: 403) [Size: 276]
/.htaccess.php        (Status: 403) [Size: 276]
/.hta.aspx            (Status: 403) [Size: 276]
/.htaccess            (Status: 403) [Size: 276]
/.htaccess.txt        (Status: 403) [Size: 276]
/.hta.txt             (Status: 403) [Size: 276]
/.hta.php             (Status: 403) [Size: 276]
/.hta.html            (Status: 403) [Size: 276]
/.htaccess.aspx       (Status: 403) [Size: 276]
/.htpasswd.txt        (Status: 403) [Size: 276]
/.htpasswd.php        (Status: 403) [Size: 276]
/.htpasswd.asp        (Status: 403) [Size: 276]
/.htpasswd.aspx       (Status: 403) [Size: 276]
/.htpasswd            (Status: 403) [Size: 276]
/.htpasswd.html       (Status: 403) [Size: 276]
/administrator        (Status: 301) [Size: 318] [--> http://10.11.1.116/administrator/]
/db                   (Status: 301) [Size: 307] [--> http://10.11.1.116/db/]
/index.html           (Status: 200) [Size: 105]
/index.html           (Status: 200) [Size: 105]
/server-status        (Status: 403) [Size: 276]
Progress: 27684 / 27690 (99.98%)

```

```shell
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.116]
└─# dirsearch -e php,html,js,asp,aspx -u http://10.11.1.116:80 -x 400,401,403 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, html, js, asp, aspx | HTTP method: GET | Threads: 30 | Wordlist size: 220545

Output File: /root/.dirsearch/reports/10.11.1.116-80/_23-03-27_14-15-13.txt

Error Log: /root/.dirsearch/logs/errors-23-03-27_14-15-13.log

Target: http://10.11.1.116:80/

[14:15:14] Starting: 
[14:15:17] 301 -  307B  - /db  ->  http://10.11.1.116/db/
[14:15:35] 301 -  318B  - /administrator  ->  http://10.11.1.116/administrator/

┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.116]

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








