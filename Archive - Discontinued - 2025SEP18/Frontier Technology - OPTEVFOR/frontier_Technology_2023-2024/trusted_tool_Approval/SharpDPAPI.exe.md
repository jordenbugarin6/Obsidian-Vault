---
created_date: 27 September 2023
updated_date: 28 September 2023
type: windows
---

Ripped off of github https://github.com/GhostPack/SharpDPAPI
- Download ZIP
- moved to C:\Users\Administrator\Desktop\zipped executables 
![[Pasted image 20230927111445.png]]
Must be compiled as .NET 3.5 Framework
![[Pasted image 20230927112330.png]]
On Windows Server 2019 opened SharpDPAPi.sln file with Visual Studio 2019
![[Pasted image 20230927124355.png]]
Once it comes up in visual studio go Project > SharpDPAPI properties
![[Pasted image 20230927124459.png]]
Select chosen framework, in this instance 4.0 should be fine.
![[Pasted image 20230927124644.png]]
Change to release version and click start
![[Pasted image 20230927124817.png]]
After successful compilation the file was saved in `C:\Users\Administrator\Desktop\unzipped executables\SharpDPAPI-master\SharpDPAP\bin\Release\SharpDPAPI.exe`
![[Pasted image 20230927125322.png]]
File was saved in C:\Desktop\Recompiled .NET executables
![[Pasted image 20230927125648.png]]
Copying SharpDPAPI to file `C:\Users\Administrator\AppData\Local\Programs\Python\Python311\xfer'ing files` 
- because python isnt an environment variable need to copy file looking to transfer out of directory where python executable is being hosted.
![[Pasted image 20230927130355.png]]
Hosting Python HTTP server
```shell
python.exe -m http.server 8080
```
![[Pasted image 20230927130815.png]]
Navigated to URL of new .NET SharpDPAPI.exe & downloaded new SharpDPAPI.exe
![[Pasted image 20230927132110.png]]
Saved in ``/root/tooltesting/

in order to locate must update the mlocate database by running the command `updatedb`
- SharpDPAPI is now updated in lovate
![[Pasted image 20230927133424.png]]
Sha256sum of SharpDPAPI.exe 4.0 .NET framework.
```bash
[root💀~/tooltesting] [192.168.146.129] [2023-09-27 13:40:34] 
 └─╼ # sha256sum SharpDPAPI.exe 
3181ef16de0ba9f971c774b3b472716167bcbe1039bb8362dff32853ef0bb999  SharpDPAPI.exe
```
![[Pasted image 20230927134121.png]]

Triage used to pull path of Masterkey
```powershell
[09/27 14:20:08] beacon> execute-assembly /root/tooltesting/SharpDPAPI.exe triage /password:Password1
```
![[Pasted image 20230927144055.png]]
Triag'd all user which is just the administrator and pulled the masterkey for administrator
![[Pasted image 20230927144438.png]]
SharpDPAPI.exe machinetriage
- used to dump LSA secrets as System
```powershell
beacon> execute-assembly /root/tooltesting/SharpDPAPI.exe machinetriage
```
![[Pasted image 20230927145122.png]]
Dumped Administrator Private Key.
Also Triages:
- System Credentials
- System Vaults
- System Certificates
![[Pasted image 20230927145238.png]]
No abnormal traffic detected in Wireshark Conversations.
- 102.194.8.227 is the kali machine reaching out to an NTP server.
![[Pasted image 20230928094941.png]]
Normal beacon traffic, nothing anomalous
![[Pasted image 20230928095414.png]]
No abnormal changes to  registry via regshot
-  Attributes/Keys modified are native/natural to windows OS registry.
![[Pasted image 20230928095038.png]]
![[Pasted image 20230928095220.png]]
No anomolous activity in procmon
![[Pasted image 20230928103016.png]]