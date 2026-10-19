---
version: 2
name: server-session-stateful-session-store-implementations-i-cb9e
description: "abstract-session-store Internal Module: Stateful Session Store Implementations Interface Underlying"
metadata:
  actual:
    adr_id: cb9ef58e-1f94-448d-8494-575e5ab76eb8
    status: accepted
    candidate_group_id: c6c0b49c-264f-4527-9db3-63e25d949e1e
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/server/session/**
---

# abstract-session-store Internal Module: Stateful Session Store Implementations Interface Underlying

Scope: applies to `src/server/session/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-SS-001** MUST: Stateful session store implementations MUST interface with the underlying storage layer exclusively through defined store methods for retrieval, insertion, updating, and deletion while retaining session identifier references in cookies.

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