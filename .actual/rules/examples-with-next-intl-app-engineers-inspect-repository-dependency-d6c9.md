---
version: 2
name: examples-with-next-intl-app-engineers-inspect-repository-dependency-d6c9
description: "Adopt next-intl for Localized Application Routing and Translation: Engineers Inspect Repository Dependency Manifest Resolution"
metadata:
  actual:
    adr_id: d6c9665a-5079-4338-835e-7dcc7f0ba725
    status: accepted
    candidate_group_id: bc4ba2d8-c628-4a0d-b685-e377c0def63f
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-next-intl/app/**
---

# Adopt next-intl for Localized Application Routing and Translation: Engineers Inspect Repository Dependency Manifest Resolution

Scope: applies to `examples/with-next-intl/app/**`.

These rules are ALWAYS ACTIVE for all route layouts, view pages, and navigation components within localized application segments.

### Rules

- **R-INTL-001** MUST: Engineers MUST inspect the repository dependency manifest and resolution artifact to resolve the exact locked version of next-intl prior to adopting or altering internationalization APIs.

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