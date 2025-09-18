
`WKSTN consultant user`
-> `WKSTN SYSTEM USER` via [[6. SharpUp Weak Service Permissions Check]]

# General Accesses
| Server IP Address | Hostname | Compromised | Low-Privilege User | High-Privilege User | Open Ports | Username:Password:Method | Links |  |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
|  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |
# Plaintext Password Credentials

| Server IP Address - Where Found | Hostname | Username | Password | Links |
| ---- | ---- | ---- | ---- | ---- |




# NTLM Hashes
| Server IP Address | Hostname | Username | Hashes | Links |  |  |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 10.10.120.100 | WKSTN | Administrator | ec585ac342e5f73c8931916e17f8bf92 | [[1. mimikatz lsadump sam]] |  |  |
| 10.10.120.100 | WKSTN | pcotton | cafd6970609208fed259fc5c89b8acac | [[2. mimikatz sekurlsa logonpasswords]] |  |  |
| 10.10.120.100 | WKSTN | consultant | 37dd0e1e8fb505d2e5baaf4a27d2 | [[2. mimikatz sekurlsa logonpasswords]] |  |  |

# Kerberos Encryption Keys / AES Keys
| Server IP Address | Hostname | Username | Kereberos Encryption Keys | Links |
| ---- | ---- | ---- | ---- | ---- |
| 10.10.120.100 | WKSTN | pcotton | des_cbc_md4       b25bb73f4aa897b550c9fd5fd35a3f005b20571ef96a37a1b4786ace3039224d | [[3. mimikatz sekurlsa ekeys]] |
| 10.10.120.100 | WKSTN | consultant | des_cbc_md4       879602bf262bd7ceda9cb919d33a6e073c216beb9ac0fb8d600bd48fb87bdcf2 |  |
| 10.10.120.100 | WKSTN | DWM-2 | des_cbc_md4       1bf7f6d4c80e095c655814167615c08fbff648f50b00c0f7f7e5e7cc945f8bda |  |
| 10.10.120.100 | WKSTN | UMFD-2 | des_cbc_md4       1bf7f6d4c80e095c655814167615c08fbff648f50b00c0f7f7e5e7cc945f8bda |  |
| 10.10.120.100 | WKSTN | DWM-1 | des_cbc_md4       1bf7f6d4c80e095c655814167615c08fbff648f50b00c0f7f7e5e7cc945f8bda |  |
| 10.10.120.100 | WKSTN | WKSTN$ |  des_cbc_md4       b85afc11e447bf88d2007465813d871b197891520f89b6e10c59956b091bd3a9 |  |
| 10.10.120.100 | WKSTN | UMFD-0 | des_cbc_md4       1bf7f6d4c80e095c655814167615c08fbff648f50b00c0f7f7e5e7cc945f8bda |  |
# Domain Cached Credentials 

| Server IP Address | Hostname | Username | MsCacheV2 | Links |
| ---- | ---- | ---- | ---- | ---- |
| 10.10.120.100 | WKSTN | `ACME\consultant` | MsCacheV2 : f479efae0fe0abc7010eeaab858e059a | [[4. mimikatz !lsadump cache]] |
| 10.10.120.100 | WKSTN | `ACME\pcotton` | MsCacheV2 : 90ebc0f1b37728762f6333a6e01bd0c6 |  |

# Kerberos Tickets

| Server IP Address | Hostname | Username | kerberos ticket | Links |
| ---- | ---- | ---- | ---- | ---- |
|  |  |  |  |  |
|  |  |  |  |  |
# Kirbi tickets
| Server IP Address | Hostname | Username | ticket.kirbi | Links |
| ---- | ---- | ---- | ---- | ---- |
|  |  |  |  |  |


# Access Paths




 
