---
version: 2
name: 6d5e0ae8-a9f4-4312-8051-b5f6d8c77804-adoption-of-auth0-nextjs-auth0-for-client-and-server-authentication-client-rendered-components-requiring-reactive-authentication
description: "Adoption of @auth0/nextjs-auth0 for Client and Server Authentication: Client Rendered Components Requiring Reactive Authentication"
metadata:
  actual:
    adr_id: 6d5e0ae8-a9f4-4312-8051-b5f6d8c77804
    status: accepted
    candidate_group_id: 09fc163c-af7c-4dcc-877f-a2c758c104bd
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - e2e/test-app/app/app-router/client/**
      - examples/with-dpop/lib/**
---

# Adoption of @auth0/nextjs-auth0 for Client and Server Authentication: Client Rendered Components Requiring Reactive Authentication

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `e2e/test-app/app/app-router/client/**`
- `examples/with-dpop/lib/**`

## Context

- The application requires user identity authentication and authorization across both server execution contexts and client-rendered user interfaces.
- Server-side components require structured configuration for authorization scopes and audiences while managing token exchange.
- Client components require access to reactive user identity session context without exposing sensitive authentication secrets.

## Problem Statement

Coordinating identity verification and session access across separate server and client runtime boundaries introduces risks of fragmented token storage, inconsistent configuration parameters, and improper exposure of security secrets to browser environments.

## Decision

1. MUST: Client-rendered components requiring reactive authentication context MUST obtain user identity via the useUser hook.

## Policy Block

- MUST Client-rendered components requiring reactive authentication context MUST obtain user identity via the useUser hook.

In scope:
- Full-stack application routes and components requiring user identity, session access, or authentication tokens.
- Server-side identity client initializations and client-rendered authentication state subscribers.

Out of scope:
- Stateless public assets and unauthenticated endpoints that do not query identity status.
- Third-party microservices utilizing distinct independent authorization protocols.

## Rationale

- Adopting @auth0/nextjs-auth0 establishes unified authentication abstractions spanning server execution and client hydration boundaries.
- Encapsulating credential coordination and authorization parameters within Auth0Client on the server protects sensitive runtime configurations.
- Exposing identity state through the useUser hook on the client eliminates duplicate token retrieval logic across user interface components.

## Consequences

Positive:
- Centralized authentication client configuration reduces divergence across server identity operations.
- Component-level session consumption via useUser provides reactive rendering based on identity state.
- Server-side token exchange isolates cryptographic parameters from client distribution.

Negative:
- Couples client and server application code to the @auth0/nextjs-auth0 SDK interface.
- Requires careful environment variable management across both runtime contexts to avoid configuration mismatches.

## Alternatives

- Custom OAuth token management and manual session cookie orchestration (rejected)
  Rejected because: Increases maintenance overhead, introduces security risks around manual token exchange, and duplicates session state tracking.
  When valid: When operating in an environment unable to run Node.js runtime abstractions or when integrating non-standard identity providers.
- Client-only authentication relying exclusively on browser-based SDK redirects (rejected)
  Rejected because: Exposes authentication negotiation details to the browser and prevents secure server-side session pre-rendering.
  When valid: When building purely static client applications without a dedicated backend server layer.

## Risks

- Misconfiguration of authorization parameters or environment variables leading to authentication failures or token leakage
  Mitigation: Enforce strict schema validation on runtime environment variables at application startup.
  Owner: engineering team
- Drift between server session state and client useUser hook state across route transitions
  Mitigation: Standardize session refresh handlers and handle session loading and error states consistently within client components.
  Owner: engineering team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Configure server-side Auth0Client within an isolated server-only module to prevent accidental bundling into client artifacts.
- Wrap client components requiring access to the useUser hook with the appropriate identity context provider higher in the component hierarchy.

## Continuation Context


Verify commands:
- Discover the repository test execution script and run the automated test suite covering authentication routes and components.
- Discover the repository static analysis script and execute linting and type checking across client and server source files.

Accept when:
- Server-side authentication client initializes successfully using resolved environment variables and passes integration tests.
- Client components render user profile information from the useUser hook without runtime exceptions or type errors.

## Enforcement

- Verified by: Automated continuous integration checks executing repository test suites and type verification.
- Verified by: Peer code reviews auditing imports of @auth0/nextjs-auth0 across server and client boundaries.
- Violation handling: Pull requests containing direct client-side cryptographic handling or custom session token implementations will be blocked.
- Exception process: Exceptions must be submitted via an architecture review request detailing alternative security mitigations and approved by the lead architect.