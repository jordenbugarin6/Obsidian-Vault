```bash
ps aux                  # All processes
ps aux --forest         # Tree view
top                     # Live process monitor
systemctl list-units --type=service   # Active services
journalctl -xe          # System logs
pmap <pid>              # Memory map of a process
lsof -i                 # Open sockets (process -> port)
ls -lah /etc/cron*      # System/user cron jobs
```