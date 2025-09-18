###  Machine Information

```shell
IP ADDRESS: 10.11.1.75
HN: bruce
OS: Windows 8.1 Enterprise 9600 x64 (name:BRUCE) (domain:bruce)
EXPLOIT/PORT: msf6 auxiliary(admin/smb/ms17_010_command) / port 445
PRIVESC: xyz user add to administrator group
USERS MENTIONED: N/A
CREDENTIALS: xyz: pw123

Lessons learned: Eternal Blue command injection with msfconsole

```

### 1. Nmap:  

#nmapfulltcp
```shell
┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV -p- -Pn 10.11.1.75 
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-20 15:55 EDT
Nmap scan report for 10.11.1.75
Host is up (0.065s latency).
Not shown: 65524 filtered tcp ports (no-response)
PORT      STATE SERVICE            VERSION
135/tcp   open  msrpc              Microsoft Windows RPC
139/tcp   open  netbios-ssn        Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds       Windows 8.1 Enterprise 9600 microsoft-ds (workgroup: WORKGROUP)
3389/tcp  open  ssl/ms-wbt-server?
|_ssl-date: 2023-03-20T20:00:28+00:00; -1s from scanner time.
| ssl-cert: Subject: commonName=bruce
| Not valid before: 2023-03-19T18:41:20
|_Not valid after:  2023-09-18T18:41:20
| rdp-ntlm-info: 
|   Target_Name: BRUCE
|   NetBIOS_Domain_Name: BRUCE
|   NetBIOS_Computer_Name: BRUCE
|   DNS_Domain_Name: bruce
|   DNS_Computer_Name: bruce
|   Product_Version: 6.3.9600
|_  System_Time: 2023-03-20T19:59:31+00:00
49152/tcp open  msrpc              Microsoft Windows RPC
49153/tcp open  msrpc              Microsoft Windows RPC
49154/tcp open  unknown
49155/tcp open  msrpc              Microsoft Windows RPC
49156/tcp open  unknown
49157/tcp open  unknown
49158/tcp open  unknown
Service Info: Host: BRUCE; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb-os-discovery: 
|   OS: Windows 8.1 Enterprise 9600 (Windows 8.1 Enterprise 6.3)
|   OS CPE: cpe:/o:microsoft:windows_8.1::-
|   Computer name: bruce
|   NetBIOS computer name: BRUCE\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2023-03-20T19:59:31+00:00
|_nbstat: NetBIOS name: BRUCE, NetBIOS user: <unknown>, NetBIOS MAC: 00505686b47b (VMware)
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   302: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2023-03-20T19:59:31
|_  start_date: 2022-07-22T14:42:16

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 322.18 seconds

```

#nmapudp
```shell
still running
```

## 1.5 SMB:
#guestlogin
```shell
#guest login allowed

└─# crackmapexec smb 10.11.1.75 -u 'guest' -p '' --sessions
SMB         10.11.1.75      445    BRUCE            [*] Windows 8.1 Enterprise 9600 x64 (name:BRUCE) (domain:bruce) (signing:False) (SMBv1:True)
SMB         10.11.1.75      445    BRUCE            [+] bruce\guest: 
SMB         10.11.1.75      445    BRUCE            [+] Enumerated sessions

#anonymous login not allowed
└─# crackmapexec smb 10.11.1.75 -u '' -p '' --sessions 
SMB         10.11.1.75      445    BRUCE            [*] Windows 8.1 Enterprise 9600 x64 (name:BRUCE) (domain:bruce) (signing:False) (SMBv1:True)
SMB         10.11.1.75      445    BRUCE            [-] bruce\: STATUS_ACCESS_DENIED 

#identified shared
┌──(root㉿kali)-[/home/kali]
└─# smbclient -L\\\\10.11.1.75 -N                      

	Sharename       Type      Comment
	---------       ----      -------
	ADMIN$          Disk      Remote Admin
	C$              Disk      Default share
	IPC$            IPC       Remote IPC
Reconnecting with SMB1 for workgroup listing.
do_connect: Connection to 10.11.1.75 failed (Error NT_STATUS_RESOURCE_NAME_NOT_FOUND)
Unable to connect with SMB1 -- no workgroup available

smbclient \\\\10.10.10.75\\ADMIN$ -U guest -N



```
### 2. Searchsploit:
#searchsploit

```shell
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.75]
└─# searchsploit eternal
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                                                                                                                             |  Path
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Eternal Lines Web Server 1.0 - Remote Denial of Service                                                                                                                                                    | multiple/dos/25075.pl
EternalMart Guestbook 1.10 - '/admin/auth.php' Remote File Inclusion                                                                                                                                       | php/webapps/2980.txt
EternalMart Mailing List Manager 1.32 - Remote File Inclusion                                                                                                                                              | php/webapps/23218.txt
Microsoft Windows - 'EternalRomance'/'EternalSynergy'/'EternalChampion' SMB Remote Code Execution (Metasploit) (MS17-010)                                                                                  | windows/remote/43970.rb
Microsoft Windows 7/2008 R2 - 'EternalBlue' SMB Remote Code Execution (MS17-010)                                                                                                                           | windows/remote/42031.py
Microsoft Windows 7/8.1/2008 R2/2012 R2/2016 R2 - 'EternalBlue' SMB Remote Code Execution (MS17-010)                                                                                                       | windows/remote/42315.py
Microsoft Windows 8/8.1/2012 R2 (x64) - 'EternalBlue' SMB Remote Code Execution (MS17-010)                                                                                                                 | windows_x86-64/remote/42030.py
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results

```

### 3. ```

### 5. Exploit : msfconsole eternal series

```shell
```

### 8. Flag

```powershell

flag
1f88aa9e73f267356f033a42d9320b50
```




# Post Flag Notes










