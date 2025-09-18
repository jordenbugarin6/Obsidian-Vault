found an exploitdb article leading to a path that could be vulnerable to sql injection
![[Pasted image 20240610151708.png]]
browsing to the location shows that it looks like data can be queried
![[Pasted image 20240610151755.png]]
# 1st SQLmap
```bash
┌──(kali㉿gobots)-[10Jun2024 19:15:06]-[~]                                                                                                                                                                  
└─$ sqlmap -u "http://10.10.110.21:3000/api/v1/users/search?q=" -p q                                                                                                                                        
        ___                                                                                                                                                                                                 
       __H__                                                                                                                                                                                                
 ___ ___[)]_____ ___ ___  {1.8.2#stable}                                                                                                                                                                    
|_ -| . [)]     | .'| . |                                                                                                                                                                                   
|___|_  [.]_|_|_|__,|  _|                                                                                                                                                                                   
      |_|V...       |_|   https://sqlmap.org                                                                                                                                                                
                                                                                                                                                                                                            
[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers as
sume no liability and are not responsible for any misuse or damage caused by this program                                                                                                                   

[*] starting @ 19:15:18 /2024-06-10/

[19:15:18] [WARNING] provided value for parameter 'q' is empty. Please, always use only valid parameter values so sqlmap could be able to run properly
[19:15:18] [INFO] testing connection to the target URL
you have not declared cookie(s), while server wants to set its own ('lang=en-US;i_like_gogs=19cce83f5f7e6c07;_csrf=GLoaTpFLdMX...NjQzMjY4MA'). Do you want to use those [Y/n] y
[19:15:23] [INFO] checking if the target is protected by some kind of WAF/IPS
[19:15:23] [INFO] testing if the target URL content is stable
[19:15:23] [INFO] target URL content is stable
[19:15:23] [WARNING] heuristic (basic) test shows that GET parameter 'q' might not be injectable
[19:15:23] [INFO] testing for SQL injection on GET parameter 'q'
[19:15:23] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause'
[19:15:24] [INFO] testing 'Boolean-based blind - Parameter replace (original value)'
[19:15:24] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'
[19:15:25] [INFO] testing 'PostgreSQL AND error-based - WHERE or HAVING clause'
[19:15:26] [INFO] testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (IN)'
[19:15:26] [INFO] testing 'Oracle AND error-based - WHERE or HAVING clause (XMLType)'
[19:15:27] [INFO] testing 'Generic inline queries'
[19:15:27] [INFO] testing 'PostgreSQL > 8.1 stacked queries (comment)'
[19:15:27] [WARNING] time-based comparison requires larger statistical model, please wait. (done)                                                                                                          
[19:15:27] [INFO] testing 'Microsoft SQL Server/Sybase stacked queries (comment)'
[19:15:28] [INFO] testing 'Oracle stacked queries (DBMS_PIPE.RECEIVE_MESSAGE - comment)'
[19:15:28] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
[19:15:29] [INFO] testing 'PostgreSQL > 8.1 AND time-based blind'
[19:15:30] [INFO] testing 'Microsoft SQL Server/Sybase time-based blind (IF)'
[19:15:30] [INFO] testing 'Oracle AND time-based blind'
it is recommended to perform only basic UNION tests if there is not at least one other (potential) technique found. Do you want to reduce the number of requests? [Y/n] n
[19:15:38] [INFO] testing 'Generic UNION query (NULL) - 1 to 10 columns'
[19:15:45] [WARNING] GET parameter 'q' does not seem to be injectable
[19:15:45] [CRITICAL] all tested parameters do not appear to be injectable. Try to increase values for '--level'/'--risk' options if you wish to perform more tests. If you suspect that there is some kind of protection mechanism involved (e.g. WAF) maybe you could try to use option '--tamper' (e.g. '--tamper=space2comment') and/or switch '--random-agent'

[*] ending @ 19:15:45 /2024-06-10/

```