---
version: 2
name: cross-cutting-testing-suite-use-playwright-test-5ad9
description: "`@playwright/test` End-to-End Testing Framework Adoption: Testing Suite Use Playwright Test Defineconfig"
metadata:
  actual:
    adr_id: 5ad95a6f-0721-4587-ade2-ff6ea78f7aa9
    status: accepted
    candidate_group_id: 403ff59f-0ebc-49a7-89f5-39b4c2e9d5ce
    evidence:
      source: deep
  scope:
    root: .
---

# `@playwright/test` End-to-End Testing Framework Adoption: Testing Suite Use Playwright Test Defineconfig

Scope: applies to the whole repository.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-E2E-001** MUST: The testing suite MUST use `@playwright/test` and `defineConfig` as the primary configuration mechanism for end-to-end browser testing.
- **R-E2E-002** MANDATORY (DISCOVERY POLICY): The consumer MUST omit all tool names, file names, commands, package managers, and version numbers and derive them from the project repository.
- **R-E2E-003** MANDATORY (LOCK-VERSION GROUNDING): Before writing code that uses a versioned library, execute in order: find dependency manifest, identify build tool, inspect repository lock or resolution artifact for exact resolved version, look up official documentation for that exact version, confirm every API exists in that exact version, and re-run steps per dependency at point of use for version-sensitive behavior.
- **R-E2E-004** MUST: Configure device simulation parameters using framework-supplied device presets to ensure tests accurately represent targeted runtime viewports.
- **R-E2E-005** MUST: Ensure all dynamic runtime values fall back to sensible local defaults when optional continuous integration environment variables are not supplied.

### Verify

```bash
# Discover and execute the project's test verification script as defined in the repository manifest
# Execute the project's static analysis and type checking scripts
```

**Accept when:**
- The project verification scripts execute the end-to-end test suite cleanly across configured device profiles without runtime syntax or configuration errors.
- Environment-dependent configuration bindings for execution mode and network port resolve correctly across local and pipeline environments.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration pipeline checks and pull request code reviews validate test configuration and test execution results. Non-standard browser testing harnesses or hardcoded environment configurations will be blocked from merging.
</enforcement>