---
version: 2
name: cross-cutting-server-route-handlers-interacting-next-a42c
description: "Adoption of @/lib/auth0 Module for Server-Side Authentication and Session Management: Server Route Handlers Interacting Next Primitives"
metadata:
  actual:
    adr_id: a42cc857-224b-4966-a61b-92c38e156922
    status: accepted
    candidate_group_id: 3b4c623c-202e-40ae-b095-2533a6255a99
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - e2e/test-app/app/app-router/api/**
      - examples/with-ipsie-session-expiry/app/api/**
      - examples/with-mrrt/**
---

# Adoption of @/lib/auth0 Module for Server-Side Authentication and Session Management: Server Route Handlers Interacting Next Primitives

Scope: applies to `e2e/test-app/app/app-router/api/**`, `examples/with-ipsie-session-expiry/app/api/**`, `examples/with-mrrt/**`.

These rules are ALWAYS ACTIVE for server route handlers executing within next/server contexts, server middleware components enforcing access control, and server endpoints performing session retrieval, mutation, or protected data access.

### Rules

- **R-AUTH-001** MUST: Server route handlers interacting with next/server primitives MUST propagate updated session headers or cookies produced by @/lib/auth0 operations back to the client response.

### Verify

```bash
# Discover and run the repository test execution script covering server route handlers and authentication flows
# Discover and run the static analysis and linting scripts to confirm uniform import of the centralized authentication module
```

**Accept when:**
- All server route handlers and middleware import session and authentication utilities exclusively from @/lib/auth0 without isolated client instantiations.
- Automated verification suites covering session retrieval, session update, and protected endpoints pass successfully with valid session assertions.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>