testing the filters from [[pinger.php testing]]

```
&& [X] means tested
%
|| [X]
$
()
;
back ticks
""
```

`crt.gif && ls` testing, looks like `&&` works bc it tried to add `ls.zip`
![[Pasted image 20250308093908.png]]
`crt.gif || ls` testing, looks like `||` works bc it tried to update `ls.zip`
![[Pasted image 20250308094130.png]]

` /*$(sleep 5)`sleep 5``*/-sleep(5)-'/*$(sleep 5)`sleep 5` #*/-sleep(5)||'"||sleep(5)||"/*`*/  causes an error
![[Pasted image 20250308095348.png]]
now if we append `|| ls` to that it doesnt do anything even tho `ls` should execute on error