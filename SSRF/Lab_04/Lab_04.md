# SSRF with filter bypass via open redirection vulnerability

1. SSRF: Stock check function.
2. Goal: Change the stock check URL to access the admin interface at http://192.168.0.12:8080/admin and delete the user carlos.

### Analysis

![](ssrf-1.1.png)

![](ssrf-1.2.png)

![](ssrf-1.3.png)

- Encode URL.

![](ssrf-1.4.png)

- Now, delete  `carlos` user.

![](ssrf-1.5.png)
![](ssrf-1.6.png)