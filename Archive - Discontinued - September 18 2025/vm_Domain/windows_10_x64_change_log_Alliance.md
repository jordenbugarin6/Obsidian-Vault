---
created_date: 29 September 2023
updated_date: 29 September 2023
type: windows/linux/template
PC Name: ALLIANCE
references: https://www.youtube.com/watch?v=xftEuVQ7kY0&t=1560s
---

`existing users`
```
Administrator | Password1
Sylvanas Windrunner (swindrunner) | Password1
Anduin Wrynn (awrynn) | Password1
```

-----------------

`2023-09-29`
```
- VMware tools installed
- Joined Horde to Warcraft-DC by making the DC a DNS server
	- Reference video url above to see how it was done
- Added swindrunner local administrator
- Added awrynn local administrator as well
- Enabled network discovery on 139/445 through file explorer, able to see machines on network now
```


TCM Notes
```
WKSTN 1 - HORDE - swindrunner local admin  make (awrynn local admin on horde)
WKSTN 2 - ALLIANCE - awrynn local admin     make (swindrunner local admin on alliance) to enable relaying attacks on the network
```

`2023-10-15`
```
- enabled rdp 3389
```



