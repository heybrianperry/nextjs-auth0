---
version: 2
name: server-developers-inspect-repository-lock-artif-c0eb
description: "Next.js Server Primitives Adoption for Server Authentication Clients: Developers Inspect Repository Lock Artifact Verify"
metadata:
  actual:
    adr_id: c0ebaff4-aab1-4bca-9a5f-703827cb17af
    status: accepted
    candidate_group_id: a345d086-5676-4977-87a4-8e8543fe1515
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/server/**
---

# Next.js Server Primitives Adoption for Server Authentication Clients: Developers Inspect Repository Lock Artifact Verify

Scope: applies to `src/server/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-AUTH-001** MUST: Developers MUST inspect the repository lock artifact to verify the exact resolved version of the framework dependency before implementing or modifying server authentication clients.

### Verify

```bash
# Discover the project dependency resolution artifact and verify that framework runtime dependencies resolve cleanly
# Discover and execute the project test runner for server-side authentication test suites
# Discover and execute the project static analysis and linting scripts to verify boundary constraints
```

**Accept when:**
- All server authentication client test suites pass when validating header resolution and authentication client lifecycle operations.
- Static analysis verifies that server authentication clients source header and server response primitives exclusively from the designated framework server modules.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>