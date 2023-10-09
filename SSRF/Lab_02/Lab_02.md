# Basic SSRF against another back-end system

1. SSRF: Stock check function.
2. Goal: Use the stock check functionality to scan the internal 192.168.0.X range for an admin interface on port 8080, then use it to delete the user carlos.

### Analysis

- Decode this URL.

![](ssrf-2.1.png)

- Brute froce.

![](ssrf-2.2.png)
![](ssrf-2.3.png)

- I found `192.168.0.139:8080`. 

![](ssrf-2.4.png)

- Delete `carlos` user.

![](ssrf-2.5.png)
![](ssrf-2.6.png)
![](ssrf-2.7.png)
![](ssrf-2.8.png)