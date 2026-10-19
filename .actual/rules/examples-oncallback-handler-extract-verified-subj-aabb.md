---
version: 2
name: examples-oncallback-handler-extract-verified-subj-aabb
description: "@auth0/nextjs-auth0 Server SDK Integration: Oncallback Handler Extract Verified Subject Organization"
metadata:
  actual:
    adr_id: aabb0084-0713-4862-9182-3d64fd0f1c98
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

# @auth0/nextjs-auth0 Server SDK Integration: Oncallback Handler Extract Verified Subject Organization

Scope: applies to `examples/with-enterprise-connect/lib/**`, `examples/with-passwordless/app/server-passwordless/**`.

These rules are ALWAYS ACTIVE for all server-side authentication handlers, callback routes, and session persistence logic within the application.

### Rules

- **R-AUTH-001** MUST: The onCallback handler MUST extract verified subject and organization claims and reject sessions when mandatory organization identifier claims are absent.

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
Claude Code MUST NOT skip or defer verification. All pull requests lacking required session HMAC signing or claim validation will be blocked from merging.
</enforcement>