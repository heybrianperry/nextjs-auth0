---
version: 2
name: examples-protected-application-views-coordinate-r-0b69
description: "Auth0 Client Module Adoption for Application Authentication and Session Management: Protected Application Views Coordinate Redirect Flows"
metadata:
  actual:
    adr_id: 0b69ae2a-19e4-4b86-92f9-5b1e82296b41
    status: accepted
    candidate_group_id: c31ceea8-7373-423a-b207-4ff7f2a56177
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-cte/app/**
      - examples/with-enterprise-connect/app/**
      - examples/with-ipsie-session-expiry/app/**
      - examples/with-next-intl/app/**
      - examples/with-passkeys/app/**
      - examples/with-passwordless-db/app/**
      - examples/with-passwordless/app/**
---

# Auth0 Client Module Adoption for Application Authentication and Session Management: Protected Application Views Coordinate Redirect Flows

Scope: applies to `examples/with-cte/app/**`, `examples/with-enterprise-connect/app/**`, `examples/with-ipsie-session-expiry/app/**`, `examples/with-next-intl/app/**`, `examples/with-passkeys/app/**`, `examples/with-passwordless-db/app/**`, `examples/with-passwordless/app/**`.

These rules are ALWAYS ACTIVE for all application routes, server components, and handlers requiring user authentication, token exchange, or session state inspection.

### Rules

- **R-AUTH-001** SHOULD: Protected application views coordinate redirect flows with framework navigation utilities when the Auth0 client module indicates unauthenticated or expired session state.

### Verify

```bash
# Discover and execute the test runner validating authentication flows
# Discover and execute linting and module import boundary verification scripts
# Discover and execute the type-checking task
```

**Accept when:**
- All automated test suites covering authentication and session validation pass without errors.
- Static analysis and architectural lint checks confirm zero unauthorized direct imports of external authentication SDKs outside the centralized client module.
- Type checking succeeds with all Auth0 API calls matching the resolved library interfaces.

<enforcement>
Claude Code MUST NOT skip or defer verification. All pull requests containing direct external identity SDK instantiations outside the designated client module are blocked, and architectural lint violations trigger build failures.
</enforcement>