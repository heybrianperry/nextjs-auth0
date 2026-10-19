---
version: 2
name: examples-with-dpop-application-business-logic-client-initia-33c5
description: "dotenv Environment Variable Configuration: Application Business Logic Client Initialization Routines"
metadata:
  actual:
    adr_id: 33c5dcf0-e280-46cf-a596-1d4c7abfbf3f
    status: accepted
    candidate_group_id: 32228038-5c64-4715-8c2b-ad6a35e9f91b
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# dotenv Environment Variable Configuration: Application Business Logic Client Initialization Routines

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for runtime environment configuration loading in server execution contexts and process environment property consumption in application client initializers and framework configurations.

### Rules

- **R-DOTENV-001** MUST_NOT: Application business logic and client initialization routines MUST_NOT access raw process environment variables directly across dispersed application layers without central configuration export.

### Verify

```bash
# Discover and run the repository test suite to verify that service components initialize correctly with expected configuration parameters.
# Discover and execute the repository configuration validation script to verify that required environment variables are parsed without errors.
```

**Accept when:**
- All configuration schema validations pass successfully with valid environment variables provided.
- Application bootstrap aborts with a descriptive error when any mandatory environment variable is absent.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated static analysis checks in CI pipelines and pull request code reviews.
</enforcement>