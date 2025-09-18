
Notable Information:
`Sysmon64`, `MsMpEng`, `elastic-endpoint`, and `elastic-agent`

`notepad.exe is me`,

```bash
[11/15 12:30:45] beacon> ps
[11/15 12:30:45] [*] Tasked beacon to list processes
[11/15 12:30:45] [+] host called home, sent: 12 bytes
[11/15 12:30:45] [*] Process List with process highlighting
[*] Current Running PID:  Yellow 2724  
[*] Explorer/Winlogon:  BLUE  
[*] Admin Tools:  LIGHT BLUE  
[*] Browsers:  GREEN  
[*] AV/EDR:  RED  

 PID   PPID  Name                         Arch  Session     User
 ---   ----  ----                         ----  -------     -----
 0     0     [System Process]                                
 4     0     System                       x64   0           NT AUTHORITY\SYSTEM 
 256   4     smss.exe                     x64   0           NT AUTHORITY\SYSTEM 
 344   336   csrss.exe                                       
 396   336   wininit.exe                  x64   0           NT AUTHORITY\SYSTEM 
 408   388   csrss.exe                                       
 460   388   winlogon.exe                 x64   1           NT AUTHORITY\SYSTEM  
 500   396   services.exe                 x64   0           NT AUTHORITY\SYSTEM 
 516   396   lsass.exe                    x64   0           NT AUTHORITY\SYSTEM 
 524   396   lsm.exe                      x64   0           NT AUTHORITY\SYSTEM 
 612   500   svchost.exe                  x64   0           NT AUTHORITY\NETWORK SERVICE 
 628   500   svchost.exe                  x64   0           NT AUTHORITY\SYSTEM 
 704   500   svchost.exe                  x64   0           NT AUTHORITY\NETWORK SERVICE 
 780   460   LogonUI.exe                  x64   1           NT AUTHORITY\SYSTEM 
 796   500   svchost.exe                  x64   0           NT AUTHORITY\LOCAL SERVICE 
 864   500   svchost.exe                  x64   0           NT AUTHORITY\SYSTEM 
 888   500   svchost.exe                  x64   0           NT AUTHORITY\LOCAL SERVICE 
 916   500   svchost.exe                  x64   0           NT AUTHORITY\SYSTEM 
 984   500   svchost.exe                  x64   0           NT AUTHORITY\SYSTEM 
 1076  500   spoolsv.exe                  x64   0           NT AUTHORITY\SYSTEM 
 1104  500   svchost.exe                  x64   0           NT AUTHORITY\LOCAL SERVICE 
 1212  500   svchost.exe                  x64   0           NT AUTHORITY\SYSTEM 
 1324  500   VGAuthService.exe            x64   0           NT AUTHORITY\SYSTEM 
 1436  500   vm3dservice.exe              x64   0           NT AUTHORITY\SYSTEM 
 1460  500   vmtoolsd.exe                 x64   0           NT AUTHORITY\SYSTEM 
 1468  1436  vm3dservice.exe              x64   1           NT AUTHORITY\SYSTEM 
 1664  500   msdtc.exe                    x64   0           NT AUTHORITY\NETWORK SERVICE 
 1884  500   svchost.exe                  x64   0           NT AUTHORITY\NETWORK SERVICE 
 2000  500   dllhost.exe                  x64   0           NT AUTHORITY\SYSTEM 
 2184  628   WmiPrvSE.exe                                    
 2352  2928  SearchProtocolHost.exe       x64   0           NT AUTHORITY\SYSTEM 
 2360  500   svchost.exe                  x64   0           NT AUTHORITY\SYSTEM 
 2420  2928  SearchFilterHost.exe         x64   0           NT AUTHORITY\SYSTEM 
 2724  1076  notepad.exe                  x86   0           NT AUTHORITY\SYSTEM  
 2808  628   WmiPrvSE.exe                 x64   0           NT AUTHORITY\SYSTEM 
 2896  500   sppsvc.exe                   x64   0           NT AUTHORITY\NETWORK SERVICE 
 2928  500   SearchIndexer.exe            x64   0           NT AUTHORITY\SYSTEM 
 3028  500   WmiApSrv.exe                 x64   0           NT AUTHORITY\SYSTEM 


```