```bash
meterpreter > ls                                   
Listing: /root                                     
==============                                     

Mode              Size  Type  Last modified              Name
----              ----  ----  -------------              ----
020666/rw-rw-rw-  0     cha   2024-04-16 20:19:06 +0000  .bash_history
100644/rw-r--r--  3106  fil   2019-12-05 14:39:21 +0000  .bashrc
040700/rwx------  4096  dir   2021-03-23 09:49:49 +0000  .cache
040755/rwxr-xr-x  4096  dir   2021-03-23 09:49:49 +0000  .groovy
040755/rwxr-xr-x  4096  dir   2021-03-23 09:49:49 +0000  .java
040755/rwxr-xr-x  4096  dir   2021-03-23 09:49:49 +0000  .local
100644/rw-r--r--  161   fil   2019-12-05 14:39:21 +0000  .profile
040700/rwx------  4096  dir   2021-03-23 09:49:49 +0000  .ssh
100600/rw-------  839   fil   2023-04-03 10:48:37 +0000  .viminfo
100400/r--------  32    fil   2021-01-04 16:58:37 +0000  flag.txt
040755/rwxr-xr-x  4096  dir   2021-03-23 09:49:49 +0000  snap

meterpreter > cat flag.txt
GENESIS{Th3_b1T_0f_d3sTrUcT1oN}
```

![[Pasted image 20240430193033.png]]