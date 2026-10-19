---
version: 2
name: examples-before-implementing-updating-authenticat-0c41
description: "Auth0 Client Module Adoption for Application Authentication and Session Management: Before Implementing Updating Authentication Integrations Developers"
metadata:
  actual:
    adr_id: 0c418c48-78a1-4bb5-b25a-0b7d8022ef57
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

# Auth0 Client Module Adoption for Application Authentication and Session Management: Before Implementing Updating Authentication Integrations Developers

Scope: applies to `examples/with-cte/app/**`, `examples/with-enterprise-connect/app/**`, `examples/with-ipsie-session-expiry/app/**`, `examples/with-next-intl/app/**`, `examples/with-passkeys/app/**`, `examples/with-passwordless-db/app/**`, `examples/with-passwordless/app/**`.

These rules are ALWAYS ACTIVE for all application routes, server components, and handlers requiring user authentication, token exchange, or session state inspection, as well as workflows integrating passwordless, enterprise connection, passkey, or credential-based identity validation.

### Rules

- **R-AUTH-001** MUST: Before implementing or updating authentication integrations, developers MUST inspect the repository dependency manifest and lock artifact to determine the exact resolved version of the authentication library and verify all invoked APIs against that version specification.

### Verify

```bash
# Discover and execute project test runner and static analysis scripts for authentication flows
# Discover and execute project linting and module import boundary verification scripts
# Discover and execute the type-checking task to confirm Auth0 API calls conform to resolved library type signatures
```

**Accept when:**
- All automated test suites covering authentication and session validation pass without errors.
- Static analysis and architectural lint checks confirm zero unauthorized direct imports of external authentication SDKs outside the centralized client module.
- Type checking succeeds with all Auth0 API calls matching the resolved library interfaces.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory.
</enforcement>