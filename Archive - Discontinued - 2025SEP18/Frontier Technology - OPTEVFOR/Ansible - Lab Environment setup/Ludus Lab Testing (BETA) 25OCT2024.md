#### Testers:
`192.51.100.7` = ERIC
`192.51.100.4` = CAM
`192.51.100.3` = BUSH
`192.51.100.5` = ELIJAH

----------------
#### Issues Encountered:
- `iptables` need to persist in ansible rules [x] 
- `root` password was found via `anaconda-ks.cfg` file unencrypted, this ruins the lab environment [ ]
- `ansible` password cracked from ansible user from template - ansible user is in `wheel` group, no password [ ]
- bring hash type down - currently the hashes take 10 mins for all four hashes
- get rid of `localhost` user
- `domain_users` file shows a `.` but needs to be an `_` [x]
- Create different templates to ensure passwords are different on Windows hosts to ensure unable to take over entire lab whe compromising one machine.
- God User ansible password is stored on WS01 and can be dumped with a `secrets` - needs to be changed - possibly same password on `DC01`
- Generic write not showing up even after running ansible rule on `DC01`
- Restore `Crond` Script

-----------------
#### Timestamp
`0858` CVE-2024-36401 GEOSERVER RCE conducted - SHELL @ 0858
`0925` root via anaconda-ks.cfg 
`0934` admin credentials found by BUSH
`0937` ansible password cracked from ansible user
`0958` cracked passwords with hashcat
`1016` winrm onto WS01 as `sg1_sam`
`1039` found path to system via `getsystem` with printspooler
`1200` cracked credentials - found `GENERICWRITE` privileges for cam
`1205` got to `8000` `http://10.2.10.7/status` web page 
`1215` SSH'd with `sg_operator` credentials
`1252` On as root on `COMMS01`

