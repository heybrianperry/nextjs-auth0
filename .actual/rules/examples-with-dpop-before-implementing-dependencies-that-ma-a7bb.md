---
version: 2
name: examples-with-dpop-before-implementing-dependencies-that-ma-a7bb
description: "dotenv Environment Variable Configuration: Before Implementing Dependencies That Manage Runtime"
metadata:
  actual:
    adr_id: a7bb9537-7d6d-4c00-af2f-21391e0a6a8b
    status: accepted
    candidate_group_id: 32228038-5c64-4715-8c2b-ad6a35e9f91b
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# dotenv Environment Variable Configuration: Before Implementing Dependencies That Manage Runtime

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for runtime environment configuration loading and process environment property consumption in application client initializers and framework configurations.

### Rules

- **R-ENV-001** MUST: Before implementing dependencies that manage runtime environment configuration, developers MUST inspect the repository lock artifact to verify the exact resolved version against public API documentation.

### Verify

```bash
# Discover and run the repository test suite to verify that service components initialize correctly with expected configuration parameters.
# Discover and execute the repository configuration validation script to verify that required environment variables are parsed without errors.
```

**Accept when:**
- All configuration schema validations pass successfully with valid environment variables provided.
- Application bootstrap aborts with a descriptive error when any mandatory environment variable is absent.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>