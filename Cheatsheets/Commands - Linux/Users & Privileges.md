```bash
whoami                  # Current user
id                      # UID, GID, groups
groups                  # Groups for current user
cat /etc/passwd         # List users
cat /etc/group          # Groups defined
getent passwd           # Enumerate users (AD/LDAP-aware)
awk -F: '($3 == 0) {print}' /etc/passwd  # Find UID 0 (root) users
sudo -l                 # Check sudo rights
sudo -V | head -n1      # Sudo version (check for vulns)
last                    # Recent logins
w                       # Who is logged in + activity
lastlog | grep -v "Never"   # Accounts that have logged in
```