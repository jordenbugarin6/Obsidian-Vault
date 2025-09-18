```bash
uname -a                # Kernel info
cat /etc/os-release     # OS + distro version
hostnamectl             # Hostname + OS + kernel details
uptime                  # System uptime
dmesg | less            # Kernel ring buffer
lsmod                   # Loaded kernel modules
cat /proc/cpuinfo | grep name   # CPU model (VM/host detection)
lsblk                   # List block devices (partitions, disks)
```

