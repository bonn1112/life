---
title: OAuth 2.1 Security Risks in Multi-tenant IAM: PKCE, Token Lifetime, and Scope Isolation
platform: Medium
status: draft
---

# OAuth 2.1 Security Risks in Multi-tenant IAM

## Introduction

OAuth 2.0/2.1 is the industry standard for managing user authentication and API access permissions.
However, implementing the standard doesn't automatically mean your implementation is secure.

In this article, I'll share three common OAuth security risks I discovered while studying OWASP ASVS,
with practical examples from multi-tenant Identity and Access Management (IAM).

## Risk 1: Missing PKCE Implementation

### Threat Scenario
- Users are using a Single-Page Application (React/Vue)
- An attacker intercepts the Authorization Code
- The attacker uses the code to obtain a Token

### Solution: PKCE (Proof Key for Code Exchange)
PKCE prevents attackers from proceeding even if they intercept the Authorization Code.

How it works:
1. Client generates a random `code_verifier`
2. Client sends `code_challenge` (hash of verifier) in Authorization Request
3. Client sends `code_verifier` in Token Request
4. Server verifies the match

## Risk 2: Inappropriate Token Lifetime

### Threat Scenario
- Access Token is intercepted
- Long lifetime (e.g., 24 hours) = 24 hours of unauthorized access

### Solution: Short-lived Access Tokens + Refresh Tokens
```
Access Token: 15 minutes (limited damage if stolen)
Refresh Token: 30 days (stored securely, HttpOnly Cookie)
```

## Risk 3: Improper Scope Isolation

### Threat Scenario
- User grants "read profile" permission
- Token can also access "delete user" API

### Solution: Strict Scope-based Authorization
```
Scope: openid profile       # Read user info
Scope: write:profile        # Update profile
Scope: delete:user          # Admin only
```

## Conclusion

Three key OAuth security risks:
1. Missing PKCE → Authorization Code interception
2. Long Token Lifetime → Extended attack window
3. Poor Scope Isolation → Privilege escalation

Address these to build secure OAuth implementations.

## References
- OWASP ASVS [V6] Authentication
- RFC 7636 (PKCE)
- OAuth 2.1 Draft Specification
