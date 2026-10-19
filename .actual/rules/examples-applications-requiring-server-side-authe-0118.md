---
version: 2
name: examples-applications-requiring-server-side-authe-0118
description: "Adopt @auth0/nextjs-auth0/server for Server-Side Authentication: Applications Requiring Server Side Authentication Adopt"
metadata:
  actual:
    adr_id: 0118aefb-ba84-4222-9e61-189068cec8c1
    status: accepted
    candidate_group_id: d7b8f89c-0b8b-4612-abbe-bf2681edc5b8
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-cte/app/api/stt/**
      - examples/with-dpop/lib/**
      - examples/with-mrrt/lib/**
---

# Adopt @auth0/nextjs-auth0/server for Server-Side Authentication: Applications Requiring Server Side Authentication Adopt

Scope: applies to `examples/with-cte/app/api/stt/**`, `examples/with-dpop/lib/**`, `examples/with-mrrt/lib/**`.

These rules are ALWAYS ACTIVE for all server-side route handlers, API endpoints, and server modules requiring user authentication or authorization verification.

### Rules

- **R-AUTH-001** MUST: Applications requiring server-side authentication MUST adopt @auth0/nextjs-auth0/server and instantiate Auth0Client to manage authentication state and authorization parameters.

### Verify

```bash
# Discover the project dependency manifests and verify the presence of the authentication library in declared dependencies.
# Discover and execute the repository test suite to confirm server authentication integration passes.
# Discover and run the project static analysis checks to verify client instantiation and route handling compliance.
```

**Accept when:**
- All server-side authentication modules instantiate Auth0Client using centralized configuration parameters.
- Repository lock resolution confirms exact dependency versions prior to execution.
- Server route handlers validate authorization context via the centralized client without inline authentication logic.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>