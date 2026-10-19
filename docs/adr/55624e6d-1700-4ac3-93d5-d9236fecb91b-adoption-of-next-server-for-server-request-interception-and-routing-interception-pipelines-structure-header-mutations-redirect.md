---
version: 2
name: 55624e6d-1700-4ac3-93d5-d9236fecb91b-adoption-of-next-server-for-server-request-interception-and-routing-interception-pipelines-structure-header-mutations-redirect
description: "Adoption of next/server for Server Request Interception and Routing: Interception Pipelines Structure Header Mutations Redirect"
metadata:
  actual:
    adr_id: 55624e6d-1700-4ac3-93d5-d9236fecb91b
    status: accepted
    candidate_group_id: 6386fe8c-1025-409b-be3e-4cff9e49397d
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-cte/**
      - examples/with-dpop/**
      - examples/with-mrrt/**
---

# Adoption of next/server for Server Request Interception and Routing: Interception Pipelines Structure Header Mutations Redirect

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `examples/with-cte/**`
- `examples/with-dpop/**`
- `examples/with-mrrt/**`

## Context

- HTTP request mediation across entry points requires consistent request inspection, URL path evaluation, and response header management.
- Multiple boundary modules within the codebase standardize on next/server primitives to handle server-side request routing and response decoration.
- Interception workflows integrate request evaluation alongside authentication context and downstream proxying requirements.

## Problem Statement

Boundary components such as request interception middleware and proxy dispatchers require a uniform approach to intercepting HTTP requests, parsing URL parameters, and modifying response headers. Without a standardized server primitive library, disparate modules risk implementing divergent request parsing, inconsistent header injection, and uncoordinated redirection mechanisms across server boundaries.

## Decision

1. SHOULD: Interception pipelines SHOULD structure header mutations and redirect parameters idempotently before forwarding control to downstream handlers.

## Policy Block

- SHOULD Interception pipelines SHOULD structure header mutations and redirect parameters idempotently before forwarding control to downstream handlers.

In scope:
- Server-side request interception layers, proxy endpoints, and boundary routing modules.
- Components responsible for mutating response headers or directing request control flow at the server boundary.

Out of scope:
- Client-side rendering components and static UI views that do not process server HTTP traffic.
- Isolated background batch processing jobs that operate outside the HTTP request lifecycle.

Exceptions:
- EXC-20-001: Direct protocol passthrough is required where lower-level transport sockets supersede framework server abstractions.

## Rationale

- Adopting next/server standardizes HTTP request evaluation and response generation across all edge and proxy boundary files.
- Using request.nextUrl and response.headers reduces implementation divergence and eliminates redundant request parsing logic across distinct features.
- Standardizing on framework server primitives aligns runtime request mediation with the server execution environment.

## Consequences

Positive:
- Consistent request interception and redirection mechanics across proxy and middleware boundaries.
- Uniform header mutation patterns for tracking request outcomes and telemetry attributes.
- Centralized reliance on framework-supported server abstractions rather than divergent internal HTTP parsers.

Negative:
- Couples request mediation and boundary logic directly to the next/server runtime API contract.
- Upgrades to the framework runtime require auditing server primitive compatibility across all interception modules.

## Alternatives

- Native platform HTTP request and response handler interfaces (rejected)
  Rejected because: Native platform interfaces lack direct integration with framework routing, path resolution, and edge runtime optimizations.
  When valid: When operating in standalone runtime environments completely independent of the framework.
- Custom internal HTTP middleware abstraction library (rejected)
  Rejected because: Maintaining an internal wrapper introduces unnecessary maintenance overhead when standardized framework primitives are already provided.
  When valid: When multiple distinct framework platforms must be supported simultaneously behind an abstract facade.

## Risks

- Breaking changes in framework server API signatures across version transitions.
  Mitigation: Enforce strict lock-version grounding and automated type checking during CI build verification.
  Owner: Engineering team
- Performance overhead from excessive header manipulation or synchronous processing in interception chains.
  Mitigation: Profile latency at the boundary and keep header inspection logic minimal and non-blocking.
  Owner: Engineering team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Discover the project dependency resolution artifacts to determine the exact installed version of next/server before employing server response primitives.
- Ensure that all URL redirection parameters and response headers populated during interception follow consistent casing and naming conventions defined across the repository.

## Continuation Context


Verify commands:
- Discover and run the project static analysis and linting scripts to verify compliance of next/server imports across boundary modules.
- Discover and execute the project test suite covering request interception and response header modification flows.

Accept when:
- Static analysis passes with zero import violations or unapproved HTTP abstraction bypasses.
- All unit and integration tests for request interception and response header mutations complete successfully.

## Enforcement

- Verified by: Automated continuous integration lint and type-checking suites.
- Verified by: Peer code review verification for any new or modified server boundary modules.
- Violation handling: Automated build failure on unapproved imports or bypasses of next/server primitives.
- Violation handling: Pull requests containing non-compliant request handling logic are blocked until refactored.
- Exception process: Submit an architectural exception request detailing the necessity for direct transport access, reviewed and approved by the architecture review board.