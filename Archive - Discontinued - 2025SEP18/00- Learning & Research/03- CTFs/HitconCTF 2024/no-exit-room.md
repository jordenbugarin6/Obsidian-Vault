The challenge
![[Pasted image 20240730105014.png]]
Building docker
```bash
┌──(root💀gobots)-[30Jul2024 14:48:31]-[/home/…/SUT/hitcon/distfiles/src]                                                                                
└─# docker build .
```
Successfully built
```bash
Removing intermediate container 8cde21e96d3f
 ---> 3e83fcdac777
Step 18/19 : COPY eth_sandbox /usr/lib/python/eth_sandbox
 ---> c5341b459ff0
Step 19/19 : RUN true     && cd tmp     && /root/.foundry/bin/forge build --out /home/ctf/compiled     && rm -rf /tmp/contracts     && true
 ---> Running in 8512c8fac590
Compiling 12 files with Solc 0.8.26
installing solc version "0.8.26"
Successfully installed solc 0.8.26
Solc 0.8.26 finished in 1.53s
Compiler run successful!
Removing intermediate container 8512c8fac590
 ---> cc948c0fefe0
Successfully built cc948c0fefe0
```
Running build
```bash
┌──(root💀gobots)-[30Jul2024 14:50:12]-[/home/…/SUT/hitcon/distfiles/src]
└─# docker run -d -p 1337:1337 cc948c0fefe0
5629c6bd59f65579b93b4db5d1d8b1c4124d87d1e6b3a6b1dfb66da20242bcc9
```
Making sure running
```bash
┌──(root💀gobots)-[30Jul2024 14:52:50]-[/home/…/SUT/hitcon/distfiles/src]
└─# docker ps                              
Device "veth3468eb4@if27" does not exist.
Device "veth3468eb4@if27" does not exist.
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS                                       NAMES
5629c6bd59f6   cc948c0fefe0   "tini -g -- /entrypo…"   49 seconds ago   Up 48 seconds   0.0.0.0:1337->1337/tcp, :::1337->1337/tcp   sharp_buck
```
##### Start
Alice, Bob and David had their own private input. They designed a polynomial which encoded their private input in x = 0.
```bash
        // set Protocol Arguments
        // // alice: B(x) = 2 - 3x + 1x^2
        int256[] memory poly = new int256[](3);
        poly[0] = 2;
        poly[1] = -3;
        poly[2] = 1;
        alice.setProtocolArgs(poly, 2);
        // // bob: B(x) = 24 - 14x + 2x^2
        poly[0] = 24;
        poly[1] = -14;
        poly[2] = 2;
        bob.setProtocolArgs(poly, 24);
        // // david: C(x) = 90 - 11x + 3x^2
        poly[0] = 90;
        poly[1] = -11;
        poly[2] = 3;
        david.setProtocolArgs(poly, 90);
```
After that, the problem of calculating the sum will be transformed into `P(0)`:
```bash
polynomial: P(x) = A(x) + B(x) + C(x)
sum = P(0)
```