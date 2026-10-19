---
version: 2
name: cross-cutting-components-outside-root-layout-boundarie-5bf2
description: "Adoption of next for Application Layout and Font Management: Components Outside Root Layout Boundaries Not"
metadata:
  actual:
    adr_id: 5bf2f961-fe92-435d-bd34-cc2d87e5ab83
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

# Adoption of next for Application Layout and Font Management: Components Outside Root Layout Boundaries Not

Scope: applies to `e2e/test-app/app/**`, `examples/with-mrrt/app/**`, `examples/with-next-intl/app/**`, `examples/with-shadcn/app/**`.

These rules are ALWAYS ACTIVE for root application layout components and presentation shell definitions across application modules and examples.

### Rules

- **R-NXT-001** MUST_NOT: Components outside root layout boundaries MUST NOT import local font loaders or duplicate global baseline stylesheet declarations.

### Verify

```bash
# Discover and run the project dependency verification command
# Discover and run the project static analysis and lint commands
# Discover and run the project build and testing scripts
```

**Accept when:**
- The project build and static analysis commands execute without errors or lint warnings.
- All root layouts correctly import the required framework and font modules while maintaining zero external font network requests.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>