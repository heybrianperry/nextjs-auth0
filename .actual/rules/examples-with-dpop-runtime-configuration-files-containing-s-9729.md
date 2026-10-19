---
version: 2
name: examples-with-dpop-runtime-configuration-files-containing-s-9729
description: "dotenv Environment Variable Configuration: Runtime Configuration Files Containing Sensitive Secrets"
metadata:
  actual:
    adr_id: 97295478-b95a-4f65-90c7-49e6e971d212
    status: accepted
    candidate_group_id: 32228038-5c64-4715-8c2b-ad6a35e9f91b
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# dotenv Environment Variable Configuration: Runtime Configuration Files Containing Sensitive Secrets

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for runtime environment configuration loading in server execution contexts and process environment property consumption in application client initializers and framework configurations.

### Rules

- **R-ENV-001** MUST_NOT: Runtime configuration files containing sensitive secrets or private credentials MUST_NOT be committed into source control repositories.

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