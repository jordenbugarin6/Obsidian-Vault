### SOCAT Linux UDP Redirection Routing
- This is to simulate snmp being open on scada 172.16.0.20 and redirecting traffic going from kali to web01 to the scada machine.
kali machine
-> web01 10.10.110.21 pivot box (where socat is located)
--> scada 172.16.0.20 
### Begin:
- need a static socat binary, utilized the one on build requires dependencies.
![[Pasted image 20240626144642.png]]
##### Socat static binary download
- https://github.com/andrew-d/static-binaries/blob/master/binaries/linux/x86_64/socat
##### Static socat transfer to web01
- on web01 transferred over the static binary to /dev/testing, a directory that I made due to the original mounted drive being at 100% capacity
![[Pasted image 20240626161344.png]]
##### Testing to make sure udp traffic is working from kali -> web01
on web01
- setting up a udp listener on port 161
```bash
root@web01:/dev/testing# nc -u -l 161
hello
```
on kali machine
- connected and sent a hello message
```bash
┌──(kali㉿gobots)-[26Jun2024 20:24:42]-[~/SUT]
└─$ nc -u 10.10.110.21 161 
hello

```
##### Testing to make sure udp traffic is working from kali -> web01 -> scada

###### 1 - WEB01
- setting up the `UDP` port forward with `socat`, any traffic that is being received on port 161 is being forked and sent to the target IP on port `161`
```
./socat UDP4-RECVFROM:161,fork UDP4-SENDTO:172.16.0.20:161
./socat.exe UDP4-RECVFROM:161,fork UDP4-SENDTO:172.16.0.20:161
```
###### 2 - Kali Machine
- sending udp traffic to web01 with testing123
```bash
nc -u 10.10.110.21 161
```
###### 3 - SCADA
- upgrading to tty and setting up `UDP` listener on port 161
```bash
root@scada:~# python3 -c 'import pty; pty.spawn("/bin/bash")'
root@scada:~# nc -ulvp 161
Listening on [0.0.0.0] (family 0, port 161)                                                           
Connection from 172.16.0.21 34889 received!   
testing123
```
![[Pasted image 20240626164829.png]]
### IPTABLES Linux UDP Redirection Routing
IPTABLES Commands:
Lists all iptables 
```bash
iptables -L
```
original IP Tables
```bash
root@web01:/dev/testing# iptables -L
Chain INPUT (policy ACCEPT)
target     prot opt source               destination         
ACCEPT     tcp  --  anywhere             anywhere             tcp dpt:domain
ACCEPT     udp  --  anywhere             anywhere             udp dpt:domain
ACCEPT     tcp  --  anywhere             anywhere             tcp dpt:bootps
ACCEPT     udp  --  anywhere             anywhere             udp dpt:bootps

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination         
DOCKER-USER  all  --  anywhere             anywhere            
DOCKER-ISOLATION-STAGE-1  all  --  anywhere             anywhere            
ACCEPT     all  --  anywhere             anywhere             ctstate RELATED,ESTABLISHED
DOCKER     all  --  anywhere             anywhere            
ACCEPT     all  --  anywhere             anywhere            
ACCEPT     all  --  anywhere             anywhere            
ACCEPT     all  --  anywhere             anywhere            
ACCEPT     all  --  anywhere             anywhere            

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination         

Chain DOCKER (1 references)
target     prot opt source               destination         
ACCEPT     tcp  --  anywhere             172.17.0.2           tcp dpt:3000

Chain DOCKER-ISOLATION-STAGE-1 (1 references)
target     prot opt source               destination         
DOCKER-ISOLATION-STAGE-2  all  --  anywhere             anywhere            
RETURN     all  --  anywhere             anywhere            

Chain DOCKER-ISOLATION-STAGE-2 (1 references)
target     prot opt source               destination         
DROP       all  --  anywhere             anywhere            
RETURN     all  --  anywhere             anywhere            

Chain DOCKER-USER (1 references)
target     prot opt source               destination         
RETURN     all  --  anywhere             anywhere   
```
iptables back up revert
- this didnt work to revert
```bash
iptables-save > /dev/testing/iptables_backup
iptables-restore < /dev/testing/iptables_backup
```
##### On kali machine testing adding specific rules and removing it amongst other iptable rules.
#iptables
- creating two iptable rules
```bash
iptables -A FORWARD -p udp --dport 5000 -d 192.168.1.10 -j ACCEPT 
iptables -A FORWARD -p udp --dport 5001 -d 192.168.1.10 -j ACCEPT 
```
- listing the iptables created with `iptables -L` to see the rules that were created
![[Pasted image 20240702121655.png]]
- command with `-D` to delete the specific rule added
```bash
iptables -D FORWARD -p udp --dport 5000 -d 192.168.1.10 -j ACCEPT
```
- showing that the rule with dport 5000 was properly removed
![[Pasted image 20240702122334.png]]
##### Helpful iptable commands
creating iptable rule that will edit the `nat` table for the `prerouting` option, take in traffic coming into 
```bash
iptables -t nat -A PREROUTING -p udp --sport 161 -j DNAT --to-destination 172.16.0.20:161
```
proof that it was added with `iptables -t nat -L PREROUTING`
![[Pasted image 20240702134956.png]]
command to delete the rule
```bash
iptables -t nat -D PREROUTING -p udp --sport 161 -j DNAT --to-destination 172.16.0.20:161
```
proof that the rule was deleted
![[Pasted image 20240702135028.png]]
prerouting & postrouting
```bash
iptables -t nat -A PREROUTING -s 10.10.14.39 -p udp --dport 161 -j DNAT --to-destination 10.10.110.21
iptables -t nat -A POSTROUTING -d 172.16.0.20 -p udp --dport 161 -j SNAT --to-source 10.10.110.21
```
to list the rules in line number format
```bash
iptables -t nat -L PREROUTING --line-numbers
iptables -t nat -L POSTROUTING --line-numbers
```
to delete the rules by stating the line numbers
```bash
iptables -t nat -D PREROUTING 1
iptables -t nat -D POSTROUTING 1
```
to delete the rules by restating the rules
```bash
iptables -t nat -D PREROUTING -s 10.10.14.39 -p udp --dport 161 -j DNAT --to-destination 10.10.110.21
iptables -t nat -D POSTROUTING -d 172.16.0.20 -p udp --dport 161 -j SNAT --to-source 10.10.110.21
```
#### Creating iptable rules that will redirect incoming udp traffic on port 161 to a destination ip and port
Hosted in the `ALCHEMY` HTB LAB:
Kali Machine 10.10.14.39 
-> WEB01 10.10.110.21 pivot box (IPTABLES Modifications)
--> SCADA 172.16.0.20 
###### Prerouting
The `PREROUTING` rule will redirect incoming SNMP traffic destined for `10.10.110.21` to `172.16.0.20`.
```bash
iptables -t nat -A PREROUTING -d 10.10.110.21 -p udp --dport 161 -j DNAT --to-destination 172.16.0.20:161
```
- **`iptables`**: This command is used to manage the Linux kernel's netfilter firewall.
- **`-t nat`**: Specifies the `nat` table in `iptables`, where Network Address Translation (NAT) rules are configured.
- **`-A PREROUTING`**: Appends (`-A`) the rule to the `PREROUTING` chain of the `nat` table. This chain is processed as soon as packets arrive on the network interface.
- **`-d 10.10.110.21`**: Matches packets with a destination IP address of `10.10.110.21`.
- **`-p udp --dport 161`**: Specifies UDP packets destined for port `161`.
- **`-j DNAT --to-destination 172.16.0.20:161`**: Performs Destination NAT (DNAT). When packets arrive with a destination IP of `10.10.110.21` and are UDP packets destined for port `161`, this rule changes (DNATs) their destination to `172.16.0.20` on port `161`. Essentially, it redirects incoming SNMP traffic aimed at `10.10.110.21` to `172.16.0.20`.
###### Postrouting
The `POSTROUTING` rule will handle the forwarding of SNMP traffic from `10.10.110.21` to `172.16.0.20` without altering the source IP address.
```bash
iptables -t nat -A POSTROUTING -s 10.10.110.21 -p udp --dport 161 -j SNAT --to-source 172.16.0.20
```
- **`iptables`**: The command to manage the Linux kernel's netfilter firewall.
- **`-t nat`**: Specifies the `nat` table where NAT rules are configured.
- **`-A POSTROUTING`**: Appends (`-A`) the rule to the `POSTROUTING` chain of the `nat` table. This chain is processed after routing decisions are made for outgoing packets.
- **`-s 10.10.110.21`**: Matches packets with a source IP address of `10.10.110.21`.
- **`-p udp --dport 161`**: Specifies UDP packets destined for port `161`.
- **`-j SNAT --to-source 172.16.0.20`**: Performs Source NAT (SNAT). When packets originate from `10.10.110.21` and are UDP packets destined for port `161`, this rule changes (SNATs) their source IP address to `172.16.0.20`. This ensures that when SNMP traffic flows out from `10.10.110.21` to `172.16.0.20`, it appears to come from `172.16.0.20` rather than `10.10.110.21`.
##### The Testing:
###### 1 - WEB01 10.10.110.21 (172.16.0.21 internal IP)
As `root` user modifying the `PREROUTING` & `POSTROUTING` nat tables.
The `PREROUTING` rule will redirect incoming SNMP traffic destined for `10.10.110.21` to `172.16.0.20`.
The `POSTROUTING` rule will handle the forwarding of SNMP traffic from `10.10.110.21` to `172.16.0.20` without altering the source IP address.
```
iptables -t nat -A PREROUTING -d 10.10.110.21 -p udp --dport 161 -j DNAT --to-destination 172.16.0.20:161
iptables -t nat -A POSTROUTING -s 10.10.110.21 -p udp --dport 161 -j SNAT --to-source 172.16.0.20
```
###### 2 - Kali Machine
- sending udp traffic to web01 with testing123
```bash
nc -u 10.10.110.21 161
testingtestingtesting
```
###### 3 - SCADA
- upgrading to tty and setting up `UDP` listener on port 161
```bash
root@scada:~# python3 -c 'import pty; pty.spawn("/bin/bash")'
root@scada:~# nc -ulvp 161
nc -ulvp 161
Listening on [0.0.0.0] (family 0, port 161)
Connection from 10.10.14.39 33424 received!
testingtestingtesting
```
![[Pasted image 20240702160029.png]]
##### The Cleanup:
to list the rules in line number format
```bash
iptables -t nat -L PREROUTING --line-numbers
iptables -t nat -L POSTROUTING --line-numbers
```
![[Pasted image 20240702161321.png]]
to delete the rules by stating the line numbers
```bash
iptables -t nat -D PREROUTING 2
iptables -t nat -D POSTROUTING 4
```
showing that the lines were deleted and are no longer showing in the `PREROUTING` & `POSTROUTING` tables
![[Pasted image 20240702161442.png]]
### Windows socat (XP and ON)
https://github.com/tech128/socat-1.7.3.0-windows
- UDP traffic cannot traverse proxychains, for this reason the path is below - this would simulate an actual SUT and already being plugged into the network.

-> WEB01
--> DC (socat location)
---> SCADA Machine

On windows machine put all `socat` files onto machine, in this example I put all the `.dlls` and executable required on the machine as a `DOMAIN ADMIN`
![[Pasted image 20240705164921.png]]
once socat was on the machine, I ran this command `shell .\socat.exe UDP4-RECVFROM:161,fork UDP4-SENDTO:172.16.0.20:161` to forward all incoming udp traffic on `161` to the 172.16.0.20

sending a `nc -u 172.16.0.2 161` to the DC![[Pasted image 20240705171213.png]]\
Receiving it on the `SCADA` machine
![[Pasted image 20240705171316.png]]
