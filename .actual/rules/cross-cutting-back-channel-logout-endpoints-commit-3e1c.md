---
version: 2
name: cross-cutting-back-channel-logout-endpoints-commit-3e1c
description: "Back-Channel Logout Architecture across Auth0-Session and Next.js Handlers: Back Channel Logout Endpoints Commit Session"
metadata:
  actual:
    adr_id: 3e1cdf84-44e1-40a8-aaaa-13275c8916ee
    status: accepted
    candidate_group_id: 67c2a90c-6ca5-4d2e-8dcd-aa6e8be75376
  scope:
    root: .
    paths:
      - src/**/*
      - tests/**/*
---

# Back-Channel Logout Architecture across Auth0-Session and Next.js Handlers: Back Channel Logout Endpoints Commit Session

Scope: applies to `src/**/*`, `tests/**/*`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-BCL-001** MUST: Back-channel logout endpoints MUST commit session invalidation in the server-side session cache before returning an HTTP 200 response.

### Verify

```bash
# Discover and execute test suite for back-channel logout handlers and token verification
npm test -- tests/handlers/backchannel-logout.test.ts tests/handlers/backchannel-logout-page-router.test.ts tests/auth0-session/handlers/backchannel-logout.test.ts tests/auth0-session/utils/logout-token-verifier.test.ts

# Discover and execute linting and type checks for session cache and route handlers
npm run lint && npx tsc --noEmit
```

**Accept when:**
- Incoming back-channel logout requests with valid tokens return HTTP 200 with 'no-store' headers.
- Tokens with invalid signatures or payloads are rejected with appropriate error statuses.
- Session cache correctly marks sessions as logged out and rejects subsequent session retrieval via isLoggedOut check.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>