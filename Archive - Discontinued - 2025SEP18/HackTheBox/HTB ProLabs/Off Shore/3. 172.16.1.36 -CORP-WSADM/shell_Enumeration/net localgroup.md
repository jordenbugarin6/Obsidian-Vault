`net localgroup`
#net #localgroup
```bash
[10/23 13:31:47] beacon> shell net localgroup
[10/23 13:31:47] [*] Tasked beacon to run: net localgroup
[10/23 13:31:48] [+] host called home, sent: 45 bytes
[10/23 13:31:48] [+] received output:


Aliases for \\WSADM



-------------------------------------------------------------------------------

*Access Control Assistance Operators

*Administrators

*Backup Operators

*Cryptographic Operators

*Device Owners

*Distributed COM Users

*Event Log Readers

*Guests

*Hyper-V Administrators

*IIS_IUSRS

*Network Configuration Operators

*Performance Log Users

*Performance Monitor Users

*Power Users

*Remote Desktop Users                                                                    can rdp around the domain

*Remote Management Users

*Replicator

*System Managed Accounts Group

*Users

The command completed successfully.
```
`net localgroup administrators'
```bash
[10/23 13:33:51] beacon> shell net localgroup administrators
[10/23 13:33:51] [*] Tasked beacon to run: net localgroup administrators
[10/23 13:33:52] [+] host called home, sent: 60 bytes
[10/23 13:33:52] [+] received output:
Alias name     administrators

Comment        Administrators have complete and unrestricted access to the computer/domain



Members



-------------------------------------------------------------------------------

Administrator

CORP\Domain Admins

CORP\wsadmin

justalocaladmin

The command completed successfully.

```