### tcpdump not port 22
```bash
root@web01:/tmp# tcpdump -i eth1  -s 1500 port not 22                                                                                                                                                       
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode                                                                                                                                  
listening on eth1, link-type EN10MB (Ethernet), capture size 1500 bytes
18:06:50.895613 IP 0.0.0.0 > all-systems.mcast.net: igmp query v3 [max resp time 1.0s]
18:06:51.377601 IP 172.16.0.3.51820 > web01.51820: UDP, length 148
18:06:56.398815 IP 172.16.0.3.51820 > web01.51820: UDP, length 148
18:06:59.666963 IP 172.16.0.2.netbios-dgm > 172.16.0.255.netbios-dgm: UDP, length 201
18:07:01.693204 IP 172.16.0.3.51820 > web01.51820: UDP, length 148
18:07:06.955713 IP 172.16.0.3.51820 > web01.51820: UDP, length 148
18:07:12.242168 IP 172.16.0.3.51820 > web01.51820: UDP, length 148
18:07:14.400555 IP 172.16.0.2.netbios-ns > 172.16.0.255.netbios-ns: UDP, length 50
18:07:15.145982 IP 172.16.0.2.netbios-ns > 172.16.0.255.netbios-ns: UDP, length 50
18:07:15.911384 IP 172.16.0.2.netbios-ns > 172.16.0.255.netbios-ns: UDP, length 50
18:07:17.448578 IP 172.16.0.3.51820 > web01.51820: UDP, length 148
18:07:22.494959 IP 172.16.0.3.51820 > web01.51820: UDP, length 148
18:07:27.668454 IP 172.16.0.3.51820 > web01.51820: UDP, length 148
18:07:28.691922 IP 172.16.0.33.netbios-ns > 172.16.0.255.netbios-ns: UDP, length 50
18:07:29.446398 IP 172.16.0.33.netbios-ns > 172.16.0.255.netbios-ns: UDP, length 50
18:07:30.329547 IP 172.16.0.33.netbios-ns > 172.16.0.255.netbios-ns: UDP, length 50
18:07:32.673056 IP 172.16.0.3.51820 > web01.51820: UDP, length 148
18:07:37.856017 IP 172.16.0.3.51820 > web01.51820: UDP, length 148
18:07:43.140929 IP 172.16.0.3.51820 > web01.51820: UDP, length 148
18:07:48.390907 IP 172.16.0.3.51820 > web01.51820: UDP, length 148
18:07:53.708259 IP 172.16.0.3.51820 > web01.51820: UDP, length 148
18:07:58.757748 IP 172.16.0.3.51820 > web01.51820: UDP, length 148
18:08:01.695750 ARP, Request who-has 172.16.0.1 tell 172.16.0.32, length 46
18:08:03.880186 IP 172.16.0.3.51820 > web01.51820: UDP, length 148
18:08:09.106400 IP 172.16.0.3.51820 > web01.51820: UDP, length 148
18:08:14.131747 IP 172.16.0.3.51820 > web01.51820: UDP, length 148
18:08:19.158073 IP 172.16.0.3.51820 > web01.51820: UDP, length 148
18:08:23.984600 ARP, Request who-has 172.16.0.3 tell web01, length 28
18:08:23.984922 ARP, Reply 172.16.0.3 is-at 00:50:56:b0:2f:48 (oui Unknown), length 46
18:08:24.223285 IP 172.16.0.3.51820 > web01.51820: UDP, length 148
18:08:29.258261 ARP, Request who-has web01 tell 172.16.0.3, length 46
18:08:29.258296 ARP, Reply web01 is-at 00:50:56:b0:61:4f (oui Unknown), length 28
18:08:29.485661 IP 172.16.0.3.51820 > web01.51820: UDP, length 148
18:08:34.774649 IP 172.16.0.3.51820 > web01.51820: UDP, length 148
18:08:36.375082 IP 172.16.0.33.netbios-ns > 172.16.0.255.netbios-ns: UDP, length 50
18:08:37.111845 IP 172.16.0.33.netbios-ns > 172.16.0.255.netbios-ns: UDP, length 50
18:08:37.867973 IP 172.16.0.33.netbios-ns > 172.16.0.255.netbios-ns: UDP, length 50
18:08:39.821442 IP 172.16.0.3.51820 > web01.51820: UDP, length 148

```