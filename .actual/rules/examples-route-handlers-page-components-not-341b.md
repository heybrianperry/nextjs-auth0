---
version: 2
name: examples-route-handlers-page-components-not-341b
description: "Auth0 Client Module Adoption for Application Authentication and Session Management: Route Handlers Page Components Not Directly"
metadata:
  actual:
    adr_id: 341b15fa-5f04-4349-ab5a-a4175f406087
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

# Auth0 Client Module Adoption for Application Authentication and Session Management: Route Handlers Page Components Not Directly

Scope: applies to `examples/with-cte/app/**`, `examples/with-enterprise-connect/app/**`, `examples/with-ipsie-session-expiry/app/**`, `examples/with-next-intl/app/**`, `examples/with-passkeys/app/**`, `examples/with-passwordless-db/app/**`, `examples/with-passwordless/app/**`.

These rules are ALWAYS ACTIVE for all application routes, server components, and handlers requiring user authentication, token exchange, or session state inspection.

### Rules

- **R-AUTH-001** MUST_NOT: Route handlers and page components MUST NOT directly handle raw authentication credentials or bypass the centralized Auth0 client module when validating session state.

### Verify

```bash
# Discover and run the project test runner and static analysis scripts validating authentication flows
# Discover and execute project linting and module import boundary verification scripts
# Discover and execute the type-checking task to confirm Auth0 client API type conformance
```

**Accept when:**
- All automated test suites covering authentication and session validation pass without errors.
- Static analysis and architectural lint checks confirm zero unauthorized direct imports of external authentication SDKs outside the centralized client module.
- Type checking succeeds with all Auth0 API calls matching the resolved library interfaces.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration and peer code review enforce that all authentication interactions consume the centralized Auth0 client module.
</enforcement>