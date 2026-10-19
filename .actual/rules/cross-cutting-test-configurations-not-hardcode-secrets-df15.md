---
version: 2
name: cross-cutting-test-configurations-not-hardcode-secrets-df15
description: "`@playwright/test` End-to-End Testing Framework Adoption: Test Configurations Not Hardcode Secrets Authentication"
metadata:
  actual:
    adr_id: df15f6c8-4e09-4ec9-9d17-6c761d3fe464
    status: accepted
    candidate_group_id: 403ff59f-0ebc-49a7-89f5-39b4c2e9d5ce
    evidence:
      source: deep
  scope:
    root: .
---

# `@playwright/test` End-to-End Testing Framework Adoption: Test Configurations Not Hardcode Secrets Authentication

Scope: applies to the whole repository.

These rules are ALWAYS ACTIVE for all end-to-end browser test suites and configuration definitions within the repository, as well as automated integration and end-to-end test execution stages in continuous integration workflows.

### Rules

- **R-E2E-001** MUST_NOT: Test configurations MUST NOT hardcode secrets, authentication credentials, or unvalidated sensitive parameters in configuration files.

### Verify

```bash
# Discover and execute the project's test verification script as defined in the repository manifest to validate test configuration validity.
# Execute the project's static analysis and type checking scripts to ensure end-to-end configuration definitions adhere to repository conventions.
```

**Accept when:**
- The project verification scripts execute the end-to-end test suite cleanly across configured device profiles without runtime syntax or configuration errors.
- Environment-dependent configuration bindings for execution mode and network port resolve correctly across local and pipeline environments.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>