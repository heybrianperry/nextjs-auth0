---
version: 2
name: client-client-boundary-interactions-dispatched-291a
description: "Adoption of pathUtils Internal Module for Client Route Resolution: Client Boundary Interactions Dispatched Through Network"
metadata:
  actual:
    adr_id: 291addc8-e87a-4c77-b491-3271e7a9db02
    status: accepted
    candidate_group_id: a2b468be-d313-45f9-8c06-f88068ede2ec
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/client/**
---

# Adoption of pathUtils Internal Module for Client Route Resolution: Client Boundary Interactions Dispatched Through Network

Scope: applies to `src/client/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-PATH-001** MUST: Client boundary interactions dispatched through network request interfaces MUST consume route paths that have been pre-validated and formatted via the pathUtils module.

### Verify

```bash
# Discover and run the project's static analysis and linting scripts to verify compliance with internal module import conventions across client files.
# Discover and run the project's test execution script to validate that all path resolution unit tests and client integration tests pass.
```

**Accept when:**
- Static analysis passes with zero violations regarding path resolution utility usage in client modules.
- All unit and integration test suites covering client authentication flows execute successfully.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>