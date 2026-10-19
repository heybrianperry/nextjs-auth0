---
version: 2
name: examples-with-dpop-token-validation-middleware-fall-back-ebf0
description: "oauth4webapi for Demonstrating Proof-of-Possession Token Binding: Token Validation Middleware Fall Back Authorization"
metadata:
  actual:
    adr_id: ebf0843a-25bb-4c81-b17a-bd0ea909e58a
    status: accepted
    candidate_group_id: c1c1a0d0-6255-4ae6-aff0-e4c2f82dfbcc
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# oauth4webapi for Demonstrating Proof-of-Possession Token Binding: Token Validation Middleware Fall Back Authorization

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-DPOP-001** MAY: Token validation middleware MAY fall back to authorization server metadata discovery when preconfigured discovery endpoints are unreachable, logging warning diagnostics during fallback execution.

### Verify

```bash
# Discover and run the project test suite verifying proof-of-possession token validation
# Discover and run repository static analysis for secrets handling and token binding compliance
```

**Accept when:**
- Token validation test suite successfully confirms valid DPoP proof tokens and confirmation claims
- Requests with invalid, expired, or missing proof signatures are rejected with appropriate error diagnostics
- No unauthorized token fallback or bypassed confirmation checks are detected during automated verification

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>