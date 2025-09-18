```bash
ip a                    # Show interfaces + IPs
ip r                    # Routing table
ss -tulwn               # Listening ports
ss -tp                  # TCP sockets + owning processes
netstat -tulnp          # Ports + processes (if available)
arp -a                  # ARP cache
ip neigh show           # ARP cache (modern)
ping -c 4 <host>        # ICMP test
dig <domain>            # DNS resolution
grep nameserver /etc/resolv.conf   # DNS servers in use
dig +short myip.opendns.com @resolver1.opendns.com   # Get public IP
```