---
version: 2
name: examples-interception-pipelines-structure-header-5562
description: "Adoption of next/server for Server Request Interception and Routing: Interception Pipelines Structure Header Mutations Redirect"
metadata:
  actual:
    adr_id: 55624e6d-1700-4ac3-93d5-d9236fecb91b
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

# Adoption of next/server for Server Request Interception and Routing: Interception Pipelines Structure Header Mutations Redirect

Scope: applies to `examples/with-cte/**`, `examples/with-dpop/**`, `examples/with-mrrt/**`.

These rules are ALWAYS ACTIVE for server-side request interception layers, proxy endpoints, and boundary routing modules responsible for mutating response headers or directing request control flow at the server boundary.

### Rules

- **R-INT-001** SHOULD: Interception pipelines structure header mutations and redirect parameters idempotently before forwarding control to downstream handlers.
- **R-INT-002** MANDATORY: Discover project dependency resolution artifacts to determine the exact installed version of next/server before employing server response primitives.
- **R-INT-003** MANDATORY: Ensure that all URL redirection parameters and response headers populated during interception follow consistent casing and naming conventions defined across the repository.

### Verify

```bash
# Discover and run the project static analysis and linting scripts to verify compliance of next/server imports across boundary modules
# Discover and execute the project test suite covering request interception and response header modification flows
```

**Accept when:**
- Static analysis passes with zero import violations or unapproved HTTP abstraction bypasses.
- All unit and integration tests for request interception and response header mutations complete successfully.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration linting, type-checking suites, and peer code reviews enforce compliance.
</enforcement>