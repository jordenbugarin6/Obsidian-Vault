---
created_date: 31 October 2023
updated_date: 31 October 2023
type: Logging Requirements
---
# 2. Document Review
##### 2.32: Document the logging of red team activities

2.32.1.1: Credentials Taken
```
What OPTEVRT is doing:
- Logging is completed in OneNote during OPTEVRT Testing.
- Personal Tester Logging page.
- Culmination of all credential page.

What OPTEVRT needs to do:
- Nothing
```
2.32.1.2 Disabling of IA Controls
```
1. Integrity
2. Availability
3. Authentication
4. Confidentiality
5. Nonrepudiation

What OPTEVRT is doing:
- Tester doesn't deal with IA of System, anything that happens to SUT is communicated with site SA.
- Possibly done in test planning phase.
What OPTEVRT needs to do:
- TBD
```
2.32.1.3 Exploit events
```
What OPTEVRT is doing:
- Exploit events are encompassed in /root/termlogs if exploited from kali.

What OPTEVRT needs to do:
- One Note documentation for initial access exploitation events from CORE IMPACT/Exploits not using kali.
- One Note page to log "Exploitation Events" to document all exploitation conducted during a test
```
2.32.1.4 Identify hosts tracking schema (e.g., touched, accessed, persistent, non-persistent, lost and cleaned)
```
What OPTEVRT is doing:
- OPTEVRT logs all commands to /root/termlogs. These commands encompass tracking of touched/accessed requirements.
- OPTEVRT logs an artifact page to timestamp when artifacts are placed on victim machines as well as when they are removed or "cleaned."

What OPTEVRT needs to do:
- Have a One Note location to log touched & accessed machines.
- OPTEVRT is currently not required to log if a beacon or access is lost, currently re-access or put new beacon on the target system without needing to log previous lost.
```
2.32.1.5 Implant Configuration (i.e., tool versions) on target systems
```
What OPTEVRT is doing:
- Cobalt Strike Server host tester pulls C2 logs at end of test.
What OPTEVRT needs to do:
- Create One Note page with version of Cobalt Strike being utilized on all target systems with beacons.
- Place Cobalt Strike Configuration in One Note
```
2.32.1.6 Scanning artifacts created/deployed (e.g., files uploaded, tools deployed, process spawned)
```
What OPTEVRT is doing:
- One Note Artifact tracking sheet with "Time Inserted", "Time Removed", "Team lead Sign Off", "Sha256SUM".
- Document process ID Spawned
```
2.32.2 Identify alternative logging method
```
What OPTEVRT is doing:
- Logging in /root/termlogs on Kali VM
- Logging in One Note in Windows Host OS
- Syncs notes to Master Machine through test.

What OPTEVRT needs to do:
```
2.32.3 Log in a searchable, retrievable, and centralized data store
```
What OPTEVRT is doing:
One Note, Master Host Sync, & /root/termlogs - all are searchable, retrievable, and centralized.

What OPTEVRT needs to do:
N/A
```
##### 2.33: Document the logging of red team host accesses
2.33.1.1 Hostname
2.33.1.2 IP Address
2.33.1.3 Mac Address
2.33.1.4 DHCP Domain
2.33.1.5 NT Domain
2.33.1.6 Fully Qualified Domain Name
```
What OPTEVRT is doing:
- Logging personal Windows/Kali/Host OS 
- Logging of all fields above are placed and logged depending on tester
What OPTEVRT needs to do:
- Have a uniform method within notes (One Note) across all testers, example below

10.10.13.93 Notes:
-----------------
Hostname: WEB01
IP Address: 10.10.13.93
Mac Address: F4:1B:96:4F:B4:90
DHCP Domain: ns1.example.org
NT Domain: testnet
FQDN:testnet.domain.local

```
2.33.1.7 Jump Points
```
What OPTEVRT is doing:
Jump points are logged depending on the tester.

What OPTEVRT needs to do:
Have a standard for jump points at the top of notes, example below:

Explanation:
From GoBots VM exploited onto WS02/WS03.
Utilized chisel to pivot from WS02/WS03 to be able to exploit SQL01.
Caught a reverse shell from SQL01, privilege escalated and dumped credentials.
Utilized credentials to Evil-WinRM to WEB01, dumped credentials leading to Domain User with "Remote Deskop Users" Privileges
Pivoted from WEB01 to NET-DC utilizing Domain User credentials

Target Jump Points:
-----------------
>kali
->WS01
--> WS02
--> WS03
---> SQL01
----> WEB01
-----> NET-DC
```
2.33.1.8 Dates
```
What OPTEVRT is doing:
- /root/termlogs document date and time. 
- OPTEVRT Testers document general notes every day of test as well as timestamp commands, dates are currently not documented with timestamps for every command ran in One Note.

What OPTEVRT needs to do:
- In One Note tester timestamp the date as well as the time.
```
2.33.1.9 Process ID of tools in memory
```
What OPTEVRT is doing:
- Cobalt Strike logs
- /root/termlogs

What OPTEVRT needs to do:
- One Note Process ID page. 
```
##### 2.34: Document Halting procedures:
*TEAM LEAD ANSWERS REQUIRED*
2.34.1 Describe the conditions and steps required for halting red team operations IAW Reference 2
```
What OPTEVRT is doing:

What OPTEVRT needs to do:
```
2.32.2 Require logging halting activities
```
What OPTEVRT is doing:

What OPTEVRT needs to do:
```
2.34.3 Describe the notification procedures
```
What OPTEVRT is doing:

What OPTEVRT needs to do:
```
2.34.3.1 Describe the internal and external notification procedures
```
What OPTEVRT is doing:

What OPTEVRT needs to do:
```
2.34.3.2 Identify list of personnel to contact
```
What OPTEVRT is doing:

What OPTEVRT needs to do:
```

