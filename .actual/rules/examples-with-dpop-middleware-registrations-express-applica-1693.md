---
version: 2
name: examples-with-dpop-middleware-registrations-express-applica-1693
description: "Express HTTP Middleware Pipeline Architecture: Middleware Registrations Express Application Instance Precede"
metadata:
  actual:
    adr_id: 16930089-f8d9-461e-b743-bbf68fbacb64
    status: accepted
    candidate_group_id: 9bb84435-f3dc-4714-8a47-97e99459c951
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# Express HTTP Middleware Pipeline Architecture: Middleware Registrations Express Application Instance Precede

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-EXP-001** MUST: Middleware registrations on the Express application instance MUST precede all route definitions to guarantee uniform inspection of incoming requests.

### Verify

```bash
# Discover and run the repository build validation and lint scripts to verify middleware chaining syntax.
# Execute the project automated integration test suite to verify that middleware handles boundary ingress correctly.
```

**Accept when:**
- All HTTP ingress routes process requests through the registered middleware pipeline without uncaught exceptions.
- Automated test suites confirm that security headers and cross-origin resource sharing headers are present on HTTP responses.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>