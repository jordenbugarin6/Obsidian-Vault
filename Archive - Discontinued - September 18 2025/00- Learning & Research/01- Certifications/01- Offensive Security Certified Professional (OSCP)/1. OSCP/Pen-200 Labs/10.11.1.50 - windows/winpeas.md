```powershell

C:\Windows\Tasks>winPEASx64.exe
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

  WinPEAS-ng by @carlospolopm

       /---------------------------------------------------------------------------------\
       |                             Do you like PEASS?                                  |
       |---------------------------------------------------------------------------------| 
       |         Get the latest version    :     https://github.com/sponsors/carlospolop |
       |         Follow on Twitter         :     @carlospolopm                           |
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
    Hostname: Bethany
 [!] Windows version not supported, build number: '9600'
    ProductName: Windows 8.1 Enterprise
    EditionID: Enterprise
    ReleaseId: 
    BuildBranch: 
    CurrentMajorVersionNumber: 
    CurrentVersion: 6.3
    Architecture: AMD64
    ProcessorCount: 3
    SystemLang: en-US
    KeyboardLang: English (United States)
    TimeZone: (UTC-08:00) Pacific Time (US & Canada)
    IsVirtualMachine: True
    Current Time: 3/5/2023 6:50:13 PM
    HighIntegrity: False
    PartOfDomain: False
    Hotfixes: KB2899189_Microsoft-Windows-CameraCodec-Package, KB2868626, KB2883200, KB2887595, KB2900986, KB2903939, KB2911106, KB2919355, KB2919394, KB2920189, KB2928680, KB2934520, KB2954879, KB2961072, KB2961908, KB2962806, KB2967917, KB2973351, KB2975061, KB2976978, KB2977765, KB2978041, KB2978126, KB2979576, KB2980654, KB2989930, KB2990967, KB2994290, KB3000850, KB3003057, KB3003667, KB3004361, KB3004365, KB3004394, KB3006137, KB3008242, KB3012199, KB3012235, KB3012702, KB3013172, KB3013410, KB3013531, KB3013538, KB3013791, KB3014442, KB3015696, KB3016074, KB3018133, KB3018467, KB3019215, KB3019978, KB3020338, KB3020370, KB3021910, KB3022777, KB3023222, KB3024751, KB3024755, KB3025417, KB3029432, KB3029438, KB3029603, KB3029606, KB3029803, KB3030377, KB3030947, KB3032663, KB3033446, KB3034348, KB3035017, KB3035126, KB3035132, KB3035527, KB3036612, KB3037579, KB3037924, KB3038002, KB3038562, KB3041857, KB3042085, KB3042553, KB3043812, KB3044374, KB3044673, KB3045171, KB3045634, KB3045685, KB3045717, KB3045719, KB3045755, KB3045992, KB3045999, KB3046002, KB3046359, KB3046480, KB3046737, KB3047254, KB3047255, KB3048043, KB3048778, KB3049989, KB3053863, KB3054169, KB3054256, KB3054464, KB3055323, KB3055642, KB3056347, KB3059316, KB3059317, KB3060383, KB3060793, KB3061421, KB3061468, KB3061512, KB3061518, KB3062760, KB3063843, KB3064059, KB3065822, KB3065988, KB3067505, KB3069392, KB3070102, KB3072630, KB3072633, KB3074886, KB3075516, KB3079777, KB3079904, KB3168965, 

  [?] Windows vulns search powered by Watson(https://github.com/rasta-mouse/Watson)

����������͹ Showing All Microsoft Updates
   HotFix ID                :   KB3168965
   Installed At (UTC)       :   3/30/2017 11:41:53 AM
   Title                    :   Security Update for Windows (KB3168965)
   Client Application ID    :   wusa
   Description              :   Fix for KB3168965

   =================================================================================================


����������͹ System Last Shutdown Date/time (from Registry)

    Last Shutdown Date/time        :    2/10/2020 8:46:06 PM

����������͹ User Environment Variables
� Check for some passwords or keys in the env variables 
    COMPUTERNAME: BETHANY
    PSExecutionPolicyPreference: Bypass
    HOMEPATH: \Users\Bethany
    LOCALAPPDATA: C:\Users\Bethany\AppData\Local
    PSModulePath: C:\Users\Bethany\Documents\WindowsPowerShell\Modules;C:\Program Files (x86)\WindowsPowerShell\Modules;C:\Windows\system32\WindowsPowerShell\v1.0\Modules\
    PROCESSOR_ARCHITECTURE: AMD64
    Path: C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\
    CommonProgramFiles(x86): C:\Program Files (x86)\Common Files
    ProgramFiles(x86): C:\Program Files (x86)
    PROCESSOR_LEVEL: 25
    LOGONSERVER: \\BETHANY
    PATHEXT: .COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC;.CPL
    HOMEDRIVE: C:
    SystemRoot: C:\Windows
    ALLUSERSPROFILE: C:\ProgramData
    PUBLIC: C:\Users\Public
    FP_NO_HOST_CHECK: NO
    APPDATA: C:\Users\Bethany\AppData\Roaming
    PROCESSOR_REVISION: 0101
    USERNAME: Bethany
    CommonProgramW6432: C:\Program Files\Common Files
    USERPROFILE: C:\Users\Bethany
    CommonProgramFiles: C:\Program Files\Common Files
    OS: Windows_NT
    USERDOMAIN_ROAMINGPROFILE: Bethany
    PROCESSOR_IDENTIFIER: AMD64 Family 25 Model 1 Stepping 1, AuthenticAMD
    ComSpec: C:\Windows\system32\cmd.exe
    PROMPT: $P$G
    SystemDrive: C:
    TEMP: C:\Users\Bethany\AppData\Local\Temp
    ProgramFiles: C:\Program Files
    NUMBER_OF_PROCESSORS: 3
    TMP: C:\Users\Bethany\AppData\Local\Temp
    ProgramData: C:\ProgramData
    ProgramW6432: C:\Program Files
    windir: C:\Windows
    USERDOMAIN: Bethany

����������͹ System Environment Variables
� Check for some passwords or keys in the env variables 
    ComSpec: C:\Windows\system32\cmd.exe
    FP_NO_HOST_CHECK: NO
    NUMBER_OF_PROCESSORS: 3
    OS: Windows_NT
    Path: C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\
    PATHEXT: .COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC
    PROCESSOR_ARCHITECTURE: AMD64
    PROCESSOR_IDENTIFIER: AMD64 Family 25 Model 1 Stepping 1, AuthenticAMD
    PROCESSOR_LEVEL: 25
    PROCESSOR_REVISION: 0101
    PSModulePath: C:\Windows\system32\WindowsPowerShell\v1.0\Modules\
    TEMP: C:\Windows\TEMP
    TMP: C:\Windows\TEMP
    USERNAME: SYSTEM
    windir: C:\Windows

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
    Some AV was detected, search for bypasses
    Name: Windows Defender
    ProductEXE: %ProgramFiles%\Windows Defender\MSASCui.exe
    pathToSignedReportingExe: %ProgramFiles%\Windows Defender\MsMpeng.exe

����������͹ Windows Defender configuration
  Local Settings
  Group Policy Settings

����������͹ UAC Status
� If you are in the Administrators group check how to bypass the UAC https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#basic-uac-bypass-full-file-system-access
    ConsentPromptBehaviorAdmin: 0 - No prompting
    EnableLUA: 0
    LocalAccountTokenFilterPolicy: 1
    FilterAdministratorToken: 0
      [*] EnableLUA != 1, UAC policies disabled.
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
    SecureProtocols: 2688
    PrivacyAdvanced: 0
    DisableCachingOfSSLPages: 0
    WarnonZoneCrossing: 0
    CertificateRevocation: 1
    EnableNegotiate: 1
    MigrateProxy: 1
    ProxyEnable: 0
    SyncMode5: 3

����������͹ HKLM Internet Settings
    CodeBaseSearchPath: CODEBASE
    EnablePunycode: 1
    WarnOnIntranet: 1
    MinorVersion: 0
    ActiveXCache: C:\Windows\Downloaded Program Files

����������͹ Drives Information
� Remember that you should search more info inside the other drives 
    C:\ (Type: Fixed)(Volume label: HDD)(Filesystem: NTFS)(Available space: 13 GB)(Permissions: Authenticated Users [AppendData/CreateDirectories])
    D:\ (Type: CDRom)

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
    Notification Packages                :       scecli
    Authentication Packages              :       msv1_0
    LsaPid                               :       524
    SecureBoot                           :       1
    ProductType                          :       4
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
   4.5.51650

  .NET & AMSI (Anti-Malware Scan Interface) support
      .NET version supports AMSI     : False
      OS supports AMSI               : False


�����������������������������������͹ Interesting Events information �������������������������������������

����������͹ Printing Explicit Credential Events (4648) for last 30 days - A process logged on using plaintext credentials

      You must be an administrator to run this check

����������͹ Printing Account Logon Events (4624) for the last 10 days.

      You must be an administrator to run this check

����������͹ Process creation events - searching logs (EID 4688) for sensitive data.

      You must be an administrator to run this check

����������͹ PowerShell events - script block logs (EID 4104) - searching for sensitive data.


����������͹ Displaying Power off/on events for last 5 days



�����������������������������������͹ Users Information �������������������������������������

����������͹ Users
� Check if you have some admin equivalent privileges https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#users-and-groups
  Current user: Bethany
  Current groups: Domain Users, Everyone, Users, Interactive, Console Logon, Authenticated Users, This Organization, Local account, Local, NTLM Authentication
   =================================================================================================

    Bethany\Administrator(Disabled): Built-in account for administering the computer/domain
        |->Groups: Administrators
        |->Password: CanChange-NotExpi-Req

    Bethany\alice
        |->Groups: Administrators
        |->Password: CanChange-NotExpi-NotReq

    Bethany\Bethany
        |->Groups: Users
        |->Password: CanChange-NotExpi-Req

    Bethany\Guest(Disabled): Built-in account for guest access to the computer/domain
        |->Groups: Guests
        |->Password: NotChange-NotExpi-NotReq


����������͹ Current User Idle Time
   Current User   :     Bethany\Bethany
   Idle Time      :     13h:39m:18s:515ms

����������͹ Display Tenant information (DsRegCmd.exe /status)

����������͹ Current Token privileges
� Check if you can escalate privilege using some enabled token https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#token-manipulation
    SeShutdownPrivilege: DISABLED
    SeChangeNotifyPrivilege: SE_PRIVILEGE_ENABLED_BY_DEFAULT, SE_PRIVILEGE_ENABLED
    SeUndockPrivilege: DISABLED
    SeIncreaseWorkingSetPrivilege: DISABLED
    SeTimeZonePrivilege: DISABLED

����������͹ Clipboard text

����������͹ Logged users
    Bethany\Bethany
    Bethany\alice

����������͹ Display information about local users
   Computer Name           :   BETHANY
   User Name               :   Administrator
   User Id                 :   500
   Is Enabled              :   False
   User Type               :   Administrator
   Comment                 :   Built-in account for administering the computer/domain
   Last Logon              :   8/22/2013 7:47:09 AM
   Logons Count            :   1
   Password Last Set       :   8/22/2013 6:47:16 AM

   =================================================================================================

   Computer Name           :   BETHANY
   User Name               :   alice
   User Id                 :   1001
   Is Enabled              :   True
   User Type               :   Administrator
   Comment                 :   
   Last Logon              :   3/5/2023 6:50:00 PM
   Logons Count            :   81
   Password Last Set       :   6/1/2016 11:43:40 PM

   =================================================================================================

   Computer Name           :   BETHANY
   User Name               :   Bethany
   User Id                 :   1002
   Is Enabled              :   True
   User Type               :   User
   Comment                 :   
   Last Logon              :   10/7/2022 7:02:36 AM
   Logons Count            :   56
   Password Last Set       :   11/15/2014 9:11:33 AM

   =================================================================================================

   Computer Name           :   BETHANY
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
    SessID    pSessionName   pUserName      pDomainName              State     SourceIP
    1         Console        Bethany        Bethany                  Active    

����������͹ Ever logged users
    IIS APPPOOL\DefaultAppPool
    Bethany\Bethany
    Bethany\alice

����������͹ Home folders found
    C:\Users\alice
    C:\Users\All Users
    C:\Users\Bethany : Bethany [AllAccess]
    C:\Users\Default
    C:\Users\Default User
    C:\Users\DefaultAppPool
    C:\Users\Public : Interactive [WriteData/CreateFiles], Bethany [AllAccess]

����������͹ Looking for AutoLogon credentials
    Some AutoLogon credentials were found
    DefaultDomainName             :  BETHANY
    DefaultUserName               :  bethany

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

    Domain: Bethany
    SID: S-1-5-21-471342483-1622715373-4132421626
    MaxPasswordAge: 42.00:00:00
    MinPasswordAge: 00:00:00
    MinPasswordLength: 0
    PasswordHistoryLength: 0
    PasswordProperties: 0
   =================================================================================================


����������͹ Print Logon Sessions
    Method:                       WMI
    Logon Server:                 
    Logon Server Dns Domain:      
    Logon Id:                     83859
    Logon Time:                   
    Logon Type:                   0
    Start Time:                   12/31/1600 4:00:00 PM
    Domain:                       Bethany
    Authentication Package:       
    Start Time:                   12/31/1600 4:00:00 PM
    User Name:                    Bethany
    User Principal Name:          
    User SID:                     

   =================================================================================================



�����������������������������������͹ Processes Information �������������������������������������

����������͹ Vulnerable Leaked Handlers
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation/leaked-handle-exploitation


�����������������������������������͹ Services Information �������������������������������������

����������͹ Interesting Services -non Microsoft-
� Check if you can overwrite some service binary or perform a DLL hijacking, also check for unquoted paths https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#services
    chdha({738C480B-AE5C-41EA-8873-774354515E62})[C:\Windows\chdha.exe] - Manual - Stopped
   =================================================================================================

    ibqtfq({8F3DD79D-D278-4288-B565-A77272356637})[C:\Windows\ibqtfq.exe] - Manual - Stopped
   =================================================================================================

    VGAuthService(VMware, Inc. - VMware Alias Manager and Ticket Service)["C:\Program Files\VMware\VMware Tools\VMware VGAuth\VGAuthService.exe"] - Auto - Running
    Alias Manager and Ticket Service
   =================================================================================================

    VMTools(VMware, Inc. - VMware Tools)["C:\Program Files\VMware\VMware Tools\vmtoolsd.exe"] - Auto - Running
    Provides support for synchronizing objects between the host and guest operating systems.
   =================================================================================================

    VMware Physical Disk Helper Service(VMware, Inc. - VMware Physical Disk Helper Service)["C:\Program Files\VMware\VMware Tools\vmacthlp.exe"] - Auto - Running
    Enables support for running virtual machines from a physical disk partition
   =================================================================================================


����������͹ Modifiable Services
� Check if you can modify any service https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#services
    LOOKS LIKE YOU CAN MODIFY OR START/STOP SOME SERVICE/s:
    wcncsvc: GenericExecute (Start/Stop)

����������͹ Looking if you can modify any service registry
� Check if you can modify the registry of a service https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#services-registry-permissions
    [-] Looks like you cannot change the registry of any service...

����������͹ Checking write permissions in PATH folders (DLL Hijacking)
� Check for DLL Hijacking in PATH folders https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#dll-hijacking
    C:\Windows\system32
    C:\Windows
    C:\Windows\System32\Wbem
    C:\Windows\System32\WindowsPowerShell\v1.0\


�����������������������������������͹ Applications Information �������������������������������������

����������͹ Current Active Window Application
    PowerUp - Notepad

����������͹ Installed Applications --Via Program Files/Uninstall registry--
� Check if you can modify installed software https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#software
    C:\Program Files\7-Zip
    C:\Program Files\Common Files
    C:\Program Files\desktop.ini
    C:\Program Files\Internet Explorer
    C:\Program Files\Uninstall Information
    C:\Program Files\VMware
    C:\Program Files\Windows Defender
    C:\Program Files\Windows Journal
    C:\Program Files\Windows Mail
    C:\Program Files\Windows Media Player
    C:\Program Files\Windows Multimedia Platform
    C:\Program Files\Windows NT
    C:\Program Files\Windows Photo Viewer
    C:\Program Files\Windows Portable Devices
    C:\Program Files\Windows Sidebar
    C:\Program Files\WindowsApps
    C:\Program Files\WindowsPowerShell


����������͹ Autorun Applications
� Check if you can modify other users AutoRuns binaries (Note that is normal that you can modify HKCU registry and binaries indicated there) https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation/privilege-escalation-with-autorun-binaries

    RegPath: HKLM\Software\Microsoft\Windows\CurrentVersion\Run
    Key: VMware User Process
    Folder: C:\Program Files\VMware\VMware Tools
    File: C:\Program Files\VMware\VMware Tools\vmtoolsd.exe -n vmusr (Unquoted and Space detected)
   =================================================================================================


    RegPath: HKLM\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Run
    Key: Adobe Reader Speed Launcher
    Folder: C:\Program Files (x86)\Adobe\Reader 8.0\Reader
    File: C:\Program Files (x86)\Adobe\Reader 8.0\Reader\Reader_sl.exe (Unquoted and Space detected)
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
    Key: msacm.l3acm
    Folder: C:\Windows\System32
    File: C:\Windows\System32\l3codeca.acm
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
    Key: msacm.l3acm
    Folder: C:\Windows\SysWOW64
    File: C:\Windows\SysWOW64\l3codeca.acm
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
    Key: vidc.cvid
    Folder: None (PATH Injection)
    File: iccvid.dll
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
    FolderPerms: Authenticated Users [AppendData/CreateDirectories]
    File: /UserInstall
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Active Setup\Installed Components\{44BBA840-CC51-11CF-AAFA-00AA00B6015C}
    Key: StubPath
    Folder: C:\Program Files\Windows Mail
    File: C:\Program Files\Windows Mail\WinMail.exe OCInstallUserConfigOE (Unquoted and Space detected)
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


    Folder: C:\Users\Bethany\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup
    FolderPerms: Bethany [AllAccess]
    File: C:\Users\Bethany\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\desktop.ini (Unquoted and Space detected)
    FilePerms: Bethany [AllAccess]
   =================================================================================================


    Folder: C:\Users\Bethany\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup
    FolderPerms: Bethany [AllAccess]
    File: C:\Users\Bethany\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\HFS.lnk (Unquoted and Space detected)
    FilePerms: Bethany [AllAccess]
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
    (Bethany\Bethany) Boot to Desktop: C:\Windows\explorer.exe 
    Trigger: At log on of Bethany\Bethany
    
   =================================================================================================


����������͹ Device Drivers --Non Microsoft--
� Check 3rd party drivers for known vulnerabilities/rootkits. https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#vulnerable-drivers
    VMware PCI VMCI Bus Device - 9.7.1.0 build-2103963 [VMware, Inc.]: \\.\GLOBALROOT\SystemRoot\System32\drivers\vmci.sys
    VMware vSockets Service - 9.7.0.0 build-2103963 [VMware, Inc.]: \\.\GLOBALROOT\SystemRoot\system32\drivers\vsock.sys
    VMware Raw Disk Helper Driver - 0.9.9.0 build-3917699 [VMware, Inc.]: C:\Program Files\VMware\VMware Tools\vmrawdsk.sys
    VMware HGFS File System Driver - 11.0.0.0 build-3917699 [VMware, Inc.]: \\.\GLOBALROOT\SystemRoot\system32\drivers\vmhgfs.sys
    VMware Pointing PS/2 Device Driver - 12.5.4.0 build-2869231 [VMware, Inc.]: \\.\GLOBALROOT\SystemRoot\System32\drivers\vmmouse.sys
    VMware SVGA 3D - 8.15.01.0046 - build-3774095 [VMware, Inc.]: \\.\GLOBALROOT\SystemRoot\system32\DRIVERS\vm3dmp.sys
    VMware server memory controller - 7.3.5.0 build-3917699 [VMware, Inc.]: C:\Program Files\Common Files\VMware\Drivers\memctl\vmmemctl.sys
    Macrovision SECURITY Driver - SECURITY Driver 4.03.086 2006/09/13 [Macrovision Corporation, Macrovision Europe Limited, and Macrovision Japan and Asia K.K.]: \\.\GLOBALROOT\SystemRoot\System32\Drivers\secdrv.SYS
    Intel(R) Gigabit Adapter - 12.6.47.0 [Intel Corporation]: \\.\GLOBALROOT\SystemRoot\system32\DRIVERS\e1i63x64.sys


�����������������������������������͹ Network Information �������������������������������������

����������͹ Network Shares
    ADMIN$ (Path: C:\Windows)
    C$ (Path: C:\)
    IPC$ (Path: )
    print$ (Path: C:\Windows\system32\spool\drivers)
    Public (Path: C:\Users\Public)
    Users (Path: C:\Users) -- Permissions: AllAccess

����������͹ Enumerate Network Mapped Drives (WMI)

����������͹ Host File
    127.0.0.1  win8.ipv6.microsoft.com

����������͹ Network Ifaces and known hosts
� The masks are only for the IPv4 addresses 
  [X] Exception: The requested protocol has not been configured into the system, or no implementation for it exists
    Ethernet 2[00:50:56:86:8D:49]: 10.11.1.50 / 255.255.0.0
        Gateways: 10.11.0.1
        DNSs: 10.11.1.1
    Loopback Pseudo-Interface 1[]: 127.0.0.1, ::1 / 255.0.0.0
        DNSs: fec0:0:0:ffff::1%1, fec0:0:0:ffff::2%1, fec0:0:0:ffff::3%1

����������͹ Current TCP Listening Ports
� Check for services restricted from the outside 
  Enumerating IPv4 connections

  Protocol   Local Address         Local Port    Remote Address        Remote Port     State             Process ID      Process Name

  TCP        0.0.0.0               80            0.0.0.0               0               Listening         4               System
  TCP        0.0.0.0               135           0.0.0.0               0               Listening         640             svchost
  TCP        0.0.0.0               445           0.0.0.0               0               Listening         4               System
  TCP        0.0.0.0               9505          0.0.0.0               0               Listening         2088            C:\HFS\hfs.exe
  TCP        0.0.0.0               49152         0.0.0.0               0               Listening         420             wininit
  TCP        0.0.0.0               49153         0.0.0.0               0               Listening         840             svchost
  TCP        0.0.0.0               49154         0.0.0.0               0               Listening         864             svchost
  TCP        0.0.0.0               49155         0.0.0.0               0               Listening         772             spoolsv
  TCP        0.0.0.0               49156         0.0.0.0               0               Listening         516             services
  TCP        0.0.0.0               49157         0.0.0.0               0               Listening         524             lsass
  TCP        10.11.1.50            139           0.0.0.0               0               Listening         4               System
  TCP        10.11.1.50            49268         192.168.119.147       1111            Established       824             C:\Windows\SysWOW64\WindowsPowerShell\v1.0\powershell.exe
  TCP        10.11.1.50            49269         192.168.119.147       1111            Close Wait        3188            C:\Windows\SysWOW64\WindowsPowerShell\v1.0\powershell.exe
  TCP        10.11.1.50            49297         192.168.119.147       1111            Close Wait        2284            C:\Windows\SysWOW64\WindowsPowerShell\v1.0\powershell.exe
  TCP        10.11.1.50            49367         192.168.119.147       1111            Close Wait        3308            C:\Windows\SysWOW64\WindowsPowerShell\v1.0\powershell.exe
  TCP        10.11.1.50            49387         192.168.119.147       1111            Close Wait        1468            C:\Windows\SysWOW64\WindowsPowerShell\v1.0\powershell.exe
  TCP        10.11.1.50            49434         192.168.119.133       1234            Close Wait        2684            
  TCP        10.11.1.50            49471         192.168.119.147       1111            Close Wait        1640            C:\Windows\SysWOW64\WindowsPowerShell\v1.0\powershell.exe
  TCP        10.11.1.50            49541         192.168.119.133       1234            Close Wait        3956            
  TCP        10.11.1.50            49561         192.168.119.133       4234            Close Wait        3636            C:\Users\Bethany\Desktop\shell.exe
  TCP        10.11.1.50            49582         192.168.119.133       1234            Established       2644            
  TCP        10.11.1.50            49602         192.168.119.147       1111            Established       2524            C:\Windows\SysWOW64\WindowsPowerShell\v1.0\powershell.exe
  TCP        10.11.1.50            49623         192.168.119.147       443             Established       2524            C:\Windows\SysWOW64\WindowsPowerShell\v1.0\powershell.exe

  Enumerating IPv6 connections

  Protocol   Local Address                               Local Port    Remote Address                              Remote Port     State             Process ID      Process Name

  TCP        [::]                                        80            [::]                                        0               Listening         4               System
  TCP        [::]                                        135           [::]                                        0               Listening         640             svchost
  TCP        [::]                                        445           [::]                                        0               Listening         4               System
  TCP        [::]                                        49152         [::]                                        0               Listening         420             wininit
  TCP        [::]                                        49153         [::]                                        0               Listening         840             svchost
  TCP        [::]                                        49154         [::]                                        0               Listening         864             svchost
  TCP        [::]                                        49155         [::]                                        0               Listening         772             spoolsv
  TCP        [::]                                        49156         [::]                                        0               Listening         516             services
  TCP        [::]                                        49157         [::]                                        0               Listening         524             lsass

����������͹ Current UDP Listening Ports
� Check for services restricted from the outside 
  Enumerating IPv4 connections

  Protocol   Local Address         Local Port    Remote Address:Remote Port     Process ID        Process Name

  UDP        0.0.0.0               5355          *:*                            320               svchost
  UDP        10.11.1.50            137           *:*                            4                 System
  UDP        10.11.1.50            138           *:*                            4                 System

  Enumerating IPv6 connections

  Protocol   Local Address                               Local Port    Remote Address:Remote Port     Process ID        Process Name


����������͹ Firewall Rules
� Showing only DENY rules (too many ALLOW rules always) 
    Current Profiles: PUBLIC
    FirewallEnabled (Domain):    True
    FirewallEnabled (Private):    True
    FirewallEnabled (Public):    True
    DENY rules:
  [X] Exception: Object reference not set to an instance of an object.

����������͹ DNS cached --limit 70--
    Entry                                 Name                                  Data
    1.0.0.127.in-addr.arpa                1.0.0.127.in-addr.arpa.               win8.ipv6.microsoft.com
    win8.ipv6.microsoft.com               win8.ipv6.microsoft.com               127.0.0.1
    win8.ipv6.microsoft.com                                                     

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
  HKCU        SecureProtocols                           2688
  HKCU        PrivacyAdvanced                           0
  HKCU        DisableCachingOfSSLPages                  0
  HKCU        WarnonZoneCrossing                        0
  HKCU        CertificateRevocation                     1
  HKCU        EnableNegotiate                           1
  HKCU        MigrateProxy                              1
  HKCU        ProxyEnable                               0
  HKCU        SyncMode5                                 3
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
    Not Found

����������͹ Checking Credential manager
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#credentials-manager-windows-vault
    [!] Warning: if password contains non-printable characters, it will be printed as unicode base64 encoded string


     Username:              Bethany\Bethany
     Password:               ihavepasswords3
     Target:                Bethany\Bethany
     PersistenceType:       Enterprise
     LastWriteTime:         11/15/2014 9:16:13 AM

   =================================================================================================


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
    MasterKey: C:\Users\Bethany\AppData\Roaming\Microsoft\Protect\S-1-5-21-471342483-1622715373-4132421626-1002\0678b095-fa72-44be-a8f5-b4fbe2eb6f65
    Accessed: 3/5/2023 5:37:57 AM
    Modified: 3/5/2023 5:37:57 AM
   =================================================================================================

    MasterKey: C:\Users\Bethany\AppData\Roaming\Microsoft\Protect\S-1-5-21-471342483-1622715373-4132421626-1002\0b50e251-01ef-4716-b406-7ab16e47c25a
    Accessed: 7/20/2015 4:33:03 PM
    Modified: 7/20/2015 4:33:03 PM
   =================================================================================================

    MasterKey: C:\Users\Bethany\AppData\Roaming\Microsoft\Protect\S-1-5-21-471342483-1622715373-4132421626-1002\100f964d-31ab-4fa2-a661-40d27665ddd9
    Accessed: 2/10/2020 2:16:46 PM
    Modified: 2/10/2020 2:16:46 PM
   =================================================================================================

    MasterKey: C:\Users\Bethany\AppData\Roaming\Microsoft\Protect\S-1-5-21-471342483-1622715373-4132421626-1002\355e0c19-729c-482e-85f1-13938ae08214
    Accessed: 11/15/2014 9:15:00 AM
    Modified: 11/15/2014 9:15:00 AM
   =================================================================================================

    MasterKey: C:\Users\Bethany\AppData\Roaming\Microsoft\Protect\S-1-5-21-471342483-1622715373-4132421626-1002\86c37806-3ab9-4cf1-86c2-dc2473a5d156
    Accessed: 4/2/2016 4:10:09 PM
    Modified: 4/2/2016 4:10:09 PM
   =================================================================================================

    MasterKey: C:\Users\Bethany\AppData\Roaming\Microsoft\Protect\S-1-5-21-471342483-1622715373-4132421626-1002\8ca5a987-13fa-4f9c-b4de-0b2d72ddf364
    Accessed: 12/7/2015 7:23:36 PM
    Modified: 12/7/2015 7:23:36 PM
   =================================================================================================

    MasterKey: C:\Users\Bethany\AppData\Roaming\Microsoft\Protect\S-1-5-21-471342483-1622715373-4132421626-1002\afc76b1a-0753-47fd-9cb4-86c82e1897f7
    Accessed: 3/29/2017 9:38:48 PM
    Modified: 3/29/2017 9:38:48 PM
   =================================================================================================

    MasterKey: C:\Users\Bethany\AppData\Roaming\Microsoft\Protect\S-1-5-21-471342483-1622715373-4132421626-1002\d87380bd-27bf-42a1-892d-613d48a061c9
    Accessed: 1/17/2018 1:55:42 AM
    Modified: 1/17/2018 1:55:42 AM
   =================================================================================================

    MasterKey: C:\Users\Bethany\AppData\Roaming\Microsoft\Protect\S-1-5-21-471342483-1622715373-4132421626-1002\d987b36e-3781-417d-970d-ebe5f9900793
    Accessed: 3/24/2022 8:15:53 AM
    Modified: 3/24/2022 8:15:53 AM
   =================================================================================================

    MasterKey: C:\Users\Bethany\AppData\Roaming\Microsoft\Protect\S-1-5-21-471342483-1622715373-4132421626-1002\e3a4484d-a233-4545-860d-294149a3a850
    Accessed: 10/7/2022 7:04:47 AM
    Modified: 10/7/2022 7:04:47 AM
   =================================================================================================

    MasterKey: C:\Users\Bethany\AppData\Roaming\Microsoft\Protect\S-1-5-21-471342483-1622715373-4132421626-1002\fbd1319f-d18d-448f-92e2-287944ecf24c
    Accessed: 2/27/2015 4:27:24 PM
    Modified: 2/27/2015 4:27:24 PM
   =================================================================================================


����������͹ Checking for DPAPI Credential Files
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#dpapi
    CredFile: C:\Users\Bethany\AppData\Local\Microsoft\Credentials\DFBE70A7E5CC19A398EBF1B96859CE5D
    Description: Local Credential Data
    MasterKey: fbd1319f-d18d-448f-92e2-287944ecf24c
    Accessed: 3/29/2015 6:50:00 PM
    Modified: 3/29/2015 6:50:00 PM
    Size: 3408
   =================================================================================================

    CredFile: C:\Users\Bethany\AppData\Roaming\Microsoft\Credentials\AB5B1AB1FFB5FA3EBDDAABF4409A0D25
    Description: Enterprise Credential Data
    MasterKey: 355e0c19-729c-482e-85f1-13938ae08214
    Accessed: 11/15/2014 9:16:13 AM
    Modified: 11/15/2014 9:16:13 AM
    Size: 506
   =================================================================================================

� Follow the provided link for further instructions in how to decrypt the creds file

����������͹ Checking for RDCMan Settings Files
� Dump credentials from Remote Desktop Connection Manager https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#remote-desktop-credential-manager
    Not Found

����������͹ Looking for Kerberos tickets
�  https://book.hacktricks.xyz/pentesting/pentesting-kerberos-88
    Not Found

����������͹ Looking for saved Wifi credentials
  [X] Exception: The service has not been started
Enumerating WLAN using wlanapi.dll failed, trying to enumerate using 'netsh'
No saved Wifi credentials found

����������͹ Looking AppCmd.exe
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#appcmd-exe
    AppCmd.exe was found in C:\Windows\system32\inetsrv\appcmd.exe
      You must be an administrator to run this check

����������͹ Looking SSClient.exe
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#scclient-sccm
    Not Found

����������͹ Enumerating SSCM - System Center Configuration Manager settings

����������͹ Enumerating Security Packages Credentials
  Version: NetNTLMv2
  Hash:    Bethany::Bethany:1122334455667788:6087a09d04757a311ec72c741690d4b0:010100000000000094454b62d64fd901faac996b0b182d04000000000800300030000000000000000000000000200000dc2a741d9e35a0f382b688a49871bb85d8a0df0348a782cf2607add48aa7f8be0a00100000000000000000000000000000000000090000000000000000000000

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
    Not Found

����������͹ Looking for GET credentials in IE history
�  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#browsers-history
    Not Found

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

    SID: S-1-5-21-471342483-1622715373-4132421626-1001
   =================================================================================================

    SID: S-1-5-21-471342483-1622715373-4132421626-1002
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
    Not Found

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
     C:\Users\Bethany\AppData\Local\Temp\{18410E84-9B37-4EC9-8D03-83912AD683CD}.tmp
     C:\Users\Bethany\AppData\Local\Packages\winstore_cw5n1h2txyewy\AC\INetCookies
     C:\Users\Bethany\AppData\Local\Packages\winstore_cw5n1h2txyewy\AC\INetCache
     C:\Users\Bethany\AppData\Local\Packages\winstore_cw5n1h2txyewy\AC\AppCache
     C:\Users\Bethany\AppData\Local\Packages\winstore_cw5n1h2txyewy\AC\AppCache\UC3WF8XB
     C:\Users\Bethany\AppData\Local\Packages\winstore_cw5n1h2txyewy\AC\AppCache\UC3WF8XB\1
     C:\Users\Bethany\AppData\Local\Packages\windows_ie_ac_001\AC\INetHistory
     C:\Users\Bethany\AppData\Local\Packages\windows_ie_ac_001\AC\INetCookies
     C:\Users\Bethany\AppData\Local\Packages\windows_ie_ac_001\AC\INetCache
     C:\Users\Bethany\AppData\Local\Packages\windows_ie_ac_001\AC\iecompatuaCache
     C:\Users\Bethany\AppData\Local\Packages\windows_ie_ac_001\AC\IECompatCache
     C:\Users\Bethany\AppData\Local\Packages\windows_ie_ac_001\AC\AppCache
     C:\Users\Bethany\AppData\Local\Packages\windows_ie_ac_001\AC\AppCache\A10YV5Q0

����������͹ Searching interesting files in other users home directories (can be slow)

     Checking folder: c:\users\alice

   =================================================================================================


����������͹ Searching executable files in non-default folders with write (equivalent) permissions (can be slow)
     File Permissions "C:\Alice's Stuff\avast_free_antivirus_setup.exe": Authenticated Users [WriteData/CreateFiles]
     File Permissions "C:\Users\Bethany\Downloads\jre-6u3-windows-i586-p-s.exe": Interactive [WriteData/CreateFiles]
     File Permissions "C:\Users\Bethany\Downloads\AdbeRdr811_en_US.exe": Interactive [WriteData/CreateFiles]
     File Permissions "C:\Users\Bethany\Desktop\winPEASx64.exe": Bethany [AllAccess]
     File Permissions "C:\Users\Bethany\Desktop\shell.exe": Bethany [AllAccess]
     File Permissions "C:\Users\Bethany\Desktop\PowerUp.ps1": Bethany [AllAccess]
     File Permissions "C:\Users\Bethany\AppData\Local\Programs\Opera\launcher.exe": Bethany [AllAccess]
     File Permissions "C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\I088V4J9\winPEASx64[1].exe": Bethany [AllAccess]
     File Permissions "C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\I088V4J9\PowerUp[1].ps1": Bethany [AllAccess]
     File Permissions "C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\I088V4J9\nc[1].exe": Bethany [AllAccess]
     File Permissions "C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\CR6ZPMP0\shell[1].exe": Bethany [AllAccess]
     File Permissions "C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\CR6ZPMP0\PowerView[1].ps1": Bethany [AllAccess]
     File Permissions "C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\42F0OL20\PowerUp[1].ps1": Bethany [AllAccess]
     File Permissions "C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\42F0OL20\ncVE7XEZU0.exe": Bethany [AllAccess]
     File Permissions "C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\2EJ1ZR7Q\winPEASx64[1].exe": Bethany [AllAccess]
     File Permissions "C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\2EJ1ZR7Q\revshell[1].exe": Bethany [AllAccess]
     File Permissions "C:\HFS\hfs.exe": Authenticated Users [WriteData/CreateFiles]
     File Permissions "C:\Users\Public\nc.exe": Bethany [AllAccess],Interactive [WriteData/CreateFiles]

����������͹ Looking for Linux shells/distributions - wsl.exe, bash.exe


�����������������������������������͹ File Analysis �������������������������������������

����������͹ Found MySQL Files
Folder: C:\inetpub\wwwroot\includes\database\mysql

����������͹ Found PHP_files Files
File: C:\inetpub\wwwroot\sites\default\settings.php

����������͹ Found Drupal Files
File: C:\inetpub\wwwroot\sites\default\settings.php

����������͹ Found CERTSB4 Files
File: C:\Users\All Users\VMware\VMware Tools\GuestProxyData\server\key.pem
                   
����������͹ Found Misc-Basic Auth Regexes
C:\inetpub\wwwroot\modules\filter\tests\filter.url-output.txt: //www.test.com">www.test.com</a>. paragraph with <a href="mailto:person@test.com">person@
C:\inetpub\wwwroot\modules\filter\tests\filter.url-output.txt: //www.test.com">www.test.com</a>. paragraph with <a href="mailto:person@test.com">person@
C:\inetpub\wwwroot\modules\filter\tests\filter.url-output.txt: //www.test.com">http://www.test.com</a> not so easy <a href="mailto:person@test.com">person@
C:\inetpub\wwwroot\modules\filter\tests\filter.url-input.txt: //www.test.com urls thrown in. *<br/> This is just a www.test.com paragraph *<br/> with some http://www.test.com urls thrown in. *<br/>This is just a www.test.com paragraph person@test.com with some http://www.test.com urls *img*<img/> thrown in. This is just a www.test.com paragraph with some http://www.test.com urls thrown in. This is just a www.test.com paragraph person@
C:\inetpub\wwwroot\modules\filter\tests\filter.url-input.txt: //www.test.com urls thrown in. <br /> This is just a www.test.com paragraph with some http://www.test.com urls thrown in. This is just a www.test.com paragraph person@test.com with some http://www.test.com urls thrown in. This is just a www.test.com paragraph with some http://www.test.com urls thrown in. This is just a www.test.com paragraph person@

����������͹ Found Misc-Passwords1 Regexes
C:\inetpub\wwwroot\misc\jquery.js: password")&&c(b).closest("form").length&&a.keyCode===13){a.liveFired=B;return la("submit",this,arguments)}})}else return false},teardown:function(){c.event.remove(this,".specialSubmit")}};if(!c.support.changeBubbles){var V,
C:\inetpub\wwwroot\misc\jquery.js: password:function(g){return"password"===g.type},submit:function(g){return"submit"===
C:\inetpub\wwwroot\misc\jquery.js: password):w.open(h,b.url,b.async);try{if(b.data!=null&&!l||a&&a.contentType)w.setRequestHeader("Content-Type",
C:\inetpub\wwwroot\modules\user\user.js: password = {
C:\inetpub\wwwroot\modules\user\user.js: passwordInput = $(this);
C:\inetpub\wwwroot\modules\user\user.js: password-confirm', outerWrapper).parent().prepend('<div class="password-confirm">' + translate['confirmTitle'] + ' <span></span></div>').addClass('confirm-parent');
C:\inetpub\wwwroot\modules\user\user.js: passwordMeter = '<div class="password-strength"><div class="password-strength-text" aria-live="assertive"></div><div class="password-strength-title">' + translate['strengthTitle'] + '</div><div class="password-indicator"><div class="indicator"></div></div></div>';
C:\inetpub\wwwroot\modules\user\user.js: passwordDescription = $('div.password-suggestions', outerWrapper).hide();
C:\inetpub\wwwroot\modules\user\user.js: passwordCheck = function () {
C:\inetpub\wwwroot\modules\user\user.js: passwordDescription.html() != result.message) {
C:\inetpub\wwwroot\modules\user\user.js: passwordCheckMatch = function () {
C:\inetpub\wwwroot\modules\user\user.js: passwordInput.val() === confirmInput.val();
C:\inetpub\wwwroot\modules\user\user.js: password !== '' && password.toLowerCase() === username.toLowerCase()) {
C:\Users\Bethany\AppData\Local\Packages\winstore_cw5n1h2txyewy\AC\AppCache\UC3WF8XB\1\WinStore[1].js: password when buying an app",onchange:WinStore.Settings.onAlwaysPromptChanged});
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\I088V4J9\PowerUp[1].ps1: password 192.168.1.101\server1 C:\App1            C:\App1\web.config            No
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\I088V4J9\PowerUp[1].ps1: password 192.168.1.101\server1 C:\inetpub\wwwroot C:\inetpub\wwwroot\web.config No
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\I088V4J9\PowerUp[1].ps1: password 192.168.1.102\server2 C:\App2            C:\App2\test\web.config       No
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\I088V4J9\PowerUp[1].ps1: password 192.168.1.102\server2 C:\App2            C:\App2\web.config            Yes
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\I088V4J9\PowerUp[1].ps1: password 192.168.1.103\server3 D:\App3            D:\App3\web.config            No
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\I088V4J9\PowerUp[1].ps1: password = $Cpassword.Substring(0,$Cpassword.Length -1)}
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\I088V4J9\PowerUp[1].ps1: password += ('=' * (4 - $Mod))}
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\I088V4J9\PowerUp[1].ps1: password += ('=' * (4 - $Mod))}
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\I088V4J9\PowerUp[1].ps1: password = @()
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\I088V4J9\PowerUp[1].ps1: password += , $Xml | Select-Xml "/Groups/User/Properties/@cpassword" | Select-Object -Expand Node | ForEach-Object {$_.Value}
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\I088V4J9\PowerUp[1].ps1: password += , $Xml | Select-Xml "/NTServices/NTService/Properties/@cpassword" | Select-Object -Expand Node | ForEach-Object {$_.Value}
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\CR6ZPMP0\psexec[1].py: password = input(core.setprompt(["32"], "Enter the password or the hash"))
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\CR6ZPMP0\PowerView[1].ps1: password for user '$Identity' : $_"
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\CR6ZPMP0\PowerView[1].ps1: PASSWD_NOTREQD                  =   32
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\CR6ZPMP0\PowerView[1].ps1: PASSWD_CANT_CHANGE              =   64
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\CR6ZPMP0\PowerView[1].ps1: PASSWORD            =   65536
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\CR6ZPMP0\PowerView[1].ps1: PASSWORD_EXPIRED                =   8388608
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\42F0OL20\PowerUp[1].ps1: password 192.168.1.101\server1 C:\App1            C:\App1\web.config            No
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\42F0OL20\PowerUp[1].ps1: password 192.168.1.101\server1 C:\inetpub\wwwroot C:\inetpub\wwwroot\web.config No
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\42F0OL20\PowerUp[1].ps1: password 192.168.1.102\server2 C:\App2            C:\App2\test\web.config       No
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\42F0OL20\PowerUp[1].ps1: password 192.168.1.102\server2 C:\App2            C:\App2\web.config            Yes
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\42F0OL20\PowerUp[1].ps1: password 192.168.1.103\server3 D:\App3            D:\App3\web.config            No
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\42F0OL20\PowerUp[1].ps1: password = $Cpassword.Substring(0,$Cpassword.Length -1)}
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\42F0OL20\PowerUp[1].ps1: password += ('=' * (4 - $Mod))}
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\42F0OL20\PowerUp[1].ps1: password += ('=' * (4 - $Mod))}
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\42F0OL20\PowerUp[1].ps1: password = @()
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\42F0OL20\PowerUp[1].ps1: password += , $Xml | Select-Xml "/Groups/User/Properties/@cpassword" | Select-Object -Expand Node | ForEach-Object {$_.Value}
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\42F0OL20\PowerUp[1].ps1: password += , $Xml | Select-Xml "/NTServices/NTService/Properties/@cpassword" | Select-Object -Expand Node | ForEach-Object {$_.Value}
C:\Users\Bethany\Desktop\PowerUp.ps1: password 192.168.1.101\server1 C:\App1            C:\App1\web.config            No
C:\Users\Bethany\Desktop\PowerUp.ps1: password 192.168.1.101\server1 C:\inetpub\wwwroot C:\inetpub\wwwroot\web.config No
C:\Users\Bethany\Desktop\PowerUp.ps1: password 192.168.1.102\server2 C:\App2            C:\App2\test\web.config       No
C:\Users\Bethany\Desktop\PowerUp.ps1: password 192.168.1.102\server2 C:\App2            C:\App2\web.config            Yes
C:\Users\Bethany\Desktop\PowerUp.ps1: password 192.168.1.103\server3 D:\App3            D:\App3\web.config            No
C:\Users\Bethany\Desktop\PowerUp.ps1: password = $Cpassword.Substring(0,$Cpassword.Length -1)}
C:\Users\Bethany\Desktop\PowerUp.ps1: password += ('=' * (4 - $Mod))}
C:\Users\Bethany\Desktop\PowerUp.ps1: password += ('=' * (4 - $Mod))}
C:\Users\Bethany\Desktop\PowerUp.ps1: password = @()
C:\Users\Bethany\Desktop\PowerUp.ps1: password += , $Xml | Select-Xml "/Groups/User/Properties/@cpassword" | Select-Object -Expand Node | ForEach-Object {$_.Value}
C:\Users\Bethany\Desktop\PowerUp.ps1: password += , $Xml | Select-Xml "/NTServices/NTService/Properties/@cpassword" | Select-Object -Expand Node | ForEach-Object {$_.Value}

����������͹ Found Misc-Usernames Regexes
C:\inetpub\wwwroot\misc\jquery.js: username?w.open(h,b.url,b.async,b.username,b.password):w.open(h,b.url,b.async);try{if(b.data!=null&&!l||a&&a.contentType)w.setRequestHeader("Content-Type",
C:\inetpub\wwwroot\modules\user\user.js: usernameBox = $('input.username');
C:\inetpub\wwwroot\modules\user\user.js: username = (usernameBox.length > 0) ? usernameBox.val() : translate.username;
C:\Users\Bethany\AppData\Local\Microsoft\Windows\INetCache\IE\CR6ZPMP0\psexec[1].py: username = input(core.setprompt(["32"], "Enter the username"))

       /---------------------------------------------------------------------------------\
       |                             Do you like PEASS?                                  |
       |---------------------------------------------------------------------------------| 
       |         Get the latest version    :     https://github.com/sponsors/carlospolop |
       |         Follow on Twitter         :     @carlospolopm                           |
       |         Respect on HTB            :     SirBroccoli                             |
       |---------------------------------------------------------------------------------|
       |                                 Thank you!                                      |
       \---------------------------------------------------------------------------------/


C:\Windows\Tasks>
