---
version: 2
name: cross-cutting-prior-implementing-modifying-code-that-630a
description: "Adoption of @/lib/auth0 Module for Server-Side Authentication and Session Management: Prior Implementing Modifying Code That Consumes"
metadata:
  actual:
    adr_id: 630adb0f-d856-4126-a737-18203d0bc365
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

# Adoption of @/lib/auth0 Module for Server-Side Authentication and Session Management: Prior Implementing Modifying Code That Consumes

Scope: applies to `e2e/test-app/app/app-router/api/**`, `examples/with-ipsie-session-expiry/app/api/**`, `examples/with-mrrt/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-AUTH-001** MUST: Prior to implementing or modifying code that consumes the external authentication library wrapped by @/lib/auth0, the consumer MUST inspect the repository lock artifact to determine the exact resolved dependency version and verify API compatibility against that exact version's documentation.

### Verify

```bash
# Discover and run the repository test execution script covering server route handlers and authentication flows
# Discover and run static analysis and linting scripts
```

**Accept when:**
- All server route handlers and middleware import session and authentication utilities exclusively from @/lib/auth0 without isolated client instantiations.
- Automated verification suites covering session retrieval, session update, and protected endpoints pass successfully with valid session assertions.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>