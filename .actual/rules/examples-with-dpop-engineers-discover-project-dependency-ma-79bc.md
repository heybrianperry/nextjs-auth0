---
version: 2
name: examples-with-dpop-engineers-discover-project-dependency-ma-79bc
description: "oauth4webapi for Demonstrating Proof-of-Possession Token Binding: Engineers Discover Project Dependency Manifest Resolve"
metadata:
  actual:
    adr_id: 79bc1570-fdea-4454-b738-7a1e877f78d2
    status: accepted
    candidate_group_id: c1c1a0d0-6255-4ae6-aff0-e4c2f82dfbcc
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# oauth4webapi for Demonstrating Proof-of-Possession Token Binding: Engineers Discover Project Dependency Manifest Resolve

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-OP-001** MUST: Engineers MUST discover the project dependency manifest and resolve the authoritative lock artifact to verify the exact resolved version of oauth4webapi before implementing token validation routines.

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