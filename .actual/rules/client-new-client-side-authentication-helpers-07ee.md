---
version: 2
name: client-new-client-side-authentication-helpers-07ee
description: "Adoption of pathUtils Internal Module for Client Route Resolution: New Client Side Authentication Helpers Hooks"
metadata:
  actual:
    adr_id: 07eeb433-8791-45bf-af37-ed4d4378202c
    status: accepted
    candidate_group_id: a2b468be-d313-45f9-8c06-f88068ede2ec
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/client/**
---

# Adoption of pathUtils Internal Module for Client Route Resolution: New Client Side Authentication Helpers Hooks

Scope: applies to `src/client/**`.

These rules are ALWAYS ACTIVE for all client-side authentication modules, hooks, providers, and navigation helpers that interact with configured route endpoints.

### Rules

- **R-PATH-001** SHOULD: New client-side authentication helpers, hooks, and provider components reuse established pathUtils resolution routines rather than introducing duplicate helper functions.

### Verify

```bash
# Discover and run the project's static analysis, linting, and test execution scripts
# Example discovery:
npm run lint || yarn lint || pnpm lint
npm test || yarn test || pnpm test
```

**Accept when:**
- Static analysis passes with zero violations regarding path resolution utility usage in client modules.
- All unit and integration test suites covering client authentication flows execute successfully.

<enforcement>
Claude Code MUST NOT skip or defer verification. All pull requests containing inline string concatenation for routes or failing verification scripts must be blocked from merging until corrected.
</enforcement>