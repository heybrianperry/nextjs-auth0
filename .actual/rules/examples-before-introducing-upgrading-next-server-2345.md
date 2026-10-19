---
version: 2
name: examples-before-introducing-upgrading-next-server-2345
description: "Adoption of next/server for Server Request Interception and Routing: Before Introducing Upgrading Next Server Dependencies"
metadata:
  actual:
    adr_id: 23458b41-ed1a-4a03-b58a-d8f66036caf7
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

# Adoption of next/server for Server Request Interception and Routing: Before Introducing Upgrading Next Server Dependencies

Scope: applies to `examples/with-cte/**`, `examples/with-dpop/**`, `examples/with-mrrt/**`.

These rules are ALWAYS ACTIVE for server-side request interception layers, proxy endpoints, boundary routing modules, and components responsible for mutating response headers or directing request control flow at the server boundary.

### Rules

- **R-NSV-001** MUST: Before introducing or upgrading next/server dependencies, developers MUST discover the repository lock artifact and verify the exact resolved version against public API documentation.

### Verify

```bash
# Discover and run the project static analysis and linting scripts to verify compliance of next/server imports across boundary modules
# Discover and execute the project test suite covering request interception and response header modification flows
```

**Accept when:**
- Static analysis passes with zero import violations or unapproved HTTP abstraction bypasses.
- All unit and integration tests for request interception and response header mutations complete successfully.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated continuous integration lint/type-checking suites and peer code review.
</enforcement>