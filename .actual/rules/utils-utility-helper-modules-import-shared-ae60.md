---
version: 2
name: utils-utility-helper-modules-import-shared-ae60
description: "Internal Constants Module Adoption: Utility Helper Modules Import Shared Operational"
metadata:
  actual:
    adr_id: ae60287e-c099-4705-9237-dad47916b8ea
    status: accepted
    candidate_group_id: b7d058aa-d221-4496-8376-bc96a764140f
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/utils/**
---

# Internal Constants Module Adoption: Utility Helper Modules Import Shared Operational

Scope: applies to `src/utils/**`.

These rules are ALWAYS ACTIVE for utility helper modules defining operational parameters, security thresholds, and configuration defaults, as well as authentication and protocol verification routines requiring standardized boundary values.

### Rules

- **R-ICMA-001** MUST: All utility helper modules MUST import shared operational parameters, threshold limits, and configuration defaults from the internal constants module rather than defining local literal values.

### Verify

```bash
# Discover and run the project verification script from the root configuration manifest
# Execute the repository linter script identified in the build configuration to check for prohibited literal constants
# Inspect the project lock resolution artifact to confirm all external dependencies match expected resolved versions
```

**Accept when:**
- All utility helper modules source operational thresholds and parameters exclusively from the designated constants module with zero unresolved literal violations.
- Automated test suites pass across all supported runtime environments, confirming proper fallback behavior when cryptographic capabilities are restricted.
- Static analysis checks confirm no hardcoded boundary values exist across utility implementations.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated static analysis, continuous integration test pipelines executing protocol verification suites, and peer code review.
</enforcement>