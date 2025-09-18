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
┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV -p- -Pn 10.11.1.111
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-23 15:36 EDT
Nmap scan report for 10.11.1.111
Host is up (0.058s latency).
Not shown: 65519 closed tcp ports (reset)
PORT      STATE SERVICE       VERSION
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds?
1433/tcp  open  ms-sql-s      Microsoft SQL Server 2017 14.00.1000.00; RTM
|_ms-sql-info: ERROR: Script execution failed (use -d to debug)
|_ms-sql-ntlm-info: ERROR: Script execution failed (use -d to debug)
|_ssl-date: 2023-03-23T19:41:22+00:00; -2s from scanner time.
| ssl-cert: Subject: commonName=SSL_Self_Signed_Fallback
| Not valid before: 2022-04-28T09:23:20
|_Not valid after:  2052-04-28T09:23:20
3389/tcp  open  ms-wbt-server Microsoft Terminal Services
| ssl-cert: Subject: commonName=1nsider
| Not valid before: 2023-03-21T16:12:11
|_Not valid after:  2023-09-20T16:12:11
| rdp-ntlm-info: 
|   Target_Name: 1NSIDER
|   NetBIOS_Domain_Name: 1NSIDER
|   NetBIOS_Computer_Name: 1NSIDER
|   DNS_Domain_Name: 1nsider
|   DNS_Computer_Name: 1nsider
|   Product_Version: 10.0.17763
|_  System_Time: 2023-03-23T19:41:14+00:00
|_ssl-date: 2023-03-23T19:41:22+00:00; -2s from scanner time.
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
8732/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
47001/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC
49670/tcp open  msrpc         Microsoft Windows RPC
49671/tcp open  msrpc         Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows


```


#nmapudp
```shell
# still running
```

## 1.5 SMB

```shell


#crackmapexec guest login - grabs domain names and version information
└─# crackmapexec smb 10.11.1.111 -u 'guest' -p '' --sessions
SMB         10.11.1.111     445    1NSIDER          [*] Windows 10.0 Build 17763 x64 (name:1NSIDER) (domain:1nsider) (signing:False) (SMBv1:False)
SMB         10.11.1.111     445    1NSIDER          [-] 1nsider\guest: STATUS_ACCOUNT_DISABLED 

#crackmapexec anonymous login
─# crackmapexec smb 10.11.1.111 -u '' -p '' --sessions 
SMB         10.11.1.111     445    1NSIDER          [*] Windows 10.0 Build 17763 x64 (name:1NSIDER) (domain:1nsider) (signing:False) (SMBv1:False)
SMB         10.11.1.111     445    1NSIDER          [-] 1nsider\: STATUS_ACCESS_DENIED

#smbclient with users and shares
smbclient \\\\10.10.10.161\\ADMIN$ -U svc-alfresco

#smbclient anonymous 
┌──(root㉿kali)-[/home/kali]
└─# smbclient -L \\\\10.11.1.111 -N  
session setup failed: NT_STATUS_ACCESS_DENIED


#smbclient wwwroot share connect - try blank password
└─# smbclient \\\\10.11.1.111\\wwwroot
Password for [WORKGROUP\kali]:
session setup failed: NT_STATUS_ACCESS_DENIED

smbmap -H 10.11.1.13
[!] Authentication error on 10.11.1.13

enum4linux -U 10.11.1.13 
```
### 2. Searchsploit:
#searchsploit

```shell
```

### 3. Web Fuzzing : Dirsearch & GoBuster
#webfuzzing #port8732
```shell
┌──(root㉿kali)-[/home/kali]
└─# gobuster dir -u http://10.11.1.111:8732 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.11.1.111:8732
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              aspx,php,txt,html,asp
[+] Timeout:                 10s
===============================================================
2023/03/23 15:53:46 Starting gobuster in directory enumeration mode
===============================================================
Progress: 27684 / 27690 (99.98%)
===============================================================
2023/03/23 16:00:22 Finished
===============================================================

```

```shell
#dirsearch medium.txt
dirsearch -e php,html,js,asp,aspx -u http://10.11.1.111:8732 -x 400,401,403 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

```shell
#nikto
┌──(root㉿kali)-[/home/kali]
└─#  nikto -host http://10.11.1.111:8732 
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          10.11.1.111
+ Target Hostname:    10.11.1.111
+ Target Port:        8732
+ Start Time:         2023-03-23 16:04:56 (GMT-4)
---------------------------------------------------------------------------
+ Server: Microsoft-HTTPAPI/2.0
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ No CGI Directories found (use '-C all' to force check all possible dirs)

```

```shell
gobuster dir -u http://10.11.1.234:10443 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx

```

```shell
dirsearch -e php,html,js,asp,aspx -u http://10.11.1.234:10443 -x 400,401,403 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

#port47001
```shell

gobuster dir -u http://10.11.1.111:47001 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx

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








