awTurning on:

/run local o = GetCVarBool("ResampleAlwaysSharpen"); SetCVar("ResampleAlwaysSharpen", not o); print("Sharpening is now " .. (o and "off" or "on"))
Turning off:
/run SetCVar("ResampleAlwaysSharpen", 0); print("Sharpening is now off")

before sharpening
![[Pasted image 20250213142751.png]]
after sharpening 
![[Pasted image 20250213142818.png]]
