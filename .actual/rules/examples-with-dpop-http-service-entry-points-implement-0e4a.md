---
version: 2
name: examples-with-dpop-http-service-entry-points-implement-0e4a
description: "Express HTTP Middleware Pipeline Architecture: Http Service Entry Points Implement Express"
metadata:
  actual:
    adr_id: 0e4a97b4-2f28-4e58-ad9b-f50b84fcc6f2
    status: accepted
    candidate_group_id: 9bb84435-f3dc-4714-8a47-97e99459c951
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# Express HTTP Middleware Pipeline Architecture: Http Service Entry Points Implement Express

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-EXP-001** MUST: HTTP service entry points MUST implement the Express application middleware pipeline using app.use to enforce boundary cross-cutting concerns prior to route handler execution.

### Verify

```bash
# Discover and run repository build validation and lint scripts to verify middleware chaining syntax
npm run build
npm run lint
# Execute project automated integration test suite to verify boundary ingress handling
npm test
```

**Accept when:**
- All HTTP ingress routes process requests through the registered middleware pipeline without uncaught exceptions.
- Automated test suites confirm that security headers and cross-origin resource sharing headers are present on HTTP responses.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>