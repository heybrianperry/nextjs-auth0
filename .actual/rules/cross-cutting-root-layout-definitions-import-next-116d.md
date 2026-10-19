---
version: 2
name: cross-cutting-root-layout-definitions-import-next-116d
description: "Adoption of next for Application Layout and Font Management: Root Layout Definitions Import Next Font"
metadata:
  actual:
    adr_id: 116db902-01be-4ebd-81d3-25fd9fe20076
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

# Adoption of next for Application Layout and Font Management: Root Layout Definitions Import Next Font

Scope: applies to `e2e/test-app/app/**`, `examples/with-mrrt/app/**`, `examples/with-next-intl/app/**`, `examples/with-shadcn/app/**`.

These rules are ALWAYS ACTIVE for root application layout components and presentation shell definitions across application modules and examples.

### Rules

- **R-LAYOUT-001** MUST: Root layout definitions MUST import next/font/local to configure and optimize local typography assets rather than relying on unmanaged external stylesheet font links.

### Verify

```bash
# Discover and execute project dependency verification, lint, build, and test scripts
```

**Accept when:**
- The project build and static analysis commands execute without errors or lint warnings.
- All root layouts correctly import the required framework and font modules while maintaining zero external font network requests.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>