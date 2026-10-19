---
version: 2
name: examples-with-dpop-ratelimit-configuration-set-standardhead-a77e
description: "Express rateLimit Middleware for HTTP Throttling: Ratelimit Configuration Set Standardheaders True Legacyheaders"
metadata:
  actual:
    adr_id: a77e3bcb-88a7-464f-be22-c3e2350eceb9
    status: accepted
    candidate_group_id: 6c224766-e92a-4e60-96d6-678c2cffb625
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# Express rateLimit Middleware for HTTP Throttling: Ratelimit Configuration Set Standardheaders True Legacyheaders

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for inbound HTTP request routing pipelines and public API routes subject to abuse prevention and client traffic throttling.

### Rules

- **R-RL-001** MUST: The rateLimit configuration MUST set standardHeaders to true and legacyHeaders to false to emit standardized rate limit metadata headers in HTTP responses.

### Verify

```bash
# Discover the test runner from the manifest and run automated integration test suites
# validating rate limit response codes and headers.
# Example discovery & execution:
TEST_RUNNER=$(node -p "require('./package.json').scripts?.test || ''")
echo "Using test runner script: $TEST_RUNNER"
npm test
```

**Accept when:**
- HTTP requests exceeding the configured threshold return HTTP status 429 Too Many Requests along with standard rate limit headers.
- HTTP requests within the configured threshold succeed and include decreasing remaining quota counts in the standard response headers.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>