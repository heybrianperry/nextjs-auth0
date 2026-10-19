---
version: 2
name: server-server-side-authentication-operations-re-a9d3
description: "Next.js Server Primitives Adoption for Server Authentication Clients: Server Side Authentication Operations Return Normalized"
metadata:
  actual:
    adr_id: a9d3b60d-ce17-47be-ad38-bdcca8e592d6
    status: accepted
    candidate_group_id: a345d086-5676-4977-87a4-8e8543fe1515
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/server/**
---

# Next.js Server Primitives Adoption for Server Authentication Clients: Server Side Authentication Operations Return Normalized

Scope: applies to `src/server/**`.

These rules are ALWAYS ACTIVE for all server-side authentication client modules managing passkey, multi-factor, and passwordless authentication flows requiring request headers or server response constructs.

### Rules

- **R-AUTH-001** SHOULD: Server-side authentication operations SHOULD return normalized response data structures defined by shared domain types to isolate callers from transport-specific details.
- **R-AUTH-002** MANDATORY: The consumer MUST derive all tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-AUTH-003** MANDATORY: Before writing code that uses a versioned library, execute in order: find dependency manifest, identify build tool, inspect lock/resolution artifact, look up official documentation for that exact version, confirm every API/class/function exists, and re-run per dependency at point of use.

### Verify

```bash
# Discover the project dependency resolution artifact and verify framework runtime dependencies resolve cleanly
# Discover and execute the project test runner for server-side authentication test suites
# Discover and execute the project static analysis and linting scripts
```

**Accept when:**
- All server authentication client test suites pass when validating header resolution and authentication client lifecycle operations.
- Static analysis verifies that server authentication clients source header and server response primitives exclusively from the designated framework server modules.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated CI test validation, static analysis, and architectural boundary checks during code review.
</enforcement>