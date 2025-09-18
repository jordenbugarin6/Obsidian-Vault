### smbmap -u calde_ldap -p CsAdlLDAPMoDeBrnd12! -H 172.16.0.2
#smbmap
```bash
proxychains smbmap -u calde_ldap -p CsAdlLDAPMoDeBrnd12! -H 172.16.0.2                                                                                                                                  

    ________  ___      ___  _______   ___      ___       __         _______                                                                            
   /"       )|"  \    /"  ||   _  "\ |"  \    /"  |     /""\       |   __ "\                                                                           
  (:   \___/  \   \  //   |(. |_)  :) \   \  //   |    /    \      (. |__) :)                                                                          
   \___  \    /\  \/.    ||:     \/   /\   \/.    |   /' /\  \     |:  ____/                                                                           
   __/  \   |: \.        |(|  _  \  |: \.        |  //  __'  \    (|  /                                                                               
   /" \   :) |.  \    /:  ||: |_)  :)|.  \    /:  | /   /  \   \  /|__/ \                                                                              
  (_______/  |___|\__/|___|(_______/ |___|\__/|___|(___/    \___)(_______)                                                                                                                                  
 -----------------------------------------------------------------------------                                                                                                                              
     SMBMap - Samba Share Enumerator | Shawn Evans - ShawnDEvans@gmail.com
                     https://github.com/ShawnDEvans/smbmap

[*] Detected 1 hosts serving SMB
[*] Established 1 SMB session(s)                                 
                                                                                                     
[+] IP: 172.16.0.2:445  Name: 172.16.0.2                Status: Authenticated
        Disk                                                    Permissions     Comment
        ----                                                    -----------     -------
        ADMIN$                                                  NO ACCESS       Remote Admin
        C$                                                      NO ACCESS       Default share
        IPC$                                                    READ ONLY       Remote IPC
        NETLOGON                                                READ ONLY       Logon server share 
        SYSVOL                                                  READ ONLY       Logon server share 
```
### smbclient \\\\172.16.0.33\\IPC$ -U 'calde_ldap' 
#smbclient 
```bash
proxychains smbclient \\\\172.16.0.33\\IPC$ -U 'calde_ldap'     

Password for [WORKGROUP\calde_ldap]:

Try "help" to get a list of possible commands.
smb: \> ls
NT_STATUS_NO_SUCH_FILE listing \*

smb: \> exit
```
### smbclient \\\\172.16.0.33\\NETLOGON -U 'calde_ldap' 
#smbclient
```bash
proxychains smbclient \\\\172.16.0.33\\NETLOGON -U 'calde_ldap'  

Password for [WORKGROUP\calde_ldap]:
tree connect failed: NT_STATUS_BAD_NETWORK_NAME
```
### smbclient \\\\172.16.0.33\\SYSVOL -U 'calde_ldap'
#smbclient
```bash
proxychains smbclient \\\\172.16.0.33\\SYSVOL -U 'calde_ldap'  

Password for [WORKGROUP\calde_ldap]: CsAdlLDAPMoDeBrnd12!
tree connect failed: NT_STATUS_BAD_NETWORK_NAME

```