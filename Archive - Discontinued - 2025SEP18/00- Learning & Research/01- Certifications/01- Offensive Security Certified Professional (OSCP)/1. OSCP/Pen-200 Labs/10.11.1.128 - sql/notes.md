###  Machine Information

```shell
IP ADDRESS: 10.11.1.128
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
└─# nmap -sC -sV -p- -Pn 10.11.1.128
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-23 16:35 EDT
Nmap scan report for 10.11.1.128
Host is up (0.099s latency).
Not shown: 65517 closed tcp ports (reset)
PORT      STATE SERVICE            VERSION
21/tcp    open  ftp                Microsoft ftpd
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_03-14-19  01:58AM             54030608 FoxitReader901_enu_Setup_Prom.exe
| ftp-syst: 
|_  SYST: Windows_NT
135/tcp   open  msrpc              Microsoft Windows RPC
139/tcp   open  netbios-ssn        Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds       Microsoft Windows Server 2008 R2 - 2012 microsoft-ds
1433/tcp  open  ms-sql-s           Microsoft SQL Server 2012 11.00.2100.00; RTM
|_ms-sql-info: ERROR: Script execution failed (use -d to debug)
| ssl-cert: Subject: commonName=SSL_Self_Signed_Fallback
| Not valid before: 2022-04-06T17:00:38
|_Not valid after:  2052-04-06T17:00:38
|_ms-sql-ntlm-info: ERROR: Script execution failed (use -d to debug)
|_ssl-date: 2023-03-23T20:49:54+00:00; -1s from scanner time.
3389/tcp  open  ssl/ms-wbt-server?
| ssl-cert: Subject: commonName=dj
| Not valid before: 2023-03-21T21:36:32
|_Not valid after:  2023-09-20T21:36:32
|_ssl-date: 2023-03-23T20:49:54+00:00; -1s from scanner time.
| rdp-ntlm-info: 
|   Target_Name: DJ
|   NetBIOS_Domain_Name: DJ
|   NetBIOS_Computer_Name: DJ
|   DNS_Domain_Name: dj
|   DNS_Computer_Name: dj
|   Product_Version: 6.3.9600
|_  System_Time: 2023-03-23T20:49:37+00:00
4167/tcp  open  http               Microsoft IIS httpd 8.5
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-title: IIS Windows Server
5800/tcp  open  vnc-http           TightVNC (user: dj; VNC TCP port: 5900)
|_http-title: TightVNC desktop [dj]
5900/tcp  open  vnc                VNC (protocol 3.8)
| vnc-info: 
|   Protocol version: 3.8
|   Security types: 
|     VNC Authentication (2)
|     Tight (16)
|   Tight auth subtypes: 
|_    STDV VNCAUTH_ (2)
5985/tcp  open  http               Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
47001/tcp open  http               Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
49152/tcp open  msrpc              Microsoft Windows RPC
49153/tcp open  msrpc              Microsoft Windows RPC
49154/tcp open  msrpc              Microsoft Windows RPC
49155/tcp open  msrpc              Microsoft Windows RPC
49156/tcp open  msrpc              Microsoft Windows RPC
49157/tcp open  msrpc              Microsoft Windows RPC
49158/tcp open  msrpc              Microsoft Windows RPC
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   302: 
|_    Message signing enabled but not required
|_clock-skew: mean: -1s, deviation: 0s, median: -1s
| smb2-time: 
|   date: 2023-03-23T20:49:38
|_  start_date: 2022-04-06T17:00:37
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 853.52 seconds

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
gobuster dir -u http://10.11.1.234:10443 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx

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








