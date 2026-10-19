---
version: 2
name: cross-cutting-server-route-handlers-middleware-requiri-d185
description: "Adoption of @/lib/auth0 Module for Server-Side Authentication and Session Management: Server Route Handlers Middleware Requiring Authentication"
metadata:
  actual:
    adr_id: d1852f80-046a-4ce1-b3f1-794931fee599
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

# Adoption of @/lib/auth0 Module for Server-Side Authentication and Session Management: Server Route Handlers Middleware Requiring Authentication

Scope: applies to `e2e/test-app/app/app-router/api/**`, `examples/with-ipsie-session-expiry/app/api/**`, `examples/with-mrrt/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-AUTH-001** MUST: All server route handlers and server middleware requiring authentication, session reading, or session mutation MUST interface exclusively through the centralized @/lib/auth0 module.

### Verify

```bash
# Discover and execute the test suite covering server route handlers and authentication flows from the dependency manifest
# Discover and run static analysis and linting scripts to confirm uniform import of the centralized authentication module
```

**Accept when:**
- All server route handlers and middleware import session and authentication utilities exclusively from @/lib/auth0 without isolated client instantiations.
- Automated verification suites covering session retrieval, session update, and protected endpoints pass successfully with valid session assertions.

<enforcement>
Claude Code MUST NOT skip or defer verification. All pull requests and code modifications must comply with centralized authentication usage and pass all continuous integration checks and peer reviews.
</enforcement>