---
version: 2
name: cross-cutting-test-configurations-define-target-execut-ffae
description: "`@playwright/test` End-to-End Testing Framework Adoption: Test Configurations Define Target Execution Profiles"
metadata:
  actual:
    adr_id: ffaeae5e-d5eb-406d-95ff-71a314bd693b
    status: accepted
    candidate_group_id: 403ff59f-0ebc-49a7-89f5-39b4c2e9d5ce
    evidence:
      source: deep
  scope:
    root: .
---

# `@playwright/test` End-to-End Testing Framework Adoption: Test Configurations Define Target Execution Profiles

Scope: applies to the whole repository.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-E2E-001** SHOULD: Test configurations SHOULD define target execution profiles utilizing the `devices` catalog provided by `@playwright/test`.

### Verify

```bash
# Discover and execute test verification and static analysis scripts as defined in the repository manifest
```

**Accept when:**
- The project verification scripts execute the end-to-end test suite cleanly across configured device profiles without runtime syntax or configuration errors.
- Environment-dependent configuration bindings for execution mode and network port resolve correctly across local and pipeline environments.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>