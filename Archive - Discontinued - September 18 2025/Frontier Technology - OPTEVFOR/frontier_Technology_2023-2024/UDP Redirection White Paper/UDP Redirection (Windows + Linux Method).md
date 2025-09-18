## SOCAT Linux UDP Redirection Routing

This document describes the process of simulating SNMP being open on SCADA (172.16.0.20) and redirecting traffic from Kali to web01, then to the SCADA machine.

**Network Configuration:**

- **Kali Machine (10.10.14.39)** - Attacking Machine
	- **web01 (10.10.110.21)** - Pivot box where `socat` is located
		- **SCADA (172.16.0.20)** 
### Socat Steps for a Linux Pivot box

#### 1. Static `socat` Binary

A static `socat` binary is required to avoid dependency issues.
- Download link: [Socat static binary](https://github.com/andrew-d/static-binaries/blob/master/binaries/linux/x86_64/socat)
- Transfer the static binary to web01, placing it in `/dev/testing` due to full capacity on the original drive.
![[Pasted image 20240626144642.png]]
##### Step 1: Configure `web01`
Transfer `socat` to `web01` and set up `UDP` port forward:
```bash
./socat UDP4-RECVFROM:161,fork UDP4-SENDTO:172.16.0.20:161
```
##### Step 2: Send Traffic from Kali Machine
Send `UDP` traffic via port `161`
```bash
nc -u 10.10.110.21 161
nc -u 10.10.13.39 161
```
##### Step 3: Configure SCADA
Upgrading `tty`
Listening for `UDP` traffic incoming from port `161`
```bash
root@scada:~# python3 -c 'import pty; pty.spawn("/bin/bash")'
root@scada:~# nc -ulvp 161
Listening on [0.0.0.0] (family 0, port 161)
Connection from 172.16.0.21 34889 received!
testing123
```
![[Pasted image 20240626164829.png]]
### IPTABLES Linux UDP Redirection Routing

**IPTABLES Commands:**
As `root` user modifying the `PREROUTING` & `POSTROUTING` nat tables.
The `PREROUTING` rule will redirect incoming SNMP traffic destined for `10.10.110.21` to `172.16.0.20`.
The `POSTROUTING` rule will handle the forwarding of SNMP traffic from `10.10.110.21` to `172.16.0.20` without altering the source IP address.
##### Step 1:  Redirect WEB01 10.10.110.21 (172.16.0.21 internal IP) UDP Traffic
List all IP rules with line numbers:
- **-L** List all rules in the selected chain or all chains if no chain is specified
```bash
iptables -t nat -L PREROUTING --line-numbers
iptables -t nat -L POSTROUTING --line-numbers
```
To redirect UDP traffic:
```bash
iptables -t nat -A PREROUTING -d 10.10.110.21 -p udp --dport 161 -j DNAT --to-destination 172.16.0.20:161
iptables -t nat -A POSTROUTING -s 10.10.110.21 -p udp --dport 161 -j SNAT --to-source 172.16.0.20
```
##### Step 2: Send Traffic from Kali Machine
```bash
nc -u 10.10.110.21 161
testingtestingtesting
```
##### Step 3: Configure SCADA 
```bash
root@scada:~# python3 -c 'import pty; pty.spawn("/bin/bash")'
root@scada:~# nc -ulvp 161
Listening on [0.0.0.0] (family 0, port 161)
Connection from 10.10.14.39 33424 received!
testingtestingtesting
```
![[Pasted image 20240702160029.png]]
###### IPTable Cleanup
To list the rules in line number format
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
showing that the lines `2` & `4` were deleted and are no longer showing in the `PREROUTING` & `POSTROUTING` tables
![[Pasted image 20240702161442.png]]
to delete the rules by restating the rules implemented with a `-D` switch instead of a `-A`
```bash
iptables -t nat -D PREROUTING -d 10.10.110.21 -p udp --dport 161 -j DNAT --to-destination 172.16.0.20:161
iptables -t nat -D POSTROUTING -s 10.10.110.21 -p udp --dport 161 -j SNAT --to-source 172.16.0.20
```

### Windows Socat (XP and Onwards)

**Network Configuration:**

- **web01 (10.10.110.21)** 
	-  **DC (172.16.0.2)** 
		- **SCADA (172.16.0.20)** 

**Download link:** [Windows Socat](https://github.com/tech128/socat-1.7.3.0-windows)
**Setup:**
- Place all necessary `socat` files and `.dlls` on the machine as a `DOMAIN ADMIN`.
- Run `socat` to forward all incoming UDP traffic on port 161 to `172.16.0.20`:

```bash
shell .\socat.exe UDP4-RECVFROM:161,fork UDP4-SENDTO:172.16.0.20:161
```

![[Pasted image 20240705164921.png]]
sending a `nc -u 172.16.0.2 161` to the DC from `WEB01` - the starting point as if we were plugged into the network like we would be on test
![[Pasted image 20240705171213.png]]\
Receiving it on the `SCADA` machine
![[Pasted image 20240705171316.png]]
### Script to make static socat (linux)

```bash
# Clone the Socat repository
git clone https://github.com/3ndG4me/socat.git
cd socat

# Clean previous builds
make clean

# Configure the build process for static linking
./configure LDFLAGS="-static"

# Compile the source code
make

# Verify the Socat binary
if [ -f "socat" ]; then
    echo "Socat binary successfully compiled."
    file socat
else
    echo "Compilation failed. Please check the output for errors."
fi

```