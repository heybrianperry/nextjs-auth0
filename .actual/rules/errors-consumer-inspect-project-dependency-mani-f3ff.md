---
version: 2
name: errors-consumer-inspect-project-dependency-mani-f3ff
description: "Adoption of sdk-error Core Module for Subsystem Error Hierarchies: Consumer Inspect Project Dependency Manifest Resolved"
metadata:
  actual:
    adr_id: f3ff3f25-67a2-4ad2-850a-71247831176a
    status: accepted
    candidate_group_id: 33495c33-7d8f-4435-9cd6-09c297f16d44
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/errors/**
---

# Adoption of sdk-error Core Module for Subsystem Error Hierarchies: Consumer Inspect Project Dependency Manifest Resolved

Scope: applies to `src/errors/**`.

These rules are ALWAYS ACTIVE for all error definitions and exception classes across SDK functional domains, protocol subsystems, and new subsystem modules introducing failure classifications or diagnostic error payloads.

### Rules

- **R-ERR-001** MUST: The consumer MUST inspect the project dependency manifest and resolved lock artifact to verify dependency alignment before modifying error hierarchies.
- **R-ERR-002** MUST: Domain error classes MUST pass domain-specific identifiers and descriptive messages up to the superclass constructor defined in the sdk-error module.
- **R-ERR-003** MUST: Custom error properties MUST preserve standard error stack traces and support structured serialization.

### Verify

```bash
# Discover and run the project test execution script from the repository manifest
# Example: npm test / yarn test / pytest / cargo test
# Discover and run the project static analysis and linting verification scripts
```

**Accept when:**
- All domain error modules specialize the base error types exported by the sdk-error module.
- The discovered verification test suite passes with zero uncaught or unclassified error exceptions across all subsystems.

<enforcement>
Claude Code MUST NOT skip or defer verification. All domain error definitions must import from the sdk-error module without cycles, and pull requests introducing root error classes bypassing the sdk-error module are blocked.
</enforcement>