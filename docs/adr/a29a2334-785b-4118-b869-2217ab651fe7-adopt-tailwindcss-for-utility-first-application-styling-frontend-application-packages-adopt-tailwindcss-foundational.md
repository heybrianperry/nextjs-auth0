---
version: 2
name: a29a2334-785b-4118-b869-2217ab651fe7-adopt-tailwindcss-for-utility-first-application-styling-frontend-application-packages-adopt-tailwindcss-foundational
description: "Adopt Tailwindcss for Utility-First Application Styling: Frontend Application Packages Adopt Tailwindcss Foundational"
metadata:
  actual:
    adr_id: a29a2334-785b-4118-b869-2217ab651fe7
    status: accepted
    candidate_group_id: 924a3d3b-dd21-474f-b737-b0a63d7dca24
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - e2e/test-app/**
      - examples/with-cte/**
      - examples/with-mrrt/**
      - examples/with-next-intl/**
      - examples/with-passkeys/**
      - examples/with-passwordless-db/**
      - examples/with-passwordless/**
      - examples/with-shadcn/**
---

# Adopt Tailwindcss for Utility-First Application Styling: Frontend Application Packages Adopt Tailwindcss Foundational

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `e2e/test-app/**`
- `examples/with-cte/**`
- `examples/with-mrrt/**`
- `examples/with-next-intl/**`
- `examples/with-passkeys/**`
- `examples/with-passwordless-db/**`
- `examples/with-passwordless/**`
- `examples/with-shadcn/**`

## Context

- Multiple independent application modules and integration test workspaces maintain distinct presentation layers that require cohesive visual layout and token management.
- Maintaining disparate styling paradigms across multiple example and test workspaces increases cognitive overhead and inhibits code sharing.
- Standardizing on a single utility-first framework across consumer workspaces aligns token definitions and simplifies presentation maintenance.

## Problem Statement

Frontend applications and reference implementations across the repository require a unified approach to styling and design token distribution. Without a standardized utility framework, separate modules risk diverging into conflicting styling methodologies, inconsistent token definitions, and unbounded stylesheet bloat that complicates cross-application component reuse and visual consistency.

## Decision

1. MUST: Frontend application packages MUST adopt tailwindcss as the foundational styling solution for user interface layout and visual presentation.

## Policy Block

- MUST Frontend application packages MUST adopt tailwindcss as the foundational styling solution for user interface layout and visual presentation.

In scope:
- User interface presentation layers and frontend application packages within the repository.
- Component styling, layout composition, and design token definitions in client-facing applications.

Out of scope:
- Non-visual backend services, database migrations, and headless background workers.
- Third-party components that provide self-contained, isolated styling runtimes.

## Rationale

- Static analysis identifies consistent adoption of tailwindcss across multiple application packages and test suites, confirming an established cross-package standard.
- A utility-first approach provides predictable styling composition and dead-code elimination without runtime CSS-in-JS overhead.
- Centralizing visual tokens via dedicated configuration definitions ensures visual alignment across diverse application implementations.

## Consequences

Positive:
- Standardizes design tokens and visual presentation across independent application workspaces.
- Eliminates fragmented bespoke stylesheet architectures and runtime styling overhead.
- Reduces stylesheet bundle size through automated utility deduplication and dead-code pruning.

Negative:
- Component markup becomes denser due to descriptive utility class composition in template source files.
- Developers must learn framework-specific utility naming conventions and configuration schemas.
- Global style overrides require deliberate layer coordination to prevent cascade ordering conflicts.

## Alternatives

- Scoped CSS Modules (rejected)
  Rejected because: Lacks centralized design token governance and requires maintaining separate companion stylesheets for every individual component.
  When valid: When building isolated component packages that cannot assume utility framework preprocessing.
- Runtime CSS-in-JS Solutions (rejected)
  Rejected because: Introduces client-side runtime evaluation overhead and complicates server-side rendering pipelines.
  When valid: When dynamic, highly programmatic style mutations depend on complex runtime state.

## Risks

- Divergence of design tokens across distinct application configurations.
  Mitigation: Extract shared theme tokens and configurations into common reusable presets.
  Owner: Frontend Architecture Team
- Overuse of arbitrary value escapes bypassing design system constraints.
  Mitigation: Enforce automated static analysis checks in verification workflows to reject unapproved arbitrary utility values.
  Owner: Frontend Architecture Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Configure content scanning boundaries precisely to target source files containing presentation markup to avoid unnecessary compilation overhead.
- Organize custom utility extensions and theme overrides within the configuration schema rather than writing raw cascading stylesheets.

## Continuation Context


Verify commands:
- Discover and run the repository linter script to validate utility class usage across presentation files.
- Discover and run the project build script to verify stylesheet generation and purge correctness across all application workspaces.

Accept when:
- Application build scripts successfully generate optimized stylesheets with zero compilation errors.
- Static analysis workflows pass without unresolved utility class or configuration schema violations.

## Enforcement

- Verified by: Continuous integration static analysis workflows validating styling rules and configuration validity.
- Verified by: Peer review of pull requests modifying presentation components or configuration modules.
- Violation handling: Automated integration checks fail when unapproved styling patterns or broken configurations are detected.
- Violation handling: Engineers must refactor non-compliant styling into approved utility patterns prior to pull request approval.
- Exception process: Submit an architectural exception request documenting technical rationale for review by the frontend architecture team.