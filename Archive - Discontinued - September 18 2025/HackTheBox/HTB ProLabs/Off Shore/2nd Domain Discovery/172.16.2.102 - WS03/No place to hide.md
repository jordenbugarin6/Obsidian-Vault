![[Pasted image 20240110233146.png]]
this flag picks up where [[Headed down another path]] leaves off, once on the machine enumerate the user directories. Not the `C:\Projects\.git`  path, it is just meant to waste your time.

this leads you to `C:\Documents and Settings\joe\Documents` which has `SharpChrome.exe` - this was the first time i've seen this so I over looked it.
![[Pasted image 20240110233546.png]]
I injected into `session 1 & session 2` and ran `execute-assembly /usr/share/poshc2/resources/modules/SharpChrome.exe logins` but was unable to get the flag when it supposedly should've been shown.
- Note that when attempting to inject into multiple `session 2` processes it would just kill my beacons for 3-5 minutes before bringing them back.

![[Pasted image 20240110233932.png]]
in order for me to get successfully get the flag I had to `rdp` in, which was inoperable/unstable/ and would constantly crash around 30 times before I was able to get the passwords in the google password storage location.

here is the `rdesktop` command that worked: 
- Note: `xfreerdp` would just hang and never connect.
```bash
┌──(root💀gobots)-[10Jan2024 19:34:46]-[~/SUT/offshore/ws03 enum/sharpchrome.exe]
└─# proxychains rdesktop -u joe -d dev.admin.offshore.com 172.16.2.102
```

navigate to google chrome password manager to see flag.

![[Pasted image 20240110235304.png]]
![[Pasted image 20240110234006.png]]