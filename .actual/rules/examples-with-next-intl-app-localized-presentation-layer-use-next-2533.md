---
version: 2
name: examples-with-next-intl-app-localized-presentation-layer-use-next-2533
description: "Adopt next-intl for Localized Application Routing and Translation: Localized Presentation Layer Use Next Intl"
metadata:
  actual:
    adr_id: 25339a94-7f7d-4c30-a67f-dde3f658a0e9
    status: accepted
    candidate_group_id: bc4ba2d8-c628-4a0d-b685-e377c0def63f
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-next-intl/app/**
---

# Adopt next-intl for Localized Application Routing and Translation: Localized Presentation Layer Use Next Intl

Scope: applies to `examples/with-next-intl/app/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-INTL-001** MUST: The localized presentation layer MUST use next-intl for message translation and internationalized route rendering.

### Verify

```bash
# Inspect the project dependency manifest and lockfile to confirm the exact resolved version of the internationalization dependency.
# Run the project static analysis and linting scripts to verify all localized views import routing primitives from the designated internal routing module.
# Execute the repository test suite to ensure localized route layouts and pages render translations without missing key errors.
```

**Accept when:**
- All localized routes and views resolve localized message keys through next-intl without runtime resolution failures.
- All localized navigation links use the internal routing module rather than unlocalized primitives.
- Repository static analysis and test validation suites pass without internationalization import or execution errors.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>