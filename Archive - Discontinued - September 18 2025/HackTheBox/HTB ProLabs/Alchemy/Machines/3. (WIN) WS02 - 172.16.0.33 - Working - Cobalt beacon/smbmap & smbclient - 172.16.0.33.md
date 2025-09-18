### smbmap -u calde_ldap -p CsAdlLDAPMoDeBrnd12! -H 172.16.0.33
- Read / Write Privileges to the Development share
#smbmap
```bash
proxychains smbmap -u calde_ldap -p CsAdlLDAPMoDeBrnd12! -H 172.16.0.33    

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
                                                                                                    
[+] IP: 172.16.0.33:445 Name: 172.16.0.33               Status: Authenticated
        Disk                                                    Permissions     Comment
        ----                                                    -----------     -------
        ADMIN$                                                  NO ACCESS       Remote Admin
        C$                                                      NO ACCESS       Default share
        DEVELOPMENT                                             READ, WRITE     Development tools
        IPC$                                                    READ ONLY       Remote IPC
```
### smbclient \\\\172.16.0.33\\DEVELOPMENT -U 'calde_ldap'
#smbclient
```bash
proxychains smbclient \\\\172.16.0.33\\DEVELOPMENT -U 'calde_ldap'                                                                                     
Password for [WORKGROUP\calde_ldap]:   CsAdlLDAPMoDeBrnd12!                                                                                                                                                                     
Try "help" to get a list of possible commands.                                                                                                                                                              
smb: \> ls                                                                                                                                                                                                  
  .                                   D        0  Thu Jun 13 19:22:22 2024                                                                             
  ..                                  D        0  Thu Jun 13 19:22:22 2024
  devgit.url                          A      201  Fri Dec  8 12:44:58 2023

7677951 blocks of size 4096. 4111128 blocks available

smb: \> get devgit.url
getting file \devgit.url of size 201 as devgit.url (1.5 KiloBytes/sec) (average 1.5 KiloBytes/sec)

smb: \> exit
```
#### devgit.url
```bash
cat devgit.url 

[{000214A0-0000-0000-C000-000000000046}]
Prop3=19,11
[InternetShortcut]
IDList=
URL=https://172.16.0.21:3000/
IconIndex=8
HotKey=0
IconFile=C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe

```
