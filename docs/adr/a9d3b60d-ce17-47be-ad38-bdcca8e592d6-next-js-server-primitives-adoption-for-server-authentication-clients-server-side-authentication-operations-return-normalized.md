---
version: 2
name: a9d3b60d-ce17-47be-ad38-bdcca8e592d6-next-js-server-primitives-adoption-for-server-authentication-clients-server-side-authentication-operations-return-normalized
description: "Next.js Server Primitives Adoption for Server Authentication Clients: Server Side Authentication Operations Return Normalized"
metadata:
  actual:
    adr_id: a9d3b60d-ce17-47be-ad38-bdcca8e592d6
    status: accepted
    candidate_group_id: a345d086-5676-4977-87a4-8e8543fe1515
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/server/**
---

# Next.js Server Primitives Adoption for Server Authentication Clients: Server Side Authentication Operations Return Normalized

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `src/server/**`

## Context

- Server authentication subsystems handling passkey, multi-factor authentication, and passwordless workflows require access to incoming request headers and server primitives to validate client credentials.
- Authentication client implementations are structured as dedicated server adapters coordinating with a shared authentication client provider abstraction.
- Direct integration with framework-level server subpath exports allows authentication adapters to read request-scoped context cleanly without manual transport parameter threading.

## Problem Statement

Server-side authentication operations require secure and consistent access to incoming HTTP headers and response constructs across multiple authentication modalities without leaking transport handling into business logic or causing request context leakage.

## Decision

1. SHOULD: Server-side authentication operations SHOULD return normalized response data structures defined by shared domain types to isolate callers from transport-specific details.

## Policy Block

- SHOULD Server-side authentication operations SHOULD return normalized response data structures defined by shared domain types to isolate callers from transport-specific details.

In scope:
- Server-side authentication client modules managing passkey, multi-factor, and passwordless authentication flows.
- Server-side adapters requiring request headers or server response constructs.

Out of scope:
- Client-side authentication UI components and client-only state hooks.
- Pure domain utility functions that do not interact with request or transport lifecycles.

## Rationale

- Static analysis indicates repeated adoption of next/headers and next/server across all specialized server authentication clients.
- Consolidating request-scoped header extraction within dedicated server client modules decouples upper-level authentication consumers from transport-level manipulation.
- Using framework-native server primitives preserves asynchronous request isolation across concurrent authentication transactions.

## Consequences

Positive:
- Establishes consistent header and cookie resolution across passkey, multi-factor, and passwordless authentication clients.
- Eliminates repetitive manual header extraction in route handlers by delegating context binding to dedicated server client adapters.
- Leverages framework-native request lifecycle handling to maintain safe request-scoped isolation.

Negative:
- Couples server authentication client modules directly to framework-specific server runtime subpaths.
- Restricts execution of server authentication clients strictly to framework server execution boundaries that support request context resolution.

## Alternatives

- Manual Header Extraction via Explicit Route Parameter Passing (rejected)
  Rejected because: Requiring caller functions to manually extract and forward transport headers pollutes domain service signatures and increases implementation variance across routes.
  When valid: When operating in a framework-agnostic runtime where framework server context abstractions are unavailable.
- Global Node Runtime Context Inspection (rejected)
  Rejected because: Relying on unmanaged process-level globals creates concurrency hazards and cross-request contamination in asynchronous server environments.
  When valid: Never valid in concurrent multi-tenant server runtimes.

## Risks

- Framework server runtime API contracts may change across minor or major framework releases, affecting header access semantics.
  Mitigation: Enforce strict lock-version grounding and encapsulate all framework subpath calls inside dedicated client adapter modules.
  Owner: engineering team
- Calling server-only header primitives outside an active request context causes runtime exceptions.
  Mitigation: Restrict client instantiation to server boundaries and enforce request lifecycle validation via integration tests.
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
- Inspect server authentication client implementations to confirm how incoming request headers and response contexts are delegated to the shared authentication client provider.
- Check the resolved framework documentation corresponding to the exact lock version to verify whether header extraction calls require synchronous or asynchronous handling in the active environment.

## Continuation Context


Verify commands:
- Discover the project dependency resolution artifact and verify that framework runtime dependencies resolve cleanly to expected versions without duplicate runtime instances.
- Discover and execute the project test runner for server-side authentication test suites to validate header extraction and authentication client flows.
- Discover and execute the project static analysis and linting scripts to verify boundary constraints across server modules.

Accept when:
- All server authentication client test suites pass when validating header resolution and authentication client lifecycle operations.
- Static analysis verifies that server authentication clients source header and server response primitives exclusively from the designated framework server modules.

## Enforcement

- Verified by: Automated CI test validation for server authentication client modules.
- Verified by: Static analysis and architectural boundary checks during code review.
- Violation handling: Code review rejection for any server authentication client that circumvents framework server subpaths or reads ambient request context directly.
- Violation handling: Mandatory refactoring of non-compliant authentication adapters prior to merge.
- Exception process: Architectural review and documentation of runtime constraints if non-framework execution environments require custom adapter layers.