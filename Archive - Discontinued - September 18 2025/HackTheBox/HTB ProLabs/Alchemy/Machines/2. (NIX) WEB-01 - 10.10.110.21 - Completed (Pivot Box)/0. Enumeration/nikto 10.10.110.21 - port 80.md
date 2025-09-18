```bash
┌──(kali㉿gobots)-[12Jun2024 16:26:51]-[~/SUT/Alchemy]
└─$ nikto -host 10.10.110.21:80
- Nikto v2.5.0                                                                                        
---------------------------------------------------------------------------
+ Target IP:          10.10.110.21
+ Target Hostname:    10.10.110.21
+ Target Port:        80                        
+ Start Time:         2024-06-12 16:27:48 (GMT0)                                                      
---------------------------------------------------------------------------
+ Server: Rocket                                                                                      
+ No CGI Directories found (use '-C all' to force check all possible dirs)                            
+ .: The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type. See: https://www.netsparker.com/web-vulnerabil
ity-scanner/vulnerabilities/missing-content-type-header/
+ /login/: This might be interesting.
+ /status/: This might be interesting.
+ /store/: This might be interesting.
+ /#wp-config.php#: #wp-config.php# file found. This file contains the credentials.
+ 8076 requests: 0 error(s) and 5 item(s) reported on remote host
+ End Time:           2024-06-12 16:35:42 (GMT0) (474 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested                                                
```