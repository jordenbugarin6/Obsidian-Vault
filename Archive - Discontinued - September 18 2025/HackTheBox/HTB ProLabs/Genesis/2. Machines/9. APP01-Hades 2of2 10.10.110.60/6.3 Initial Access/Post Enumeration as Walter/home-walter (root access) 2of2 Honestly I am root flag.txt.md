
![[Pasted image 20240502113222.png]]
can see that theres an empty file named `.sudo_as_admin_successful' 
navigate to the `.ssh` directory and pull the `id_rsa`
- make sure that there's an extra line at the end of the key.
![[Pasted image 20240502113915.png]]
```bash
-----BEGIN RSA PRIVATE KEY-----
MIIEpgIBAAKCAQEAvg4mlI0dH0hlwIh1Dhwmg6fpBI47/OjMPWw2Bjit7TbFLEOl
hud+f3mQKexloXhJaUqLfl5BIgEPOCwMT6mZEoOii4oN99ZG6OPRSZCGohChoPBC
QR9//VNn6CANYGuc8sddkI6cl0DHJthYtql2+5S6QVXFeJ9196dZJA+I35tMI0rj
u3U/XH9cElFA+hzSYNfSHhi8co3GxUNkBjM96DAzG3hUauRJciwebOmY0Xd3ujXs
RFuvis2mQ28ITc9NVJ7BXWt0euz7SFu2HZGWYM1Og01YsYcY8J+rItn227rn18qP
Q2ESNKAdr412385pEeZV59SnA50gthfaaFLYLQIDAQABAoIBAQCSdoNCzbDYr8lC
Y6aZlhYUNaz8RsRx9dGXsDG9/6YBfcjbgNIqMXIpuLvhovz7P6CLVNhFLUvScbCR
4FgoeBGv0+PK1zxGd0o0JYTexVMLx/dW+HCGkUjoJ4OWvkSwvp239u3i/hQs983B
4M4VDmnUHVygBwJkH7cggEXQ5WvcrRPq4lXjN7QZCksjTM64xNLfKG4fflMjueC+
SWLgT2gMPLJwKfHCpCGSIPnoINEQZSTm6p/W/UqjSRuuTlBaKWfppE0HhO5SLqCE
GKNQXShJgLhWDb5tog7Zkn41Ln8htxcrPS+y96ngMxdQ1F467ML1Zu0o5X8L74C2
R4m78pphAoGBAOYqsFL12a79LMnMxs3c3KXTsaPX/6TlPEZG1AmOsiYWPlQdsu3k
AGttXcKIwcQ6Eqm4lRK3yq2LYO3rXj8GT48HVX8AnRZxGiJntN4bqLHhbZJNrOj+
PfXMJvSVtt5jLFYGoyDgzykXnnLBoRSoYL/R5MHxlsDMjFwlKNRcaXBVAoGBANNi
83qEXTS25j1umn4I3HZabyj0//ul4wPKUcQU/Ex2IThtDgWK4Tr8AknmyaasCGtO
aGzTPsSxVLWW7IFmtsPObuRGugMHBAlRAtsQXl/AmWyQgo2jzZfEdNymbUali+ds
IYVyg7vj3wEs7iMdDONaWCFKjENnI+y1BbYmScB5AoGBANmkljTsWxo4NujfpUG2
zkJUKk7nCcrQJS3C/e/HqjePowKBTtfaWHc85IL2NFusGke4zeX0O0fdWxu/C9CG                   
1CZIZhUA7InzCyZrcEDyYJNLugO1RYLQHqDVmiR/iXtCxgLWpdyKF/ogZmjXJc1V
5p6cCDdIjifjg/oB/VjJxb49AoGBAMDCcOh+H0hcqKPIYhUgG3nJiag9kdh2MwdX
zSwTPuayqiR8PdcMB8rz11pwm93i7mJ7w3nJQGm4k1hr4gs2EN+JNVHwtNrh4Opl
90awLH8AcGexd3uVrXsB6Nb05J0RhPxpfD/mZv5FEyxNPnLCoOgJkGf7ROCKAxZt
FGI/k+1xAoGBAISuVrvA8x4r8oC9KSIRIMnz9uUC6CO088ejelvL41ZQRafF9XfV
id3zpvv4t6o/WsdmOYLtgEEGbdKcVG3WrvUmkVgSBv8qKwMUzqD0OuBYeObq5Cte
GqCFHPe88hC70QZxs/Q2RNHhmUgU9NmcWaNbJao4zPXEZjpcC1EUKfWL
-----END RSA PRIVATE KEY-----

```

# `chmod 600 id_rsa`

![[Pasted image 20240502114011.png]]

# `ssh -i id_rsa root@10.10.110.60`

![[Pasted image 20240502114111.png]]

```bash
root@APP01-Hades:~# cat flag.txt
GENESIS{IN_THRU_TH3_FR0NT_D00R!}
```
# Honestly, I am root flag.txt
![[Pasted image 20240502114822.png]]
