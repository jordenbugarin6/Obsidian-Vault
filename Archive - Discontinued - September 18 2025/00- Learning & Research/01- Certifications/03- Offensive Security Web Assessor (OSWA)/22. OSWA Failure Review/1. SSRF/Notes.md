If `SSRF` is present you are able to by pass `authentication` because you are able to act as the internal sevrer to send requests. You are essentially `impersonating the server as a proxy`
 - in this picture we are essentially utilizing the `API Gateway` server to reach the `/files, /users, /render` endpoint and that redirects us internally
![[Pasted image 20250107133848.png]]

Notes:

`RCE` is not possible with `SSRF`, only able to read internal files. However if you are able to access an internal `/API` and create an `SSH` key you may be able to get `RCE`
- `double encoding` occurs when multiple systems have to process the data to read it 

- If you have `gobuster` results test those endpoints that were previously unreachable with the `SSRF` vulnerability
- need to create wordlist of endpoints that could exist from labs in OSA-WEB-200 tab