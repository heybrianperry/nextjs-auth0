---
version: 2
name: examples-response-metadata-boundary-transmission-6072
description: "Adoption of next/server for Server Request Interception and Routing: Response Metadata Boundary Transmission Results Set"
metadata:
  actual:
    adr_id: 60720395-d24a-4cf2-96f7-0757ecfb75ea
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

# Adoption of next/server for Server Request Interception and Routing: Response Metadata Boundary Transmission Results Set

Scope: applies to `examples/with-cte/**`, `examples/with-dpop/**`, `examples/with-mrrt/**`.

These rules are ALWAYS ACTIVE for server-side request interception layers, proxy endpoints, and boundary routing modules.

### Rules

- **R-NS-001** MUST: Response metadata and boundary transmission results MUST be set through the response.headers interface on generated response instances.

### Verify

```bash
# Discover and run the project static analysis and linting scripts to verify compliance of next/server imports across boundary modules
# Discover and execute the project test suite covering request interception and response header modification flows
```

**Accept when:**
- Static analysis passes with zero import violations or unapproved HTTP abstraction bypasses.
- All unit and integration tests for request interception and response header mutations complete successfully.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>