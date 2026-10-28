# Task-1 Security-Fundamentals-Assessment

## Overview
Security assessment performed on OWASP Juice Shop, an intentionally
vulnerable web application used for authorized security training.
Testing was conducted entirely within this authorized lab environment.

## Tools Used
- OWASP Juice Shop (https://juice-shop.herokuapp.com)
- Firefox Browser (DevTools for inspecting requests/headers)

## Findings

### 1. SQL Injection — Login Bypass
- **Affected Component**: `/rest/user/login`
- **Risk**: High — allows full authentication bypass using crafted SQL in the email field, granting attacker access to any account.
- **Evidence**: See `evidence/sqli-login-1.png` & `evidence/sqli-login-2.png`
- **Recommended Mitigation**: Use parameterized queries / prepared statements instead of concatenating user input into SQL.

### 2. Reflected XSS — Search Bar
- **Affected Component**: `/#/search`
- **Risk**: Medium — attacker-supplied script executes in victim's browser.
- **Evidence**: See `evidence/xss-search-1.png` & `evidence/xss-search-2.png`
- **Recommended Mitigation**: Sanitize and encode user input before rendering; apply a Content-Security-Policy header.

### 3. Broken Access Control — Basket IDs
- **Affected Component**: `/api/BasketItems/{id}`
- **Risk**: Medium — IDs are sequential and not checked against the logged-in user, exposing other users' basket data.
- **Evidence**: See `evidence/idor-basket-access.png`
- **Recommended Mitigation**: Enforce server-side authorization checks on every object access (not just authentication).

## Conclusion
This assessment reinforced the importance of input validation, proper authorization checks, and secure HTTP headers. All testing was performed against an intentionally vulnerable training application in a local authorized environment.
