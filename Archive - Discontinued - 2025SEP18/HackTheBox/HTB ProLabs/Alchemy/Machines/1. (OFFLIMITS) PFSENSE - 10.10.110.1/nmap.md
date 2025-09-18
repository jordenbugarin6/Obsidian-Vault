```bash
nmap -T4 --min-rate=1000 -sC -sV -p- 10.10.110.0/24 -Pn

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

```