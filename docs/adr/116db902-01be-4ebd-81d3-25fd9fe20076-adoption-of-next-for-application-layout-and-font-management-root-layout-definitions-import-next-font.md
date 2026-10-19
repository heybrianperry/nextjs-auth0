---
version: 2
name: 116db902-01be-4ebd-81d3-25fd9fe20076-adoption-of-next-for-application-layout-and-font-management-root-layout-definitions-import-next-font
description: "Adoption of next for Application Layout and Font Management: Root Layout Definitions Import Next Font"
metadata:
  actual:
    adr_id: 116db902-01be-4ebd-81d3-25fd9fe20076
    status: accepted
    candidate_group_id: 730a51f3-0da2-4ea4-a952-639ced2b239b
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - e2e/test-app/app/**
      - examples/with-mrrt/app/**
      - examples/with-next-intl/app/**
      - examples/with-shadcn/app/**
---

# Adoption of next for Application Layout and Font Management: Root Layout Definitions Import Next Font

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `e2e/test-app/app/**`
- `examples/with-mrrt/app/**`
- `examples/with-next-intl/app/**`
- `examples/with-shadcn/app/**`

## Context

- The project requires a consistent application architecture across multiple application targets and example modules.
- Application entry layouts across the repository consistently import next and next/font/local alongside global styling declarations.
- Adopting a unified layout structure ensures standardized rendering, font delivery, and styling encapsulation across web applications.

## Problem Statement

Disparate web applications and example packages require a unified foundation for layout composition, font optimization, and global styling integration to avoid duplicated setup and divergent rendering lifecycles.

## Decision

1. MUST: Root layout definitions MUST import next/font/local to configure and optimize local typography assets rather than relying on unmanaged external stylesheet font links.

## Policy Block

- MUST Root layout definitions MUST import next/font/local to configure and optimize local typography assets rather than relying on unmanaged external stylesheet font links.

In scope:
- Root application layout components and presentation shell definitions across application modules and examples.

Out of scope:
- Non-presentation utility modules, isolated business logic libraries, and standalone background workers.

## Rationale

- Static analysis across multiple application targets confirms consistent imports of next, next/font/local, and global stylesheet modules at layout boundaries.
- Centralizing font management through next/font/local optimizes asset delivery and eliminates layout shift without third-party network dependencies.
- Standardizing on next across applications ensures architectural consistency and shared conventions across production applications and examples.

## Consequences

Positive:
- Establishes a consistent root layout architecture and font configuration across all application workspaces.
- Enables local font loading with reduced layout shift and zero external network font requests at runtime.
- Ensures global styling baselines apply predictably across all child route segments.

Negative:
- Couples layout components and font loading mechanisms directly to next framework conventions.
- Requires adherence to framework-specific asset colocation and module resolution constraints.

## Alternatives

- External network font loading via remote style tags (rejected)
  Rejected because: Introduces third-party runtime network latency, potential availability risks, and cumulative layout shift during page hydration.
  When valid: When application environments lack local font assets or require dynamically hosted cloud font services.
- Custom layout wrappers without framework conventions (rejected)
  Rejected because: Fractures architectural alignment across application packages and loses native framework optimizations for fonts and routing.
  When valid: When building framework-agnostic microfrontends or static prototypes.

## Risks

- Breaking API changes across framework releases impacting font loading and layout contracts.
  Mitigation: Enforce strict lockfile version grounding and verify compatibility against documentation before adopting framework updates.
  Owner: engineering team
- Inadvertent duplication of global stylesheets across multiple nested layouts.
  Mitigation: Enforce layout boundaries through automated lint rules and static analysis in build pipelines.
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
- Verify that all local font declarations configure display swap and subset options in accordance with design requirements.
- Ensure that global style imports remain scoped exclusively to the top-level layout boundary to prevent cascade conflicts in child routes.

## Continuation Context


Verify commands:
- Discover the repository dependency verification command from project metadata and verify that dependency resolution succeeds.
- Discover the project static analysis and lint commands and execute them to verify compliance with root layout import conventions.
- Discover and run the project build and testing scripts to ensure all layout components compile and render without errors.

Accept when:
- The project build and static analysis commands execute without errors or lint warnings.
- All root layouts correctly import the required framework and font modules while maintaining zero external font network requests.

## Enforcement

- Verified by: Automated continuous integration checks executing repository linting, type-checking, and build validation.
- Verified by: Peer code review verifying adherence to layout structure and font loading standards.
- Violation handling: Pull requests violating layout or font import constraints will fail automated CI pipelines and require remediation prior to merge.
- Exception process: Architectural exceptions require formal proposal, review, and written approval by the engineering architecture lead.