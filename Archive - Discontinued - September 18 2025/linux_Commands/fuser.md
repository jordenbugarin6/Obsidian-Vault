---
created_date: 
updated_date: 28 September 2023
type: linux
---
###### Proof of Concept
```bash
#This will kill all processes using TCP port 80 forcefully
fuser -KILL -n tcp 80

#This will kill all processes using TCP port 80
fuser -k -n tcp 80

# works forsure
 └─╼ # fuser -k 8443/tcp
8443/tcp:            380778

```

`fuser` command is use to kill port processes on linux machines.