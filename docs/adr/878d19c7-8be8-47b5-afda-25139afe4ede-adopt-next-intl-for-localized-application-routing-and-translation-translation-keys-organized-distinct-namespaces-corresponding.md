---
version: 2
name: 878d19c7-8be8-47b5-afda-25139afe4ede-adopt-next-intl-for-localized-application-routing-and-translation-translation-keys-organized-distinct-namespaces-corresponding
description: "Adopt next-intl for Localized Application Routing and Translation: Translation Keys Organized Distinct Namespaces Corresponding"
metadata:
  actual:
    adr_id: 878d19c7-8be8-47b5-afda-25139afe4ede
    status: accepted
    candidate_group_id: bc4ba2d8-c628-4a0d-b685-e377c0def63f
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-next-intl/app/**
---

# Adopt next-intl for Localized Application Routing and Translation: Translation Keys Organized Distinct Namespaces Corresponding

Status: proposed
Date: 2025-02-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `examples/with-next-intl/app/**`

## Context

- The application requires internationalization support across multiple route segments, layouts, and page views.
- Routing structures and view components must handle locale-specific paths and localized message formatting uniformly.
- Static analysis shows repeated adoption of next-intl and next-intl/server alongside internal localization routing abstractions across layout and page components.

## Problem Statement

Internationalized web applications risk fragmented locale handling, mismatched route navigation, and inconsistent server rendering when localization libraries and routing primitives are applied ad hoc across pages and layouts. A centralized and consistent adoption pattern is necessary to govern translation and localized navigation.

## Decision

1. SHOULD: Translation keys SHOULD be organized into distinct namespaces corresponding to application features and views.

## Policy Block

- SHOULD Translation keys SHOULD be organized into distinct namespaces corresponding to application features and views.

In scope:
- All route layouts, view pages, and navigation components within localized application segments.

Out of scope:
- Non-localized API endpoints, health endpoints, or standalone utility modules that operate independently of user-facing locale contexts.

Exceptions:
- EXC-20-001: A route segment explicitly operates outside locale negotiation, such as system health check endpoints.

## Rationale

- Adopting next-intl provides unified support for internationalization across both server-rendered and client-rendered component trees.
- Coordinating localized navigation through a central internal routing module prevents broken links and unlocalized path transitions across locale segments.
- Standardizing on next-intl and next-intl/server across all localized layouts and pages reduces duplicated locale resolution logic and ensures maintainability.

## Consequences

Positive:
- Standardizes localized message retrieval and route navigation across both server and client execution contexts.
- Eliminates duplicated locale negotiation and routing wrapper logic across pages.
- Ensures consistent server-side rendering support for localized layouts and views.

Negative:
- Couples route definitions and navigation components directly to next-intl and its companion routing layer.
- Requires developers to maintain structured message catalogs aligned across supported locales.
- Adds architectural overhead when refactoring layouts and views due to locale context propagation.

## Alternatives

- Custom in-house internationalization and routing logic (rejected)
  Rejected because: Requires ongoing maintenance of routing wrappers, locale negotiation, and server-side translation state.
  When valid: When application requirements cannot be satisfied by standard internationalization libraries and minimal footprint is critical.
- Client-only internationalization rendering (rejected)
  Rejected because: Fails to provide localized content during server rendering, degrading initial render performance and search indexing.
  When valid: When the entire application runs strictly as a single-page client application with no server rendering.

## Risks

- Breaking changes across major versions of the internationalization library could disrupt route configuration and message rendering.
  Mitigation: Pin exact library versions via the lockfile and verify documentation compatibility before upgrading.
  Owner: engineering team
- Missing translation keys in message catalogs can cause missing content or runtime fallback behavior.
  Mitigation: Implement automated validation to ensure all translation keys exist in all supported locale message files.
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
- Ensure localized route segments supply necessary locale parameters to root layout translation providers before rendering descendant views.
- Centralize route configuration within the internal localization routing module to maintain a single source of truth for supported locales and path aliases.
- Utilize next-intl/server utilities in server-rendered modules to fetch messages and configure metadata ahead of view rendering.

## Continuation Context


Verify commands:
- Inspect the project dependency manifest and lockfile to confirm the exact resolved version of the internationalization dependency.
- Run the project static analysis and linting scripts to verify all localized views import routing primitives from the designated internal routing module.
- Execute the repository test suite to ensure localized route layouts and pages render translations without missing key errors.

Accept when:
- All localized routes and views resolve localized message keys through next-intl without runtime resolution failures.
- All localized navigation links use the internal routing module rather than unlocalized primitives.
- Repository static analysis and test validation suites pass without internationalization import or execution errors.

## Enforcement

- Verified by: Automated static analysis checks in the continuous integration pipeline ensuring localized views import routing primitives from the central localization module.
- Verified by: Peer review of component additions within localized route directories.
- Verified by: Execution of localized route test suites in continuous integration.
- Violation handling: Build failures triggered on pull requests that import unlocalized navigation primitives in localized route structures.
- Violation handling: Rejection of pull requests introducing independent localization mechanisms without prior architectural exception.
- Exception process: Submit an architectural change request detailing why the standard internationalization library cannot support the specific route or view requirement.
- Exception process: Obtain approval from the technical lead before introducing alternative localization or routing mechanisms.