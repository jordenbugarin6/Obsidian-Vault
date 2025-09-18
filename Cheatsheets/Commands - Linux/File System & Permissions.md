
```bash
ls -alh /etc/           # Config files
find / -perm -4000 2>/dev/null   # SUID binaries
getcap -r / 2>/dev/null          # List binaries with capabilities
find / -type f -name "*.conf" 2>/dev/null   # Config files
df -h                   # Disk usage
mount | column -t       # Mounted file systems
stat <file>             # Show file timestamps (atime, mtime, ctime)
lsattr -R /etc 2>/dev/null      # File attributes (immutable, append-only)
find / -writable -type d 2>/dev/null    # World-writable dirs
find / -perm -2 -type f 2>/dev/null     # World-writable files
grep -Ri "password" /etc 2>/dev/null    # Look for cleartext creds
```