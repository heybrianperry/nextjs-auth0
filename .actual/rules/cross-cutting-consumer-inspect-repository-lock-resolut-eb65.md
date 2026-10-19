---
version: 2
name: cross-cutting-consumer-inspect-repository-lock-resolut-eb65
description: "`@playwright/test` End-to-End Testing Framework Adoption: Consumer Inspect Repository Lock Resolution Artifact"
metadata:
  actual:
    adr_id: eb657468-8c42-4ee3-9a97-5bc92f9d4a0a
    status: accepted
    candidate_group_id: 403ff59f-0ebc-49a7-89f5-39b4c2e9d5ce
    evidence:
      source: deep
  scope:
    root: .
---

# `@playwright/test` End-to-End Testing Framework Adoption: Consumer Inspect Repository Lock Resolution Artifact

Scope: applies to the whole repository.

These rules are ALWAYS ACTIVE for all end-to-end browser test suites and configuration definitions within the repository, as well as automated integration and end-to-end test execution stages in continuous integration workflows.

### Rules

- **R-PLAYWRIGHT-001** MUST: The consumer MUST inspect the repository lock or resolution artifact to determine the exact resolved version of `@playwright/test` prior to authoring or updating test suites and configurations.
- **R-PLAYWRIGHT-002** MANDATORY: The consumer MUST derive all tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-PLAYWRIGHT-003** MANDATORY (LOCK-VERSION GROUNDING): Before writing code that uses a versioned library, execute in order:
  1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
  2. Identify the build tool from the manifest.
  3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
  4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
  5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
  6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- **R-PLAYWRIGHT-004** SHOULD: Configure device simulation parameters using framework-supplied device presets to ensure tests accurately represent targeted runtime viewports.
- **R-PLAYWRIGHT-005** SHOULD: Ensure all dynamic runtime values fall back to sensible local defaults when optional continuous integration environment variables are not supplied.

### Verify

```bash
# Discover and execute the project's test verification script as defined in the repository manifest to validate test configuration validity.
# Execute the project's static analysis and type checking scripts to ensure end-to-end configuration definitions adhere to repository conventions.
```

**Accept when:**
- The project verification scripts execute the end-to-end test suite cleanly across configured device profiles without runtime syntax or configuration errors.
- Environment-dependent configuration bindings for execution mode and network port resolve correctly across local and pipeline environments.

<enforcement>
Claude Code MUST NOT skip or defer verification. Pull requests introducing non-standard browser testing harnesses or hardcoded environment configurations will be blocked from merging.
</enforcement>