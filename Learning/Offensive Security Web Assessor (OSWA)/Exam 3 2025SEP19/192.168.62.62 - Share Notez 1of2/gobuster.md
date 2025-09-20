
```bash
┌──(kali㉿gobots)-[20Sep2025 03:53:51]-[~]                                                                     
└─$ gobuster dir -u http://192.168.62.62:80 -w /usr/share/wordlists/dirb/common.txt                            
===============================================================                                                
Gobuster v3.6                                                                                                  
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)                                                  
===============================================================                                                
[+] Url:                     http://192.168.62.62:80                                                           
[+] Method:                  GET                                                                               
[+] Threads:                 10                                                                                
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt                                              
[+] Negative Status codes:   404                                                                               
[+] User Agent:              gobuster/3.6                                                                      
[+] Timeout:                 10s
===============================================================                                                
Starting gobuster in directory enumeration mode
===============================================================                                                
/.hta                 (Status: 403) [Size: 278]
/.htaccess            (Status: 403) [Size: 278]
/.htpasswd            (Status: 403) [Size: 278]
/admin.php            (Status: 200) [Size: 2897]
/autobackup           (Status: 301) [Size: 319] [--> http://192.168.62.62/autobackup/]                         
/index.php            (Status: 200) [Size: 3326]
/server-status        (Status: 403) [Size: 278]
/static               (Status: 301) [Size: 315] [--> http://192.168.62.62/static/]                             
Progress: 4614 / 4615 (99.98%)
===============================================================                                                
Finished                                                   
===============================================================       
```

```bash
┌──(kali㉿gobots)-[20Sep2025 03:54:07]-[~]
└─$ gobuster dir -u http://192.168.62.62:80/autobackup/ -w /usr/share/wordlists/dirb/common.txt 
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.62.62:80/autobackup/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.hta                 (Status: 403) [Size: 278]
/.htpasswd            (Status: 403) [Size: 278]
/.htaccess            (Status: 403) [Size: 278]
/robots.txt           (Status: 403) [Size: 278]
Progress: 4614 / 4615 (99.98%)
===============================================================
Finished
===============================================================
```