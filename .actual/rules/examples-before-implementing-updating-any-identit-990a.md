---
version: 2
name: examples-before-implementing-updating-any-identit-990a
description: "@auth0/nextjs-auth0 Server SDK Integration: Before Implementing Updating Any Identity Integration"
metadata:
  actual:
    adr_id: 990a511c-28fc-4b0c-a501-94e94975f892
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

# @auth0/nextjs-auth0 Server SDK Integration: Before Implementing Updating Any Identity Integration

Scope: applies to `examples/with-enterprise-connect/lib/**`, `examples/with-passwordless/app/server-passwordless/**`.

These rules are ALWAYS ACTIVE for all server-side authentication handlers, callback routes, session persistence logic, and identity verification workflows within the application.

### Rules

- **R-AUTH-001** MUST: Before implementing or updating any identity integration, the consumer MUST inspect the repository dependency lock artifact to determine the exact locked version of @auth0/nextjs-auth0 and verify API compatibility against that version reference documentation.

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