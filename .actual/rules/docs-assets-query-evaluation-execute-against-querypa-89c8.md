---
version: 2
name: docs-assets-query-evaluation-execute-against-querypa-89c8
description: "Lunr Search Integration: Query Evaluation Execute Against Queryparser Instances"
metadata:
  actual:
    adr_id: 89c8a7ef-4325-4cae-8f4f-c9fae209f8e6
    status: accepted
    candidate_group_id: 114ecd47-c00c-419f-94d4-752c22fe63aa
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - docs/assets/**
---

# Lunr Search Integration: Query Evaluation Execute Against Queryparser Instances

Scope: applies to `docs/assets/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-LUNR-001** MUST: Query evaluation MUST execute against QueryParser instances instantiated with active query tokens rather than invoking unparsed lexical strings directly.

### Verify

\`\`\`bash
# Locate the project dependency manifest and lock artifact to determine active search engine resolution
# Discover the project verification script from the repository manifest and execute the test runner to validate search integration suites
# Discover and run the project build and static analysis commands to ensure lexer event integration conforms to type definitions
\`\`\`

**Accept when:**
- All client search unit and integration tests pass without unhandled lexer event warnings.
- Index loading verifies schema compatibility without version mismatch diagnostic warnings.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>