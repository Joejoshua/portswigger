# Basic SSRF against the local server

1. SSRF: Stock check functionality.
2. Goal: Change the stock check URL to access the admin interface at http://localhost/admin and delete the user carlos.

### Analysis

![](ssrf-1.1.png)

- `(ctrl + shift + u)`: URL decode.

![](ssrf-1.2.png)

- Test SSRF Attack.

![](ssrf-1.3.png)

- You will see `admin` page.

![](ssrf-1.4.png)

- In admin page you gonna see Users.

![](ssrf-1.5.png)

- Delete carlos user.

![](ssrf-1.6.png)
![](ssrf-1.7.png)
![](ssrf-1.8.png)
