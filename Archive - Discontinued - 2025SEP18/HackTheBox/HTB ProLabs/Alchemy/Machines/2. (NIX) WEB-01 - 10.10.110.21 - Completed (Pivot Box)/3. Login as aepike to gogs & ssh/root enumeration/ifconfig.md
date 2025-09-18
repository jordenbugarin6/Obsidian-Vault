```bash
root@web01:~# ifconfig                                                                                                                                                                                      
docker0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500                                                                                                                                               
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255                                                                                                                                      
        ether 02:42:65:27:95:09  txqueuelen 0  (Ethernet)                                                                                                                                                   
        RX packets 3498027  bytes 5649265260 (5.6 GB)                                                                                                                                                       
        RX errors 0  dropped 0  overruns 0  frame 0 
        TX packets 3175890  bytes 367419388 (367.4 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.10.110.21  netmask 255.255.255.0  broadcast 10.10.110.255
        ether 00:50:56:b0:b4:3c  txqueuelen 1000  (Ethernet)
        RX packets 6233757  bytes 1089706795 (1.0 GB)
        RX errors 0  dropped 32  overruns 0  frame 0
        TX packets 5698734  bytes 6475125961 (6.4 GB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.16.0.21  netmask 255.255.255.0  broadcast 172.16.0.255
        ether 00:50:56:b0:61:4f  txqueuelen 1000  (Ethernet)
        RX packets 1428161  bytes 366748427 (366.7 MB)
        RX errors 0  dropped 51  overruns 0  frame 0
        TX packets 1378239  bytes 178885409 (178.8 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 26276  bytes 2304470 (2.3 MB)
        RX errors 0  dropped 0  overruns 0  frame 0 
        TX packets 26276  bytes 2304470 (2.3 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
lxcbr0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 10.0.3.1  netmask 255.255.255.0  broadcast 0.0.0.0
        ether 00:16:3e:00:00:00  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

vethcaf4631: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        ether fa:7c:83:1e:57:fe  txqueuelen 0  (Ethernet)
        RX packets 3498027  bytes 5698237638 (5.6 GB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 3175890  bytes 367419388 (367.4 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

```