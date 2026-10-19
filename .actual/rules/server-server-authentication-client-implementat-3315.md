---
version: 2
name: server-server-authentication-client-implementat-3315
description: "Next.js Server Primitives Adoption for Server Authentication Clients: Server Authentication Client Implementations Not Access"
metadata:
  actual:
    adr_id: 3315bf17-c128-4e00-98c8-1986c1f8dd0a
    status: accepted
    candidate_group_id: a345d086-5676-4977-87a4-8e8543fe1515
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/server/**
---

# Next.js Server Primitives Adoption for Server Authentication Clients: Server Authentication Client Implementations Not Access

Scope: applies to `src/server/**`.

These rules are ALWAYS ACTIVE for server-side authentication client modules managing passkey, multi-factor, and passwordless authentication flows, and server-side adapters requiring request headers or server response constructs.

### Rules

- **R-AUTH-001** MUST_NOT: Server authentication client implementations MUST NOT access request headers through ambient unmanaged globals or bypass framework server runtime APIs.

### Verify

```bash
# Discover the project dependency resolution artifact and verify framework runtime dependencies
# Discover and execute the project test runner for server-side authentication test suites
# Discover and execute the project static analysis and linting scripts to verify boundary constraints
```

**Accept when:**
- All server authentication client test suites pass when validating header resolution and authentication client lifecycle operations.
- Static analysis verifies that server authentication clients source header and server response primitives exclusively from the designated framework server modules.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated CI test validation, static analysis, and architectural boundary checks during code review are mandatory enforcement mechanisms.
</enforcement>