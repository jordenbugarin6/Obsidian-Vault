```bash
┌──(kali㉿gobots)-[12Jun2024 16:33:28]-[~/SUT/Alchemy]
└─$ nikto -host 10.10.110.21:3000
- Nikto v2.5.0
---------------------------------------------------------------------------
+ Target IP:          10.10.110.21
+ Target Hostname:    10.10.110.21
+ Target Port:        3000
+ Start Time:         2024-06-12 16:33:38 (GMT0)
---------------------------------------------------------------------------
+ Server: No banner retrieved
+ /: The anti-clickjacking X-Frame-Options header is not present. See: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options
+ /: The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type. See: https://www.netsparker.com/web-vulnerability-scanner/vulnerabilities/missing-content-type-header/
+ /: Cookie lang created without the httponly flag. See: https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ /debug/: Possible debug directory/program found.
+ 8073 requests: 0 error(s) and 4 item(s) reported on remote host
+ End Time:           2024-06-12 16:38:34 (GMT0) (296 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested
```