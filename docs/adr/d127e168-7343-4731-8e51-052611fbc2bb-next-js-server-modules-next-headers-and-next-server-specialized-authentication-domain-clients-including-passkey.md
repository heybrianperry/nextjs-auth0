---
version: 2
name: d127e168-7343-4731-8e51-052611fbc2bb-next-js-server-modules-next-headers-and-next-server-specialized-authentication-domain-clients-including-passkey
description: "Next.js Server Modules next/headers and next/server: Specialized Authentication Domain Clients Including Passkey"
metadata:
  actual:
    adr_id: d127e168-7343-4731-8e51-052611fbc2bb
    status: accepted
    candidate_group_id: b5f7f0c9-7911-4dae-a8d2-ba285f4925c3
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/server/**
---

# Next.js Server Modules next/headers and next/server: Specialized Authentication Domain Clients Including Passkey

Status: proposed
Date: 2025-05-14
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `src/server/**`

## Context

- Authentication client infrastructure requires reliable access to incoming request headers and outgoing cookie headers across diverse server execution contexts.
- Multiple server-side authentication domain modules share common server runtime integration requirements for credential handling and session persistence.
- Direct dependency on low-level transport protocols creates tight coupling and impedes seamless operation across modern server-side component rendering and route handling boundaries.
- Server execution environments exhibit distinct capabilities and limitations regarding cookie persistence, such as read-only constraints during component rendering cycles.

## Problem Statement

Server-side authentication subsystems must manage credentials, sessions, and state across specialized flows such as passkeys, passwordless logins, and multi-factor authentication. Disparate approaches to reading and mutating HTTP headers and cookies across differing server environments introduce coupling, cookie state synchronization failures, and runtime exceptions when modifying headers in read-only contexts. A unified framework module integration is required to standardize request context access and header lifecycle management across all server client modules.

## Decision

1. SHOULD: Specialized authentication domain clients, including passkey, multi-factor authentication, and passwordless modules, SHOULD delegate client lifecycle and provider initialization through the shared server authentication client provider infrastructure.

## Policy Block

- SHOULD Specialized authentication domain clients, including passkey, multi-factor authentication, and passwordless modules, SHOULD delegate client lifecycle and provider initialization through the shared server authentication client provider infrastructure.

In scope:
- Server-side authentication client modules and domain extensions managing session tokens, request headers, or cookies.
- Server components, route handlers, and server actions requiring authentication state or token retrieval.

Out of scope:
- Client-side interactive components executing exclusively in the browser runtime.
- Pure utility functions and data transformation routines devoid of server context or request lifecycle interactions.

Exceptions:
- EXC-001: Legacy request and response routing layers require direct transport object access.

## Rationale

- Adopting next/headers and next/server provides standardized primitives for accessing request cookies and response construction within server execution environments.
- Consolidating domain authentication modules around uniform server runtime modules reduces redundant transport handling code across server client implementations.
- Standardizing on framework-native header utilities enables explicit runtime distinction between read-only server component contexts and mutable request handlers, preventing silent session persistence failures.

## Consequences

Positive:
- Establishes a uniform API surface for header and cookie resolution across all server-side authentication client implementations.
- Isolates domain authentication logic from raw transport primitives and lower-level socket representations.
- Facilitates clear runtime diagnostics when cookie mutation is attempted in non-writable server rendering cycles.

Negative:
- Binds server authentication client modules to the lifecycle contracts and runtime assumptions of Next.js server modules.
- Requires developers to account for execution-phase differences between read-only component rendering and mutable action or handler invocations.

## Alternatives

- Direct low-level transport request and response object manipulation (rejected)
  Rejected because: Direct transport object manipulation couples server clients to low-level runtime abstractions, breaking compatibility with modern server component and edge runtime environments.
  When valid: Valid only in standalone custom server runtimes operating outside modern component-based framework architectures.
- Proprietary bespoke context passing abstraction layer (rejected)
  Rejected because: Creating custom context wrappers duplicates framework-provided functionality and increases maintenance overhead across domain clients.
  When valid: Valid in framework-agnostic universal SDKs distributed across multiple dissimilar full-stack frameworks.

## Risks

- Attempting to persist refreshed session cookies within read-only server execution phases causes runtime warnings or failed session updates.
  Mitigation: Detect the active execution context and emit explicit diagnostic warnings advising callers to invoke token refreshes from mutable route or action boundaries.
  Owner: Server Authentication Engineering Team
- Breaking API changes across framework runtime releases may alter header or cookie resolution mechanics.
  Mitigation: Adhere to lock-file version grounding before updates and encapsulate framework module invocations behind internal provider wrappers.
  Owner: Platform Architecture Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Encapsulate invocations of framework server modules within the internal server authentication provider layer so that specialized domain clients consume a consistent interface.
- Ensure error and warning paths clearly inform consumers when cookie mutations fail due to invocation within read-only server component render cycles.

## Continuation Context


Verify commands:
- Discover and run the project static analysis and linting scripts to verify compliance with server module import boundaries.
- Discover and execute the project automated test suite to confirm session handling and cookie interactions pass across server execution scenarios.
- Discover and execute the type-checking script to ensure compatibility of all server runtime module imports against resolved framework declarations.

Accept when:
- All server authentication client modules import next/headers and next/server in alignment with architectural boundary constraints.
- Automated tests verify that cookie reads succeed in server contexts and that mutations in read-only rendering cycles emit diagnostic warnings without unhandled exceptions.
- Project static analysis, linting, and type verification suites pass with zero errors.

## Enforcement

- Verified by: Automated static analysis checks in continuous integration pipelines validating import boundaries.
- Verified by: Peer code review verifying adherence to server runtime module usage standards for authentication clients.
- Verified by: Integration tests validating session retrieval and cookie behavior under server component and route contexts.
- Violation handling: Continuous integration builds fail upon detection of unauthorized transport layer imports in server client modules.
- Violation handling: Pull requests attempting direct HTTP transport manipulation without approved policy exceptions will be rejected.
- Exception process: Submit an architectural review request detailing the runtime constraints that prevent using next/headers or next/server.
- Exception process: Secure documented approval from the platform architecture team prior to merging non-standard context handling.