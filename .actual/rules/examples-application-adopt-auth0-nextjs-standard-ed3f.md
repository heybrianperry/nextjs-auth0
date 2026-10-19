---
version: 2
name: examples-application-adopt-auth0-nextjs-standard-ed3f
description: "@auth0/nextjs-auth0 Server SDK Integration: Application Adopt Auth0 Nextjs Standard Library"
metadata:
  actual:
    adr_id: ed3f8c2a-c7f6-415e-8282-da6c09a6f624
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

# @auth0/nextjs-auth0 Server SDK Integration: Application Adopt Auth0 Nextjs Standard Library

Scope: applies to `examples/with-enterprise-connect/lib/**`, `examples/with-passwordless/app/server-passwordless/**`.

These rules are ALWAYS ACTIVE for all server-side authentication handlers, callback routes, and session persistence logic within the application.

### Rules

- **R-AUTH-001** MUST: The application MUST adopt @auth0/nextjs-auth0 as the standard library for server-side identity verification, session signing, and authentication error handling across server routes and callback workflows.

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