---
version: 2
name: cross-cutting-frontend-application-packages-adopt-tail-a29a
description: "Adopt Tailwindcss for Utility-First Application Styling: Frontend Application Packages Adopt Tailwindcss Foundational"
metadata:
  actual:
    adr_id: a29a2334-785b-4118-b869-2217ab651fe7
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

# Adopt Tailwindcss for Utility-First Application Styling: Frontend Application Packages Adopt Tailwindcss Foundational

Scope: applies to `e2e/test-app/**`, `examples/with-cte/**`, `examples/with-mrrt/**`, `examples/with-next-intl/**`, `examples/with-passkeys/**`, `examples/with-passwordless-db/**`, `examples/with-passwordless/**`, `examples/with-shadcn/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-TW-001** MUST: Frontend application packages MUST adopt tailwindcss as the foundational styling solution for user interface layout and visual presentation.
- **R-TW-002** MANDATORY: The consumer MUST discover tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-TW-003** MANDATORY: Before writing code that uses a versioned library, execute the lock-version grounding sequence: find dependency manifest, identify build tool, inspect repository lock or resolution artifact for exact resolved version, look up official documentation for that exact version, confirm every API/class/function exists in that version, and re-run steps per dependency at point of use.
- **R-TW-004** MANDATORY: Configure content scanning boundaries precisely to target source files containing presentation markup to avoid unnecessary compilation overhead.
- **R-TW-005** MANDATORY: Organize custom utility extensions and theme overrides within the configuration schema rather than writing raw cascading stylesheets.

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