Return:
[[Penetration Testing v2/htb_pro_Labs/offshore/3. 172.16.1.36 -CORP-WSADM/Initial Access]]

Pulled logins.xlsx, needs a password to login

Passwords Tried:

![[Penetration Testing v2/htb_pro_Labs/offshore/2. 172.16.1.30 - CORP-MS01/screenshots/Pasted image 20231019150303.png]]
Sync'd file to have it pulled to my kali machine
- Convert logins.xlsx to logins-hash.txt with `office2john`
```bash
[root💀~/offshore/ms01] [10.10.14.39] [2023-10-20 13:07:10]  
 └─╼ # office2john logins.xlsx > logins-hash.txt  
```
Ensure that the file was properly transferred to hash.txt
```bash
[root💀~/offshore/ms01] [10.10.14.39] [2023-10-20 13:08:17] 
 └─╼ # cat logins-hash.txt 
logins.xlsx:$office$*2013*100000*256*16*6e2731071c58ebe3183c5b977ca7b3b7*066bf7f3cdf4cafe11174c18628cc37f*82f49a87dd9a11168d4f6fe3527edde1151e78baeccd6a7d32d7a0badc75f531
```
Prosper
```bash
[root💀~/offshore/ms01] [10.10.14.39] [2023-10-20 13:08:29] 
 └─╼ # john --rules --wordlist=/usr/share/wordlists/rockyou.txt logins-hash.txt
Using default input encoding: UTF-8
Loaded 1 password hash (Office, 2007/2010/2013 [SHA1 256/256 AVX2 8x / SHA512 256/256 AVX2 4x AES])
Cost 1 (MS Office version) is 2013 for all loaded hashes
Cost 2 (iteration count) is 100000 for all loaded hashes
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
0g 0:00:00:10 0.00% (ETA: 2024-06-04 00:45) 0g/s 36.71p/s 36.71c/s 36.71C/s jeffrey..jerome
broken           (logins.xlsx)     
1g 0:00:00:15 DONE (2023-10-20 13:09) 0.06406g/s 38.94p/s 38.94c/s 38.94C/s evelyn..flores
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
```
![[Penetration Testing v2/htb_pro_Labs/offshore/2. 172.16.1.30 - CORP-MS01/screenshots/Pasted image 20231020133008.png]]
Login to `logins.xlsx` with password
![[Penetration Testing v2/htb_pro_Labs/offshore/2. 172.16.1.30 - CORP-MS01/screenshots/Pasted image 20231020133145.png]]

![[Penetration Testing v2/htb_pro_Labs/offshore/2. 172.16.1.30 - CORP-MS01/screenshots/Pasted image 20231020133351.png]]
Going to spray credentials:
![[Penetration Testing v2/htb_pro_Labs/offshore/2. 172.16.1.30 - CORP-MS01/screenshots/Pasted image 20231020133854.png]]
Flag that was in sheet2
```bash
OFFSHORE{p@ssw0rds_1n_cl3ar_t3xT}
```