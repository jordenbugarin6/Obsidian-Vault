#### Keyboard Filtering
```
&&
%
||
$
()
;
back ticks
""
```

`127.0.0.1&&%20id` attempted, blacklisted special characters `&&`, `%`
![[Pasted image 20250308090647.png]]
`||` blacklisted, `127.0.0.1 || id` didnt work
![[Pasted image 20250308090914.png]]
tested `$(whoami)`, `$`, `()` is blacklisted
![[Pasted image 20250308091104.png]]
`;` is filtered, tested `127.0.0.1;cat`
![[Pasted image 20250308091302.png]]
backticks are filtered
![[Pasted image 20250308091439.png]]
`""` are filtered
![[Pasted image 20250308091606.png]]