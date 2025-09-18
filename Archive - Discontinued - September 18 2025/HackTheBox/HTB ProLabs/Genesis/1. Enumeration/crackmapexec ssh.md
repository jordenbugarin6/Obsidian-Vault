# credentials for test, Ferus, and Administrator
```bash
┌──(kali㉿gobots)-[04Apr2024 15:30:22]-[~/SUT]                                                                                                                                                      [40/202]
└─$ crackmapexec ssh 10.10.110.0/24 -u userlist -p passwordlist                                                                                                                                             
SSH         10.10.110.10    22     10.10.110.10     [*] SSH-2.0-OpenSSH_8.4p1 Debian-5+deb11u1                                           
SSH         10.10.110.45    22     10.10.110.45     [*] SSH-2.0-OpenSSH_8.9p1 Ubuntu-3ubuntu0.1                                          
SSH         10.10.110.102   22     10.10.110.102    [*] SSH-2.0-OpenSSH_8.9p1 Ubuntu-3ubuntu0.1                                          
SSH         10.10.110.78    22     10.10.110.78     [*] SSH-2.0-OpenSSH_8.9p1 Ubuntu-3ubuntu0.1                                          
SSH         10.10.110.60    22     10.10.110.60     [*] SSH-2.0-OpenSSH_8.9p1 Ubuntu-3ubuntu0.1                                          
SSH         10.10.110.12    22     10.10.110.12     [*] SSH-2.0-OpenSSH_8.9p1 Ubuntu-3ubuntu0.1                                          
SSH         10.10.110.10    22     10.10.110.10     [-] test:t3st123 Authentication failed.                                              
SSH         10.10.110.10    22     10.10.110.10     [-] test:MeatLoaf007 Authentication failed.                                          
SSH         10.10.110.10    22     10.10.110.10     [-] test:LongAgoFarAway Authentication failed.                                       
SSH         10.10.110.10    22     10.10.110.10     [-] Ferus:t3st123 Authentication failed.                                             
SSH         10.10.110.119   22     10.10.110.119    [*] SSH-2.0-OpenSSH_8.9p1 Ubuntu-3ubuntu0.1                                          
SSH         10.10.110.10    22     10.10.110.10     [-] Ferus:MeatLoaf007 Authentication failed.                                         
SSH         10.10.110.10    22     10.10.110.10     [-] Ferus:LongAgoFarAway Authentication failed.                                      
SSH         10.10.110.10    22     10.10.110.10     [-] Administrator:t3st123 Authentication failed.                                     
SSH         10.10.110.10    22     10.10.110.10     [-] Administrator:MeatLoaf007 Authentication failed.                                 
SSH         10.10.110.10    22     10.10.110.10     [-] Administrator:LongAgoFarAway Authentication failed.                              
SSH         10.10.110.78    22     10.10.110.78     [-] test:t3st123 Authentication failed.                                              
SSH         10.10.110.78    22     10.10.110.78     [-] test:MeatLoaf007 Authentication failed.                                          
SSH         10.10.110.78    22     10.10.110.78     [-] test:LongAgoFarAway Authentication failed.                                       
SSH         10.10.110.78    22     10.10.110.78     [-] Ferus:t3st123 Authentication failed.                                             
SSH         10.10.110.78    22     10.10.110.78     [-] Ferus:MeatLoaf007 Authentication failed.                                         
SSH         10.10.110.78    22     10.10.110.78     [-] Ferus:LongAgoFarAway Authentication failed.                                      
SSH         10.10.110.78    22     10.10.110.78     [-] Administrator:t3st123 Authentication failed.                                     
SSH         10.10.110.78    22     10.10.110.78     [-] Administrator:MeatLoaf007 Authentication failed.                                 
SSH         10.10.110.78    22     10.10.110.78     [-] Administrator:LongAgoFarAway Authentication failed.                              
SSH         10.10.110.45    22     10.10.110.45     [-] test:t3st123 Authentication failed.                                              
SSH         10.10.110.45    22     10.10.110.45     [-] test:MeatLoaf007 Authentication failed.                                          
SSH         10.10.110.45    22     10.10.110.45     [-] test:LongAgoFarAway Authentication failed.                                       
SSH         10.10.110.45    22     10.10.110.45     [-] Ferus:t3st123 Authentication failed.
SSH         10.10.110.45    22     10.10.110.45     [-] Ferus:MeatLoaf007 Authentication failed.
SSH         10.10.110.45    22     10.10.110.45     [-] Ferus:LongAgoFarAway Authentication failed.
SSH         10.10.110.45    22     10.10.110.45     [-] Administrator:t3st123 Authentication failed.
SSH         10.10.110.45    22     10.10.110.45     [-] Administrator:MeatLoaf007 Authentication failed.
SSH         10.10.110.45    22     10.10.110.45     [-] Administrator:LongAgoFarAway Authentication failed.
SSH         10.10.110.60    22     10.10.110.60     [-] test:t3st123 Authentication failed.
SSH         10.10.110.60    22     10.10.110.60     [-] test:MeatLoaf007 Authentication failed.
SSH         10.10.110.60    22     10.10.110.60     [-] test:LongAgoFarAway Authentication failed.
SSH         10.10.110.60    22     10.10.110.60     [-] Ferus:t3st123 Authentication failed.
SSH         10.10.110.60    22     10.10.110.60     [-] Ferus:MeatLoaf007 Authentication failed.
SSH         10.10.110.60    22     10.10.110.60     [-] Ferus:LongAgoFarAway Authentication failed.
SSH         10.10.110.205   22     10.10.110.205    [*] SSH-2.0-OpenSSH_8.9p1 Ubuntu-3ubuntu0.1
SSH         10.10.110.60    22     10.10.110.60     [-] Administrator:t3st123 Authentication failed.
SSH         10.10.110.60    22     10.10.110.60     [-] Administrator:MeatLoaf007 Authentication failed.
SSH         10.10.110.60    22     10.10.110.60     [-] Ferus:MeatLoaf007 Authentication failed.
SSH         10.10.110.60    22     10.10.110.60     [-] Ferus:LongAgoFarAway Authentication failed.
SSH         10.10.110.205   22     10.10.110.205    [*] SSH-2.0-OpenSSH_8.9p1 Ubuntu-3ubuntu0.1
SSH         10.10.110.60    22     10.10.110.60     [-] Administrator:t3st123 Authentication failed.
SSH         10.10.110.60    22     10.10.110.60     [-] Administrator:MeatLoaf007 Authentication failed.
SSH         10.10.110.60    22     10.10.110.60     [-] Administrator:LongAgoFarAway Authentication failed.
SSH         10.10.110.102   22     10.10.110.102    [-] test:t3st123 Authentication failed.
SSH         10.10.110.102   22     10.10.110.102    [-] test:MeatLoaf007 Authentication failed.
SSH         10.10.110.102   22     10.10.110.102    [-] test:LongAgoFarAway Authentication failed.
SSH         10.10.110.102   22     10.10.110.102    [-] Ferus:t3st123 Authentication failed.
SSH         10.10.110.102   22     10.10.110.102    [-] Ferus:MeatLoaf007 Authentication failed.
SSH         10.10.110.102   22     10.10.110.102    [-] Ferus:LongAgoFarAway Authentication failed.
SSH         10.10.110.102   22     10.10.110.102    [-] Administrator:t3st123 Authentication failed.
SSH         10.10.110.102   22     10.10.110.102    [-] Administrator:MeatLoaf007 Authentication failed.
SSH         10.10.110.102   22     10.10.110.102    [-] Administrator:LongAgoFarAway Authentication failed.
SSH         10.10.110.205   22     10.10.110.205    [-] test:t3st123 Authentication failed.
SSH         10.10.110.205   22     10.10.110.205    [-] test:MeatLoaf007 Authentication failed.
SSH         10.10.110.205   22     10.10.110.205    [-] test:LongAgoFarAway Authentication failed.
SSH         10.10.110.205   22     10.10.110.205    [-] Ferus:t3st123 Authentication failed.
SSH         10.10.110.205   22     10.10.110.205    [-] Ferus:MeatLoaf007 Authentication failed.
SSH         10.10.110.205   22     10.10.110.205    [-] Ferus:LongAgoFarAway Authentication failed.
SSH         10.10.110.205   22     10.10.110.205    [-] Administrator:t3st123 Authentication failed.
SSH         10.10.110.205   22     10.10.110.205    [-] Administrator:MeatLoaf007 Authentication failed.
SSH         10.10.110.205   22     10.10.110.205    [-] Administrator:LongAgoFarAway Authentication failed.
SSH         10.10.110.12    22     10.10.110.12     [-] test:t3st123 Authentication failed.
SSH         10.10.110.12    22     10.10.110.12     [-] test:MeatLoaf007 Authentication failed.
SSH         10.10.110.12    22     10.10.110.12     [-] test:LongAgoFarAway Authentication failed.
SSH         10.10.110.12    22     10.10.110.12     [-] Ferus:t3st123 Authentication failed.
SSH         10.10.110.12    22     10.10.110.12     [-] Ferus:MeatLoaf007 Authentication failed.
SSH         10.10.110.12    22     10.10.110.12     [-] Ferus:LongAgoFarAway Authentication failed.
SSH         10.10.110.12    22     10.10.110.12     [-] Administrator:t3st123 Authentication failed.
SSH         10.10.110.12    22     10.10.110.12     [-] Administrator:MeatLoaf007 Authentication failed.
SSH         10.10.110.12    22     10.10.110.12     [-] Administrator:LongAgoFarAway Authentication failed.
SSH         10.10.110.119   22     10.10.110.119    [-] test:t3st123 Authentication failed.
SSH         10.10.110.119   22     10.10.110.119    [-] test:MeatLoaf007 Authentication failed.
SSH         10.10.110.119   22     10.10.110.119    [-] test:LongAgoFarAway Authentication failed.
SSH         10.10.110.119   22     10.10.110.119    [-] Ferus:t3st123 Authentication failed.
SSH         10.10.110.119   22     10.10.110.119    [-] Ferus:MeatLoaf007 Authentication failed.
SSH         10.10.110.119   22     10.10.110.119    [-] Ferus:LongAgoFarAway Authentication failed.
SSH         10.10.110.119   22     10.10.110.119    [-] Administrator:t3st123 Authentication failed.
SSH         10.10.110.119   22     10.10.110.119    [-] Administrator:MeatLoaf007 Authentication failed.
SSH         10.10.110.119   22     10.10.110.119    [-] Administrator:LongAgoFarAway Authentication failed.

```