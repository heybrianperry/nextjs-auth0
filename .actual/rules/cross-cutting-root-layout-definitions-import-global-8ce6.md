---
version: 2
name: cross-cutting-root-layout-definitions-import-global-8ce6
description: "Adoption of next for Application Layout and Font Management: Root Layout Definitions Import Global Stylesheets"
metadata:
  actual:
    adr_id: 8ce6d850-ff9d-43f6-ab14-4ff34a2e40f4
    status: accepted
    candidate_group_id: 730a51f3-0da2-4ea4-a952-639ced2b239b
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - e2e/test-app/app/**
      - examples/with-mrrt/app/**
      - examples/with-next-intl/app/**
      - examples/with-shadcn/app/**
---

# Adoption of next for Application Layout and Font Management: Root Layout Definitions Import Global Stylesheets

Scope: applies to `e2e/test-app/app/**`, `examples/with-mrrt/app/**`, `examples/with-next-intl/app/**`, `examples/with-shadcn/app/**`.

These rules are ALWAYS ACTIVE for root application layout components and presentation shell definitions across application modules and examples.

### Rules

- **R-LAYOUT-001** SHOULD: Root layout definitions SHOULD import global stylesheets at the top-level layout boundary to ensure uniform baseline styling across nested route segments.

### Verify

```bash
# Discover and execute project dependency verification, lint, build, and test commands
# Example discovery flow:
# 1. Inspect package manifest for test/lint/build scripts
# 2. Run dependency check
# 3. Run linter and static analysis
# 4. Run build and tests
npm run lint
npm run build
```

**Accept when:**
- The project build and static analysis commands execute without errors or lint warnings.
- All root layouts correctly import the required framework and font modules while maintaining zero external font network requests.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>