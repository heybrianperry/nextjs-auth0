---
version: 2
name: examples-request-interception-layers-server-proxy-821b
description: "Adoption of next/server for Server Request Interception and Routing: Request Interception Layers Server Proxy Modules"
metadata:
  actual:
    adr_id: 821b7e70-b1a0-4237-bbc7-55fb45a16da5
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

# Adoption of next/server for Server Request Interception and Routing: Request Interception Layers Server Proxy Modules

Scope: applies to `examples/with-cte/**`, `examples/with-dpop/**`, `examples/with-mrrt/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-NXT-001** MUST: All request interception layers and server proxy modules MUST utilize next/server as the standard module for request interception, URL resolution, and response generation.

### Verify

```bash
# Discover and run the project static analysis and linting scripts to verify compliance of next/server imports across boundary modules
# Discover and execute the project test suite covering request interception and response header modification flows
```

**Accept when:**
- Static analysis passes with zero import violations or unapproved HTTP abstraction bypasses.
- All unit and integration tests for request interception and response header mutations complete successfully.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration lint and type-checking suites, along with peer code review, enforce next/server primitives.
</enforcement>