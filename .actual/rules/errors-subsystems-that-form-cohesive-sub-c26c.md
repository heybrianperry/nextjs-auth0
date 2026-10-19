---
version: 2
name: errors-subsystems-that-form-cohesive-sub-c26c
description: "Adoption of sdk-error Core Module for Subsystem Error Hierarchies: Subsystems That Form Cohesive Sub Domains"
metadata:
  actual:
    adr_id: c26c4a1a-2155-415e-ad31-9eefb42b8da8
    status: accepted
    candidate_group_id: 33495c33-7d8f-4435-9cd6-09c297f16d44
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/errors/**
---

# Adoption of sdk-error Core Module for Subsystem Error Hierarchies: Subsystems That Form Cohesive Sub Domains

Scope: applies to `src/errors/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ERR-001** MAY: Subsystems that form cohesive sub-domains MAY establish intermediate error abstractions between their domain errors and the sdk-error module.
- **R-ERR-002** MANDATORY: Domain error classes MUST pass domain-specific identifiers and descriptive messages up to the superclass constructor defined in the sdk-error module.
- **R-ERR-003** MANDATORY: Custom error properties MUST preserve standard error stack traces and support structured serialization.

### Verify

```bash
# Discover and run the project test execution script from the repository manifest to verify error inheritance compliance
# Discover and run the project static analysis and linting verification scripts to ensure all domain error definitions import from the sdk-error module without cycles
```

**Accept when:**
- All domain error modules specialize the base error types exported by the sdk-error module.
- The discovered verification test suite passes with zero uncaught or unclassified error exceptions across all subsystems.

<enforcement>
Claude Code MUST NOT skip or defer verification. Violation handling: Pull requests introducing root error classes that bypass the sdk-error module are blocked from merging.
</enforcement>