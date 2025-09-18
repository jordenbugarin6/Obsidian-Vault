​  
**Group**: APT99  
​  
**Suspected attribution**: China  
​  
**Target sectors**: While APT99's targeting scope is global, its activities are primarily concentrated in the United Kingdom. They have prioritized IT firms that support the country's high-tech industry.  
​  
**Overview**: The group's focus suggests intent to collect proprietary or customer data for commercial or operational purposes that serve strategic requirements related to national priorities, or create additional accesses and vectors to facilitate future campaigns. Government entities targeting suggests a potential secondary intent to collect geopolitical data that may benefit nation-state decision making.  
​  
**Associated malware**: The group leverages leaked and cracked versions of Cobalt Strike.  
​  
**Attack vectors**: For initial compromise intelligence has observed APT99 leverage spearphishing with malicious attachments and/or hyperlinks typically resulting in Beacon execution. APT99 frequently registers and leverages domains that masquerade as legitimate web services and organizations that are relevant to the intended target. Furthermore, this group routinely identifies and exploits misconfigurations in Active Directory environments using open source tooling.  
​  
**Domains**: The following domains have been acquired and setup for use to simulate APT99.  
​

- qrictgydszhlhw.info
- nbqtddutqn.org
- znkfchsslimnfp.info
- bforgbdaurgjettxago.com  
    ​  
      
    ​

## Assignment

​  
You have been tasked to emulate APT99 for your client. The goal is to compromise the `ACME`, `KATO` and `ESAE` forests, collecting flags as evidence along the way. The assessment will begin as an assume breach, for which you have been provided access to an `ACME Workstation`.  
​  
  
​

## Flags

​  
Every machine will have a flag located in the `C:\Users\Administrator\Desktop` directory. Some will require privilege escalation to access. Should you wish to revert the lab, the best procedure is to stop everything first, restore the VMs back to the original snapshots, then start the lab again. If you find that flags are missing, try power-cycling the AdminBox. If that doesn't work, reach out to support@zeropointsecurity.co.uk