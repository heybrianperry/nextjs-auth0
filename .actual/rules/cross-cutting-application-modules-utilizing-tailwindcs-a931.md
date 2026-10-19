---
version: 2
name: cross-cutting-application-modules-utilizing-tailwindcs-a931
description: "Adopt Tailwindcss for Utility-First Application Styling: Application Modules Utilizing Tailwindcss Declare Configuration"
metadata:
  actual:
    adr_id: a9314a5e-5f98-48ef-9dfa-f5506c44b609
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

# Adopt Tailwindcss for Utility-First Application Styling: Application Modules Utilizing Tailwindcss Declare Configuration

Scope: applies to `e2e/test-app/**`, `examples/with-cte/**`, `examples/with-mrrt/**`, `examples/with-next-intl/**`, `examples/with-passkeys/**`, `examples/with-passwordless-db/**`, `examples/with-passwordless/**`, `examples/with-shadcn/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-TW-001** MUST: Application modules utilizing tailwindcss MUST declare configuration modules that define design tokens and scope content scanning strictly to presentation source files.

### Verify

```bash
# Discover and run the repository linter script to validate utility class usage across presentation files.
# Discover and run the project build script to verify stylesheet generation and purge correctness across all application workspaces.
```

**Accept when:**
- Application build scripts successfully generate optimized stylesheets with zero compilation errors.
- Static analysis workflows pass without unresolved utility class or configuration schema violations.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>