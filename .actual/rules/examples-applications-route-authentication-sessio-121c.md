---
version: 2
name: examples-applications-route-authentication-sessio-121c
description: "Auth0 Client Module Adoption for Application Authentication and Session Management: Applications Route Authentication Session Verification Token"
metadata:
  actual:
    adr_id: 121cdf27-55f4-41b0-9b6a-dc34b77b326a
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

# Auth0 Client Module Adoption for Application Authentication and Session Management: Applications Route Authentication Session Verification Token

Scope: applies to `examples/with-cte/app/**`, `examples/with-enterprise-connect/app/**`, `examples/with-ipsie-session-expiry/app/**`, `examples/with-next-intl/app/**`, `examples/with-passkeys/app/**`, `examples/with-passwordless-db/app/**`, `examples/with-passwordless/app/**`.

These rules are ALWAYS ACTIVE for all application routes, server components, and handlers requiring user authentication, token exchange, or session state inspection.

### Rules

- **R-AUTH-001** MUST: Applications MUST route all authentication, session verification, and token exchange operations through the centralized Auth0 client module rather than instantiating independent authentication SDK instances in individual route handlers.

### Verify

```bash
# Discover and execute project test runner validating authentication flows
# Discover and execute linting and module import boundary verification scripts
# Discover and execute type-checking task
```

**Accept when:**
- All automated test suites covering authentication and session validation pass without errors.
- Static analysis and architectural lint checks confirm zero unauthorized direct imports of external authentication SDKs outside the centralized client module.
- Type checking succeeds with all Auth0 API calls matching the resolved library interfaces.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>