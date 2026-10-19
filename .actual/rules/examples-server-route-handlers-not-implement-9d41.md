---
version: 2
name: examples-server-route-handlers-not-implement-9d41
description: "Adopt @auth0/nextjs-auth0/server for Server-Side Authentication: Server Route Handlers Not Implement Manual"
metadata:
  actual:
    adr_id: 9d41787d-97e1-427e-a786-8deab364f023
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

# Adopt @auth0/nextjs-auth0/server for Server-Side Authentication: Server Route Handlers Not Implement Manual

Scope: applies to `examples/with-cte/app/api/stt/**`, `examples/with-dpop/lib/**`, `examples/with-mrrt/lib/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-AUTH-001** MUST_NOT: Server route handlers MUST NOT implement manual or ad-hoc token parsing routines when interacting with identity provider endpoints.

### Verify

```bash
# Discover project dependency manifests and verify the presence of the authentication library in declared dependencies
# Discover and execute the repository test suite to confirm server authentication integration passes
# Discover and run the project static analysis checks to verify client instantiation and route handling compliance
```

**Accept when:**
- All server-side authentication modules instantiate Auth0Client using centralized configuration parameters.
- Repository lock resolution confirms exact dependency versions prior to execution.
- Server route handlers validate authorization context via the centralized client without inline authentication logic.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>