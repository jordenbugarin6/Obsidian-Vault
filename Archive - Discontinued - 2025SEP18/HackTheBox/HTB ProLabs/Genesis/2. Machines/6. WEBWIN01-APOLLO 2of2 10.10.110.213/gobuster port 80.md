```bash
┌──(kali㉿gobots)-[06May2024 17:39:46]-[~/SUT/10.10.110.60]                                                                            
└─$ gobuster dir -u http://10.10.110.213 -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -x php,txt,html,asp,aspx                ===============================================================                                                                                  
Gobuster v3.6                                                                                                                                    
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)                                                                                    
===============================================================                                                                                  
[+] Url:                     http://10.10.110.213                                                                                               
[+] Method:                  GET                                                                                                                 
[+] Threads:                 10                                                                                                                  
[+] Wordlist:                /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt                                                        
[+] Negative Status codes:   404                                                                                                                 
[+] User Agent:              gobuster/3.6                                                                                                        
[+] Extensions:              html,asp,aspx,php,txt                                                                                               
[+] Timeout:                 10s                                                                                                                 
===============================================================                                                                                  
Starting gobuster in directory enumeration mode                                                                                                  
===============================================================                                                                                  
/.html                (Status: 403) [Size: 1046]                                                                                                 
/images               (Status: 301) [Size: 340] [--> http://10.10.110.213/images/]                                                               
/index.html           (Status: 200) [Size: 7781]                                                                                                 
/Images               (Status: 301) [Size: 340] [--> http://10.10.110.213/Images/]                                                               
/assets               (Status: 301) [Size: 340] [--> http://10.10.110.213/assets/]                                                               
/Index.html           (Status: 200) [Size: 7781]                                                                                                 
/examples             (Status: 503) [Size: 1060]                                                                                                 
/lang.php             (Status: 200) [Size: 381]                                                                                                  
/gr.php               (Status: 200) [Size: 9973]                                                                                                 
/flag.txt             (Status: 200) [Size: 16]                                                                                                   
/licenses             (Status: 403) [Size: 1205]                                                                                                 
/IMAGES               (Status: 301) [Size: 340] [--> http://10.10.110.213/IMAGES/]                                                               
/%20                  (Status: 403) [Size: 1046]                                                                                                 
/Assets               (Status: 301) [Size: 340] [--> http://10.10.110.213/Assets/]                                                               
/INDEX.html           (Status: 200) [Size: 7781]
/*checkout*           (Status: 403) [Size: 1046]
/*checkout*.txt       (Status: 403) [Size: 1046]
/*checkout*.php       (Status: 403) [Size: 1046]
/*checkout*.aspx      (Status: 403) [Size: 1046]
/*checkout*.html      (Status: 403) [Size: 1046]
/*checkout*.asp       (Status: 403) [Size: 1046]
/phpmyadmin           (Status: 403) [Size: 1046]
/webalizer            (Status: 403) [Size: 1046]
/*docroot*            (Status: 403) [Size: 1046]
```

# flag.txt
![[Pasted image 20240506141230.png]]
# gr.php
![[Pasted image 20240506141326.png]]
