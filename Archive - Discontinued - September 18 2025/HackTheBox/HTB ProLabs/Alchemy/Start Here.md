![[Pasted image 20240604113051.png]]

# Introduction
```  
Introduction

Alchemy LLC has been contracted by Sogard Brewing Co. to evaluate the security of their recently established brewery factory. The primary aim of this collaboration is to fortify the factory against potential cyber threats, ensuring the safety, security, and reliability of its operations. A crucial aspect of this initiative is the integration of Information Technology (IT) networks with Operational Technology (OT) infrastructure. a move designed to enhance the oversight, control, and efficiency of the brewery's operations.  
  
This new Industrial Control Systems (ICS) environment is equipped with a set of proprietary Programmable Logic Controllers (PLCs). Each PLC is accompanied by a Human Machine Interface (HMI) and an alarm monitoring system, which warns the operators when the system detects process anomalies.  
  
The team's main objective is to determine whether brewery operations can be disrupted based on current architecture. The team should assess the company's public interface (i.e., the IT network) and emphasize the weaknesses allowing an adversary to impact the physical process or steal the brewery's Intellectual Property (IP).  
  
Rules of Engagement:

- This environment does not require brute forcing or unreasonable guessing. All the required information is readily available within the lab, provided through comprehensive documentation and various files.
- When assessing the OT side, avoid fuzzing the PLCs. This practice is strongly discouraged in real OT environments due to the risk of causing instability and undefined behaviour.

  
This **Red Team Operator Level 2** lab will expose players to:  
  

- Enumeration of IT and OT networks
- Exploiting misconfigurations
- Lateral movement
- Privilege escalation
- Tunneling and pivoting
- Documentation analysis
- Modbus network analysis
- Web application attacks
- In-depth understanding of Modbus protocol
- Structured Text PLC code review
- Dynamic Analysis of Ladder Logic
```