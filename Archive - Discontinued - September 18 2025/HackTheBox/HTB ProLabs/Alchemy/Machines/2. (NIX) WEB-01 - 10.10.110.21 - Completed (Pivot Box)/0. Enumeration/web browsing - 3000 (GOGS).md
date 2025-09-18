`http://10.10.110.21:3000`
![[Pasted image 20240610145418.png]]
# Searchsploit
```bash
┌──(kali㉿gobots)-[10Jun2024 18:49:58]-[~]
└─$ searchsploit gogs  
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------- 
 Exploit Title                                                                                                       |  Path
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------- 
Gogs - 'label' SQL Injection                                                                                         | multiple/webapps/35237.txt
Gogs - 'users'/'repos' '?q' SQL Injection                                                                            | multiple/webapps/35238.txt
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------- 
Shellcodes: No Results
Papers: No Results
```
# Msfconsole
```bash
msf6 > search gogs

Matching Modules
================

   #  Name                                    Disclosure Date  Rank       Check  Description
   -  ----                                    ---------------  ----       -----  -----------
   0  exploit/multi/http/gitea_git_hooks_rce  2020-10-07       excellent  Yes    Gitea Git Hooks Remote Code Execution
   1  exploit/multi/http/gogs_git_hooks_rce   2020-10-07       excellent  Yes    Gogs Git Hooks Remote Code Execution


Interact with a module by name or index. For example info 1, use 1 or use exploit/multi/http/gogs_git_hooks_rce

msf6 > 
```
requires a password, possibly a dependency
```bash
msf6 exploit(multi/http/gogs_git_hooks_rce) > show options                                                                                                                                                   
                                                                                                                                                                                                             
Module options (exploit/multi/http/gogs_git_hooks_rce):                                                                                                                                                      
                                                                                                                                                                                                             
   Name       Current Setting  Required  Description                                                                                                                                                         
   ----       ---------------  --------  -----------                                                                                                                                                         
   PASSWORD                    yes       Password to use                                                                                                                                                     
   Proxies                     no        A proxy chain of format type:host:port[,type:host:port][...]                                                                                                        
   RHOSTS                      yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html                                                              
   RPORT      3000             yes       The target port (TCP)                                                                                                                                               
   SSL        false            no        Negotiate SSL/TLS for outgoing connections
   SSLCert                     no        Path to a custom SSL certificate (default is randomly generated)
   TARGETURI  /                yes       Base path
   URIPATH                     no        The URI to use for this exploit (default is random)
   USERNAME                    yes       Username to authenticate with
   VHOST                       no        HTTP server virtual host


   When CMDSTAGER::FLAVOR is one of auto,tftp,wget,curl,fetch,lwprequest,psh_invokewebrequest,ftp_http:

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   SRVHOST  0.0.0.0          yes       The local host or network interface to listen on. This must be an address on the local machine or 0.0.0.0 to listen on all addresses.
   SRVPORT  8080             yes       The local port to listen on.


Payload options (linux/x64/meterpreter/reverse_tcp):

   Name   Current Setting  Required  Description
   ----   ---------------  --------  -----------
   LHOST                   yes       The listen address (an interface may be specified)
   LPORT  4444             yes       The listen port

```