
SharPersist - used to setup persistence

SharpUp (ghostpack)- used to identify methods to privilege escalate

The PowerShell `Get-Acl` cmdlet will show the permissions of various objects (including files and directories)
- used to priv esc, detecting Unquoted Service Path

Rubeus - used to extract Kerberos Granting Tickets using native windows API's so less suspicious

DCSYNC - Used to dump AES/NTLM of krbtgt account


Domain Reconnaissance:
PowerView.ps1 - Domain enumeration
Seatbelt.exe - Computer enumeration once PTH happened utilizing jking credentials.
WinRM- Utilized with PTH : The SMB Beacon is an excellent choice when moving laterally, because the SMB protocol is used extensively in a Windows environment, so this traffic blends in very well.