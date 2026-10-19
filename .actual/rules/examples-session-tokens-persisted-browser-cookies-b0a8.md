---
version: 2
name: examples-session-tokens-persisted-browser-cookies-b0a8
description: "@auth0/nextjs-auth0 Server SDK Integration: Session Tokens Persisted Browser Cookies Cryptographically"
metadata:
  actual:
    adr_id: b0a8c71a-cd10-4c52-a9c4-39f9ec6ecbd0
    status: accepted
    candidate_group_id: 25736760-026b-4644-b875-f2e425f720b0
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-enterprise-connect/lib/**
      - examples/with-passwordless/app/server-passwordless/**
---

# @auth0/nextjs-auth0 Server SDK Integration: Session Tokens Persisted Browser Cookies Cryptographically

Scope: applies to `examples/with-enterprise-connect/lib/**`, `examples/with-passwordless/app/server-passwordless/**`.

These rules are ALWAYS ACTIVE for all server-side authentication handlers, callback routes, and session persistence logic within the application.

### Rules

- **R-AUTH-001** MUST: Session tokens persisted to browser cookies MUST be cryptographically signed using an HMAC signature over the base64url-encoded session payload with a server-managed secret.

### Verify

```bash
# Discover and execute repository test suite for authentication flows via the project task runner
# Discover and execute static analysis checks for session and authentication handlers
```

**Accept when:**
- Authentication callbacks successfully instantiate Auth0Client, validate identity claims, and emit HMAC-signed session cookies.
- Session cookies are transmitted with HTTP-only, secure, and lax SameSite attributes matching server session expiration timestamps.
- All authentication-related unit and integration tests pass successfully in the project verification environment.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>