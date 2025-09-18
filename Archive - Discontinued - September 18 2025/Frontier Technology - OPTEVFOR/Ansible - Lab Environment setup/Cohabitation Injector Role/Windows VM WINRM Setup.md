#### Initial WINRM GPO Configuration
```bash
Computer Configuration └── Administrative Templates └── Windows Components └── Windows Remote Management (WinRM) └── WinRM Service
```
![[Pasted image 20241015170335.png]]
#### Enable Private Network Connecion to enable WINRM to properly work

`Get-NetConnectionProfile`              
![[Pasted image 20241018174314.png]]
`Set-NetConnectionProfile -InterfaceAlias "Ethernet0" -NetworkCategory Private`
![[Pasted image 20241018174345.png]]
`Enable-PSRemoting -Force`
![[Pasted image 20241018174411.png]]