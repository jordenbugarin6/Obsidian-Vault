```bash
Nmap scan report for 10.10.110.213
Host is up, received echo-reply ttl 126 (0.034s latency).
Scanned at 2024-03-30 04:14:03 UTC for 5114s
Not shown: 65521 closed tcp ports (reset)
PORT      STATE SERVICE      REASON          VERSION
80/tcp    open  http         syn-ack ttl 126 Apache httpd 2.4.37 ((Win32) OpenSSL/1.0.2p PHP/5.6.39)
|_http-server-header: Apache/2.4.37 (Win32) OpenSSL/1.0.2p PHP/5.6.39
| http-methods: 
|   Supported Methods: POST OPTIONS HEAD GET TRACE
|_  Potentially risky methods: TRACE
|_http-title: Genesis Security
135/tcp   open  msrpc        syn-ack ttl 126 Microsoft Windows RPC
139/tcp   open  netbios-ssn  syn-ack ttl 126 Microsoft Windows netbios-ssn
443/tcp   open  ssl/http     syn-ack ttl 126 Apache httpd 2.4.37 ((Win32) OpenSSL/1.0.2p PHP/5.6.39)
|_http-server-header: Apache/2.4.37 (Win32) OpenSSL/1.0.2p PHP/5.6.39
| ssl-cert: Subject: commonName=localhost
| Issuer: commonName=localhost
| Public Key type: rsa
| Public Key bits: 1024
| Signature Algorithm: sha1WithRSAEncryption
| Not valid before: 2009-11-10T23:48:47
| Not valid after:  2019-11-08T23:48:47
| MD5:   a0a4:4cc9:9e84:b26f:9e63:9f9e:d229:dee0
| SHA-1: b023:8c54:7a90:5bfa:119c:4e8b:acca:eacf:3649:1ff6
| -----BEGIN CERTIFICATE-----
| MIIBnzCCAQgCCQC1x1LJh4G1AzANBgkqhkiG9w0BAQUFADAUMRIwEAYDVQQDEwls
| b2NhbGhvc3QwHhcNMDkxMTEwMjM0ODQ3WhcNMTkxMTA4MjM0ODQ3WjAUMRIwEAYD
| VQQDEwlsb2NhbGhvc3QwgZ8wDQYJKoZIhvcNAQEBBQADgY0AMIGJAoGBAMEl0yfj
| 7K0Ng2pt51+adRAj4pCdoGOVjx1BmljVnGOMW3OGkHnMw9ajibh1vB6UfHxu463o
| J1wLxgxq+Q8y/rPEehAjBCspKNSq+bMvZhD4p8HNYMRrKFfjZzv3ns1IItw46kgT
| gDpAl1cMRzVGPXFimu5TnWMOZ3ooyaQ0/xntAgMBAAEwDQYJKoZIhvcNAQEFBQAD
| gYEAavHzSWz5umhfb/MnBMa5DL2VNzS+9whmmpsDGEG+uR0kM1W2GQIdVHHJTyFd
| aHXzgVJBQcWTwhp84nvHSiQTDBSaT6cQNQpvag/TaED/SEQpm0VqDFwpfFYuufBL
| vVNbLkKxbK2XwUvu0RxoLdBMC/89HqrZ0ppiONuQ+X2MtxE=
|_-----END CERTIFICATE-----
| tls-alpn: 
|_  http/1.1
|_ssl-date: TLS randomness does not represent time
|_http-title: Genesis Security
| http-methods: 
|   Supported Methods: POST OPTIONS HEAD GET TRACE
|_  Potentially risky methods: TRACE
445/tcp   open  microsoft-ds syn-ack ttl 126 Microsoft Windows Server 2008 R2 - 2012 microsoft-ds
5985/tcp  open  http         syn-ack ttl 126 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
47001/tcp open  http         syn-ack ttl 126 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
49152/tcp open  msrpc        syn-ack ttl 126 Microsoft Windows RPC
49153/tcp open  msrpc        syn-ack ttl 126 Microsoft Windows RPC
49154/tcp open  msrpc        syn-ack ttl 126 Microsoft Windows RPC
49155/tcp open  msrpc        syn-ack ttl 126 Microsoft Windows RPC
49156/tcp open  msrpc        syn-ack ttl 126 Microsoft Windows RPC
49157/tcp open  msrpc        syn-ack ttl 126 Microsoft Windows RPC
49158/tcp open  msrpc        syn-ack ttl 126 Microsoft Windows RPC
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   3:0:2: 
|_    Message signing enabled but not required
| smb-security-mode: 
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 11472/tcp): CLEAN (Couldn't connect)
|   Check 2 (port 12137/tcp): CLEAN (Couldn't connect)
|   Check 3 (port 58760/udp): CLEAN (Failed to receive data)
|   Check 4 (port 44108/udp): CLEAN (Timeout)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
|_clock-skew: mean: 6s, deviation: 0s, median: 5s
| smb2-time: 
|   date: 2024-03-30T05:39:07
|_  start_date: 2024-03-25T22:15:32
```