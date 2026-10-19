---
version: 2
name: server-session-session-store-implementations-extend-imp-94d2
description: "abstract-session-store Internal Module: Session Store Implementations Extend Implement Abstract"
metadata:
  actual:
    adr_id: 94d21eaa-f767-4353-be7c-01727a847be3
    status: accepted
    candidate_group_id: c6c0b49c-264f-4527-9db3-63e25d949e1e
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/server/session/**
---

# abstract-session-store Internal Module: Session Store Implementations Extend Implement Abstract

Scope: applies to `src/server/session/**`.

These rules are ALWAYS ACTIVE for all server-side session management implementations, including stateless encrypted cookie adapters, stateful data store adapters, authentication middleware, and request handlers managing session lifecycle, rolling, or cookie dispatch.

### Rules

- **R-AST-001** MUST: All session store implementations MUST extend or implement the abstract-session-store module contract to govern session lifecycle operations, cookie issuance, and payload normalization.

### Verify

```bash
# Discover and run the project test suite verifying session store implementations against the abstract session store contract.
# Discover and run the lint and type-check scripts across server session modules to confirm compliance with session interface definitions.
```

**Accept when:**
- All unit and integration tests for stateless and stateful session stores pass without errors.
- Session rolling hooks execute correctly and default to rolling upon hook failure.
- Cookie size threshold warnings trigger when session payloads exceed configured byte limits.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory.
</enforcement>