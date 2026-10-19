---
version: 2
name: cross-cutting-back-channel-logout-handlers-cryptograph-787d
description: "Back-Channel Logout Architecture across Auth0-Session and Next.js Handlers: Back Channel Logout Handlers Cryptographically Verify"
metadata:
  actual:
    adr_id: 787d01e6-47b4-4199-9fee-eee51511d4ad
    status: accepted
    candidate_group_id: 67c2a90c-6ca5-4d2e-8dcd-aa6e8be75376
  scope:
    root: .
    paths:
      - src/**/*
      - tests/**/*
---

# Back-Channel Logout Architecture across Auth0-Session and Next.js Handlers: Back Channel Logout Handlers Cryptographically Verify

Scope: applies to `src/**/*`, `tests/**/*`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-BCL-001** MUST: Back-channel logout handlers MUST cryptographically verify incoming logout tokens using asymmetric verification via LogoutTokenVerifier prior to invalidating sessions.

### Verify

```bash
npm test -- tests/handlers/backchannel-logout.test.ts tests/handlers/backchannel-logout-page-router.test.ts tests/auth0-session/handlers/backchannel-logout.test.ts tests/auth0-session/utils/logout-token-verifier.test.ts
npm run lint
npm run typecheck
```

**Accept when:**
- Incoming back-channel logout requests with valid tokens return HTTP 200 with 'no-store' headers.
- Tokens with invalid signatures or payloads are rejected with appropriate error statuses.
- Session cache correctly marks sessions as logged out and rejects subsequent session retrieval via isLoggedOut check.

<enforcement>
Claude Code MUST NOT skip or defer verification. All back-channel logout requests must undergo cryptographic validation, set appropriate cache headers, and integrate with the session cache invalidation checks.
</enforcement>