---
version: 2
name: f02f08f6-639d-4c11-9f99-6126275223cb-next-js-application-framework-adoption-application-code-not-bypass-framework-routing
description: "Next.js Application Framework Adoption: Application Code Not Bypass Framework Routing"
metadata:
  actual:
    adr_id: f02f08f6-639d-4c11-9f99-6126275223cb
    status: accepted
    candidate_group_id: cf525615-6f42-4da5-82c9-6e313038bd53
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - e2e/test-app/pages/pages-router/server/**
      - examples/with-ipsie-session-expiry/app/**
      - examples/with-mrrt/app/**
---

# Next.js Application Framework Adoption: Application Code Not Bypass Framework Routing

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `e2e/test-app/pages/pages-router/server/**`
- `examples/with-ipsie-session-expiry/app/**`
- `examples/with-mrrt/app/**`

## Context

- The codebase requires a consistent framework architecture for web applications to unify client-side navigation, layout hierarchies, and server-rendered entrypoints.
- Multiple application modules demonstrate reliance on the Next.js ecosystem for structural page rendering, layout composition, and server-side data fetching mechanisms.
- Without a standardized framework adoption decision, divergent rendering paradigms and ad-hoc routing patterns could fragment application maintenance and deployment workflows.

## Problem Statement

Building web applications across multiple workspaces without a standardized web framework leads to incompatible routing models, fragmented layout composition, and inconsistent server-side data fetching strategies. The architecture requires a unified framework standard that formalizes page routing, layout composition, and server rendering lifecycles.

## Decision

1. MUST_NOT: Application code MUST NOT bypass the framework routing and rendering architecture by introducing competing presentation servers or uncoordinated routing handlers.

## Policy Block

- MUST_NOT Application code MUST NOT bypass the framework routing and rendering architecture by introducing competing presentation servers or uncoordinated routing handlers.

In scope:
- Web application packages, frontend routing entrypoints, and server-rendered view modules within the repository.
- Layout components and server-side request handlers requiring framework lifecycle coordination.

Out of scope:
- Standalone utility packages or backend-only microservices that do not render web interfaces.
- Static asset processing pipelines running independently of application presentation layers.

Exceptions:
- EXC-20-001: A service requires an isolated, non-React API gateway or purely headless daemon process.

## Rationale

- Next.js provides an integrated model uniting client routing, server-rendered data fetching interfaces such as getServerSideProps, and shared layout management within a single framework boundary.
- Empirical evidence confirms widespread framework adoption across existing application entrypoints and layout definitions, indicating established operational familiarity.
- Standardizing on this framework ensures uniform component lifecycle management, cohesive routing execution, and predictable boundary separation between client and server layers.

## Consequences

Positive:
- Provides a unified, standardized architectural pattern for routing, layout hierarchy, and server-side page execution across web applications.
- Enables structured data fetching at server boundaries using established framework mechanisms like getServerSideProps.
- Simplifies presentation state and shared component encapsulation through declarative layout structures.

Negative:
- Couples web application routing and data retrieval lifecycles tightly to the adopted framework conventions.
- Increases cognitive overhead when coordinating boundary differences between server execution environments and client execution contexts.
- Requires strict lock-step dependency management to prevent framework interface discrepancies across workspace packages.

## Alternatives

- Unframeworked React client-side single page application with custom server-side rendering pipeline (rejected)
  Rejected because: Custom server rendering and routing solutions impose substantial maintenance overhead, lack integrated layout mechanisms, and increase architectural fragmentation.
  When valid: Valid only for lightweight client-only static dashboards with zero server-side rendering or search engine indexing requirements.
- Alternative full-stack meta-frameworks (rejected)
  Rejected because: The repository already contains established implementations and dependencies centered on Next.js, and adopting a divergent framework would duplicate infrastructure and operational complexity.
  When valid: Valid if application requirements shift to an ecosystem where Next.js does not provide required platform targets.

## Risks

- Breaking API changes across framework major versions affecting server data fetching methods or layout paradigms.
  Mitigation: Strict adherence to lock-version grounding, rigorous automated test validation during dependency updates, and adherence to official version documentation.
  Owner: Engineering Team
- Accidental leaking of server-only secrets or execution logic into client bundles across hybrid page boundaries.
  Mitigation: Enforce strict separation between server-side data retrieval interfaces and client presentation components via automated linting and code reviews.
  Owner: Engineering Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Organize route structures and shared layouts in accordance with the project routing convention, ensuring reusable wrapper components encapsulate global styling and third-party context providers.
- When implementing data-dependent views, evaluate whether data must be retrieved server-side during the request lifecycle using framework server methods or rendered statically based on caching and freshness requirements.

## Continuation Context


Verify commands:
- Discover and run the project build script declared in the repository manifest to verify route compilation and static page generation.
- Discover and run the repository automated test suite to validate page rendering, layout composition, and server-side fetching behavior.

Accept when:
- The project build script completes with exit code 0 and successfully generates all configured routes and layouts without compilation errors.
- All automated test suites for server-rendered endpoints and layout components pass successfully.

## Enforcement

- Verified by: Automated continuous integration build and test verification pipelines.
- Verified by: Peer code review checking adherence to framework lifecycle rules, layout conventions, and server-client boundary separation.
- Violation handling: Pull requests introducing uncoordinated routing implementations or failing framework build steps must be blocked from merging until corrected.
- Exception process: Exceptions require submission of an architectural variance proposal approved by the engineering architecture team.