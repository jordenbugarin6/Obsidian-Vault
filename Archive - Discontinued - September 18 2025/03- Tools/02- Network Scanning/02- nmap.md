###### Links:
[[2.2.1 - 2.2.7 Web Application Enumeration]]

---------------------
#### Generic NMAP 
`nmap -Pn enum-sandbox` to skip ICMP host discovery since we did a prior ping to ensure that the box was already up
![[Pasted image 20240715162225.png]]`nmap -sV enum-sandbox`  for service/version detection
- Nmap identified PostgreSQL running on port 5555 instead of providing a default value of "freeciv"
![[Pasted image 20240715162443.png]]
#### NMAP scripts
`nmap -p 80 --script http-methods enum-sandbox`  futilizing NSE scripts (written in LUA) to identify http-methods
![[Pasted image 20240715163258.png]]