---
version: 2
name: errors-subsystem-error-modules-expose-typed-8f1c
description: "Adoption of sdk-error Core Module for Subsystem Error Hierarchies: Subsystem Error Modules Expose Typed Domain"
metadata:
  actual:
    adr_id: 8f1c5d51-b048-472c-a508-d4cdcf99c225
    status: accepted
    candidate_group_id: 33495c33-7d8f-4435-9cd6-09c297f16d44
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/errors/**
---

# Adoption of sdk-error Core Module for Subsystem Error Hierarchies: Subsystem Error Modules Expose Typed Domain

Scope: applies to `src/errors/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ERR-001** SHOULD: Subsystem error modules SHOULD expose typed domain error contracts that encapsulate protocol-specific failure contexts while preserving the base inheritance from the sdk-error module.

### Verify

```bash
# Discover the project test execution script from the repository manifest and run the test suite to verify error inheritance compliance.
# Discover and run the project static analysis and linting verification scripts to ensure all domain error definitions import from the sdk-error module without cycles.
```

**Accept when:**
- All domain error modules specialize the base error types exported by the sdk-error module.
- The discovered verification test suite passes with zero uncaught or unclassified error exceptions across all subsystems.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory.
</enforcement>