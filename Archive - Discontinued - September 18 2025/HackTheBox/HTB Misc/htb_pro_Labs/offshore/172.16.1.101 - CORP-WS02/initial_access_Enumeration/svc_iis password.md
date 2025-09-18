
[[Penetration Testing v2/htb_pro_Labs/offshore/10.10.110.124 - 172.16.1.24 - WEB-WIN01 - SQL01/172.16.1.24 chicken scratch]]

found user `svc_iis` password in `C:\Backups\`
![[Penetration Testing v2/htb_pro_Labs/offshore/172.16.1.101 - CORP-WS02/screenshots/Pasted image 20231115183807.png]]
pulled file back to kali machine `/root/SUT/172.16.1.101` directory


![[Penetration Testing v2/htb_pro_Labs/offshore/172.16.1.101 - CORP-WS02/screenshots/Pasted image 20231115183958.png]]

```bash
┌──(root💀gobots)-[15Nov2023 15:59:13]-[~/SUT/offshore/172.16.1.101_WS02]
└─# cat web.config_sample     
<configuration>      
    <system.web>      
        <authentication mode="Forms">      
            <credentials passwordFormat="Clear">      
                <user name="svc_iis" password="Vintage!" />      
            </credentials>      
        </authentication>      
        <authorization>      
            <allow users="test" />      
            <deny users="*" />      
        </authorization>      
    </system.web>      
    <location path="admin">
        <system.web>
            <authorization>              
                <allow roles="admin" />
                <deny users="*"/>
            </authorization>
        </system.web>
    </location> 
    <system.webServer>      
        <directoryBrowse enabled="true" />      
        <security>      
            <authentication>      
                <anonymousAuthentication enabled="false" />      
                <basicAuthentication enabled="true" />      
                <windowsAuthentication enabled="false" />      
            </authentication>      
        </security>      
    </system.webServer>      
</configuration>

```