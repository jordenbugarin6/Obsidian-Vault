###  Machine Information

```shell
IP ADDRESS: 10.11.1.14
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
┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV -p- -Pn 10.11.1.14
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-21 14:57 EDT
Nmap scan report for 10.11.1.14
Host is up (0.072s latency).
Not shown: 65528 filtered tcp ports (no-response)
PORT    STATE  SERVICE VERSION
21/tcp  open   ftp     Microsoft ftpd
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| 01-17-07  06:42PM       <DIR>          AdminScripts
| 01-17-07  06:43PM       <DIR>          ftproot
| 01-17-07  06:43PM       <DIR>          iissamples
| 01-17-07  06:43PM       <DIR>          Scripts
|_03-21-23  08:05AM       <DIR>          wwwroot
| ftp-syst: 
|_  SYST: Windows_NT
23/tcp  closed telnet
25/tcp  closed smtp
80/tcp  open   http    Microsoft IIS httpd 5.1
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: Microsoft-IIS/5.1
| http-methods: 
|_  Potentially risky methods: TRACE DELETE COPY MOVE PROPFIND PROPPATCH SEARCH MKCOL LOCK UNLOCK PUT
| http-webdav-scan: 
|   Public Options: OPTIONS, TRACE, GET, HEAD, DELETE, PUT, POST, COPY, MOVE, MKCOL, PROPFIND, PROPPATCH, LOCK, UNLOCK, SEARCH
|   Server Date: Tue, 21 Mar 2023 19:02:23 GMT
|   WebDAV type: Unknown
|   Server Type: Microsoft-IIS/5.1
|_  Allowed Methods: OPTIONS, TRACE, GET, HEAD, DELETE, COPY, MOVE, PROPFIND, PROPPATCH, SEARCH, MKCOL, LOCK, UNLOCK
110/tcp closed pop3
220/tcp closed imap3
443/tcp open   https?
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 294.58 seconds


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
└─# gobuster dir -u http://10.11.1.14:80 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.11.1.14:80
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              php,txt,html,asp,aspx
[+] Timeout:                 10s
===============================================================
2023/03/21 15:07:52 Starting gobuster in directory enumeration mode
===============================================================
[ERROR] 2023/03/21 15:07:52 [!] Get "http://10.11.1.14:80/.txt": EOF
[ERROR] 2023/03/21 15:07:52 [!] Get "http://10.11.1.14:80/.aspx": EOF
[ERROR] 2023/03/21 15:07:52 [!] Get "http://10.11.1.14:80/.bash_history.asp": EOF
[ERROR] 2023/03/21 15:07:52 [!] Get "http://10.11.1.14:80/.bash_history": EOF
/_vti_bin/_vti_adm/admin.dll (Status: 500) [Size: 100]
/_vti_bin/_vti_aut/author.dll (Status: 500) [Size: 100]
/_vti_bin/shtml.dll   (Status: 500) [Size: 100]
/admin2               (Status: 403) [Size: 152]
/admin3               (Status: 403) [Size: 152]
/admin-admin          (Status: 403) [Size: 152]
/advert.html          (Status: 403) [Size: 152]
/con.asp              (Status: 500) [Size: 61]
/datenschutz.txt      (Status: 403) [Size: 152]
/example.php          (Status: 403) [Size: 152]
/global.asa           (Status: 500) [Size: 80]
Progress: 11000 / 27690 (39.73%)[ERROR] 2023/03/21 15:10:27 [!] Get "http://10.11.1.14:80/gpl.php": context deadline exceeded (Client.Timeout exceeded while awaiting headers)
/help_answer          (Status: 403) [Size: 152]
/iisadmin             (Status: 403) [Size: 135]
/index.htm            (Status: 200) [Size: 7]
Progress: 16260 / 27690 (58.72%)2023/03/21 15:11:35 Unsolicited response received on idle HTTP channel starting with "<html><body><h1> HTTP/1.1 204 No Content</h1></body></html>"; err=<nil>
/nul.asp              (Status: 204) [Size: 0]
Progress: 17948 / 27690 (64.82%)[ERROR] 2023/03/21 15:11:57 [!] Get "http://10.11.1.14:80/playing.txt": EOF
/printers             (Status: 401) [Size: 24]
/scripts              (Status: 302) [Size: 149] [--> http://10.11.1.14/scripts/]
/Scripts              (Status: 302) [Size: 149] [--> http://10.11.1.14/Scripts/]
/system-admin.txt     (Status: 403) [Size: 152]
/tsweb                (Status: 302) [Size: 147] [--> http://10.11.1.14/tsweb/]
Progress: 25131 / 27690 (90.76%)[ERROR] 2023/03/21 15:13:27 [!] Get "http://10.11.1.14:80/uncategorized.txt": context deadline exceeded (Client.Timeout exceeded while awaiting headers)
[ERROR] 2023/03/21 15:13:27 [!] Get "http://10.11.1.14:80/under_update.asp": context deadline exceeded (Client.Timeout exceeded while awaiting headers)
Progress: 27664 / 27690 (99.91%)



gobuster dir -u http://10.11.1.14:80/tsweb/ -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx

```

```shell
#dirsearch medium.txt
┌──(root㉿kali)-[/home/kali]
└─# dirsearch -e php,html,js,asp,aspx -u http://10.11.1.14:80 -x 400,401,403 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, html, js, asp, aspx | HTTP method: GET | Threads: 30 | Wordlist size: 220545

Output File: /root/.dirsearch/reports/10.11.1.14-80/_23-03-21_15-29-50.txt

Error Log: /root/.dirsearch/logs/errors-23-03-21_15-29-50.log

Target: http://10.11.1.14:80/

[15:29:51] Starting: 
[15:29:53] 302 -  149B  - /scripts  ->  http://10.11.1.14/scripts/
[15:30:16] 302 -  149B  - /Scripts  ->  http://10.11.1.14/Scripts/
[15:39:20] 302 -  149B  - /SCRIPTS  ->  http://10.11.1.14/SCRIPTS/

```

```shell
gobuster dir -u http://10.11.1.14:80 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx

```

```shell
dirsearch -e php,html,js,asp,aspx -u http://10.11.1.14:80 -x 400,401,403 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
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








