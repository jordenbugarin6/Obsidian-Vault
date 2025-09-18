```shell

┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.229]
└─# nmap -sC -sV -p- -Pn 10.11.1.229
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-27 18:29 EDT
Nmap scan report for 10.11.1.229
Host is up (0.060s latency).
Not shown: 65529 filtered tcp ports (no-response)
PORT     STATE SERVICE       VERSION
25/tcp   open  smtp          hMailServer smtpd
| smtp-commands: MAIL, SIZE 20480000, AUTH LOGIN, HELP
|_ 211 DATA HELO EHLO MAIL NOOP QUIT RCPT RSET SAML TURN VRFY
80/tcp   open  http          Microsoft IIS httpd 10.0
|_http-title: Home Page - Long Live the Squirrel
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
110/tcp  open  pop3          hMailServer pop3d
|_pop3-capabilities: UIDL TOP USER
143/tcp  open  imap          hMailServer imapd
|_imap-capabilities: CAPABILITY CHILDREN IMAP4rev1 SORT QUOTA RIGHTS=texkA0001 IDLE IMAP4 completed OK NAMESPACE ACL
587/tcp  open  smtp          hMailServer smtpd
| smtp-commands: MAIL, SIZE 20480000, AUTH LOGIN, HELP
|_ 211 DATA HELO EHLO MAIL NOOP QUIT RCPT RSET SAML TURN VRFY
3389/tcp open  ms-wbt-server Microsoft Terminal Services
| ssl-cert: Subject: commonName=mail
| Not valid before: 2023-03-20T22:00:38
|_Not valid after:  2023-09-19T22:00:38
| rdp-ntlm-info: 
|   Target_Name: MAIL
|   NetBIOS_Domain_Name: MAIL
|   NetBIOS_Computer_Name: MAIL
|   DNS_Domain_Name: mail
|   DNS_Computer_Name: mail
|   Product_Version: 10.0.14393
|_  System_Time: 2023-03-27T22:31:23+00:00
|_ssl-date: 2023-03-27T22:31:28+00:00; -2s from scanner time.
Service Info: Host: MAIL; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: -2s, deviation: 0s, median: -3s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 151.60 seconds
```

```shell
gobuster dir -u http://10.11.1.229 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx

#dirsearch syntax
dirsearch -e php,html,js,asp,aspx -u http://10.11.1.229:80 -x 400,401,403 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```