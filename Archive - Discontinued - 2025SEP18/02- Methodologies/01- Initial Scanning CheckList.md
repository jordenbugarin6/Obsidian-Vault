---
created_date: 01 September 2023
updated_date: 11 September 2023
type: windows/linux/template
---
### Machine Information
```
IP Address:
Hostname:
Operating System:
Exploit & Port:
Privilege Escalation:
Credentials:

Path to Box:

-> NIX01 - 192.168.1.1
--> NIX02 - 192.168.1.2
```
### High-Level Summary

A brief description of the attack chain with machine names, including the depth of compromise should be included here.

-------------
### Initial Scanning

- [ ] `Ping`
- [ ] `Rustscan`
- [ ] `Quick TCP Nmap`
- [ ] `Full TCP Nmap`
- [ ] `Full UDP Nmap`

#ping
- Pinging to ensure box is up, get brief OS information.
```bash
ping $ip_address
```

#rustscan 
- Typically way faster than nmap, gives very brief port information - but enough to get started while other nmap scripts run.
```bash
rustscan -a $ip_address
```

#quick #tcp #nmap 
- Quick Nmap to get initial port information.
```bash
nmap -sC -sV -Pn $ip_address
```

#full #tcp #nmap 
- Full TCP Nmap to get all port information.
```bash
nmap -sC -sV -p- -Pn $ip_address
```
##### Initial Scanning Notes:
#initial #scanning #notes
- NOTES
- NOTES
- NOTES
-------


---
---

# Summary of Findings

|No.|Vulnerability Name|OTG|Affected Host/Path|Impact|Likelihood|Risk|Observation/Implication|Recommendation|Test Evidence|
|---|------------------|---|------------------|------|----------|----|-----------------------|--------------|-------------|
|{{index}}|{{vulnerability}}|{{otg}}|{{entity}}|{{impact}}|{{likelihood}}|{{risk}}|{{comment}}|{{remediation}}|{{evidence}}|


