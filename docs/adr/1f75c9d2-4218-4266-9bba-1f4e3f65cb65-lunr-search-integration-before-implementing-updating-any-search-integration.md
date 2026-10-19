---
version: 2
name: 1f75c9d2-4218-4266-9bba-1f4e3f65cb65-lunr-search-integration-before-implementing-updating-any-search-integration
description: "Lunr Search Integration: Before Implementing Updating Any Search Integration"
metadata:
  actual:
    adr_id: 1f75c9d2-4218-4266-9bba-1f4e3f65cb65
    status: accepted
    candidate_group_id: 114ecd47-c00c-419f-94d4-752c22fe63aa
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - docs/assets/**
---

# Lunr Search Integration: Before Implementing Updating Any Search Integration

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `docs/assets/**`

## Context

- Client-side documentation and search interfaces require client-directed text search capabilities without relying on persistent remote query backends.
- Lexical analysis and query parsing must process search inputs via structured token streams to support query features such as term presence and field scoping.
- Serialized search indices deployed to client bundles require compatibility verification against the active search engine runtime to prevent index parsing anomalies.

## Problem Statement

Client-side search components require a decoupled integration mechanism to parse and evaluate structured queries directly in the client runtime while preventing runtime failures caused by mismatched serialized search index structures.

## Decision

1. MUST: Before implementing or updating any search integration code, consumers MUST inspect the repository lock or resolution artifact to confirm the exact resolved version of the search dependency matches the serialized search index schema.

## Policy Block

- MUST Before implementing or updating any search integration code, consumers MUST inspect the repository lock or resolution artifact to confirm the exact resolved version of the search dependency matches the serialized search index schema.

In scope:
- Client-side search integration components that parse and execute text queries against serialized indices.
- Runtime modules interacting with query lexer event emissions and query parser instances.

Out of scope:
- Server-side search indexing and backend query retrieval services operating outside client runtime bundles.
- Static asset generation and pre-rendering processes that do not evaluate runtime search queries.

Exceptions:
- EX-27-001: Direct unparsed string filtering is required in lightweight static contexts where serialized indices are not bundled.

## Rationale

- Token-driven event emission via QueryLexer isolates lexical processing steps, ensuring structured parsing across diverse query criteria.
- Enforcing runtime index version checks safeguards against silent query parsing degradation when search index structures change across updates.
- Evidence indicates single-file footprint within bundled assets, necessitating clear architectural boundaries if client search capabilities are formalized.

## Consequences

Positive:
- Provides deterministic query parsing through structured token stream emissions.
- Prevents silent query evaluation failures by detecting index schema mismatches at initialization.
- Decouples query tokenization from search execution logic.

Negative:
- Increases client runtime complexity by maintaining query lexer and parser event boundaries.
- Requires strict synchronization between build-time serialized indices and client runtime search dependencies.

## Alternatives

- Server-side search API proxying query requests to a remote search engine service (rejected)
  Rejected because: Introduces network latency and operational overhead for client-side search across offline documentation assets.
  When valid: Valid when dataset size exceeds client memory constraints or requires authenticated remote indices.
- Native regular expression string scanning across raw text payloads (rejected)
  Rejected because: Lacks support for structured query expressions, field scoping, boost factors, and edit distances.
  When valid: Valid when searching small unindexed single-field text lists.

## Risks

- Serialized search index format drifts from the runtime search engine parser.
  Mitigation: Enforce lock artifact resolution checks and validate index compatibility during initialization.
  Owner: engineering team
- Client bundle payload expansion resulting from bundling full search lexer and parser logic.
  Mitigation: Lazy-load client search modules only upon initial search interaction.
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
- Locate the project dependency manifest and lock artifact to determine the active client search engine resolution before authoring custom lexer extensions.
- Initialize query parsing within a protected block to capture index version diagnostics before executing queries against the pre-built index.

## Continuation Context


Verify commands:
- Discover the project verification script from the repository manifest and execute the test runner to validate search integration suites.
- Discover and run the project build and static analysis commands to ensure lexer event integration conforms to type definitions.

Accept when:
- All client search unit and integration tests pass without unhandled lexer event warnings.
- Index loading verifies schema compatibility without version mismatch diagnostic warnings.

## Enforcement

- Verified by: Automated continuous integration test suites verifying client search query parsing.
- Verified by: Peer code review checking adherence to event lexer boundaries and lock artifact version verification.
- Violation handling: Pull requests bypassing query lexer event boundaries or omitting lock version checks are blocked from merging.
- Exception process: Exceptions must be submitted via architectural review request and documented in the project documentation directory.