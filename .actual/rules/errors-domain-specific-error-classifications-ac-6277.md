---
version: 2
name: errors-domain-specific-error-classifications-ac-6277
description: "Adoption of sdk-error Core Module for Subsystem Error Hierarchies: Domain Specific Error Classifications Across Sdk"
metadata:
  actual:
    adr_id: 6277a021-d76f-4ff9-b083-f3c4e38c239b
    status: accepted
    candidate_group_id: 33495c33-7d8f-4435-9cd6-09c297f16d44
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/errors/**
---

# Adoption of sdk-error Core Module for Subsystem Error Hierarchies: Domain Specific Error Classifications Across Sdk

Scope: applies to `src/errors/**`.

These rules are ALWAYS ACTIVE for all error definitions and exception classes across SDK functional domains, protocol subsystems, and new subsystem modules introducing failure classifications or diagnostic error payloads.

### Rules

- **R-ERR-001** MUST: All domain-specific error classifications across SDK functional subsystems MUST import and specialize the base error definitions provided by the sdk-error module rather than declaring unlinked root error classes.

### Verify

```bash
# Discover and run the project test execution script from the repository manifest
# Discover and run the project static analysis and linting verification scripts to ensure all domain error definitions import from the sdk-error module without cycles.
```

**Accept when:**
- All domain error modules specialize the base error types exported by the sdk-error module.
- The discovered verification test suite passes with zero uncaught or unclassified error exceptions across all subsystems.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>