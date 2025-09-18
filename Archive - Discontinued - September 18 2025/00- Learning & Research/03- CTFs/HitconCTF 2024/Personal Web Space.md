# Personal Web Space 1

[](https://github.com/t510599/My-CTF-Challenges/tree/master/HITCON%20CTF/2024/Personal%20Web%20Space#personal-web-space-1)

- Tags: `web`, `misc`
- Score: 262/500
- Solves: 27

## Description

[](https://github.com/t510599/My-CTF-Challenges/tree/master/HITCON%20CTF/2024/Personal%20Web%20Space#description)

> Your dream space to create your own website.
> 
> [http://www.pws.chal.hitconctf.com/](http://www.pws.chal.hitconctf.com/)

## Overview

[![infra](https://github.com/t510599/My-CTF-Challenges/raw/master/HITCON%20CTF/2024/Personal%20Web%20Space/infra.svg)](https://github.com/t510599/My-CTF-Challenges/blob/master/HITCON%20CTF/2024/Personal%20Web%20Space/infra.svg)

ssh (sftp) TCP forwarding + access LAN

## Recon
1. By scanning or direct access to `http://www.pws.chal.hitconctf.com/`, one can get robots.txt -> flag.txt, apache2.zip.
2. Read apache2 conf, find that /flag.txt is ProxyPass to [http://internal/flag.txt](http://internal/flag.txt), but flag got substituted.  
    In addition, `Range` header has been unset in `RequestHeader unset Range`

    ```apache
    # location /flag.txt -> reverse proxy to the internal/flag.txt
    <Location /flag.txt>
       ProxyPass http://internal/flag.txt
       # what are u trying to do?
       RequestHeader unset Range
    
       # censor flags in the response
       AddOutputFilterByType SUBSTITUTE text/plain
       Substitute "s/hitcon\{.*?\}/hitcon\{**censored**\}/"
    </Location>
    ```
    
3. SFTP is run by openssh-server.  
    Read /etc/ssh/sshd_config with sftp, find that group `webuser` has been restricted to `internal-sftp` by `ForceCommand`, so no shell access.
    
    ```ssh
    Match Group webuser
      ForceCommand internal-sftp
    ```
    

## Solution
Look further, you can notice that `AllowTcpForwarding` defaults to `yes`, and there is no further restriction on group `webuser`.

In addition, if you look at last few lines of sshd_config, you will see example for `anoncvs`:

```ssh
#Match User anoncvs
#       X11Forwarding no
#       AllowTcpForwarding no
#       PermitTTY no
#       ForceCommand cvs server
```

`AllowTcpForwarding` is explicitly set to `no` here, which would be the hint for use TCP forwarding feature.

Create dynamic forwarding tunnel with no tty (`-N`).

```shell
ssh -D 4090 -N userXXX@file.pws.chal.hitconctf.com
```

Then you can fetch the internal server through tunnel (`-x socks5h` for DNS lookup through proxy).

```shell
curl -x socks5h://localhost:4090 http://internal/flag.txt
```

Flag.txt
`hitcon{My_l4n_had_b33n_sEEn_through_why??!!}`
