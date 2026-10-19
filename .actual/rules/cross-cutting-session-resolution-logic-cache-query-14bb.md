---
version: 2
name: cross-cutting-session-resolution-logic-cache-query-14bb
description: "Back-Channel Logout Architecture across Auth0-Session and Next.js Handlers: Session Resolution Logic Cache Query Isloggedout"
metadata:
  actual:
    adr_id: 14bb472f-d882-4e6c-bbef-7c3abcd26139
    status: accepted
    candidate_group_id: 67c2a90c-6ca5-4d2e-8dcd-aa6e8be75376
  scope:
    root: .
    paths:
      - src/**/*
      - tests/**/*
---

# Back-Channel Logout Architecture across Auth0-Session and Next.js Handlers: Session Resolution Logic Cache Query Isloggedout

Scope: applies to `src/**/*`, `tests/**/*`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-BLL-001** MUST: Session resolution logic in the session cache MUST query the isLoggedOut check to reject requests matching terminated sessions.

### Verify

```bash
npm test tests/handlers/backchannel-logout.test.ts tests/handlers/backchannel-logout-page-router.test.ts tests/auth0-session/handlers/backchannel-logout.test.ts tests/auth0-session/utils/logout-token-verifier.test.ts
npm run lint
npm run typecheck
```

**Accept when:**
- Incoming back-channel logout requests with valid tokens return HTTP 200 with 'no-store' headers.
- Tokens with invalid signatures or payloads are rejected with appropriate error statuses.
- Session cache correctly marks sessions as logged out and rejects subsequent session retrieval via isLoggedOut check.

<enforcement>
Claude Code MUST NOT skip or defer verification. All pull requests touching back-channel logout handlers or session cache logic must pass automated unit, integration, and cryptographic verification checks.
</enforcement>