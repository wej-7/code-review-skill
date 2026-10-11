---
name: code-review
description: Review code for bugs, security issues, and readability problems, with a short fix suggestion for each finding. Use when a user requests a code review.
---

# Code Review

## Instructions

1. Read the requested code or diff and enough surrounding context to understand its intended behavior.
2. Check for bugs, including incorrect logic, edge cases, and error handling.
3. Check for security issues, including untrusted input, exposed secrets, and missing authorization.
4. Check for readability problems, including unclear names, confusing control flow, and unnecessary complexity.
5. Report findings under **Bugs**, **Security issues**, and **Readability problems**. For each finding, include the file and line when available, a brief explanation of its impact, and a short fix suggestion. List the most serious findings first within each category.
6. Report only issues supported by the code; state uncertainty when context is missing. If a category has no findings, say "No issues found." Review without changing code unless asked to implement fixes.

## Example

For this Python code in `lookup.py`:

```python
def f(db, x):
    q = "SELECT email FROM users WHERE name = '" + x + "'"
    return db.execute(q).fetchone()[0]
```

**Bugs**

- `lookup.py:3`: A missing user makes `fetchone()` return `None`, so indexing fails. Fix: check for a missing row before reading the email.

**Security issues**

- `lookup.py:2`: Concatenating untrusted input into SQL allows injection. Fix: use a parameterized query.

**Readability problems**

- `lookup.py:1-2`: Names such as `f`, `x`, and `q` obscure the intent. Fix: rename them to `get_user_email`, `username`, and `query`.
