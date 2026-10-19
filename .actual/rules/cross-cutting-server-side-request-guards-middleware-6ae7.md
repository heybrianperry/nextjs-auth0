---
version: 2
name: cross-cutting-server-side-request-guards-middleware-6ae7
description: "Adoption of @/lib/auth0 Module for Server-Side Authentication and Session Management: Server Side Request Guards Middleware Components"
metadata:
  actual:
    adr_id: 6ae760f4-83fb-4dd5-94b2-b9a088b92f1a
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

# Adoption of @/lib/auth0 Module for Server-Side Authentication and Session Management: Server Side Request Guards Middleware Components

Scope: applies to `e2e/test-app/app/app-router/api/**`, `examples/with-ipsie-session-expiry/app/api/**`, `examples/with-mrrt/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-AUTH-001** SHOULD: Server-side request guards and middleware components SHOULD delegate session validation and expiration handling directly to the session utilities exposed by @/lib/auth0.

### Verify

```bash
# Discover and execute the test suite covering server route handlers and authentication flows
# Discover and run the static analysis and linting scripts to confirm uniform import of @/lib/auth0
```

**Accept when:**
- All server route handlers and middleware import session and authentication utilities exclusively from @/lib/auth0 without isolated client instantiations.
- Automated verification suites covering session retrieval, session update, and protected endpoints pass successfully with valid session assertions.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>