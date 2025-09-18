```shell
09:34
# starting working on 192.168.119.101, webserver has a login page - refer to image 1
```

![[1. MS01 webpage.png]]








```shell
#webpage shows PassCore v4.2.0 version, looking up exploits and default credentials
	#nothing found with passcore moving onto nmap for the 192.168.119.102
```









https://upload.offsec.com



```shell
(root㉿kali)-[/home/kali]
└─# dig 192.168.119.100                                     

; <<>> DiG 9.18.10-2-Debian <<>> 192.168.119.100
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 5875
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; MBZ: 0x0005, udp: 512
;; QUESTION SECTION:
;192.168.119.100.		IN	A

;; AUTHORITY SECTION:
.			5	IN	SOA	a.root-servers.net. nstld.verisign-grs.com. 2023031000 1800 900 604800 86400

;; Query time: 27 msec
;; SERVER: 192.168.128.2#53(192.168.128.2) (UDP)
;; WHEN: Fri Mar 10 11:29:14 EST 2023
;; MSG SIZE  rcvd: 119
```




```shell
# had to revert kali machine

```

```shell
#dirsearch .101
┌──(root㉿kali)-[/home/kali]
└─# dirsearch -u http://192.168.119.101:8080 -x 400,401,403

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 30 | Wordlist size: 10927

Output File: /root/.dirsearch/reports/192.168.119.101-8080/_23-03-10_12-44-14.txt

Error Log: /root/.dirsearch/logs/errors-23-03-10_12-44-14.log

Target: http://192.168.119.101:8080/

[12:44:14] Starting: 
[12:44:35] 200 -  492B  - /index.html
```



```shell
# working crackmapexec
┌──(root㉿kali)-[/home/kali]
└─# crackmapexec smb 192.168.119.101 -u '' -p '' --sessions
SMB         192.168.119.101 445    MS01             [*] Windows 10.0 Build 17763 (name:MS01) (domain:oscp.exam) (signing:False) (SMBv1:False)
SMB         192.168.119.101 445    MS01             [-] oscp.exam\: STATUS_ACCESS_DENIED 
                                                                                                                                                                                                                                             
┌──(root㉿kali)-[/home/kali]
└─# crackmapexec smb 192.168.119.101 -u 'guest' -p '' --sessions
SMB         192.168.119.101 445    MS01             [*] Windows 10.0 Build 17763 (name:MS01) (domain:oscp.exam) (signing:False) (SMBv1:False)
SMB         192.168.119.101 445    MS01             [-] oscp.exam\guest: STATUS_ACCOUNT_DISABLED 
                                                                                                                                                                                                                                             
┌──(root㉿kali)-[/home/kali]
└─# crackmapexec smb 192.168.119.100 -u '' -p '' --sessions    
SMB         192.168.119.100 445    DC01             [*] Windows 10.0 Build 17763 x64 (name:DC01) (domain:oscp.exam) (signing:True) (SMBv1:False)
SMB         192.168.119.100 445    DC01             [-] oscp.exam\: STATUS_ACCESS_DENIED 
                                                                                                                                                                                                                                             
┌──(root㉿kali)-[/home/kali]
└─# crackmapexec smb 192.168.119.100 -u 'guest' -p '' --sessions
SMB         192.168.119.100 445    DC01             [*] Windows 10.0 Build 17763 x64 (name:DC01) (domain:oscp.exam) (signing:True) (SMBv1:False)
SMB         192.168.119.100 445    DC01             [-] oscp.exam\guest: STATUS_ACCOUNT_DISABLED 
                                                                                                                                                                                                                                             
┌──(root㉿kali)-[/home/kali]
```

```shell

┌──(root㉿kali)-[/home/kali]
└─# nmap -sU --top-ports 10 -sV 192.168.119.100
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-10 13:00 EST
Nmap scan report for 192.168.119.100
Host is up (0.10s latency).

PORT     STATE         SERVICE      VERSION
53/udp   open          domain       (generic dns response: SERVFAIL)
67/udp   open|filtered dhcps
123/udp  open          ntp          NTP v3
135/udp  open|filtered msrpc
137/udp  open|filtered netbios-ns
138/udp  open|filtered netbios-dgm
161/udp  open|filtered snmp
445/udp  open|filtered microsoft-ds
631/udp  open|filtered ipp
1434/udp open|filtered ms-sql-m
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port53-UDP:V=7.93%I=7%D=3/10%Time=640B706F%P=x86_64-pc-linux-gnu%r(NBTS
SF:tat,32,"\x80\xf0\x80\x82\0\x01\0\0\0\0\0\0\x20CKAAAAAAAAAAAAAAAAAAAAAAA
SF:AAAAAAA\0\0!\0\x01");


root㉿kali)-[/home/kali]
└─# nmap -sU --top-ports 10 -sV 192.168.119.101
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-10 13:03 EST
Nmap scan report for 192.168.119.101
Host is up (0.19s latency).

PORT     STATE         SERVICE      VERSION
53/udp   open|filtered domain
67/udp   open|filtered dhcps
123/udp  open|filtered ntp
135/udp  open|filtered msrpc
137/udp  open|filtered netbios-ns
138/udp  open|filtered netbios-dgm
161/udp  open|filtered snmp
445/udp  open|filtered microsoft-ds
631/udp  open|filtered ipp
1434/udp open|filtered ms-sql-m
```

```shell
- try sql
- try ipp exploit
```