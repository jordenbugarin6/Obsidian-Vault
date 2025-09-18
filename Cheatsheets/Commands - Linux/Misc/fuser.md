`fuser` command is use to kill port processes on Linux machines.

```bash
#this will kill all processes using TCP port 80 forcefully
fuser -KILL -n tcp 80 

#this will kill all processes using TCP port 80
fuser -k -n tcp 80

#works forsure
fuser -k 8443/tcp
8443/tcp:            380778

```