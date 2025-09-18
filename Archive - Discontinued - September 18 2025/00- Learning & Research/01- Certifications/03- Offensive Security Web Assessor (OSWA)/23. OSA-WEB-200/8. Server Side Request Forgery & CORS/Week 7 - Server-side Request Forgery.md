
when presented with a `website` should be asking two questions
- 1st thing is look at the `image paths`
- 2nd is change the `URL's` to check for `LFI` or `Directory Traversal`
![[Pasted image 20250107233339.png]]
if we click the `image` on the left we get brought to a page that we can begin testing these things
![[Pasted image 20250107233614.png]]
if we change the `url=/etc/passwd` we can see nothing processes on the webpage because the webpage is only meant to process `.jpg`
![[Pasted image 20250107233839.png]]
the `reason` that is is stuck as an `image` is because of the `Content-Type` header which is an `image` - the screen shot is shitty but you can make it out, and the `/etc/passwd` is being shown below -so to see the contents you have to look in `BURP`
![[Pasted image 20250107234608.png]]
now since we have that we can check for `LFI` or `Directory Traversal` - both are similar 
- for example in this `RESPONSE` we can see the `PHP` code but that doesn't mean we have `LFI` because we cannot execute it a instance of `LFI` is if we were able to say execute `cat /etc/passwd`, but here we are just navigating to `/etc/passwd` to see the contents of the file
- here we still have `Directory traversal` because we are just seeing the contents of `url-GenericRenderPage.php`
![[Pasted image 20250107235120.png]]
another vulnerability on this website is `SSRF` where we can use `url=http://google.com` to reach google from the webserver while utilizing it as a proxy
![[Pasted image 20250107235521.png]]
and in the `response` we can see that google is being hit but not from our `kali` but from the `victim 192.168.118.10` which means `SSRF` is present because the `Server` is making the request for us
![[Pasted image 20250107235833.png]]
we can also hit our own `machine` by utilizing this
![[Pasted image 20250107235924.png]]
and we can see that it hit
![[Pasted image 20250107235941.png]]
this is what the `php` code of `GenericRenderPage.php` looks like
- it is getting the `url`
- using `fopen` to initiate the `url` request 
- a header is added to force the `image` type - if this line didnt exist than `remote file inclusion` would be vlnerable as well
- and `fpassthru` writes image to the `buffer` and sends it - no idea what this means
![[Pasted image 20250108001248.png]]
If `SSRF` is present you are able to by pass `authentication` because you are able to act as the internal sevrer to send requests. You are essentially `impersonating the server as a proxy`
 - in this picture we are essentially utilizing the `API Gateway` server to reach the `/files, /users, /render` endpoint and that redirects us internally
![[Pasted image 20250107133848.png]]

Notes:

`RCE` is not possible with `SSRF`, only able to read internal files. However if you are able to access an internal `/API` and create an `SSH` key you may be able to get `RCE`
- `double encoding` occurs when multiple systems have to process the data to read it 