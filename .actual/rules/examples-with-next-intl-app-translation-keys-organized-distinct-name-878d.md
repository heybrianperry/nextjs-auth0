---
version: 2
name: examples-with-next-intl-app-translation-keys-organized-distinct-name-878d
description: "Adopt next-intl for Localized Application Routing and Translation: Translation Keys Organized Distinct Namespaces Corresponding"
metadata:
  actual:
    adr_id: 878d19c7-8be8-47b5-afda-25139afe4ede
    status: accepted
    candidate_group_id: bc4ba2d8-c628-4a0d-b685-e377c0def63f
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-next-intl/app/**
---

# Adopt next-intl for Localized Application Routing and Translation: Translation Keys Organized Distinct Namespaces Corresponding

Scope: applies to `examples/with-next-intl/app/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-INT-001** SHOULD: Translation keys SHOULD be organized into distinct namespaces corresponding to application features and views.

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
Claude Code MUST NOT skip or defer verification. Automated static analysis checks and continuous integration pipelines verify compliance, and build/pull-request rejections apply for violations.
</enforcement>