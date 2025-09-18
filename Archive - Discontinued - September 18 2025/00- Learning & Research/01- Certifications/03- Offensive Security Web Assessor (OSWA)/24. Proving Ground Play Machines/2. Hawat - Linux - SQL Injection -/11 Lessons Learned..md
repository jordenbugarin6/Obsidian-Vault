1. Be very patient when enumerating, always full gobuster - even tho it may take forever - with better enumeration i wouldve found the `/cloud` endpoint faster
2. if working in burp just `URL-ENCODE` the entire request to make it easier - there are 2 different versions of `URL-Encoding`
3. wherever phpinfo is is typically the working port which is why when uploading the `shell.php` we had to work at the `30445` endpoint.
4. ferrox buster is good

walkthrough used for assistance 
https://medium.com/@ardian.danny/oscp-practice-series-12-proving-grounds-hawat-7f3b6ee3720b