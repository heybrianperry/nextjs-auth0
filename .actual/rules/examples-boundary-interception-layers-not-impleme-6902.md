---
version: 2
name: examples-boundary-interception-layers-not-impleme-6902
description: "Adoption of next/server for Server Request Interception and Routing: Boundary Interception Layers Not Implement Custom"
metadata:
  actual:
    adr_id: 690243c6-d009-41e4-b3b9-9387f199d4d2
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

# Adoption of next/server for Server Request Interception and Routing: Boundary Interception Layers Not Implement Custom

Scope: applies to `examples/with-cte/**`, `examples/with-dpop/**`, `examples/with-mrrt/**`.

These rules are ALWAYS ACTIVE for server-side request interception layers, proxy endpoints, and boundary routing modules.

### Rules

- **R-NS-001** MUST_NOT: Boundary interception layers MUST NOT implement custom HTTP request parsing abstractions that bypass next/server runtime primitives.

### Verify

```bash
# Discover and run the project static analysis and linting scripts to verify compliance of next/server imports across boundary modules.
# Discover and execute the project test suite covering request interception and response header modification flows.
```

**Accept when:**
- Static analysis passes with zero import violations or unapproved HTTP abstraction bypasses.
- All unit and integration tests for request interception and response header mutations complete successfully.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration lint and type-checking suites, as well as peer code review verification, are mandatory.
</enforcement>