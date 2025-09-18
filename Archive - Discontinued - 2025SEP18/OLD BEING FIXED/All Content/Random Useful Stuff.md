##### How to fix default paths
#PATH
```shell
export PATH=$PATH:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
/usr/bin:/sbin:/binusr/local/sbin:/usr/local/bin:/usr/sbin:
```
##### Accesschk
- `Using AccessChk to View Which Files and Folders a User Has Access To`
#accesschk #windows 
```
- Look into AccessChk to view file/folder permissions if needed.
```
##### Hashcat utilization
#hashcat
```
.\hashcat.exe -m 18200 ..\hash.txt ..\rockyou.txt -o ..cracked.txt
```

#### SNMP Walk
#snmpwalk
```bash
┌──(root㉿kali)-[/home/kali/Documents/hackthebox/pit]
└─# snmpwalk -v1 -c public 10.10.10.241 . > snmpwalk-full

┌──(root㉿kali)-[/home/kali/Documents/hackthebox/pit]
└─# gedit snmpwalk-full      

# examples of stuff to look for in the results.

System release info
CentOS Linux release 8.3.2011

SELinux Settings
user

                Labeling   MLS/       MLS/                          
SELinux User    Prefix     MCS Level  MCS Range                      SELinux Roles

guest_u         user       s0         s0                             guest_r
root            user       s0         s0-s0:c0.c1023                 staff_r sysadm_r system_r unconfined_r
staff_u         user       s0         s0-s0:c0.c1023                 staff_r sysadm_r unconfined_r
sysadm_u        user       s0         s0-s0:c0.c1023                 sysadm_r
system_u        user       s0         s0-s0:c0.c1023                 system_r unconfined_r
unconfined_u    user       s0         s0-s0:c0.c1023                 system_r unconfined_r
user_u          user       s0         s0                             user_r
xguest_u        user       s0         s0                             xguest_r
login

Login Name           SELinux User         MLS/MCS Range        Service

__default__          unconfined_u         s0-s0:c0.c1023       *
michelle             user_u               s0                   *
root                 unconfined_u         s0-s0:c0.c1023       *

iso.3.6.1.4.1.2021.9.1.2.2 = STRING: "/var/www/html/seeddms51x/seeddms"
iso.3.6.1.4.1.2021.9.1.3.1 = STRING: "/dev/mapper/cl-root"
iso.3.6.1.4.1.2021.9.1.3.2 = STRING: "/dev/mapper/cl-seeddms"



snmpwalk -v2c -c public 10.10.10.241
	- ippsec snmpwalk command for pit box
```
#### getfacl
```
- able to look at files with additional privileges, originally in photo below you wouldnt be able to see that michelle has privileges but if you getfacl you are able to see that she has write and execute privileges.

getfacl /usr/local/monitoring
	- ippsec command on pit box.
```
##### Random Notes
- can use lput with psexec to put files up.