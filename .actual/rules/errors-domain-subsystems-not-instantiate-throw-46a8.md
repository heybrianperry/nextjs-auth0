---
version: 2
name: errors-domain-subsystems-not-instantiate-throw-46a8
description: "Adoption of sdk-error Core Module for Subsystem Error Hierarchies: Domain Subsystems Not Instantiate Throw Generic"
metadata:
  actual:
    adr_id: 46a8dcd1-2cb0-4809-a1e1-cf142089469b
    status: accepted
    candidate_group_id: 33495c33-7d8f-4435-9cd6-09c297f16d44
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/errors/**
---

# Adoption of sdk-error Core Module for Subsystem Error Hierarchies: Domain Subsystems Not Instantiate Throw Generic

Scope: applies to `src/errors/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ERR-001** MUST_NOT: Domain subsystems MUST NOT instantiate or throw generic system error primitives directly when a specialized error derivative from the sdk-error module exists.

### Verify

```bash
# Discover the project test execution script from the repository manifest and run the test suite to verify error inheritance compliance.
# Discover and run the project static analysis and linting verification scripts to ensure all domain error definitions import from the sdk-error module without cycles.
```

**Accept when:**
- All domain error modules specialize the base error types exported by the sdk-error module.
- The discovered verification test suite passes with zero uncaught or unclassified error exceptions across all subsystems.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>