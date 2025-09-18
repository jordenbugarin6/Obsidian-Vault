- instructor did some CORS the last 30 Mins of the `SSRF` request

when the instructor navigates to the `maliciouspage.html` and gives it a `URL` to fetch, in this case google `CORS` policy blocks it.
- CORS is enforced by the browser, if this were able to actually get to `google` then we'd be able to read your email
- By default `CORS` blocks a domain from interacting with a new domain
![[Pasted image 20250120201452.png]]
here we can see the `GET` request is sent, but `CORS` blocks the `Response` back with a 301 error
![[Pasted image 20250120201834.png]]this is `malicious.html` source code, and the highlighted portion is the portion that generates the error
- this line blocks the reading of the `JS` response - this is the purpose of `CORS`
![[Pasted image 20250120202032.png]]
when testing this against a regular `python3` server with this request it is still blocked by `CORS`
![[Pasted image 20250120202725.png]]
however if we look at the `python3` server we can see the request come through, but the response is blocked
![[Pasted image 20250120202822.png]]
now if a developer wants to allow `CORS` all they have to do is add the `Access-Control-Allow-Origin` header typically with a `*`  to whitelist every domain.
- `pythonwebserver.py` has the header active 
![[Pasted image 20250120221905.png]]
because this `pythonwebserver.py` has the header active we are able to access it without any issues with `CORS`
![[Pasted image 20250120222159.png]]
in `BURP` we can see the `HEADER` in the response which is how the `BROWSER` knows that `CORS` is allowing everything - However this header alone does not mean that it is vulnerable by itself - most of the time.
![[Pasted image 20250120222253.png]]
in order for `CORS` to be vulnerable it needs `Access-Control-Allow-Origin` as well as `Access-Control-Allow-Credentials` - this header tells tbrowsers that it is allowed to send cookies to other domains or not - if it is `true` that means that it is authenticated 
![[Pasted image 20250120222524.png]]
***ALL CORS EXPLOITS MUST BE AUTHENTICATED***
- so if there is only `Access-Control-Allow-Origin: *` and no `Access-Control-Allow-Credentials: true` that means that it is set to `FALSE` by default meaning it is not vulnerable to `CORS`
![[Pasted image 20250120222639.png]]
`CORS` alone cannot be set to multiple domains like this 
![[Pasted image 20250120222827.png]]
The server needs to add these headers so in order to get around this `DEVELOPERS` set the `Access-Control-Allow-Origin` to be set to the `ORIGIN`, this is shown in `pythonwebserverv2.py`
- this is how a website would be vulnerable to `CORS`
![[Pasted image 20250120223146.png]]
so when this is sent, this is what it looks like in `CORS`, we can see that the `Access-Control-Allow-Origin` is mimic'ing the `ORIGIN`
![[Pasted image 20250120223402.png]]now if we send it to `REPEATER` we can see that `test.com` is being repeated by being reflected - `THIS IS VULNERABLE TO CORS`
![[Pasted image 20250120223451.png]]
if `CORS` is vulnerable we can phish any authenticated user on their behalf its like `XSS` cross domain

#### CSRF NOTE
Browsers default to `LAX` meaning unless the developer sets it to `NONE` then `CSRF` and `PHISHING` users will be unaccessible by default
![[Pasted image 20250120224126.png]]