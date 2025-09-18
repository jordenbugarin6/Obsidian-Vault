![[Pasted image 20250128163809.png]]
downloaded `go` so can use `gocheck`
![[Pasted image 20250128164836.png]]
added `C:\Program Files\Go\bin` to be an environment variable


failed, need internet connection - need to find how to get internet connection
```bash
C:\Users\swindrunner\Desktop\Testing Tools\gocheck>go build gocheck.go                                                                                                                                                                       gocheck.go:7:2: github.com/Velocidex/amsi@v0.0.0-20200608120838-e5d93b76f119: Get "https://proxy.golang.org/github.com/%21velocidex/amsi/@v/v0.0.0-20200608120838-e5d93b76f119.mod": dial tcp: lookup proxy.golang.org: no such host         
```
getting go dependencies on my linux machine 
```bash
┌──(root💀gobots)-[28Jan2025 22:02:18]-[/var/www/html/tools/gocheck]
└─# dir
Makefile  README.md  assets  bin  cmd  go.mod  go.sum  gocheck.go  scanner  utils
                                                                                                     
┌──(root💀gobots)-[28Jan2025 22:02:19]-[/var/www/html/tools/gocheck]
└─# go mod tidy
go: downloading github.com/fatih/color v1.16.0
go: downloading github.com/spf13/cobra v1.8.0
go: downloading github.com/Velocidex/amsi v0.0.0-20200608120838-e5d93b76f119
go: downloading github.com/mattn/go-colorable v0.1.13
go: downloading github.com/mattn/go-isatty v0.0.20
go: downloading golang.org/x/sys v0.14.0
go: downloading github.com/inconshreveable/mousetrap v1.1.0
                                                                                                     
┌──(root💀gobots)-[28Jan2025 22:02:23]-[/var/www/html/tools/gocheck]
└─# ls
Makefile  README.md  assets  bin  cmd  go.mod  go.sum  gocheck.go  scanner  utils
                                                                                                     
┌──(root💀gobots)-[28Jan2025 22:02:51]-[/var/www/html/tools/gocheck]
└─# go env GOPATH
/root/go

```
copying over `go mod`
```bash
┌──(root💀gobots)-[28Jan2025 22:04:02]-[/var/www/html/tools/gocheck]
└─# ls                                                     
Makefile  README.md  assets  bin  cmd  go.mod  go.sum  gocheck.go  scanner  utils
                                                                                                                                                                                                           
┌──(root💀gobots)-[28Jan2025 22:06:17]-[/var/www/html/tools/gocheck]
└─# cp -r /root/go/pkg/mod .                               
                                                                                                                                                                                                           
┌──(root💀gobots)-[28Jan2025 22:06:35]-[/var/www/html/tools/gocheck]
└─# ls
Makefile  README.md  assets  bin  cmd  go.mod  go.sum  gocheck.go  mod  scanner  utils

```
identify location of `go path` in the windows machine
```bash
C:\Users\swindrunner\Desktop\Testing Tools\gocheck>go env GOPATH                                                                                                        C:\Users\swindrunner\go                       
```
said fuck it and disabled defender on `guardian` to get `go` and `gochecker` on guardian to begin testing `av`

gocheck downloaded
![[Pasted image 20250128175134.png]]