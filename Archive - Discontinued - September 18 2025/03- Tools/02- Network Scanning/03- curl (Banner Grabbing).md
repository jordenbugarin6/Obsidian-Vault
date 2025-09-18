###### Links:
[[2.2.1 - 2.2.7 Web Application Enumeration]]

---------------------
#### HTTP Banner Grabbing
`curl -I http://enum-sandbox` manual banner grabbing `HTTP` protocols
Example:
![[Pasted image 20240715164536.png]]
`-i` presents the longer output
![[Pasted image 20240715164719.png]]

---------------------
#### Non-HTTP Banner grabbing
`netcat -v enum-sandbox 22` to grab version of ssh running
![[Pasted image 20240715164956.png]]