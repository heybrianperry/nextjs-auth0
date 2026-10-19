---
version: 2
name: examples-session-cookies-configured-http-only-95a6
description: "@auth0/nextjs-auth0 Server SDK Integration: Session Cookies Configured Http Only Secure"
metadata:
  actual:
    adr_id: 95a69484-67cc-4a2c-b7fd-21f50c73ea5f
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

# @auth0/nextjs-auth0 Server SDK Integration: Session Cookies Configured Http Only Secure

Scope: applies to `examples/with-enterprise-connect/lib/**`, `examples/with-passwordless/app/server-passwordless/**`.

These rules are ALWAYS ACTIVE for all server-side authentication handlers, callback routes, session persistence logic, and identity verification workflows.

### Rules

- **R-AUTH-001** MUST: Session cookies MUST be configured with HTTP-only, secure, and lax SameSite attributes, and the cookie expiration MUST mirror the server-side session expiration timestamp.

### Verify

```bash
sh -c 'echo "Discover and execute repository test suite for authentication flows via the project task runner"'
sh -c 'echo "Discover and execute static analysis checks for session and authentication handlers"'
```

**Accept when:**
- Authentication callbacks successfully instantiate Auth0Client, validate identity claims, and emit HMAC-signed session cookies.
- Session cookies are transmitted with HTTP-only, secure, and lax SameSite attributes matching server session expiration timestamps.
- All authentication-related unit and integration tests pass successfully in the project verification environment.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>