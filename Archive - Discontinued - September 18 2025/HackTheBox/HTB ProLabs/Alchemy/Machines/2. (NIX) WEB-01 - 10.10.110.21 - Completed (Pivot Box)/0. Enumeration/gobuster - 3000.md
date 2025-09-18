```bash
┌──(kali㉿gobots)-[12Jun2024 16:19:12]-[~/SUT/Alchemy]                                                                                                                                                      
└─$ gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://10.10.110.21:3000 -x php,txt,html,asp,aspx -t 50                                                                 
===============================================================                                                                                                                                             
Gobuster v3.6                                                                                                                                                                                               
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)                                                                                                                                               
===============================================================                                                                                                                                             
[+] Url:                     http://10.10.110.21:3000                                                                                                                                                       
[+] Method:                  GET                                                                                                                                                                            
[+] Threads:                 50                                                                                                                                                                             
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt                                                                                                                   
[+] Negative Status codes:   404                                                                                                                                                                            
[+] User Agent:              gobuster/3.6                                                                                                                                                                   
[+] Extensions:              html,asp,aspx,php,txt                                                                                                                                                          
[+] Timeout:                 10s                                                                                                                                                                            
===============================================================                                                                                                                                             
Starting gobuster in directory enumeration mode                                                                                                                                                             
===============================================================                                                                                                                                             
/img                  (Status: 302) [Size: 28] [--> /img/]                                                                                                                                                  
/admin                (Status: 302) [Size: 34] [--> /user/login]                                                                                                                                            
/assets               (Status: 302) [Size: 31] [--> /assets/]                                                                                                                                               
/issues               (Status: 302) [Size: 34] [--> /user/login]                                                                                                                                            
/plugins              (Status: 302) [Size: 32] [--> /plugins/]                                                                                                                                              
/css                  (Status: 302) [Size: 28] [--> /css/]                                                                                                                                                  
/avatars              (Status: 302) [Size: 32] [--> /avatars/]                                                                                                                                              
/js                   (Status: 302) [Size: 27] [--> /js/]     
```