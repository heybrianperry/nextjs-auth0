---
version: 2
name: server-session-consumers-inspect-repository-dependency-7585
description: "abstract-session-store Internal Module: Consumers Inspect Repository Dependency Manifest Lock"
metadata:
  actual:
    adr_id: 7585d7f2-511f-4c02-b95f-06d15ab5a90b
    status: accepted
    candidate_group_id: c6c0b49c-264f-4527-9db3-63e25d949e1e
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/server/session/**
---

# abstract-session-store Internal Module: Consumers Inspect Repository Dependency Manifest Lock

Scope: applies to `src/server/session/**`.

These rules are ALWAYS ACTIVE for all server-side session management implementations, authentication middleware, and request handlers managing session lifecycle, rolling, or cookie dispatch.

### Rules

- **R-AST-001** MUST: Consumers MUST inspect the repository dependency manifest and lock resolution artifacts to lock the exact version of any external cryptographic or server dependencies prior to implementation.

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