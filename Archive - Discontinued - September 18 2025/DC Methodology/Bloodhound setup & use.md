
```bash
┌──(root💀gobots)-[20Jun2024 17:16:32]-[/home/…/SUT/Alchemy/172.16.0.2/BloodHound.py-master]               
└─# proxychains -q bloodhound-python -c All -u calde_ldap -p CsAdlLDAPMoDeBrnd12! -d alchemy.htb -dc dc.alchemy.htb -ns 172.16.0.2 --dns-tcp                                                                                        
INFO: Found AD domain: alchemy.htb                                                                                                                                                                             
INFO: Getting TGT for user                                                                                                                                                                                     
WARNING: Failed to get Kerberos TGT. Falling back to NTLM authentication. Error: [Errno Connection error (dc.alchemy.htb:88)] [Errno -2] Name or service not known                                             
INFO: Connecting to LDAP server: dc.alchemy.htb                                                                                                                                                                
INFO: Found 1 domains                                                                                      
INFO: Found 1 domains in the forest                                                                           
INFO: Found 1 computers                                                                                       
INFO: Connecting to LDAP server: dc.alchemy.htb                                                           
INFO: Found 9 users                                                                                            
INFO: Found 50 groups                                                                                          
INFO: Found 2 gpos                                                                                            
INFO: Found 1 ous                                                                                           
INFO: Found 19 containers                                                                                     
INFO: Found 0 trusts                                                                                
INFO: Starting computer enumeration with 10 workers                                               
INFO: Querying computer: dc.alchemy.htb                                                                        
INFO: Done in 00M 08S            
```
