---
version: 2
name: server-authentication-client-modules-executing-d87b
description: "Next.js Server Primitives Adoption for Server Authentication Clients: Authentication Client Modules Executing Server Environment"
metadata:
  actual:
    adr_id: d87bd7d3-086c-4a47-ad06-d75d42993f8e
    status: accepted
    candidate_group_id: a345d086-5676-4977-87a4-8e8543fe1515
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/server/**
---

# Next.js Server Primitives Adoption for Server Authentication Clients: Authentication Client Modules Executing Server Environment

Scope: applies to `src/server/**`.

These rules are ALWAYS ACTIVE for server-side authentication client modules managing passkey, multi-factor, and passwordless authentication flows requiring request headers or server response constructs.

### Rules

- **R-AUTH-001** MUST: Authentication client modules executing in the server environment MUST delegate shared client state initialization to the centralized authentication client provider abstraction.

### Verify

```bash
# Discover the project dependency resolution artifact and verify framework runtime dependencies
# Execute the project test runner for server-side authentication test suites
# Execute the project static analysis and linting scripts to verify boundary constraints
```

**Accept when:**
- All server authentication client test suites pass when validating header resolution and authentication client lifecycle operations.
- Static analysis verifies that server authentication clients source header and server response primitives exclusively from the designated framework server modules.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>