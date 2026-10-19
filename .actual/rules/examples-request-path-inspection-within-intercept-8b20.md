---
version: 2
name: examples-request-path-inspection-within-intercept-8b20
description: "Adoption of next/server for Server Request Interception and Routing: Request Path Inspection Within Interception Modules"
metadata:
  actual:
    adr_id: 8b200dac-7935-4e9a-a482-f7f09774efa1
    status: accepted
    candidate_group_id: 6386fe8c-1025-409b-be3e-4cff9e49397d
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-cte/**
      - examples/with-dpop/**
      - examples/with-mrrt/**
---

# Adoption of next/server for Server Request Interception and Routing: Request Path Inspection Within Interception Modules

Scope: applies to `examples/with-cte/**`, `examples/with-dpop/**`, `examples/with-mrrt/**`.

These rules are ALWAYS ACTIVE for server-side request interception layers, proxy endpoints, boundary routing modules, and components responsible for mutating response headers or directing request control flow at the server boundary.

### Rules

- **R-ADR-001** MUST: Request path inspection within interception modules MUST access request path parameters via the request.nextUrl interface rather than manual string parsing.

### Verify

```bash
# Discover and run the project static analysis and linting scripts to verify compliance of next/server imports across boundary modules.
# Discover and execute the project test suite covering request interception and response header modification flows.
```

**Accept when:**
- Static analysis passes with zero import violations or unapproved HTTP abstraction bypasses.
- All unit and integration tests for request interception and response header mutations complete successfully.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration lint and type-checking suites, as well as peer code reviews, enforce these rules and will fail on unapproved imports or bypasses of next/server primitives.
</enforcement>