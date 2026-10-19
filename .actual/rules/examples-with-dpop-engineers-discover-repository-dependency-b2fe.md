---
version: 2
name: examples-with-dpop-engineers-discover-repository-dependency-b2fe
description: "Express HTTP Middleware Pipeline Architecture: Engineers Discover Repository Dependency Manifest Resolution"
metadata:
  actual:
    adr_id: b2fed0d5-0366-4a35-897e-1cbec53fddca
    status: accepted
    candidate_group_id: 9bb84435-f3dc-4714-8a47-97e99459c951
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# Express HTTP Middleware Pipeline Architecture: Engineers Discover Repository Dependency Manifest Resolution

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-EXP-001** MUST: Engineers MUST discover the repository dependency manifest and resolution artifact to verify the exact locked version of Express and all associated middleware packages prior to implementation.
- **R-EXP-002** MUST: Register telemetry and logging middleware immediately after instantiating the Express application to capture full request latency.
- **R-EXP-003** MUST: Ensure body parsing middleware precedes any route handler or custom middleware that inspects request payload data.
- **R-EXP-004** MUST: Follow lock-version grounding by finding the dependency manifest, identifying the build tool, inspecting the lock artifact, looking up official documentation for that exact version, confirming every API/class/function exists, and re-running per dependency at point of use.

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