---
version: 2
name: cross-cutting-shared-design-tokens-such-color-3fc4
description: "Adopt Tailwindcss for Utility-First Application Styling: Shared Design Tokens Such Color Palettes"
metadata:
  actual:
    adr_id: 3fc44185-7bab-460a-a688-0ef3ff43ad95
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

# Adopt Tailwindcss for Utility-First Application Styling: Shared Design Tokens Such Color Palettes

Scope: applies to `e2e/test-app/**`, `examples/with-cte/**`, `examples/with-mrrt/**`, `examples/with-next-intl/**`, `examples/with-passkeys/**`, `examples/with-passwordless-db/**`, `examples/with-passwordless/**`, `examples/with-shadcn/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-STYL-001** SHOULD: Shared design tokens such as color palettes, spacing units, and typography scales SHOULD be standardized within the configuration definition rather than duplicated as arbitrary values.
- **R-STYL-002** MANDATORY: The consumer MUST derive all tool names, file names, commands, package managers, and version numbers from the project repository (DISCOVERY POLICY).
- **R-STYL-003** MANDATORY: Before writing code that uses a versioned library, execute the lock-version grounding steps in order (dependency manifest -> build tool -> repository lock -> official documentation -> API confirmation -> per-dependency re-run).
- **R-STYL-004** MANDATORY: Configure content scanning boundaries precisely to target source files containing presentation markup to avoid unnecessary compilation overhead.
- **R-STYL-005** MANDATORY: Organize custom utility extensions and theme overrides within the configuration schema rather than writing raw cascading stylesheets.

### Verify

```bash
# Discover and run the repository linter script to validate utility class usage across presentation files
# Discover and run the project build script to verify stylesheet generation and purge correctness across all application workspaces
```

**Accept when:**
- Application build scripts successfully generate optimized stylesheets with zero compilation errors.
- Static analysis workflows pass without unresolved utility class or configuration schema violations.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration static analysis workflows and peer reviews validate styling rules and configuration validity; engineers must refactor non-compliant styling into approved utility patterns prior to pull request approval.
</enforcement>