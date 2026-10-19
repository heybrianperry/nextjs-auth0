---
version: 2
name: cross-cutting-applications-repository-adopt-next-core-058e
description: "Adoption of next for Application Layout and Font Management: Applications Repository Adopt Next Core Presentation"
metadata:
  actual:
    adr_id: 058ec000-6319-4f4f-be27-894a4867b0f7
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

# Adoption of next for Application Layout and Font Management: Applications Repository Adopt Next Core Presentation

Scope: applies to `e2e/test-app/app/**`, `examples/with-mrrt/app/**`, `examples/with-next-intl/app/**`, `examples/with-shadcn/app/**`.

These rules are ALWAYS ACTIVE for root application layout components and presentation shell definitions across application modules and examples.

### Rules

- **R-APP-001** MUST: Applications in the repository MUST adopt next as the core presentation framework for structuring root layout hierarchies.

### Verify

```bash
# Discover and execute project dependency verification, static analysis, linting, build, and testing scripts
# (Commands are project-dependent and derived from repository metadata)
```

**Accept when:**
- The project build and static analysis commands execute without errors or lint warnings.
- All root layouts correctly import the required framework and font modules while maintaining zero external font network requests.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>