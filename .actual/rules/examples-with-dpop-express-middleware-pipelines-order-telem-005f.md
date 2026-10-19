---
version: 2
name: examples-with-dpop-express-middleware-pipelines-order-telem-005f
description: "Express HTTP Middleware Pipeline Architecture: Express Middleware Pipelines Order Telemetry Logging"
metadata:
  actual:
    adr_id: 005f8500-0a7a-42a8-b9c6-5cb5bbb6519a
    status: accepted
    candidate_group_id: 9bb84435-f3dc-4714-8a47-97e99459c951
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# Express HTTP Middleware Pipeline Architecture: Express Middleware Pipelines Order Telemetry Logging

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for HTTP API service ingress definitions using Express and boundary middleware registration pipelines.

### Rules

- **R-EXP-001** SHOULD: Express middleware pipelines order telemetry and logging handlers first, followed by transport security and cross-origin controls, body parsing, and endpoint routing.
- **R-EXP-002** MANDATORY: The consumer MUST discover tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-EXP-003** MANDATORY: Before writing code that uses a versioned library, execute lock-version grounding (find dependency manifest, identify build tool, inspect lock or resolution artifact for exact resolved version, look up official documentation for that exact version, confirm every API/class/function exists in that version, and re-run per dependency at point of use).
- **R-EXP-004** MANDATORY: Register telemetry and logging middleware immediately after instantiating the Express application to capture full request latency.
- **R-EXP-005** MANDATORY: Ensure body parsing middleware precedes any route handler or custom middleware that inspects request payload data.

### Verify

```bash
# Discover and run repository build validation, lint scripts, and integration test suite to verify middleware chaining and boundary ingress handling
```

**Accept when:**
- All HTTP ingress routes process requests through the registered middleware pipeline without uncaught exceptions.
- Automated test suites confirm that security headers and cross-origin resource sharing headers are present on HTTP responses.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>