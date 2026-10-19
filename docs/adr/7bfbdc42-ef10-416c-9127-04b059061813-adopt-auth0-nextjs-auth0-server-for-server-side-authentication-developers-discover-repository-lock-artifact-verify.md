---
version: 2
name: 7bfbdc42-ef10-416c-9127-04b059061813-adopt-auth0-nextjs-auth0-server-for-server-side-authentication-developers-discover-repository-lock-artifact-verify
description: "Adopt @auth0/nextjs-auth0/server for Server-Side Authentication: Developers Discover Repository Lock Artifact Verify"
metadata:
  actual:
    adr_id: 7bfbdc42-ef10-416c-9127-04b059061813
    status: accepted
    candidate_group_id: d7b8f89c-0b8b-4612-abbe-bf2681edc5b8
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-cte/app/api/stt/**
      - examples/with-dpop/lib/**
      - examples/with-mrrt/lib/**
---

# Adopt @auth0/nextjs-auth0/server for Server-Side Authentication: Developers Discover Repository Lock Artifact Verify

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `examples/with-cte/app/api/stt/**`
- `examples/with-dpop/lib/**`
- `examples/with-mrrt/lib/**`

## Context

- Server-side endpoints and route handlers require consistent identity verification and token handling.
- Multiple server components across the codebase instantiate Auth0Client with explicit authorization parameters such as audience and scope.
- Centralized server client initialization isolates environment-driven runtime configuration from route business logic.

## Problem Statement

Server-side endpoints risk inconsistent authentication handling, drifted authorization parameters, and insecure token management when route handlers implement bespoke identity verification logic.

## Decision

1. MUST: Developers MUST discover the repository lock artifact and verify the exact resolved version of @auth0/nextjs-auth0/server against official documentation before calling its APIs.

## Policy Block

- MUST Developers MUST discover the repository lock artifact and verify the exact resolved version of @auth0/nextjs-auth0/server against official documentation before calling its APIs.

In scope:
- All server-side route handlers, API endpoints, and server modules requiring user authentication or authorization verification.
- Server-side client initialization configuring identity provider authorization parameters.

Out of scope:
- Client-side single-page UI components operating strictly in browser contexts without direct server token management.
- Public static assets and unauthenticated health check endpoints.

## Rationale

- Adopting @auth0/nextjs-auth0/server provides a structured, tested integration surface for server-side OpenID Connect and OAuth2 flows.
- Centralizing Auth0Client construction ensures uniform application of authorization parameters, audience validation, and security configurations across all server routes.
- Observed codebase implementations consistently leverage @auth0/nextjs-auth0/server across multiple server modules to manage authentication boundaries.

## Consequences

Positive:
- Standardizes identity provider interaction and authorization parameter management across server entry points.
- Centralizes audience, scope, and cryptographic verification settings within shared server utility modules.
- Prevents fragmented authentication configurations and duplicated token lifecycle handling across route handlers.

Negative:
- Couples server-side authentication architecture directly to the vendor SDK interface and updates.
- Requires consistent synchronization of audience and scope configurations across disparate deployment environments.
- Server routes depend on shared module instantiation patterns rather than purely decoupled protocols.

## Alternatives

- Custom OAuth2 and OpenID Connect manual implementation (rejected)
  Rejected because: Increases maintenance overhead, introduces token parsing risks, and duplicates protocol compliance logic across endpoints.
  When valid: When running in a minimal runtime environment where third-party authentication client libraries cannot be resolved.
- Generic stateless token middleware without centralized client instances (rejected)
  Rejected because: Fails to provide unified authorization parameter configuration and protocol-specific session handling across server routes.
  When valid: When services operate strictly as downstream resource servers verifying pre-validated bearer tokens without user authentication flows.

## Risks

- Breaking changes in SDK minor or major updates may disrupt server route authentication.
  Mitigation: Strictly adhere to the lock-version grounding process to verify method signatures and breaking changes across updates.
  Owner: engineering team
- Misconfigured audience or scope parameters could lead to unauthorized access or token rejection.
  Mitigation: Implement fail-fast runtime configuration validation before client initialization.
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
- Centralize Auth0Client instantiation in a dedicated server module and export configured client instances for route consumption.
- Source authorization parameters such as audience and scope dynamically from validated runtime environment sources.

## Continuation Context


Verify commands:
- Discover the project dependency manifests and verify the presence of the authentication library in declared dependencies.
- Discover and execute the repository test suite to confirm server authentication integration passes.
- Discover and run the project static analysis checks to verify client instantiation and route handling compliance.

Accept when:
- All server-side authentication modules instantiate Auth0Client using centralized configuration parameters.
- Repository lock resolution confirms exact dependency versions prior to execution.
- Server route handlers validate authorization context via the centralized client without inline authentication logic.

## Enforcement

- Verified by: Automated static analysis checks enforcing imported client module boundaries.
- Verified by: Continuous integration test suites verifying authentication flows on server routes.
- Verified by: Peer code review inspecting route handler authentication dependencies.
- Violation handling: Pull requests introducing ad-hoc authentication logic or unapproved client configurations are blocked.
- Violation handling: Static analysis violations generate automated build failures requiring immediate remediation.
- Exception process: Submit an architectural review request detailing technical constraints preventing standard client usage.
- Exception process: Demonstrate equivalent token verification and session protection mechanisms.
- Exception process: Obtain explicit sign-off from the security and architecture teams before deployment.