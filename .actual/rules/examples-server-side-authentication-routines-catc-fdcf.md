---
version: 2
name: examples-server-side-authentication-routines-catc-fdcf
description: "Auth0 Client Module Adoption for Application Authentication and Session Management: Server Side Authentication Routines Catch Handle"
metadata:
  actual:
    adr_id: fdcf578d-d0fc-4c03-9b91-52a6b900ba65
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

# Auth0 Client Module Adoption for Application Authentication and Session Management: Server Side Authentication Routines Catch Handle

Scope: applies to `examples/with-cte/app/**`, `examples/with-enterprise-connect/app/**`, `examples/with-ipsie-session-expiry/app/**`, `examples/with-next-intl/app/**`, `examples/with-passkeys/app/**`, `examples/with-passwordless-db/app/**`, `examples/with-passwordless/app/**`.

These rules are ALWAYS ACTIVE for all application routes, server components, and handlers requiring user authentication, token exchange, or session state inspection, excluding public static informational routes and independent external microservices.

### Rules

- **R-AUTH-001** SHOULD: Server-side authentication routines catch and handle specialized authentication error types exposed by the Auth0 library to provide structured feedback during failed verification attempts.

### Verify

```bash
# Discover the project test runner and static analysis scripts from the dependency manifest and execute the test suite validating authentication flows.
# Discover the project linting and module import boundary verification scripts to confirm that all authentication references originate from the centralized Auth0 client module.
# Discover and execute the type-checking task to confirm that all invocations of Auth0 client APIs conform to the resolved library type signatures.
```

**Accept when:**
- All automated test suites covering authentication and session validation pass without errors.
- Static analysis and architectural lint checks confirm zero unauthorized direct imports of external authentication SDKs outside the centralized client module.
- Type checking succeeds with all Auth0 API calls matching the resolved library interfaces.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>