```bash
ls -alh /var/log/       # List logs
tail -n 50 /var/log/syslog    # Debian logs
tail -n 50 /var/log/messages  # RedHat logs
journalctl -u ssh --no-pager | tail -50   # SSH-specific logs
dmesg | grep -i usb     # Detect USB insertions
tac /var/log/syslog | less    # Read logs in reverse
```