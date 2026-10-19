---
version: 2
name: cross-cutting-session-stores-transaction-managers-appl-d9da
description: "jose Adoption for Cryptographic Operations and Token Management: Session Stores Transaction Managers Apply Payload"
metadata:
  actual:
    adr_id: d9da367b-1fa2-47fe-bfeb-557947ac34bb
    status: accepted
    candidate_group_id: b93acc58-b784-4e2f-ad35-c3ca460b1a5e
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/server/**
      - src/types/**
      - src/utils/**
---

# jose Adoption for Cryptographic Operations and Token Management: Session Stores Transaction Managers Apply Payload

Scope: applies to `src/server/**`, `src/types/**`, `src/utils/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-JOSE-001** SHOULD: Session stores and transaction managers SHOULD apply payload clamping and size validation to ensure encrypted token outputs conform to transport constraints.

### Verify

```bash
echo "Discover and execute project test suite for cryptographic and session verification"
echo "Discover and execute project linter and dependency checks for unauthorized cryptographic libraries"
```

**Accept when:**
- All cryptographic signing, encryption, decryption, and verification operations compile and pass automated test suites using the standardized token library.
- No unapproved third-party or platform-specific cryptographic token libraries are referenced in session or authentication workflows.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>