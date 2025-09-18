# General Accesses
- * = used

#### Visual
Attacker (10.10.14.39)
-> WEB-01 (10.10.110.21 // )
--> SCADA (172.16.0.20)

| Server IP Address           | Hostname | Usernames                                      | Password                                         | Where were the credentials found                                                                                                                                                                                                                      | What the credentials were used for                                                                                                                                     | What this led to                                                                                                                       | Flags                                                                                                                                                               | Links                                                                                           |
| --------------------------- | -------- | ---------------------------------------------- | ------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| 10.10.110.21<br>(1st PIVOT) | WEB-01   | calde_ldap*<br>calde_ldap@alchemy.htb<br>calde | CsAdlLDAPMoDeBrnd12!                             | The credentials were found by setting up responder to host an `ldap` server and utilize the post request for `http://10.10.110.21/login` in burpsuite, send to repeater and change the IP address that the `ldapuri` is sending to your kali machine. | Logging into `http://10.10.110.21:3000` as `calde_ldap` user                                                                                                           | Ability to `git clone` all repo's and utilize `git log` or just sifting through all website commits and get credentials to aepike user | N/A                                                                                                                                                                 | [[Initial Credentials - 'calde_ldap' user]]                                                     |
| 10.10.110.21                | WEB-01   | aepike*<br>aepike@alchemy.htb                  | LandIAtErOUs                                     | Credentials were found utilizing `git log` once the repos were pulled with `calde_ldap` access                                                                                                                                                        | Logging into `http://10.10.110.21:3000` as `aepike` user & `ssh aepike@10.10.110.21`                                                                                   | Led to grabbing the first flag & Privilege Escalation via `pwnkit`<br><br>Initial Network Access to internal network `172.16.0.0/24`   | Overfly:<br>ALCHEMY{Imp0R7AN7_9i7_uS3R2} <br><br>A New Beginning:<br>ALCHEMY{7h3_8391nn1n9_0f_7h3_3nd}                                                              | [[1. Initial Login - Flag 1 (Overfly)]]   <br>                  [[7. Flag 2 (A New Beginning)]] |
| 172.16.0.2                  | DC       | calde_ldap<br>james<br>Administrator (Local)   | CsAdlLDAPMoDeBrnd12!<br>greenday<br>tXxAtjrJnKrz | `james` credentials were found by kerberoasting the `DC` and breaking the hashes via john.<br>`Administrator` credentials were found in [[8. machine password.xlsx]]                                                                                  | `james` credentials were utilized to xfreerdp into the DC<br>`Administrator` credentials were used to DCSync against the domain and get Domain Administrator NTLM Hash | Domain Administrator NTLM Hash                                                                                                         | Anxiety:<br>ALCHEMY{WhA7_50M37H1Ng_15n7_R1gH7}<br><br>What would you trade:<br>ALCHEMY{d34R_L0RD_wH47_y34r_15_17?}<br><br>                                          | [[7. xfreerdp (1st flag) Anxiety]]<br><br>[[11. psexec as DA (2nd Flag) What would you trade]]  |
| 172.16.0.20                 | SCADA    | admin                                          | admin                                            | Default credentials for SCADABR application hosted on `http://172.16.0.20` through proxy                                                                                                                                                              | Authenticated Web Shell with searchsploit script `49734.py`                                                                                                            | Initial access via RCE on 172.16.0.20, and privilege escalation via `/usr/bin/lxc` container process                                   | Is free will an illusion:<br>ALCHEMY{Wh47_d347H_4_d3s7In47i0N_0R_7h3_j0URn3y}<br><br>We have never been modern:<br>ALCHEMY{whA7_HaV3_1_D0N3?_F0R91V3_91V3_l0RD}<br> | [[1. Is free will an illusion]]<br><br>[[2. We have never been modern]]                         |
|                             |          |                                                |                                                  |                                                                                                                                                                                                                                                       |                                                                                                                                                                        |                                                                                                                                        |                                                                                                                                                                     |                                                                                                 |
|                             |          |                                                |                                                  |                                                                                                                                                                                                                                                       |                                                                                                                                                                        |                                                                                                                                        |                                                                                                                                                                     |                                                                                                 |
|                             |          |                                                |                                                  |                                                                                                                                                                                                                                                       |                                                                                                                                                                        |                                                                                                                                        |                                                                                                                                                                     |                                                                                                 |


# Running userlist
```bash
calde_ldap
calde_ldap@alchemy.htb
calde
aepike
aepike@alchemy.htb
thanos
james
Administrator
```
### Username Links
[[3. proxychains evil-winrm (calde_ldap) net users]]
# Running passlist

```bash
CsAdlLDAPMoDeBrnd12!
LandIAtErOUs
greenday
changeme
tXxAtjrJnKrz
UaqcsvzMxEjZ
```
### Password Links
[[3. proxychains evil-winrm (calde_ldap) net users]]
[[8. machine password.xlsx]]
# NTLM Hashes from DC
```bash
Administrator:500:aad3b435b51404eeaad3b435b51404ee:731c191234d0934dee79dd57169c6da7:::                             
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::                                     
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:855e94c0c14a2cef0f6229eef8f34836:::                                    
aepike:1104:aad3b435b51404eeaad3b435b51404ee:950e9197f5d470df2ee2a4c292d5609f:::                                   
calde:1105:aad3b435b51404eeaad3b435b51404ee:892a5f495cea43597dfe34c765add078:::                                    
calde_ldap:1106:aad3b435b51404eeaad3b435b51404ee:377d3f6ce5c66bc5e71c5d0921a7e7f0:::                               
thanos:1107:aad3b435b51404eeaad3b435b51404ee:cf3a5525ee9414229e66279623ed5c58:::                                   
james:1108:aad3b435b51404eeaad3b435b51404ee:c9b30a86acaea990bf9fa6c35ac9dd92:::                                    
DC$:1001:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
```
### NTLM Links
[[10. impacket-secretsdump (DCSync)]]

