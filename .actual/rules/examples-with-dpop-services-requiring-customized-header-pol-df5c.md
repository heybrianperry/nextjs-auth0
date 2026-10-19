---
version: 2
name: examples-with-dpop-services-requiring-customized-header-pol-df5c
description: "Adopt Helmet for HTTP Security Headers: Services Requiring Customized Header Policies Pass"
metadata:
  actual:
    adr_id: df5c4aed-90d7-421b-a38c-002edec822db
    status: accepted
    candidate_group_id: 06493b99-f9c8-438f-b320-b4939e124ca8
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# Adopt Helmet for HTTP Security Headers: Services Requiring Customized Header Policies Pass

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-HLMT-001** SHOULD: Services requiring customized header policies pass explicit configuration options into Helmet rather than disabling the middleware entirely.

### Verify

```bash
grep -rn "app.use(helmet" . || echo "Verify Helmet middleware registration in HTTP server setup"
find . -maxdepth 3 -name "*test*" -o -name "*spec*" | head -n 1 && echo "Execute discovered test runner to validate response headers"
```

**Accept when:**
- HTTP server setup code contains Helmet middleware registration prior to route definitions
- Discovered test suite executes successfully and confirms security headers are present on HTTP responses

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>