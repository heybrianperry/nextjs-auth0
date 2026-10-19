---
version: 2
name: examples-application-components-consume-helper-fo-203e
description: "Auth0 Client Module Adoption for Application Authentication and Session Management: Application Components Consume Helper Forms Session"
metadata:
  actual:
    adr_id: 203eeeca-9984-4d3d-b7de-06895b7fd774
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

# Auth0 Client Module Adoption for Application Authentication and Session Management: Application Components Consume Helper Forms Session

Scope: applies to `examples/with-cte/app/**`, `examples/with-enterprise-connect/app/**`, `examples/with-ipsie-session-expiry/app/**`, `examples/with-next-intl/app/**`, `examples/with-passkeys/app/**`, `examples/with-passwordless-db/app/**`, `examples/with-passwordless/app/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-AUTH-001** MAY: Application components MAY consume helper forms and session transfer utilities exposed alongside the centralized Auth0 client module when supporting multi-step authentication workflows.

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
Claude Code MUST NOT skip or defer verification. All authentication references must originate from the centralized Auth0 client module, and direct external identity SDK instantiations outside the designated client module are prohibited.
</enforcement>