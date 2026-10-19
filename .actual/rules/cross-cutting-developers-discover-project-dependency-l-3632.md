---
version: 2
name: cross-cutting-developers-discover-project-dependency-l-3632
description: "Adoption of next for Application Layout and Font Management: Developers Discover Project Dependency Lock Artifact"
metadata:
  actual:
    adr_id: 36326cb1-a4fc-4651-9a15-0df05f9c4fb9
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

# Adoption of next for Application Layout and Font Management: Developers Discover Project Dependency Lock Artifact

Scope: applies to `e2e/test-app/app/**`, `examples/with-mrrt/app/**`, `examples/with-next-intl/app/**`, `examples/with-shadcn/app/**`.

These rules are ALWAYS ACTIVE for root application layout components and presentation shell definitions across application modules and examples.

### Rules

- **R-NXT-001** MUST: Developers MUST discover the project dependency lock artifact and verify the exact resolved version of next before authoring layout or font integration code.

### Verify

```bash
# Discover and execute the project dependency verification command
# Discover and execute the project static analysis and lint commands
# Discover and run the project build and testing scripts
```

**Accept when:**
- The project build and static analysis commands execute without errors or lint warnings.
- All root layouts correctly import the required framework and font modules while maintaining zero external font network requests.

<enforcement>
Claude Code MUST NOT skip or defer verification. All layout components and font configurations must comply with locked framework versions and static analysis requirements.
</enforcement>