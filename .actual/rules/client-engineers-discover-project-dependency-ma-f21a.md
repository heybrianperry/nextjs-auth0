---
version: 2
name: client-engineers-discover-project-dependency-ma-f21a
description: "Adoption of pathUtils Internal Module for Client Route Resolution: Engineers Discover Project Dependency Manifest Lock"
metadata:
  actual:
    adr_id: f21ad8b7-e5fe-48bc-9a31-0d3de6f834f1
    status: accepted
    candidate_group_id: a2b468be-d313-45f9-8c06-f88068ede2ec
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/client/**
---

# Adoption of pathUtils Internal Module for Client Route Resolution: Engineers Discover Project Dependency Manifest Lock

Scope: applies to `src/client/**`.

These rules are ALWAYS ACTIVE for client-side authentication modules, hooks, providers, and navigation helpers that interact with configured route endpoints, and client network boundary calls that dispatch requests to configured server authentication paths.

### Rules

- **R-PATH-001** MUST: Engineers MUST discover the project dependency manifest and lock artifact to verify locked versions of all external dependencies before integrating client module routines.

### Verify

```bash
# Discover and run the project's static analysis and linting scripts
# Discover and run the project's test execution script
```

**Accept when:**
- Static analysis passes with zero violations regarding path resolution utility usage in client modules.
- All unit and integration test suites covering client authentication flows execute successfully.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration pipeline execution checks code style, import boundaries, and test assertions.
</enforcement>