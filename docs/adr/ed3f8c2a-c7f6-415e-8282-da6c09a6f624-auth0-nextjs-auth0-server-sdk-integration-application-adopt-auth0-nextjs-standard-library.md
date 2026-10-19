---
version: 2
name: ed3f8c2a-c7f6-415e-8282-da6c09a6f624-auth0-nextjs-auth0-server-sdk-integration-application-adopt-auth0-nextjs-standard-library
description: "@auth0/nextjs-auth0 Server SDK Integration: Application Adopt Auth0 Nextjs Standard Library"
metadata:
  actual:
    adr_id: ed3f8c2a-c7f6-415e-8282-da6c09a6f624
    status: accepted
    candidate_group_id: 25736760-026b-4644-b875-f2e425f720b0
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-enterprise-connect/lib/**
      - examples/with-passwordless/app/server-passwordless/**
---

# @auth0/nextjs-auth0 Server SDK Integration: Application Adopt Auth0 Nextjs Standard Library

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `examples/with-enterprise-connect/lib/**`
- `examples/with-passwordless/app/server-passwordless/**`

## Context

- Server-rendered applications requiring enterprise single sign-on and passwordless authentication need consistent identity lifecycle management on the server tier.
- Client-side token exposure presents security risks, necessitating server-managed session state with cryptographic tamper protection.
- Disparate authentication callbacks require standardized error handling, identity claim extraction, and uniform cookie emission.

## Problem Statement

Without a standardized server-side authentication library and session persistence strategy, disparate endpoints implement inconsistent token validation, claim parsing, and cookie generation. This fragmentation introduces security vulnerabilities such as cookie forgery, improper claim verification, and fragmented error handling across authentication flows.

## Decision

1. MUST: The application MUST adopt @auth0/nextjs-auth0 as the standard library for server-side identity verification, session signing, and authentication error handling across server routes and callback workflows.

## Policy Block

- MUST The application MUST adopt @auth0/nextjs-auth0 as the standard library for server-side identity verification, session signing, and authentication error handling across server routes and callback workflows.

In scope:
- All server-side authentication handlers, callback routes, and session persistence logic within the application.
- Identity verification workflows including enterprise identity connections and passwordless authentication flows.

Out of scope:
- Purely client-side authentication mechanisms that do not route through server-side callback handlers.
- Static, unauthenticated public pages that do not interact with user identity or session state.

## Rationale

- Centralizing authentication through @auth0/nextjs-auth0 provides a cohesive server-side integration model with Auth0Client and dedicated error primitives.
- Cryptographic HMAC signing of session payloads ensures that session cookies cannot be tampered with or forged by clients.
- Synchronizing cookie expiration with the signed session expiration timestamp ensures clean session termination on both client and server.

## Consequences

Positive:
- Eliminates token exposure in the browser by managing authentication and session state entirely within server boundaries.
- Guarantees session integrity through server-side HMAC signing of session cookie payloads.
- Standardizes authentication failure handling and redirection across various authentication methods using dedicated error primitives.

Negative:
- Requires cryptographic operations on the server for each session issuance and validation cycle.
- Couples server route handlers to the custom session payload format and server runtime cryptographic key management.

## Alternatives

- Client-side token storage in local storage or unencrypted cookies (rejected)
  Rejected because: Exposes sensitive identity tokens and claims to cross-site scripting attacks and lacks cryptographic tamper protection.
  When valid: Static single-page applications without a backend or server runtime.
- Custom server-side session store with database-backed session identifiers (rejected)
  Rejected because: Introduces external database latency and stateful storage dependencies for stateless server route handlers.
  When valid: Systems requiring immediate centralized session revocation across multiple distributed server instances.

## Risks

- Compromise or improper rotation of the session signing secret could allow session forgery or invalidate active sessions.
  Mitigation: Manage the signing secret through secure environment secret management and implement key rotation mechanisms with fallback verification.
  Owner: engineering team
- Missing or malformed organization claims in enterprise tokens could cause unexpected authentication rejections.
  Mitigation: Enforce strict schema validation and structured error redirection within onCallback lifecycle handlers.
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
- Ensure that the cryptographic secret used for HMAC signing is loaded from protected environment configuration and is never committed to source control.
- Align session lifetime constants across cookie configuration and signed session expiration payload attributes.

## Continuation Context


Verify commands:
- sh -c 'echo "Discover and execute repository test suite for authentication flows via the project task runner"'
- sh -c 'echo "Discover and execute static analysis checks for session and authentication handlers"'

Accept when:
- Authentication callbacks successfully instantiate Auth0Client, validate identity claims, and emit HMAC-signed session cookies.
- Session cookies are transmitted with HTTP-only, secure, and lax SameSite attributes matching server session expiration timestamps.
- All authentication-related unit and integration tests pass successfully in the project verification environment.

## Enforcement

- Verified by: Automated continuous integration pipeline running static analysis and identity integration tests.
- Verified by: Peer code review verifying compliance with session signing and error handling rules.
- Violation handling: Pull requests lacking required session HMAC signing or claim validation will be blocked from merging.
- Violation handling: Security reviews will flag any unencrypted or client-accessible session tokens.
- Exception process: Exceptions require documented security architecture review and formal approval from the identity security lead.