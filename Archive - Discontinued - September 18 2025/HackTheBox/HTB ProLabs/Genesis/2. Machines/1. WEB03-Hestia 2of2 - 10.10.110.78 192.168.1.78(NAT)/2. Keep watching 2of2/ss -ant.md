```bash
meterpreter > shell
Process 65528 created.
Channel 10 created.
ss -ant
State  Recv-Q Send-Q         Local Address:Port           Peer Address:Port Process
LISTEN 0      4096           127.0.0.53%lo:53                  0.0.0.0:*           
LISTEN 0      128                  0.0.0.0:22                  0.0.0.0:*           
ESTAB  0      0               192.168.1.78:22              10.10.14.39:52726       
ESTAB  0      176             192.168.1.78:37542           10.10.14.39:4444        
LISTEN 0      4096                       *:34721                     *:*           
LISTEN 0      4096                       *:38501                     *:*           
LISTEN 0      4096                       *:46055                     *:*           
LISTEN 0      1000                       *:41735                     *:*           
LISTEN 0      4096                       *:6123                      *:*           
LISTEN 0      4096                       *:8081                      *:*           
LISTEN 0      128                     [::]:22                     [::]:*           
LISTEN 0      4096                       *:39319                     *:*           
ESTAB  0      0      [::ffff:192.168.1.78]:38501 [::ffff:192.168.1.78]:35306       
ESTAB  0      0      [::ffff:192.168.1.78]:53432  [::ffff:10.10.14.39]:1337        
ESTAB  0      0      [::ffff:192.168.1.78]:35306 [::ffff:192.168.1.78]:38501       
ESTAB  0      0         [::ffff:127.0.0.1]:54498    [::ffff:127.0.0.1]:6123        
ESTAB  0      0         [::ffff:127.0.0.1]:6123     [::ffff:127.0.0.1]:54498  
```