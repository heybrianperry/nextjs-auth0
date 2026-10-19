---
version: 2
name: cross-cutting-server-endpoints-not-instantiate-isolate-331e
description: "Adoption of @/lib/auth0 Module for Server-Side Authentication and Session Management: Server Endpoints Not Instantiate Isolated Hoc"
metadata:
  actual:
    adr_id: 331e44fe-6116-4f53-8b11-0e9dbe6e6036
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

# Adoption of @/lib/auth0 Module for Server-Side Authentication and Session Management: Server Endpoints Not Instantiate Isolated Hoc

Scope: applies to `e2e/test-app/app/app-router/api/**`, `examples/with-ipsie-session-expiry/app/api/**`, `examples/with-mrrt/**`.

These rules are ALWAYS ACTIVE for all server runtime route handlers, middleware components, and server endpoints performing session retrieval, mutation, or protected data access within next/server contexts.

### Rules

- **R-AUTH-001** MUST_NOT: Server endpoints MUST NOT instantiate isolated or ad-hoc authentication client instances outside the centralized @/lib/auth0 module.

### Verify

```bash
# Discover and execute repository test and lint scripts via dependency manifest
# (e.g., npm test, npm run lint)
```

**Accept when:**
- All server route handlers and middleware import session and authentication utilities exclusively from @/lib/auth0 without isolated client instantiations.
- Automated verification suites covering session retrieval, session update, and protected endpoints pass successfully with valid session assertions.

<enforcement>
Claude Code MUST NOT skip or defer verification. All pull requests and code modifications must be verified through repository test suites and peer code reviews ensuring authentication utilities are consumed solely through the centralized @/lib/auth0 module.
</enforcement>