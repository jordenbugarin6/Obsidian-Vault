## Overview
This methodology provides structured phases and specific tasks for assessing the security of a web application. Each phase includes objectives, tools, and example commands to streamline your testing process.

---

## Methodology Checklist

### 1. **Information Gathering**
- [ ] **Objective**: Collect information about the target application.
- [ ] **Passive Reconnaissance**:
  - [ ] Check for subdomains, DNS records, and public disclosures.
  - [ ] Tools: `Sublist3r`, `theHarvester`, `crt.sh`.
  - [ ] **Example Command**:
    - [ ] `Sublist3r -d <target_domain>`
- [ ] **Search Engine Recon**:
  - [ ] Search for sensitive files or information using Google Dorking.
  - [ ] Tools: Search Engines (Google, Bing).
  - [ ] **Example Search**:
    - [ ] `site:<target_domain> filetype:pdf`

### 2. **Application Mapping**
- [ ] **Objective**: Identify all accessible points and inputs.
- [ ] **Content Discovery**:
  - [ ] Enumerate directories and files.
  - [ ] Tools: `Gobuster`, `dirb`.
  - [ ] **Example Command**:
    - [ ] `gobuster dir -u <target_url> -w <wordlist>`
- [ ] **Identify Input Fields**:
  - [ ] Locate all form fields, parameters, and headers for potential testing.
  - [ ] Tools: Browser Developer Tools, Burp Suite.
  
### 3. **Vulnerability Identification**
- [ ] **Objective**: Identify vulnerabilities in the application.
- [ ] **Authentication Testing**:
  - [ ] Test login mechanisms and password reset functionalities.
  - [ ] Tools: Burp Suite, `Hydra`.
  - [ ] **Example Command**:
    - [ ] `hydra -l <username> -P <password_list> <target_url> http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect"`
- [ ] **Session Management**:
  - [ ] Test for session fixation, hijacking, and weaknesses in session tokens.
  - [ ] Tools: Burp Suite, OWASP ZAP.
- [ ] **Access Control**:
  - [ ] Check for vertical and horizontal privilege escalation.
  - [ ] Tools: Burp Suite, Postman.
  
### 4. **Input-Based Vulnerabilities**
- [ ] **Objective**: Test user inputs for potential vulnerabilities.
- [ ] **SQL Injection**:
  - [ ] Test for SQLi in parameters, headers, and cookies.
  - [ ] Tools: `sqlmap`, Burp Suite.
  - [ ] **Example Command**:
    - [ ] `sqlmap -u <target_url> --dbs`
- [ ] **Cross-Site Scripting (XSS)**:
  - [ ] Test for reflective, stored, and DOM-based XSS.
  - [ ] Tools: Burp Suite, OWASP ZAP.
  - [ ] **Example Payload**:
    - [ ] `<script>alert('XSS')</script>`
- [ ] **Command Injection**:
  - [ ] Check for command execution via vulnerable parameters.
  - [ ] Tools: Burp Suite, `commix`.
  - [ ] **Example Payload**:
    - [ ] `; cat /etc/passwd`
  
### 5. **Business Logic Testing**
- [ ] **Objective**: Test for flaws in the application’s business logic.
- [ ] **Test Workflows and Restrictions**:
  - [ ] Bypass logical constraints (e.g., invalid price manipulation).
  - [ ] Tools: Burp Suite, Manual Testing.
- [ ] **Rate-Limiting and Brute-Force Protections**:
  - [ ] Check if application blocks excessive requests.
  - [ ] Tools: `intruder` in Burp Suite.
  
### 6. **Security Misconfigurations**
- [ ] **Objective**: Identify misconfigurations in application and server settings.
- [ ] **Sensitive File Exposure**:
  - [ ] Look for config files, environment files, and backup files.
  - [ ] Tools: `dirsearch`, Burp Suite.
- [ ] **Error Handling**:
  - [ ] Identify error messages that reveal stack traces or sensitive data.
  - [ ] Tools: Burp Suite, Manual Inspection.
- [ ] **HTTP Headers Security**:
  - [ ] Check headers for security settings like CSP, HSTS, X-Frame-Options.
  - [ ] Tools: `Nikto`, `curl`.
  - [ ] **Example Command**:
    - [ ] `curl -I <target_url>`
  
### 7. **Exploitation**
- [ ] **Objective**: Exploit identified vulnerabilities.
- [ ] **Automated Exploits**:
  - [ ] Use tools to automate exploitation where possible.
  - [ ] Tools: Metasploit, Burp Suite.
- [ ] **Manual Exploitation**:
  - [ ] Craft custom payloads based on vulnerability findings.

### 8. **Post-Exploitation**
- [ ] **Objective**: Further explore compromised assets and escalate access.
- [ ] **Explore Application Data**:
  - [ ] Access sensitive information within the application.
  - [ ] Tools: SQL, Manual Browsing.
- [ ] **Privilege Escalation**:
  - [ ] Attempt to gain higher privileges if necessary.
  - [ ] Tools: Custom scripts, Metasploit.

### 9. **Reporting**
- [ ] **Objective**: Document findings, proofs, and recommendations.
- [ ] **Summary of Findings**: High-level overview.
- [ ] **Detailed Findings**: Screenshots, commands, and evidence.
- [ ] **Remediation Recommendations**: Steps for fixing vulnerabilities.

---

### Appendix: Tools Summary

| Phase                 | Tool                  | Purpose                          |
|-----------------------|-----------------------|----------------------------------|
| Information Gathering | `Sublist3r`, `theHarvester` | Domain and subdomain discovery |
| Application Mapping   | `Gobuster`, Burp Suite | Content discovery               |
| Vulnerability Scanning| `sqlmap`, OWASP ZAP   | Identifying and exploiting vulnerabilities |
| Business Logic Testing| Burp Suite            | Logical and workflow tests      |
| Misconfigurations     | `dirsearch`, `Nikto`  | File exposure and header checks |
| Exploitation          | Metasploit, Burp Suite| Automated exploitation          |
| Post-Exploitation     | SQL, Custom scripts   | Data extraction and privilege escalation |
