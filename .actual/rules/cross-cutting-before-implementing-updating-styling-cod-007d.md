---
version: 2
name: cross-cutting-before-implementing-updating-styling-cod-007d
description: "Adopt Tailwindcss for Utility-First Application Styling: Before Implementing Updating Styling Code Engineers"
metadata:
  actual:
    adr_id: 007dded0-81ca-47e4-b29b-582758cb70c6
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

# Adopt Tailwindcss for Utility-First Application Styling: Before Implementing Updating Styling Code Engineers

Scope: applies to `e2e/test-app/**`, `examples/with-cte/**`, `examples/with-mrrt/**`, `examples/with-next-intl/**`, `examples/with-passkeys/**`, `examples/with-passwordless-db/**`, `examples/with-passwordless/**`, `examples/with-shadcn/**`.

These rules are ALWAYS ACTIVE for user interface presentation layers and frontend application packages within the repository.

### Rules

- **R-TAILWIND-001** MUST: Before implementing or updating styling code, engineers MUST discover the repository dependency manifest and resolution artifact to resolve the exact locked version of tailwindcss and consult the matching public documentation.

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