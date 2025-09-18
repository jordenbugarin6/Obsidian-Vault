```bash
┌──(kali㉿gobots)-[10Jun2024 18:42:32]-[~]
└─$ gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://10.10.110.21 -x php,txt,html,asp,aspx -t 50     
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.110.21
[+] Method:                  GET
[+] Threads:                 50
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Extensions:              php,txt,html,asp,aspx
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/contact              (Status: 200) [Size: 10870] [X]
/login                (Status: 200) [Size: 10390]
/events               (Status: 200) [Size: 13335]
/store                (Status: 200) [Size: 12981]
/admin                (Status: 500) [Size: 21]
/menu                 (Status: 200) [Size: 37276]
/status               (Status: 200) [Size: 2] [X]
/masterclass          (Status: 200) [Size: 18512]
Progress: 1323360 / 1323366 (100.00%)
===============================================================
Finished
===============================================================

```
# /contact
![[Pasted image 20240612115029.png]]
# /login
![[Pasted image 20240612115209.png]]