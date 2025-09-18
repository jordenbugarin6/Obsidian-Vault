https://github.com/unode/firefox_decrypt

Simple tool to conduct testing on:


gitcloned the tool
```bash
┌──(root💀gobots)-[27Aug2025 04:36:22]-[/home/kali/Downloads]                                                                                                                                                
└─# git clone https://github.com/unode/firefox_decrypt.git                                                                                                                                                   
Cloning into 'firefox_decrypt'...
remote: Enumerating objects: 1382, done.
remote: Counting objects: 100% (292/292), done.
remote: Compressing objects: 100% (38/38), done.
remote: Total 1382 (delta 273), reused 254 (delta 254), pack-reused 1090 (from 2)
Receiving objects: 100% (1382/1382), 482.80 KiB | 8.94 MiB/s, done.
Resolving deltas: 100% (870/870), done.
```
in a new firefox application browse to facebook and pretend to login with `testing:testing`
![[Pasted image 20250827004807.png]]
and save the  credentials to the firefox browser - once saved to the browser utilize `about:profiles` to get the `root` directory of the firefox profile

![[Pasted image 20250827005704.png]]
once we have the root we can run the tool and dump the passwords
![[Pasted image 20250827005947.png]]
```bash
┌──(root💀gobots)-[27Aug2025 04:40:04]-[/home/kali/Downloads/firefox_decrypt]
└─# python3 firefox_decrypt.py /home/kali/.mozilla/firefox/f5egog0k.default-esr
2025-08-27 04:41:30,619 - WARNING - profile.ini not found in /home/kali/.mozilla/firefox/f5egog0k.default-esr
2025-08-27 04:41:30,619 - WARNING - Continuing and assuming '/home/kali/.mozilla/firefox/f5egog0k.default-esr' is a profile location

Website:   https://www.facebook.com
Username: 'testing'
Password: 'testing'
```
after browsing to `about:logins` we can see that these save credentials were properly dumped
![[Pasted image 20250827010203.png]]