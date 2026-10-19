---
version: 2
name: d12caddb-9d2f-4c25-88a9-c0649917879f-adoption-of-auth0-nextjs-auth0-types-for-shared-authentication-type-contracts-consumers-discover-ecosystem-lock-artifact-resolve
description: "Adoption of @auth0/nextjs-auth0/types for Shared Authentication Type Contracts: Consumers Discover Ecosystem Lock Artifact Resolve"
metadata:
  actual:
    adr_id: d12caddb-9d2f-4c25-88a9-c0649917879f
    status: accepted
    candidate_group_id: 38f5d321-324d-4414-965e-59757a28e09c
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - e2e/test-app/pages/api/pages-router/get-session/**
      - examples/with-cte/app/api/cte/**
      - examples/with-passkeys/**
      - examples/with-passwordless-db/components/**
---

# Adoption of @auth0/nextjs-auth0/types for Shared Authentication Type Contracts: Consumers Discover Ecosystem Lock Artifact Resolve

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `e2e/test-app/pages/api/pages-router/get-session/**`
- `examples/with-cte/app/api/cte/**`
- `examples/with-passkeys/**`
- `examples/with-passwordless-db/components/**`

## Context

- The codebase implements authentication workflows across both client-side components and server-side execution boundaries, including server actions, route handlers, and API endpoints.
- Identity data structures such as session payloads, credential challenge options, and authenticator states must remain type-safe across these disparate execution contexts.
- Direct dependency on runtime SDK entry points in client-rendered components risks leaking server-only runtime logic into browser bundles or creating circular dependencies.
- Static analysis identifies consistent, cross-module imports of typing definitions specifically from the @auth0/nextjs-auth0/types export.

## Problem Statement

Handling authentication workflows across heterogeneous execution environments without a unified type contract leads to interface fragmentation, duplicate type declarations, and runtime type drift between client components, server actions, and API handlers. A dedicated, lightweight type import mechanism is required to guarantee end-to-end type safety without importing runtime authentication dependencies into client bundles.

## Decision

1. MUST: Consumers MUST discover the ecosystem lock artifact and resolve the exact locked version of the identity library before implementing or altering type references.

## Policy Block

- MUST Consumers MUST discover the ecosystem lock artifact and resolve the exact locked version of the identity library before implementing or altering type references.

In scope:
- Modules handling authentication requests, session retrieval, passkey challenges, or identity data structures across client and server boundaries.

Out of scope:
- Internal application modules and domain entities unrelated to identity provider authentication, session management, or authorization verification.

## Rationale

- Consuming shared type definitions from @auth0/nextjs-auth0/types establishes a single source of truth for identity constructs across client components, route handlers, and server actions as evidenced across multiple implementation modules.
- Separating type imports from runtime SDK modules ensures that client-rendered code remains decoupled from server execution primitives while preserving full type checking.
- Standardizing on the upstream type package avoids drift between provider identity protocols and internal application handling logic.

## Consequences

Positive:
- Enforces consistent data shapes for sessions, credential options, and authentication challenges across client and server tiers.
- Eliminates redundant local type definitions and reduces maintenance overhead when identity schemas evolve.
- Prevents accidental inclusion of server runtime modules into client-side bundles through dedicated type-only imports.

Negative:
- Couples internal authentication interfaces and contracts to upstream changes in the identity library type definitions.
- Requires ongoing vigilance to ensure third-party type definitions match the operational runtime behavior across distinct framework routers.

## Alternatives

- Authoring internal bespoke TypeScript interfaces for all authentication payloads and session objects (rejected)
  Rejected because: Creating custom local type definitions introduces manual maintenance overhead and increases the risk of subtle contract divergence from the upstream identity provider.
  When valid: When abstracting multiple interchangeable identity providers behind a provider-agnostic domain layer.
- Importing types directly from the primary runtime entry point of the identity library (rejected)
  Rejected because: Primary runtime imports can cause bundling complications when referenced within client-rendered components and blur module boundary separation.
  When valid: When executing strictly within a unified server-only runtime without client-side type sharing requirements.

## Risks

- Upstream updates to library type definitions may introduce breaking signature changes during dependency updates.
  Mitigation: Lock version dependencies strictly and inspect upstream release notes and type contracts prior to upgrading.
  Owner: engineering team
- Inadvertent consumption of runtime exports alongside type contracts in client-side code.
  Mitigation: Enforce strict linter rules and static import analysis to ensure only type-only imports are drawn from shared identity modules in browser-targeted code.
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
- Use explicit type-only import syntax when referencing contracts from the identity types module to guarantee full removal during compilation.
- Maintain clear boundary separation by defining application-specific server actions or API responses that compose upstream identity contracts rather than mutating upstream types directly.

## Continuation Context


Verify commands:
- Discover and run the project type checker script defined in the dependency manifest to verify that all authentication type references resolve cleanly.
- Discover and execute the repository static analysis and linting scripts to verify that identity type imports comply with module boundary rules.

Accept when:
- All imports from @auth0/nextjs-auth0/types pass static type validation without errors across client and server boundaries.
- No circular dependencies or leaked server-side runtime code are detected in client bundles during verification builds.

## Enforcement

- Verified by: Automated continuous integration pipeline executing repository verification and type validation scripts.
- Verified by: Peer code review auditing authentication contract usage and import paths.
- Violation handling: Pull requests containing untyped authentication structures or local duplicate type definitions must fail build checks and be revised.
- Exception process: Exceptions for proprietary authentication adapters require approval from the lead architect and must be documented with an architectural note.