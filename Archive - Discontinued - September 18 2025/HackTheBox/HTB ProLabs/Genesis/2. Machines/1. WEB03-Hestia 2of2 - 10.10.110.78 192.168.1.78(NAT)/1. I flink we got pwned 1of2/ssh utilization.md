# save `ipp_rsa`
![[Pasted image 20240401124355.png]]
# `chmod 600`

```bash
┌──(kali㉿gobots)-[01Apr2024 16:40:53]-[~/SUT/Genesis_proLab_htB/WEB03-Hestia/loot]
└─$ chmod 600 ipp_rsa 
```

# Login and failed `sudo -l`

```bash
┌──(kali㉿gobots)-[01Apr2024 16:40:57]-[~/SUT/Genesis_proLab_htB/WEB03-Hestia/loot]                                                                                                                         
└─$ ssh -i ipp_rsa ipp@10.10.110.78                                                                                                                                                                         
Welcome to Ubuntu 22.04.2 LTS (GNU/Linux 5.15.0-69-generic x86_64)                                                                                                                                          
                                                                                                                                                                                                            
 * Documentation:  https://help.ubuntu.com                                                                                                                                                                  
 * Management:     https://landscape.canonical.com                                                                                                                                                          
 * Support:        https://ubuntu.com/advantage                                                                                                                                                             
                                                                                                                                                                                                            
  System information as of Mon Apr  1 04:41:10 PM UTC 2024                                                                                                                                                  
                                                                                                                                                                                                            
  System load:  0.0419921875      Processes:               212                                                                                                                                              
  Usage of /:   89.9% of 4.49GB   Users logged in:         0                                                                                                                                                
  Memory usage: 45%               IPv4 address for ens160: 192.168.1.78                                                                                                                                     
  Swap usage:   0%                                                                                                                                                                                          
                                                                                                                                                                                                            
  => / is using 89.9% of 4.49GB                                                                                                                                                                             
                                                                                                                                                                                                            
                                                                                                                                                                                                            
 * Introducing Expanded Security Maintenance for Applications.                                                                                                                                              
   Receive updates to over 25,000 software packages with your                                                                                                                                               
   Ubuntu Pro subscription. Free for personal use.                                                                                                                                                          

     https://ubuntu.com/pro

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


The list of available updates is more than a week old.
To check for new updates run: sudo apt update

Last login: Wed Apr  5 07:30:50 2023 from 10.10.14.12
ipp@WEB03-Hestia:~$ sudo -l
[sudo] password for ipp: 

```
# Unsetting history to not be recorded
```bash
ipp@WEB03-Hestia:~$  HISTIGNORE='*'
```