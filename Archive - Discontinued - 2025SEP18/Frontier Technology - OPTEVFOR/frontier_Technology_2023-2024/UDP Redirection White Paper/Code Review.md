```bash
# Search for system calls
grep -rnw . -e 'system('
grep -rnw . -e 'exec('

# Search for network activity
grep -rnw . -e 'wget'
grep -rnw . -e 'curl'
grep -rnw . -e 'nc'

# Search for bash commands
grep -rnw . -e 'bash'
```