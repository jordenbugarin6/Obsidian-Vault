```bash
nmap -T4 --min-rate=1000 -sC -sV -p- 10.10.110.0/24 -Pn

┌──(kali㉿gobots)-[10Jun2024 17:39:38]-[~/SUT/Alchemy_HTB/Initial_network_enum]
└─$ cat 10.10.110.0-24_all.nmap 
# Nmap 7.94SVN scan initiated Tue Jun  4 17:03:17 2024 as: nmap -T4 --min-rate=1000 -sC -sV -p- -Pn -oA 10.10.110.0-24_all -vv 10.10.110.0/24
Warning: Hit PCRE_ERROR_MATCHLIMIT when probing for service http with the regex '^HTTP/1\.1 \d\d\d (?:[^\r\n]*\r\n(?!\r\n))*?.*\r\nServer: Virata-EmWeb/R([\d_]+)\r\nContent-Type: text/html; ?charset=UTF-8\r\nExpires: .*<title>HP (Color |)LaserJet ([\w._ -]+)&nbsp;&nbsp;&nbsp;'
Nmap scan report for 10.10.110.0
Host is up, received user-set.
Scanned at 2024-06-04 17:03:18 UTC for 1185s
All 65535 scanned ports on 10.10.110.0 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.1
Host is up, received user-set (0.13s latency).
Scanned at 2024-06-04 17:03:18 UTC for 1185s
Not shown: 65533 filtered tcp ports (no-response)
PORT    STATE SERVICE  REASON         VERSION
22/tcp  open  ssh      syn-ack ttl 63 OpenSSH 9.4 (protocol 2.0)
443/tcp open  ssl/http syn-ack ttl 63 nginx
| http-methods: 
|_  Supported Methods: GET HEAD
|_http-title: pfSense - Login
| ssl-cert: Subject: commonName=pfSense-646b882d43d57/organizationName=pfSense webConfigurator Self-Signed Certificate
| Subject Alternative Name: DNS:pfSense-646b882d43d57
| Issuer: commonName=pfSense-646b882d43d57/organizationName=pfSense webConfigurator Self-Signed Certificate
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2023-05-22T15:20:13
| Not valid after:  2024-06-23T15:20:13
| MD5:   7c6e:3748:c644:e528:8196:4921:d7e5:b016
| SHA-1: da89:813a:b794:d147:01c0:1e50:cbc2:8746:117f:831b
| -----BEGIN CERTIFICATE-----
| MIIElDCCA3ygAwIBAgIIfwhW03y+XwIwDQYJKoZIhvcNAQELBQAwWjE4MDYGA1UE
| ChMvcGZTZW5zZSB3ZWJDb25maWd1cmF0b3IgU2VsZi1TaWduZWQgQ2VydGlmaWNh
| dGUxHjAcBgNVBAMTFXBmU2Vuc2UtNjQ2Yjg4MmQ0M2Q1NzAeFw0yMzA1MjIxNTIw
| MTNaFw0yNDA2MjMxNTIwMTNaMFoxODA2BgNVBAoTL3BmU2Vuc2Ugd2ViQ29uZmln
| dXJhdG9yIFNlbGYtU2lnbmVkIENlcnRpZmljYXRlMR4wHAYDVQQDExVwZlNlbnNl
| LTY0NmI4ODJkNDNkNTcwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCr
| yKP9fJZirzrCWZdVtWO6ryP8hgh8QbrArVlQCtWKk+TBJ0kmWA82aig4vS9l7BDi
| TnXBbLoTWZtkk/NLIj2nThEYltZvkZJ1XJiwkCsjtB2GNG4mtELrZSZ7jr5+NTan
| QKuG2QqqrSCzaMPt/3e//vKZBsnyUIRLxu2AILLPxceHSi17wU4LX0645wYBj4pg
| MCcligY52W/pOEzuB98ZO4aAXjUwP7iRO2cyg7vNCiQM/p9wnagnvzP8XQ8r1plH
| j0nE2nIa++L+19NLU+mNoPsoJ/Jc6EQAu4GYaSpm4VvDxkiLMPo4Z+9gcu3/jSd1
| khZEsgTz9GrSrdtO4BuPAgMBAAGjggFcMIIBWDAJBgNVHRMEAjAAMBEGCWCGSAGG
| +EIBAQQEAwIGQDALBgNVHQ8EBAMCBaAwMwYJYIZIAYb4QgENBCYWJE9wZW5TU0wg
| R2VuZXJhdGVkIFNlcnZlciBDZXJ0aWZpY2F0ZTAdBgNVHQ4EFgQUyGnhRYEBLFgV
| 6KKxHDDvq+umibUwgYsGA1UdIwSBgzCBgIAUyGnhRYEBLFgV6KKxHDDvq+umibWh
| XqRcMFoxODA2BgNVBAoTL3BmU2Vuc2Ugd2ViQ29uZmlndXJhdG9yIFNlbGYtU2ln
| bmVkIENlcnRpZmljYXRlMR4wHAYDVQQDExVwZlNlbnNlLTY0NmI4ODJkNDNkNTeC
| CH8IVtN8vl8CMCcGA1UdJQQgMB4GCCsGAQUFBwMBBggrBgEFBQcDAgYIKwYBBQUI
| AgIwIAYDVR0RBBkwF4IVcGZTZW5zZS02NDZiODgyZDQzZDU3MA0GCSqGSIb3DQEB
| CwUAA4IBAQBEsyywWff1G3eG+Zv1YjvUErg8HqhtI8ekY4KC4AVgHcFSMfF8DS/D
| WpZXaoicyl4RbqM3YKjUFLYDl7q22Nw6BRKwWd8vNoAkrdAaFasgLIipLq764AWZ
| ehnXjwPut0L/+9HFO+OBIh6cwGE6ytS+WG7kUsAI4z6KlINVj9ywWy82K0nCI07i
| ef5+Vufan20NkNCJUXydg612dHv5nn7LHDjtq+ThWIWal1UnNMeZos7JmGVi8mae
| 764vGAcxHba4gSV0KfEFe8dWrPF1uzWtykQU456u9rFm90LHI0Bom1M3788Tutuo
| 5EXaUKaTS3K6Mci3bmVLKpjSedM0nzX2
|_-----END CERTIFICATE-----

Nmap scan report for 10.10.110.2
Host is up, received user-set.
Scanned at 2024-06-04 17:03:18 UTC for 1185s
All 65535 scanned ports on 10.10.110.2 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.3
Host is up, received user-set (2.3s latency).
Scanned at 2024-06-04 17:03:18 UTC for 1185s
All 65535 scanned ports on 10.10.110.3 are in ignored states.
Not shown: 65460 filtered tcp ports (no-response), 75 filtered tcp ports (host-unreach)

Nmap scan report for 10.10.110.4
Host is up, received user-set (2.4s latency).
Scanned at 2024-06-04 17:03:18 UTC for 1185s
All 65535 scanned ports on 10.10.110.4 are in ignored states.
Not shown: 65475 filtered tcp ports (no-response), 60 filtered tcp ports (host-unreach)

Nmap scan report for 10.10.110.5
Host is up, received user-set (2.3s latency).
Scanned at 2024-06-04 17:03:18 UTC for 1185s
All 65535 scanned ports on 10.10.110.5 are in ignored states.
Not shown: 65283 filtered tcp ports (no-response), 252 filtered tcp ports (host-unreach)

Nmap scan report for 10.10.110.6
Host is up, received user-set (2.7s latency).
Scanned at 2024-06-04 17:03:18 UTC for 1185s
All 65535 scanned ports on 10.10.110.6 are in ignored states.
Not shown: 65055 filtered tcp ports (no-response), 480 filtered tcp ports (host-unreach)

Nmap scan report for 10.10.110.7
Host is up, received user-set (2.3s latency).
Scanned at 2024-06-04 17:03:18 UTC for 1185s
All 65535 scanned ports on 10.10.110.7 are in ignored states.
Not shown: 65494 filtered tcp ports (no-response), 41 filtered tcp ports (host-unreach)

Increasing send delay for 10.10.110.21 from 5 to 10 due to 11 out of 19 dropped probes since last increase.
Warning: Hit PCRE_ERROR_MATCHLIMIT when probing for service http with the regex '^HTTP/1\.0 404 Not Found\r\n(?:[^<]+|<(?!/head>))*?<style>\nbody \{ background-color: #fcfcfc; color: #333333; margin: 0; padding:0; \}\nh1 \{ font-size: 1\.5em; font-weight: normal; background-color: #9999cc; min-height:2em; line-height:2em; border-bottom: 1px inset black; margin: 0; \}\nh1, p \{ padding-left: 10px; \}\ncode\.url \{ background-color: #eeeeee; font-family:monospace; padding:0 2px;\}\n</style>'
Warning: Hit PCRE_ERROR_MATCHLIMIT when probing for service http with the regex '^HTTP/1\.0 404 Not Found\r\n(?:[^<]+|<(?!/head>))*?<style>\nbody \{ background-color: #ffffff; color: #000000; \}\nh1 \{ font-family: sans-serif; font-size: 150%; background-color: #9999cc; font-weight: bold; color: #000000; margin-top: 0;\}\n</style>'
Warning: Hit PCRE_ERROR_MATCHLIMIT when probing for service http with the regex '^HTTP/1\.0 404 Not Found\r\n(?:[^<]+|<(?!/head>))*?<style>\nbody \{ background-color: #fcfcfc; color: #333333; margin: 0; padding:0; \}\nh1 \{ font-size: 1\.5em; font-weight: normal; background-color: #9999cc; min-height:2em; line-height:2em; border-bottom: 1px inset black; margin: 0; \}\nh1, p \{ padding-left: 10px; \}\ncode\.url \{ background-color: #eeeeee; font-family:monospace; padding:0 2px;\}\n</style>'
Warning: Hit PCRE_ERROR_MATCHLIMIT when probing for service http with the regex '^HTTP/1\.0 404 Not Found\r\n(?:[^<]+|<(?!/head>))*?<style>\nbody \{ background-color: #ffffff; color: #000000; \}\nh1 \{ font-family: sans-serif; font-size: 150%; background-color: #9999cc; font-weight: bold; color: #000000; margin-top: 0;\}\n</style>'
Nmap scan report for 10.10.110.8
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.8 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.9
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.9 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.10
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.10 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.11
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.11 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.12
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.12 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.13
Host is up, received user-set (3.1s latency).
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.13 are in ignored states.
Not shown: 65438 filtered tcp ports (no-response), 97 filtered tcp ports (host-unreach)

Nmap scan report for 10.10.110.14
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.14 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.15
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.15 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.16
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.16 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.17
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.17 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.18
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.18 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.19
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.19 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.20
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.20 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.21
Host is up, received user-set (0.028s latency).
Scanned at 2024-06-04 17:23:03 UTC for 6318s
Not shown: 65532 closed tcp ports (reset)
PORT     STATE SERVICE REASON         VERSION
22/tcp   open  ssh     syn-ack ttl 63 OpenSSH 7.6p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 02:b6:ea:1a:74:33:80:7a:82:17:bb:9e:4b:f9:37:d1 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDc+QirIo5h3pHwq1LUqfd6/HLBFxtOe++1EGY31O+l25rxZRWXrUtZhvEWQZ4x4xDYHhwYVFihyeRtxW1WJP/w4lnYjRZcaHMfkygqdRApSZ8sDe0UoPY+PriuKtrB2hDcXx30+GZzTi2zOXWFRgNodAEBcLMYUmC3keFwbynPuBUzChEpbLZJiwilRfRaHVXJyUu+ai6Dk5WAIyrDG4SJBcHgxnM+3xumpHyulKLazAZZQyKlovJ6R8lj8HRkTj47UYUzZ19jIOeBgS+Xx3eXuG/cU4YNRjDgoCdcLvDrD6SJTYLZP1jkYr49WSXVfAB8YxwVh49Z4AXpzl98NdtZ
|   256 fa:80:84:a2:e4:3a:2d:1f:8a:9b:23:6e:01:8e:da:be (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBD6pStj4wjWZoix1ZBW0ry7ooJVS45sXrendVEKUjZS534MrrhFKsUDv07R+hrrwaeiiUj2qk9/c8rOP4ZlMaLE=
|   256 a4:2f:d9:45:84:88:0f:23:0f:a1:97:ff:43:b1:c3:23 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIDpzykAXoA3r/pQPicIXy9zew64SRULVpPua/fSZzap1
80/tcp   open  http    syn-ack ttl 63 Rocket
|_http-title: Index - Sogard Brewing Co
|_http-server-header: Rocket
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
| fingerprint-strings: 
|   FourOhFourRequest, HTTPOptions: 
|     HTTP/1.0 404 Not Found
|     content-type: text/plain; charset=utf-8
|     server: Rocket
|     x-content-type-options: nosniff
|     x-frame-options: SAMEORIGIN
|     permissions-policy: interest-cohort=()
|     content-length: 15
|     date: Tue, 04 Jun 2024 19:06:45 GMT
|     Error Code: 404
|   GetRequest: 
|     HTTP/1.0 200 OK
|     content-type: text/html; charset=utf-8
|     server: Rocket
|     x-content-type-options: nosniff
|     x-frame-options: SAMEORIGIN
|     permissions-policy: interest-cohort=()
|     content-length: 19359
|     date: Tue, 04 Jun 2024 19:06:45 GMT
|     <!DOCTYPE html>
|     <!--[if IE 8 ]>
|     <html lang="en" class="no-js ie8"></html><![endif]-->
|     <!--[if IE 9 ]>
|     <html lang="en" class="no-js ie9"></html><![endif]-->
|     <html class="no-js" lang="en">
|     <head>
|     <meta charset="UTF-8">
|     <meta name="description" content="Booze - Creative HTML Template">
|     <meta name="author" content="createIT">
|     <title>Index - Sogard Brewing Co</title>
|     <meta http-equiv="X-UA-Compatible" content="IE=edge">
|     <meta name="viewport" content="width=device-width initial-scale=1 shrink-to-fit=no">
|     <meta name="format-detection" content="telephone=no">
|     <link rel="stylesheet" href="/assets/css/bootstrap.min.css">
|     <link
|   RTSPRequest, X11Probe: 
|     HTTP/1.1 400 Bad Request
|     content-length: 0
|_    date: Tue, 04 Jun 2024 19:06:45 GMT
3000/tcp open  ppp?    syn-ack ttl 62
| fingerprint-strings: 
|   GenericLines, Help, RTSPRequest: 
|     HTTP/1.1 400 Bad Request
|     Content-Type: text/plain; charset=utf-8
|     Connection: close
|     Request
|   GetRequest: 
|     HTTP/1.0 200 OK
|     Content-Type: text/html; charset=UTF-8
|     Set-Cookie: lang=en-US; Path=/; Max-Age=2147483647
|     Set-Cookie: i_like_gogs=36b3a141b247fbb8; Path=/; HttpOnly
|     Set-Cookie: _csrf=M8o_O2PdocyFA95dpJvGimlL9Zs6MTcxNzUyODAwNTc2MDA5Nzk5Nw; Path=/; Domain=10.10.110.21; Expires=Wed, 05 Jun 2024 19:06:45 GMT; HttpOnly
|     X-Content-Type-Options: nosniff
|     X-Frame-Options: deny
|     Date: Tue, 04 Jun 2024 19:06:45 GMT
|     <!DOCTYPE html>
|     <html>
|     <head data-suburl="">
|     <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
|     <meta http-equiv="X-UA-Compatible" content="IE=edge"/>
|     <meta name="author" content="Gogs" />
|     <meta name="description" content="Gogs is a painless self-hosted Git service" />
|     <meta name="keywords" content="go, git, self-hosted, gogs">
|     <meta name="referrer" content="no-referrer" />
|     <meta name="_csrf" content="M8o_O2PdocyFA95dpJvGimlL9Zs6MTcxNzUyODAwNTc2MD
|   HTTPOptions: 
|     HTTP/1.0 500 Internal Server Error
|     Content-Type: text/plain; charset=utf-8
|     Set-Cookie: lang=en-US; Path=/; Max-Age=2147483647
|     X-Content-Type-Options: nosniff
|     Date: Tue, 04 Jun 2024 19:06:50 GMT
|     Content-Length: 108
|_    template: base/footer:15:47: executing "base/footer" at <.PageStartTime>: invalid value; expected time.Time
2 services unrecognized despite returning data. If you know the service/version, please submit the following fingerprints at https://nmap.org/cgi-bin/submit.cgi?new-service :
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port80-TCP:V=7.94SVN%I=7%D=6/4%Time=665F65C3%P=x86_64-pc-linux-gnu%r(Ge
SF:tRequest,300D,"HTTP/1\.0\x20200\x20OK\r\ncontent-type:\x20text/html;\x2
SF:0charset=utf-8\r\nserver:\x20Rocket\r\nx-content-type-options:\x20nosni
SF:ff\r\nx-frame-options:\x20SAMEORIGIN\r\npermissions-policy:\x20interest
SF:-cohort=\(\)\r\ncontent-length:\x2019359\r\ndate:\x20Tue,\x2004\x20Jun\
SF:x202024\x2019:06:45\x20GMT\r\n\r\n<!DOCTYPE\x20html>\n<!--\[if\x20IE\x2
SF:08\x20\]>\n<html\x20lang=\"en\"\x20class=\"no-js\x20ie8\"></html><!\[en
SF:dif\]-->\n<!--\[if\x20IE\x209\x20\]>\n<html\x20lang=\"en\"\x20class=\"n
SF:o-js\x20ie9\"></html><!\[endif\]-->\n<html\x20class=\"no-js\"\x20lang=\
SF:"en\">\n\x20\x20<head>\n\x20\x20\x20\x20<meta\x20charset=\"UTF-8\">\n\x
SF:20\x20\x20\x20<meta\x20name=\"description\"\x20content=\"Booze\x20-\x20
SF:Creative\x20HTML\x20Template\">\n\x20\x20\x20\x20<meta\x20name=\"author
SF:\"\x20content=\"createIT\">\n\x20\x20\x20\x20<title>Index\x20-\x20Sogar
SF:d\x20Brewing\x20Co</title>\n\x20\x20\x20\x20<meta\x20http-equiv=\"X-UA-
SF:Compatible\"\x20content=\"IE=edge\">\n\x20\x20\x20\x20<meta\x20name=\"v
SF:iewport\"\x20content=\"width=device-width\x20initial-scale=1\x20shrink-
SF:to-fit=no\">\n\x20\x20\x20\x20<meta\x20name=\"format-detection\"\x20con
SF:tent=\"telephone=no\">\n\x20\x20\x20\x20<link\x20rel=\"stylesheet\"\x20
SF:href=\"/assets/css/bootstrap\.min\.css\">\n\x20\x20\x20\x20<link\x20")%
SF:r(HTTPOptions,101,"HTTP/1\.0\x20404\x20Not\x20Found\r\ncontent-type:\x2
SF:0text/plain;\x20charset=utf-8\r\nserver:\x20Rocket\r\nx-content-type-op
SF:tions:\x20nosniff\r\nx-frame-options:\x20SAMEORIGIN\r\npermissions-poli
SF:cy:\x20interest-cohort=\(\)\r\ncontent-length:\x2015\r\ndate:\x20Tue,\x
SF:2004\x20Jun\x202024\x2019:06:45\x20GMT\r\n\r\nError\x20Code:\x20404")%r
SF:(RTSPRequest,54,"HTTP/1\.1\x20400\x20Bad\x20Request\r\ncontent-length:\
SF:x200\r\ndate:\x20Tue,\x2004\x20Jun\x202024\x2019:06:45\x20GMT\r\n\r\n")
SF:%r(X11Probe,54,"HTTP/1\.1\x20400\x20Bad\x20Request\r\ncontent-length:\x
SF:200\r\ndate:\x20Tue,\x2004\x20Jun\x202024\x2019:06:45\x20GMT\r\n\r\n")%
SF:r(FourOhFourRequest,101,"HTTP/1\.0\x20404\x20Not\x20Found\r\ncontent-ty
SF:pe:\x20text/plain;\x20charset=utf-8\r\nserver:\x20Rocket\r\nx-content-t
SF:ype-options:\x20nosniff\r\nx-frame-options:\x20SAMEORIGIN\r\npermission
SF:s-policy:\x20interest-cohort=\(\)\r\ncontent-length:\x2015\r\ndate:\x20
SF:Tue,\x2004\x20Jun\x202024\x2019:06:45\x20GMT\r\n\r\nError\x20Code:\x204
SF:04");
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port3000-TCP:V=7.94SVN%I=7%D=6/4%Time=665F65C3%P=x86_64-pc-linux-gnu%r(
SF:GenericLines,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\x2
SF:0text/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400\x20Bad
SF:\x20Request")%r(GetRequest,205F,"HTTP/1\.0\x20200\x20OK\r\nContent-Type
SF::\x20text/html;\x20charset=UTF-8\r\nSet-Cookie:\x20lang=en-US;\x20Path=
SF:/;\x20Max-Age=2147483647\r\nSet-Cookie:\x20i_like_gogs=36b3a141b247fbb8
SF:;\x20Path=/;\x20HttpOnly\r\nSet-Cookie:\x20_csrf=M8o_O2PdocyFA95dpJvGim
SF:lL9Zs6MTcxNzUyODAwNTc2MDA5Nzk5Nw;\x20Path=/;\x20Domain=10\.10\.110\.21;
SF:\x20Expires=Wed,\x2005\x20Jun\x202024\x2019:06:45\x20GMT;\x20HttpOnly\r
SF:\nX-Content-Type-Options:\x20nosniff\r\nX-Frame-Options:\x20deny\r\nDat
SF:e:\x20Tue,\x2004\x20Jun\x202024\x2019:06:45\x20GMT\r\n\r\n<!DOCTYPE\x20
SF:html>\n<html>\n<head\x20data-suburl=\"\">\n\t<meta\x20http-equiv=\"Cont
SF:ent-Type\"\x20content=\"text/html;\x20charset=UTF-8\"\x20/>\n\t<meta\x2
SF:0http-equiv=\"X-UA-Compatible\"\x20content=\"IE=edge\"/>\n\t\n\t\t<meta
SF:\x20name=\"author\"\x20content=\"Gogs\"\x20/>\n\t\t<meta\x20name=\"desc
SF:ription\"\x20content=\"Gogs\x20is\x20a\x20painless\x20self-hosted\x20Gi
SF:t\x20service\"\x20/>\n\t\t<meta\x20name=\"keywords\"\x20content=\"go,\x
SF:20git,\x20self-hosted,\x20gogs\">\n\t\n\t<meta\x20name=\"referrer\"\x20
SF:content=\"no-referrer\"\x20/>\n\t<meta\x20name=\"_csrf\"\x20content=\"M
SF:8o_O2PdocyFA95dpJvGimlL9Zs6MTcxNzUyODAwNTc2MD")%r(Help,67,"HTTP/1\.1\x2
SF:0400\x20Bad\x20Request\r\nContent-Type:\x20text/plain;\x20charset=utf-8
SF:\r\nConnection:\x20close\r\n\r\n400\x20Bad\x20Request")%r(HTTPOptions,1
SF:4A,"HTTP/1\.0\x20500\x20Internal\x20Server\x20Error\r\nContent-Type:\x2
SF:0text/plain;\x20charset=utf-8\r\nSet-Cookie:\x20lang=en-US;\x20Path=/;\
SF:x20Max-Age=2147483647\r\nX-Content-Type-Options:\x20nosniff\r\nDate:\x2
SF:0Tue,\x2004\x20Jun\x202024\x2019:06:50\x20GMT\r\nContent-Length:\x20108
SF:\r\n\r\ntemplate:\x20base/footer:15:47:\x20executing\x20\"base/footer\"
SF:\x20at\x20<\.PageStartTime>:\x20invalid\x20value;\x20expected\x20time\.
SF:Time\n")%r(RTSPRequest,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nConten
SF:t-Type:\x20text/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n
SF:400\x20Bad\x20Request");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Nmap scan report for 10.10.110.22
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.22 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.23
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.23 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.24
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.24 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.25
Host is up, received user-set (3.1s latency).
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.25 are in ignored states.
Not shown: 65534 filtered tcp ports (no-response), 1 filtered tcp ports (host-unreach)

Nmap scan report for 10.10.110.26
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.26 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.27
Host is up, received user-set (3.1s latency).
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.27 are in ignored states.
Not shown: 65432 filtered tcp ports (no-response), 103 filtered tcp ports (host-unreach)

Nmap scan report for 10.10.110.28
Host is up, received user-set (3.1s latency).
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.28 are in ignored states.
Not shown: 65460 filtered tcp ports (no-response), 75 filtered tcp ports (host-unreach)

Nmap scan report for 10.10.110.29
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.29 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.30
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.30 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.31
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.31 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.32
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.32 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.33
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.33 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.34
Host is up, received user-set (3.1s latency).
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.34 are in ignored states.
Not shown: 65452 filtered tcp ports (no-response), 83 filtered tcp ports (host-unreach)

Nmap scan report for 10.10.110.35
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.35 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.36
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.36 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.37
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.37 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.38
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.38 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.39
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.39 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.40
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.40 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.41
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.41 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.42
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.42 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.43
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.43 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.44
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.44 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.45
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.45 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.46
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.46 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.47
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.47 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.48
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.48 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.49
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.49 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.50
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.50 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.51
Host is up, received user-set (3.1s latency).
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.51 are in ignored states.
Not shown: 65425 filtered tcp ports (no-response), 110 filtered tcp ports (host-unreach)

Nmap scan report for 10.10.110.52
Host is up, received user-set (3.1s latency).
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.52 are in ignored states.
Not shown: 65425 filtered tcp ports (no-response), 110 filtered tcp ports (host-unreach)

Nmap scan report for 10.10.110.53
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.53 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.54
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.54 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.55
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.55 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.56
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.56 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.57
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.57 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.58
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.58 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.59
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.59 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.60
Host is up, received user-set (3.1s latency).
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.60 are in ignored states.
Not shown: 65418 filtered tcp ports (no-response), 117 filtered tcp ports (host-unreach)

Nmap scan report for 10.10.110.61
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.61 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.62
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.62 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap scan report for 10.10.110.63
Host is up, received user-set.
Scanned at 2024-06-04 17:23:03 UTC for 6318s
All 65535 scanned ports on 10.10.110.63 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

```