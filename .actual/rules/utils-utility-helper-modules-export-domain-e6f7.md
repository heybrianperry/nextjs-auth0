---
version: 2
name: utils-utility-helper-modules-export-domain-e6f7
description: "Internal Constants Module Adoption: Utility Helper Modules Export Domain Specific"
metadata:
  actual:
    adr_id: e6f7d6e4-2414-4aa6-86c1-2be9519c5521
    status: accepted
    candidate_group_id: b7d058aa-d221-4496-8376-bc96a764140f
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/utils/**
---

# Internal Constants Module Adoption: Utility Helper Modules Export Domain Specific

Scope: applies to `src/utils/**`.

These rules are ALWAYS ACTIVE for utility helper modules defining operational parameters, security thresholds, configuration defaults, and authentication/protocol verification routines.

### Rules

- **R-ICM-001** MAY: Utility helper modules MAY export domain-specific derived constants provided they compose values sourced directly from the internal constants module.

### Verify

```bash
# Discover and run the project verification script from the root configuration manifest
# Execute the repository linter script identified in the build configuration to check for prohibited literal constants and enforce centralized imports
# Inspect the project lock resolution artifact to confirm all external dependencies match the expected resolved versions
```

**Accept when:**
- All utility helper modules source operational thresholds and parameters exclusively from the designated constants module with zero unresolved literal violations.
- Automated test suites pass across all supported runtime environments, confirming proper fallback behavior when cryptographic capabilities are restricted.
- Static analysis checks confirm no hardcoded boundary values exist across utility implementations.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static analysis, continuous integration pipelines, and peer code reviews enforce compliance.
</enforcement>