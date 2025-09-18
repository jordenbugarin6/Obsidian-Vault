```bash
ss -lp  '( dport = :60388 )' src 192.168.151.105 | grep -Po "(?<=pid=).*(?=,)"| sort | uniq | xargs kill

ss -lp  '( dport = :1000 )' src 10.10.14.39 | grep -Po "(?<=pid=).*(?=,)"| sort | uniq | xargs kill

kill -9 <process ID> to force kill a process
```