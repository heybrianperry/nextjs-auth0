---
version: 2
name: examples-with-dpop-when-client-exceeds-configured-request-8bc0
description: "Express rateLimit Middleware for HTTP Throttling: When Client Exceeds Configured Request Quota"
metadata:
  actual:
    adr_id: 8bc0c36e-3a92-42c0-a822-60b5aaa29ee0
    status: accepted
    candidate_group_id: 6c224766-e92a-4e60-96d6-678c2cffb625
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# Express rateLimit Middleware for HTTP Throttling: When Client Exceeds Configured Request Quota

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for inbound HTTP request routing pipelines and public API routes subject to abuse prevention and client traffic throttling.

### Rules

- **R-RL-001** MUST: When a client exceeds the configured request quota, the rateLimit middleware MUST reject the request with an explicit client-facing error message and an appropriate HTTP client error status.

### Verify

```bash
# Discover the project test execution runner from the manifest and run automated integration test suites
# validating rate limit response codes and headers.
```

**Accept when:**
- HTTP requests exceeding the configured threshold return HTTP status 429 Too Many Requests along with standard rate limit headers.
- HTTP requests within the configured threshold succeed and include decreasing remaining quota counts in the standard response headers.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>