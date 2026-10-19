---
version: 2
name: server-session-stateless-session-store-implementations-087f
description: "abstract-session-store Internal Module: Stateless Session Store Implementations Calculate Serialized"
metadata:
  actual:
    adr_id: 087f8e73-23da-42e6-8d9e-fd6836e42b17
    status: accepted
    candidate_group_id: c6c0b49c-264f-4527-9db3-63e25d949e1e
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/server/session/**
---

# abstract-session-store Internal Module: Stateless Session Store Implementations Calculate Serialized

Scope: applies to `src/server/session/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-AST-001** MUST: Stateless session store implementations MUST calculate serialized session payload byte sizes and issue a warning when cookie sizes exceed predefined header safety thresholds.

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