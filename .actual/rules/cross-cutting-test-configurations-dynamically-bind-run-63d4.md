---
version: 2
name: cross-cutting-test-configurations-dynamically-bind-run-63d4
description: "`@playwright/test` End-to-End Testing Framework Adoption: Test Configurations Dynamically Bind Runtime Server"
metadata:
  actual:
    adr_id: 63d47ad5-40c4-4e13-b6e4-8a0ede9b08d0
    status: accepted
    candidate_group_id: 403ff59f-0ebc-49a7-89f5-39b4c2e9d5ce
    evidence:
      source: deep
  scope:
    root: .
---

# `@playwright/test` End-to-End Testing Framework Adoption: Test Configurations Dynamically Bind Runtime Server

Scope: applies to the whole repository.

These rules are ALWAYS ACTIVE for all end-to-end browser test suites and configuration definitions within the repository, as well as automated integration and end-to-end test execution stages in continuous integration workflows.

### Rules

- **R-E2E-001** MUST: Test configurations MUST dynamically bind runtime server port values and continuous integration execution settings from environment variables rather than hardcoded literals.

### Verify

```bash
# Discover and execute the project's test verification script as defined in the repository manifest to validate test configuration validity.
# Execute the project's static analysis and type checking scripts to ensure end-to-end configuration definitions adhere to repository conventions.
```

**Accept when:**
- The project verification scripts execute the end-to-end test suite cleanly across configured device profiles without runtime syntax or configuration errors.
- Environment-dependent configuration bindings for execution mode and network port resolve correctly across local and pipeline environments.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration pipeline checks and pull request code reviews validate test configuration and execution results.
</enforcement>