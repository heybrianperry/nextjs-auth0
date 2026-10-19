---
version: 2
name: client-client-modules-not-perform-manual-4eae
description: "Adoption of pathUtils Internal Module for Client Route Resolution: Client Modules Not Perform Manual String"
metadata:
  actual:
    adr_id: 4eaef2d8-4552-4afd-9dbe-6b4646094b7c
    status: accepted
    candidate_group_id: a2b468be-d313-45f9-8c06-f88068ede2ec
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/client/**
---

# Adoption of pathUtils Internal Module for Client Route Resolution: Client Modules Not Perform Manual String

Scope: applies to `src/client/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-PATH-001** MUST_NOT: Client modules MUST NOT perform manual string concatenation or regex formatting to construct authentication endpoint URLs.

### Verify

```bash
# Discover and run the project's static analysis and linting scripts
# Discover and run the project's test execution script
npm run lint
npm run test
```

**Accept when:**
- Static analysis passes with zero violations regarding path resolution utility usage in client modules.
- All unit and integration test suites covering client authentication flows execute successfully.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>