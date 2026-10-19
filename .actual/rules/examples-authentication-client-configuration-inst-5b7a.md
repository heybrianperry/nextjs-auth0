---
version: 2
name: examples-authentication-client-configuration-inst-5b7a
description: "@auth0/nextjs-auth0 Server SDK Integration: Authentication Client Configuration Instantiate Auth0client Explicit"
metadata:
  actual:
    adr_id: 5b7ab3e6-7251-4634-b870-bd285a6c791d
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

# @auth0/nextjs-auth0 Server SDK Integration: Authentication Client Configuration Instantiate Auth0client Explicit

Scope: applies to `examples/with-enterprise-connect/lib/**`, `examples/with-passwordless/app/server-passwordless/**`.

These rules are ALWAYS ACTIVE for all server-side authentication handlers, callback routes, and session persistence logic within the application.

### Rules

- **R-AUTH-001** MUST: Authentication client configuration MUST instantiate Auth0Client with explicit authorization parameters and configure session creation using the onCallback lifecycle handler.

### Verify

```bash
sh -c 'echo "Discover and execute repository test suite for authentication flows via the project task runner"'
sh -c 'echo "Discover and execute static analysis checks for session and authentication handlers"
```

**Accept when:**
- Authentication callbacks successfully instantiate Auth0Client, validate identity claims, and emit HMAC-signed session cookies.
- Session cookies are transmitted with HTTP-only, secure, and lax SameSite attributes matching server session expiration timestamps.
- All authentication-related unit and integration tests pass successfully in the project verification environment.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>