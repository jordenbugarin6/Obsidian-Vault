# cracking password with `rockyou.txt`
```bash
┌──(root💀gobots)-[01Apr2024 17:48:48]-[/home/…/SUT/Genesis_proLab_htB/WEB03-Hestia/loot]
└─# unshadow passwd.txt shadow.txt > unshadowed.txt

┌──(root💀gobots)-[01Apr2024 17:49:06]-[/home/…/SUT/Genesis_proLab_htB/WEB03-Hestia/loot]
└─# ls -la                  
total 24
drwxr-xr-x 2 kali kali 4096 Apr  1 17:49 .
drwxr-xr-x 3 kali kali 4096 Apr  1 17:46 ..
-rw------- 1 kali kali 1679 Apr  1 16:40 ipp_rsa
-rw-r--r-- 1 root root   32 Apr  1 17:47 passwd.txt 
-rw-r--r-- 1 root root  123 Apr  1 17:47 shadow.txt 
-rw-r--r-- 1 root root  129 Apr  1 17:49 unshadowed.txt

┌──(root💀gobots)-[01Apr2024 17:49:08]-[/home/…/SUT/Genesis_proLab_htB/WEB03-Hestia/loot]
└─# john --wordlist=/usr/share/wordlists/rockyou.txt unshadowed.txt
Using default input encoding: UTF-8
Loaded 1 password hash (sha512crypt, crypt(3) $6$ [SHA512 256/256 AVX2 4x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
0g 0:00:00:04 0.19% (ETA: 18:23:58) 0g/s 8090p/s 8090c/s 8090C/s dyesebel..kaytee
0g 0:00:01:34 4.44% (ETA: 18:24:31) 0g/s 7796p/s 7796c/s 7796C/s 192613..182419
0g 0:00:01:35 4.48% (ETA: 18:24:36) 0g/s 7785p/s 7785c/s 7785C/s 106302..10082002
0g 0:00:01:47 5.07% (ETA: 18:24:27) 0g/s 7774p/s 7774c/s 7774C/s pajorafe..pablo.
0g 0:00:02:45 8.16% (ETA: 18:22:58) 0g/s 7980p/s 7980c/s 7980C/s sanabhe..samskie
0g 0:00:06:30 20.58% (ETA: 18:20:49) 0g/s 8108p/s 8108c/s 8108C/s tmviolin17..tmr101596
0g 0:00:10:29 34.19% (ETA: 18:19:54) 0g/s 8025p/s 8025c/s 8025C/s nlbf24e..nks1998
0g 0:00:14:14 47.25% (ETA: 18:19:22) 0g/s 8054p/s 8054c/s 8054C/s josskenneth..josoelpublicidades
```
didnt crack with `rockyou.txt`
![[Pasted image 20240401142215.png]]

# Trying with top 10 million (failed)
```bash
┌──(root💀gobots)-[01Apr2024 18:25:39]-[/home/…/SUT/Genesis_proLab_htB/WEB03-Hestia/loot]
└─# john --wordlist=/usr/share/wordlists/seclists/Passwords/xato-net-10-million-passwords-1000000.txt unshadowed.txt
Using default input encoding: UTF-8
Loaded 1 password hash (sha512crypt, crypt(3) $6$ [SHA512 256/256 AVX2 4x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status

```
![[Pasted image 20240401142910.png]]
