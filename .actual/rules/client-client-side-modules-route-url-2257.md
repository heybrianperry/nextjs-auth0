---
version: 2
name: client-client-side-modules-route-url-2257
description: "Adoption of pathUtils Internal Module for Client Route Resolution: Client Side Modules Route Url Path"
metadata:
  actual:
    adr_id: 2257106a-537c-4043-b879-58f2ea0ba663
    status: accepted
    candidate_group_id: a2b468be-d313-45f9-8c06-f88068ede2ec
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/client/**
---

# Adoption of pathUtils Internal Module for Client Route Resolution: Client Side Modules Route Url Path

Scope: applies to `src/client/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-PATH-001** MUST: Client-side modules MUST route all URL path resolution, normalization, and route concatenation through the internal pathUtils module.

### Verify

```bash
# Discover and run the project's static analysis, linting, and test scripts
# to verify compliance with internal module import conventions across client files.
```

**Accept when:**
- Static analysis passes with zero violations regarding path resolution utility usage in client modules.
- All unit and integration test suites covering client authentication flows execute successfully.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>