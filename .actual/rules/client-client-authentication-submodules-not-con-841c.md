---
version: 2
name: client-client-authentication-submodules-not-con-841c
description: "Adoption of Shared Internal Errors Module for Client Authentication Submodules: Client Authentication Submodules Not Construct Hoc"
metadata:
  actual:
    adr_id: 841ce077-108e-4a2a-82ed-31c1d2d16ef1
    status: accepted
    candidate_group_id: 62626e87-6d3f-40ac-af82-3a586d2993b7
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/client/**
---

# Adoption of Shared Internal Errors Module for Client Authentication Submodules: Client Authentication Submodules Not Construct Hoc

Scope: applies to `src/client/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-AUTH-001** MUST_NOT: Client authentication submodules MUST NOT construct ad-hoc error literals or leak raw unhandled exceptions from external network calls or platform authenticator operations.

### Verify

```bash
# Discover and execute project test script from dependency manifest
# Discover and execute project static analysis and linting scripts
# Discover and execute project type checking script
```

**Accept when:**
- All client authentication test suites execute and pass, confirming proper wrapping and propagation of internal errors.
- Static analysis and type checking complete with zero errors and no boundary violations.
- All thrown errors across client authentication submodules inherit from standard internal error abstractions.

<enforcement>
Claude Code MUST NOT skip or defer verification. All client authentication routines must normalize errors using the shared internal errors module.
</enforcement>