# SSRF with blacklist-based input filter

1. SSRF: Stock check funtion.
2. Goal: Change the stock check URL to access the admin interface at http://localhost/admin and delete the user carlos.

### Analysis

![](ssrf-1.1.png)

1. Decode URL. 

![](ssrf-1.2.png)

2. `http://localhost/` - I got block.

![](ssrf-1.3.png)

3. `http://127.0.0.1/` - Still got block.

![](ssrf-1.4.png)

4. `http://127.1/` - Use this for bypass.

![](ssrf-1.5.png)

5. `/admin` - I got another block. 

![](ssrf-1.6.png)

6. I use double url encode - `Convert selection > URL > URL-encode all characters`.

![](ssrf-1.7.png)

7. Now, delete `carlos` user.

![](ssrf-1.8.png)
![](ssrf-1.9.png)
![](ssrf-1.10.png)