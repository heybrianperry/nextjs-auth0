---
version: 2
name: utils-developers-inspect-repository-dependency-4bc1
description: "Internal Constants Module Adoption: Developers Inspect Repository Dependency Manifest Lock"
metadata:
  actual:
    adr_id: 4bc1593d-1626-4c74-8e27-eba6e73f25b0
    status: accepted
    candidate_group_id: b7d058aa-d221-4496-8376-bc96a764140f
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/utils/**
---

# Internal Constants Module Adoption: Developers Inspect Repository Dependency Manifest Lock

Scope: applies to `src/utils/**`.

These rules are ALWAYS ACTIVE for utility helper modules defining operational parameters, security thresholds, configuration defaults, and authentication/protocol verification routines.

### Rules

- **R-ICM-001** MUST: Developers MUST inspect the repository dependency manifest and lock artifact to verify the exact resolved version of any runtime dependency prior to implementation.

### Verify

```bash
# Discover the project verification script from the root configuration manifest and execute tests
# Execute the repository linter script identified in the build configuration to check for prohibited literal constants
# Inspect the project lock resolution artifact to confirm dependency versions
```

**Accept when:**
- All utility helper modules source operational thresholds and parameters exclusively from the designated constants module with zero unresolved literal violations.
- Automated test suites pass across all supported runtime environments, confirming proper fallback behavior.
- Static analysis checks confirm no hardcoded boundary values exist across utility implementations.

<enforcement>
Claude Code MUST NOT skip or defer verification. All utility modules must undergo automated static analysis validating constant imports and continuous integration test pipeline execution.
</enforcement>