---
version: 2
name: examples-with-dpop-environment-variable-inputs-validated-ag-c2f8
description: "dotenv Environment Variable Configuration: Environment Variable Inputs Validated Against Typed"
metadata:
  actual:
    adr_id: c2f8e8ad-ba6a-4d22-97e3-62b6c099c8f4
    status: accepted
    candidate_group_id: 32228038-5c64-4715-8c2b-ad6a35e9f91b
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# dotenv Environment Variable Configuration: Environment Variable Inputs Validated Against Typed

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for runtime environment configuration loading in server execution contexts and process environment property consumption in application client initializers and framework configurations.

### Rules

- **R-DOTENV-001** SHOULD: All environment variable inputs be validated against a typed configuration schema at startup, terminating execution immediately if mandatory variables are missing or malformed.

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