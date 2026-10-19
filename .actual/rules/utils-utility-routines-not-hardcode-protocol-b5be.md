---
version: 2
name: utils-utility-routines-not-hardcode-protocol-b5be
description: "Internal Constants Module Adoption: Utility Routines Not Hardcode Protocol Boundary"
metadata:
  actual:
    adr_id: b5be5b70-9286-42b2-ba44-9252569ace4b
    status: accepted
    candidate_group_id: b7d058aa-d221-4496-8376-bc96a764140f
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/utils/**
---

# Internal Constants Module Adoption: Utility Routines Not Hardcode Protocol Boundary

Scope: applies to `src/utils/**`.

These rules are ALWAYS ACTIVE for utility helper modules defining operational parameters, security thresholds, and configuration defaults, as well as authentication and protocol verification routines requiring standardized boundary values.

### Rules

- **R-UTIL-001** MUST_NOT: Utility routines MUST NOT hardcode protocol boundary values, timeout durations, or security limits within local module scopes.

### Verify

```bash
# Discover and execute the project verification script from the root configuration manifest
# Execute the repository linter script identified in the build configuration to check for prohibited literal constants
# Inspect the project lock resolution artifact to confirm all external dependencies match expected resolved versions
```

**Accept when:**
- All utility helper modules source operational thresholds and parameters exclusively from the designated constants module with zero unresolved literal violations.
- Automated test suites pass across all supported runtime environments, confirming proper fallback behavior.
- Static analysis checks confirm no hardcoded boundary values exist across utility implementations.

<enforcement>
Claude Code MUST NOT skip or defer verification. All pull requests containing inline magic literals or unapproved constant declarations will be rejected during continuous integration.
</enforcement>