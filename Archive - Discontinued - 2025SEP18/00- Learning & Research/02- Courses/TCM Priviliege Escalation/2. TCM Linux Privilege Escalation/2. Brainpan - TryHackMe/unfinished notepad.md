```

Brainpan1
Windows Bufferoverflow
IP:	10.10.35.20

Brainpan is perfect for OSCP practice and has been highly recommended to complete before the exam. Exploit a buffer overflow vulnerability by analyzing a Windows executable on a Linux machine. If you get stuck on this machine, don't give up (or look at writeups), just try harder. 
```

```
start: 11:51 AM 1/14/2023
ping 10.10.35.20

nmap -sC -sV -oA nmap 10.10.35.20

															nmap -sC -sV -oA nmap 10.10.35.20
															Starting Nmap 7.92 ( https://nmap.org ) at 2023-01-14 16:53 EST
															Nmap scan report for 10.10.35.20
															Host is up (0.21s latency).
															Not shown: 998 closed tcp ports (reset)
															PORT      STATE SERVICE VERSION
															9999/tcp  open  abyss?
															| fingerprint-strings: 
															|   NULL: 
															|     _| _| 
															|     _|_|_| _| _|_| _|_|_| _|_|_| _|_|_| _|_|_| _|_|_| 
															|     _|_| _| _| _| _| _| _| _| _| _| _| _|
															|     _|_|_| _| _|_|_| _| _| _| _|_|_| _|_|_| _| _|
															|     [________________________ WELCOME TO BRAINPAN _________________________]
															|_    ENTER THE PASSWORD
															10000/tcp open  http    SimpleHTTPServer 0.6 (Python 2.7.3)
															|_http-title: Site doesn't have a title (text/html).
															1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
															SF-Port9999-TCP:V=7.92%I=7%D=1/14%Time=63C3245C%P=x86_64-pc-linux-gnu%r(NU
															SF:LL,298,"_\|\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20
															SF:\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20_\|\x20\x20\x20\x20
															SF:\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x2
															SF:0\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x
															SF:20\n_\|_\|_\|\x20\x20\x20\x20_\|\x20\x20_\|_\|\x20\x20\x20\x20_\|_\|_\|
															SF:\x20\x20\x20\x20\x20\x20_\|_\|_\|\x20\x20\x20\x20_\|_\|_\|\x20\x20\x20\
															SF:x20\x20\x20_\|_\|_\|\x20\x20_\|_\|_\|\x20\x20\n_\|\x20\x20\x20\x20_\|\x
															SF:20\x20_\|_\|\x20\x20\x20\x20\x20\x20_\|\x20\x20\x20\x20_\|\x20\x20_\|\x
															SF:20\x20_\|\x20\x20\x20\x20_\|\x20\x20_\|\x20\x20\x20\x20_\|\x20\x20_\|\x
															SF:20\x20\x20\x20_\|\x20\x20_\|\x20\x20\x20\x20_\|\n_\|\x20\x20\x20\x20_\|
															SF:\x20\x20_\|\x20\x20\x20\x20\x20\x20\x20\x20_\|\x20\x20\x20\x20_\|\x20\x
															SF:20_\|\x20\x20_\|\x20\x20\x20\x20_\|\x20\x20_\|\x20\x20\x20\x20_\|\x20\x
															SF:20_\|\x20\x20\x20\x20_\|\x20\x20_\|\x20\x20\x20\x20_\|\n_\|_\|_\|\x20\x
															SF:20\x20\x20_\|\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20_\|_\|_\|\x20\x20_
															SF:\|\x20\x20_\|\x20\x20\x20\x20_\|\x20\x20_\|_\|_\|\x20\x20\x20\x20\x20\x
															SF:20_\|_\|_\|\x20\x20_\|\x20\x20\x20\x20_\|\n\x20\x20\x20\x20\x20\x20\x20
															SF:\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x2
															SF:0\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x
															SF:20\x20_\|\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x
															SF:20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\n\x20\x20\x20\x20\x20\x20\x2
															SF:0\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x
															SF:20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\
															SF:x20\x20_\|\n\n\[________________________\x20WELCOME\x20TO\x20BRAINPAN\x
															SF:20_________________________\]\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20
															SF:\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20ENTER\x
															SF:20THE\x20PASSWORD\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x
															SF:20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\n\n\
															SF:x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20
															SF:\x20\x20\x20\x20\x20\x20\x20\x20>>\x20");

Not going to struggle for no reason, i have no idea how to even start with buffer overflow so just goin got watch video and do again by myself
```

```
12:01 PM 1/14/2023
dirsearch -u http://10.10.35.20:10000 -x 400,401,403

													└─# dirsearch -u http://10.10.35.20:10000 -x 400,401,403

													  _|. _ _  _  _  _ _|_    v0.4.2
													 (_||| _) (/_(_|| (_| )

													Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 30 | Wordlist size: 10927

													Output File: /root/.dirsearch/reports/10.10.35.20-10000/_23-01-14_17-02-59.txt

													Error Log: /root/.dirsearch/logs/errors-23-01-14_17-02-59.log

													Target: http://10.10.35.20:10000/

													[17:02:59] Starting: 
													[17:04:11] 301 -    0B  - /bin  ->  /bin/
													[17:04:11] 200 -  230B  - /bin/
													[17:04:40] 200 -  215B  - /index.html

													Task Completed
```

```
12:08 PM 1/14/2023
nc 10.10.35.20 9999 

													_|                            _|                                        
													_|_|_|    _|  _|_|    _|_|_|      _|_|_|    _|_|_|      _|_|_|  _|_|_|  
													_|    _|  _|_|      _|    _|  _|  _|    _|  _|    _|  _|    _|  _|    _|
													_|    _|  _|        _|    _|  _|  _|    _|  _|    _|  _|    _|  _|    _|
													_|_|_|    _|          _|_|_|  _|  _|    _|  _|_|_|      _|_|_|  _|    _|
																								_|                          
																								_|

													[________________________ WELCOME TO BRAINPAN _________________________]
																			  ENTER THE PASSWORD                              

																			  >> hello
																			  ACCESS DENIED
```

```
