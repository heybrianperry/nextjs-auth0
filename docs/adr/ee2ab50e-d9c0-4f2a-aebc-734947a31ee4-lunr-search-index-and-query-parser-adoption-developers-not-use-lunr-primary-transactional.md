---
version: 2
name: ee2ab50e-d9c0-4f2a-aebc-734947a31ee4-lunr-search-index-and-query-parser-adoption-developers-not-use-lunr-primary-transactional
description: "Lunr Search Index and Query Parser Adoption: Developers Not Use Lunr Primary Transactional"
metadata:
  actual:
    adr_id: ee2ab50e-d9c0-4f2a-aebc-734947a31ee4
    status: accepted
    candidate_group_id: 0c86c4c8-50ef-4b9e-b5d2-5a9c569fd2f1
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - docs/assets/**
---

# Lunr Search Index and Query Parser Adoption: Developers Not Use Lunr Primary Transactional

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `docs/assets/**`

## Context

- Client-side documentation interfaces require static in-memory index querying capabilities without relying on a remote datastore server.
- The codebase includes compiled search execution routines that invoke lunr query parsing and lexer event handling for text retrieval.
- The pattern appears restricted to a single asset bundle representing static documentation search rather than a core domain datastore architecture.

## Problem Statement

The project requires an in-memory datastore for fast keyword querying within client-facing documentation, but adopting an embedded search library within static client bundles risks index version mismatches and unmanaged serialization overhead without clear architectural governance.

## Decision

1. MUST_NOT: Developers MUST NOT use lunr as a primary transactional datastore for domain state or persistent records.

## Policy Block

- MUST_NOT Developers MUST NOT use lunr as a primary transactional datastore for domain state or persistent records.

In scope:
- Static documentation search interfaces requiring client-side index querying
- In-memory token-based text search evaluation using lunr QueryParser

Out of scope:
- Primary persistent transactional application data storage
- Server-side datastores and relational persistence layers

## Rationale

- Evidence indicates that lunr is used for query parsing and token emission within client documentation search artifacts.
- Isolating search retrieval to an in-memory lunr index satisfies documentation querying without provisioning external datastore infrastructure.
- Single-file detection in compiled documentation indicates this is localized search functionality rather than a project-wide primary datastore standard.

## Consequences

Positive:
- Enables instantaneous zero-latency search querying directly within the client execution environment.
- Eliminates network latency and external server dependencies for static text lookup.

Negative:
- Increases client bundle payload size due to embedded serialized search index and parser overhead.
- Creates potential version mismatch failures when loading serialized indexes created with disparate library builds.

## Alternatives

- Server-side primary search datastore (rejected)
  Rejected because: Introduces unnecessary operational overhead and hosting dependencies for static client-side documentation search.
  When valid: Valid when query volume or corpus size exceeds client memory constraints.
- Standard browser string pattern matching without indexing (rejected)
  Rejected because: Lacks tokenization, stemming, field boosting, and edit distance capabilities supported by lunr QueryLexer.
  When valid: Valid for small static lists with trivial substring lookup requirements.

## Risks

- Serialized search index incompatibility resulting from version drift across build cycles.
  Mitigation: Enforce pipeline registration and lock-file version alignment before serializing and loading indexes.
  Owner: engineering team
- Excessive bundle size degradation when indexing extensive documentation corpora.
  Mitigation: Monitor client artifact payload sizes and partition search indices if memory limits are approached.
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
- Query tokenization pipelines should configure lexer tokens for fields, terms, and edit distance to maintain consistent relevance scoring.
- Verify that custom pipeline functions are registered prior to index serialization to avoid deserialization warnings during runtime execution.

## Continuation Context


Verify commands:
- Discover and run the project test runner to execute unit and integration suites validating client search index generation.
- Discover and run the project static analysis and linting suite to verify compliance with query parser and lexer invocation standards.

Accept when:
- Search query execution returns expected ranked results without emitting pipeline or version mismatch warnings.
- All discovered automated test suites pass without regressions.

## Enforcement

- Verified by: Automated continuous integration build checks
- Verified by: Peer code review of client search implementation and bundle configuration
- Violation handling: Pull requests that misconfigure query execution or violate serialization constraints must be blocked until resolved.
- Exception process: Exceptions require architectural review and approval from the technical lead documenting why client-side search indexing is insufficient.