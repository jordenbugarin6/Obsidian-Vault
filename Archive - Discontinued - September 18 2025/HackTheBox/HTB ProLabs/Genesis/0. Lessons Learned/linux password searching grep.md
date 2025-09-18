```bash
```bash
adam@DEV01-Ares:~$ cat /etc/group                                                                                          
root:x:0:                                                                                                                  
daemon:x:1:                                                                                                                
bin:x:2:                                                                                                                   
sys:x:3:                                                                                                                   
adm:x:4:syslog,adam                                                                                                        
```
members of the `adm` group are allowed to read `/var/log`
```bash
adam@DEV01-Ares:~$ grep -i password /var/log/apache2/access.log.*
10.10.14.3 - - [03/Dec/2020:09:06:26 +0000] "GET /login/?username=admin&password=8NJxgU2CtVsJYZE5 HTTP/1.1" 200 625 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:82.0) Gecko/20100101 Firefox/82.0"
10.10.14.3 - - [03/Dec/2020:09:06:26 +0000] "GET /login/?username=admin&password=$@#G34123421 HTTP/1.1" 200 625 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:82.0) Gecko/20100101 Firefox/82.0"
```
![[Pasted image 20240529170325.png]]
```