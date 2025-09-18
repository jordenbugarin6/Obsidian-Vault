```bash
dpkg -l                 # Debian-based installed packages
rpm -qa                 # RedHat-based installed packages
which <binary>          # Locate binary in PATH
whereis <binary>        # Show binary, man page, source
strings /usr/bin/<binary> | less   # Inspect a binary for hints
echo $PATH | tr ':' '\n'           # Print PATH directories
```