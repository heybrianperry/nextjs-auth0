---
version: 2
name: server-session-session-store-implementations-not-bypass-72f0
description: "abstract-session-store Internal Module: Session Store Implementations Not Bypass Abstract"
metadata:
  actual:
    adr_id: 72f01894-04e6-4e48-b813-111d0b5cc7eb
    status: accepted
    candidate_group_id: c6c0b49c-264f-4527-9db3-63e25d949e1e
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/server/session/**
---

# abstract-session-store Internal Module: Session Store Implementations Not Bypass Abstract

Scope: applies to `src/server/session/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-SESSION-001** MUST_NOT: Session store implementations MUST NOT bypass the abstract session store contract or normalize-session utilities to mutate session state directly.

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
Claude Code MUST NOT skip or defer verification.
</enforcement>