---
version: 2
name: server-server-side-authentication-client-operat-d1e4
description: "Next.js Server Primitives Adoption for Server Authentication Clients: Server Side Authentication Client Operations Requiring"
metadata:
  actual:
    adr_id: d1e41ed7-3b79-4722-b1a2-b37ec6f65860
    status: accepted
    candidate_group_id: a345d086-5676-4977-87a4-8e8543fe1515
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/server/**
---

# Next.js Server Primitives Adoption for Server Authentication Clients: Server Side Authentication Client Operations Requiring

Scope: applies to `src/server/**`.

These rules are ALWAYS ACTIVE for server-side authentication client modules managing passkey, multi-factor, and passwordless authentication flows, and server-side adapters requiring request headers or server response constructs.

### Rules

- **R-AUTH-001** MUST: Server-side authentication client operations requiring incoming request context MUST obtain headers and server response constructs exclusively through Next.js server module primitives via dedicated server client adapters.

### Verify

```bash
# Discover the project dependency resolution artifact and verify that framework runtime dependencies resolve cleanly
# Execute the project test runner for server-side authentication test suites
# Execute the project static analysis and linting scripts to verify boundary constraints across server modules
```

**Accept when:**
- All server authentication client test suites pass when validating header resolution and authentication client lifecycle operations.
- Static analysis verifies that server authentication clients source header and server response primitives exclusively from the designated framework server modules.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated CI test validation and static analysis checks must be enforced during code review.
</enforcement>