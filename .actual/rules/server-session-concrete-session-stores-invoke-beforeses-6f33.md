---
version: 2
name: server-session-concrete-session-stores-invoke-beforeses-6f33
description: "abstract-session-store Internal Module: Concrete Session Stores Invoke Beforesessionrolled Lifecycle"
metadata:
  actual:
    adr_id: 6f33c967-212e-4be0-9738-ea264af47897
    status: accepted
    candidate_group_id: c6c0b49c-264f-4527-9db3-63e25d949e1e
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/server/session/**
---

# abstract-session-store Internal Module: Concrete Session Stores Invoke Beforesessionrolled Lifecycle

Scope: applies to `src/server/session/**`.

These rules are ALWAYS ACTIVE for all server-side session management implementations, including stateless encrypted cookie adapters, stateful data store adapters, authentication middleware, and request handlers managing session lifecycle, rolling, or cookie dispatch.

### Rules

- **R-AST-001** MUST: Concrete session stores MUST invoke the beforeSessionRolled lifecycle hook when renewing or rolling an existing session, defaulting to rolling the session if an error is encountered during hook execution.

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
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration test suites covering session store lifecycle scenarios and peer code review verifying adherence to the abstract session store contract.
</enforcement>