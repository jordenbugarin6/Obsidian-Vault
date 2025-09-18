open ports
```shell
22/tcp   
111/tcp  
135/tcp  
445/tcp  
2049/tcp 
5357/tcp open  wsdapi - webserver port?     
```


NFS Enum
#showmount
```shell
# shows what file shares are available
┌──(root㉿kali)-[/home/kali]
└─# showmount -e 192.168.118.124
Export list for 192.168.118.124:
/BackUp (everyone)
```

- made /mnt/nfs to have a place to mount to.

```shell
# mounted to nfs drive
┌──(root㉿kali)-[/home/kali]
└─# mount -t nfs 192.168.118.124:/BackUp /mnt/nfs

# cd'd to the drive
┌──(root㉿kali)-[/home/kali]
└─# cd /mnt/nfs  

# going to begin looking at information we have
┌──(root㉿kali)-[/mnt/nfs]
└─# ls
'2020 BackUp'  '2021 BackUp'  '2022 BackUp'
```

