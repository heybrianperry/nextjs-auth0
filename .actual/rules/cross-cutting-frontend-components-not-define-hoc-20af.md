---
version: 2
name: cross-cutting-frontend-components-not-define-hoc-20af
description: "Adopt Tailwindcss for Utility-First Application Styling: Frontend Components Not Define Hoc Inline"
metadata:
  actual:
    adr_id: 20afc7e7-cd3c-4268-a110-05c2c3fa4ebe
    status: accepted
    candidate_group_id: 924a3d3b-dd21-474f-b737-b0a63d7dca24
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - e2e/test-app/**
      - examples/with-cte/**
      - examples/with-mrrt/**
      - examples/with-next-intl/**
      - examples/with-passkeys/**
      - examples/with-passwordless-db/**
      - examples/with-passwordless/**
      - examples/with-shadcn/**
---

# Adopt Tailwindcss for Utility-First Application Styling: Frontend Components Not Define Hoc Inline

Scope: applies to `e2e/test-app/**`, `examples/with-cte/**`, `examples/with-mrrt/**`, `examples/with-next-intl/**`, `examples/with-passkeys/**`, `examples/with-passwordless-db/**`, `examples/with-passwordless/**`, `examples/with-shadcn/**`.

These rules are ALWAYS ACTIVE for user interface presentation layers, frontend application packages, component styling, layout composition, and design token definitions.

### Rules

- **R-TW-001** MUST_NOT: Frontend components MUST_NOT define ad-hoc inline styles or uncoordinated global style declarations where equivalent utility definitions exist.

### Verify

```bash
# Discover and run the repository linter script to validate utility class usage across presentation files.
# Discover and run the project build script to verify stylesheet generation and purge correctness across all application workspaces.
```

**Accept when:**
- Application build scripts successfully generate optimized stylesheets with zero compilation errors.
- Static analysis workflows pass without unresolved utility class or configuration schema violations.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration static analysis workflows and peer reviews validate styling rules and configuration validity.
</enforcement>