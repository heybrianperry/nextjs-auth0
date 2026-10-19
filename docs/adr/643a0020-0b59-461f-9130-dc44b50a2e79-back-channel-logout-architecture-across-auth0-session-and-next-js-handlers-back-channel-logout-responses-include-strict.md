---
version: 2
name: 643a0020-0b59-461f-9130-dc44b50a2e79-back-channel-logout-architecture-across-auth0-session-and-next-js-handlers-back-channel-logout-responses-include-strict
description: "Back-Channel Logout Architecture across Auth0-Session and Next.js Handlers: Back Channel Logout Responses Include Strict"
metadata:
  actual:
    adr_id: 643a0020-0b59-461f-9130-dc44b50a2e79
    status: accepted
    candidate_group_id: 67c2a90c-6ca5-4d2e-8dcd-aa6e8be75376
  scope:
    root: .
    paths:
      - src/**/*
      - tests/**/*
---

# Back-Channel Logout Architecture across Auth0-Session and Next.js Handlers: Back Channel Logout Responses Include Strict

Status: proposed
Date: 2026-10-02
Deciders: AI (signal conversion)

## Scope Paths

Applies to:
- `src/**/*`
- `tests/**/*`

## Context

- OpenID Connect session management historically relied on front-channel logout flows where the Identity Provider (IdP) redirects the user's browser to an application endpoint to clear local cookies and session state. However, front-channel logout fails when the user closes their browser, experiences network interruptions during redirection, or when an administrative logout is initiated directly at the IdP without user interaction.
- To support robust out-of-band session termination, the application boundary needs to support OpenID Connect Back-Channel Logout across both Next.js App Router and Pages Router paradigms. This requires handling incoming server-to-server HTTP requests from the IdP, cryptographically verifying logout tokens, setting appropriate cache headers, and coordinating session invalidation within the server-side session cache.

## Problem Statement

How should incoming Identity Provider back-channel logout requests be validated, processed, and coordinated across Next.js routing layers to guarantee server-side session invalidation without client browser involvement?

## Decision

1. MUST: Back-channel logout responses MUST include strict 'no-store' cache-control headers across both App Router and Pages Router implementations.

## Policy Block

- MUST Back-channel logout responses MUST include strict 'no-store' cache-control headers across both App Router and Pages Router implementations.

In scope:
- src/handlers/backchannel-logout.ts
- src/auth0-session/handlers/backchannel-logout.ts
- src/auth0-session/utils/logout-token-verifier.ts
- src/session/cache.ts
- Next.js App Router and Pages Router authentication route handlers

Out of scope:
- Client-side user-initiated browser navigation and front-channel redirects

## Rationale

- Asymmetric verification through LogoutTokenVerifier ensures that session invalidation cannot be triggered by unauthenticated or forged third-party requests.
- Applying strict 'no-store' cache headers prevents edge nodes, CDN proxies, or intermediary HTTP caches from caching back-channel logout responses or leaking logout state.
- Invalidating the server-side session store prior to sending an HTTP 200 acknowledgment ensures consistency between IdP expectations and local application state.
- Integrating the isLoggedOut check directly into session cache resolution prevents race conditions and ensures immediate revocation of credentials across subsequent incoming requests.

## Consequences

Positive:
- Sessions can be terminated immediately and securely out-of-band by the Identity Provider without requiring user browser interaction.
- Unified support across Next.js App Router and Pages Router architectures.
- Cryptographic assurance that session revocation requests originate from the trusted IdP.

Negative:
- Requires maintaining and querying an invalidated session marker store (isLoggedOut checks) across distributed instances.
- Adds cryptographic computation overhead to verify JWT logout tokens on incoming logout calls.

## Alternatives

- Front-channel browser-redirect logout only (rejected)
  Rejected because: Relies entirely on active end-user browser navigation, failing to terminate sessions when the browser is closed or when IdP administrative revocation occurs out-of-band.
- Synchronous peer-to-peer instance notification without shared session cache (rejected)
  Rejected because: Requires peer discovery and direct mesh networking between server instances, which is unsupported in serverless and edge deployment environments.

## Risks

- Invalidated session markers in distributed server instances may consume unbounded memory if retention policies are undefined.
  Mitigation: Establish TTL-based expiration for logout markers corresponding to the maximum session lifetime.
  Owner: Application Architecture Team
- IdP key rotation could cause LogoutTokenVerifier to fail valid logout requests if public keys are not dynamically fetched.
  Mitigation: Implement JWKS key caching and dynamic refresh within LogoutTokenVerifier.
  Owner: Identity Integration Team

## Implementation Notes

- Core logout handling logic is abstracted in src/auth0-session/handlers/backchannel-logout.ts and adapted for Next.js in src/handlers/backchannel-logout.ts.
- Session invalidation state is maintained within src/session/cache.ts and checked on subsequent user requests.
- Handlers support both Pages Router and App Router route conventions while ensuring Auth0NextResponse sets no-store cache headers.

## Continuation Context


Verify commands:
- Discover and execute test suite for back-channel logout handlers and token verification
- Discover and execute linting and type checks for session cache and route handlers

Accept when:
- Incoming back-channel logout requests with valid tokens return HTTP 200 with 'no-store' headers.
- Tokens with invalid signatures or payloads are rejected with appropriate error statuses.
- Session cache correctly marks sessions as logged out and rejects subsequent session retrieval via isLoggedOut check.

## Enforcement

- Verified by: Automated unit and integration test suites covering Pages Router and App Router back-channel logout handlers.
- Verified by: Cryptographic test coverage for LogoutTokenVerifier token parsing and signature validation.
- Verified by: Automated HTTP header assertions verifying 'no-store' responses.
- Violation handling: Pull requests lacking token verification or cache-control headers will fail CI checks and be blocked from merging.
- Violation handling: Unverified route implementations must be remediated to implement handleBackchannelLogout.
- Exception process: Architecture review approval is required for environments operating without server-side session stores, requiring a formal exception record.

## References

- file:src/auth0-session/handlers/backchannel-logout.ts
- file:src/auth0-session/utils/logout-token-verifier.ts
- file:src/handlers/backchannel-logout.ts
- file:src/handlers/auth.ts
- file:src/session/cache.ts
- file:src/init.ts
- file:src/shared.ts
- file:src/http/auth0-next-response.ts
- tests/handlers/backchannel-logout.test.ts
- tests/handlers/backchannel-logout-page-router.test.ts
- tests/auth0-session/handlers/backchannel-logout.test.ts
- tests/auth0-session/utils/logout-token-verifier.test.ts
- commit:52f2675da49a7a55ab5e86987762bb665654d26a
- commit:65c622b7ff75b17d63e6c6409e0aef5be1fc67e2
- commit:821a33d2e4b30273a0da1bc0e3d2b23db0dd93fc
- commit:8789b9a7bede33694746fc1d4f02b2e694c4df8a
- commit:e4402bb49ef89693ab5803b385d0c8e74658487f
- commit:8b2ff7e9f33206b99c878658b4cf9319fdf3eb85