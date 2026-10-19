<!-- actual-ai:adr-governance:start -->
# Project ADRs

This project's conventions are encoded as ADRs under `.actual/rules/`. **The ADRs ARE the pattern.** Follow them verbatim instead of reading existing implementations to figure out how to do something.

> **Note:** this directive is calibrated for one-shot tasks (a single discrete feature). For multi-task interactive sessions, consult the ADRs for each task transition rather than holding to the per-session caps below.

## Workflow (follow in order)

1. **Identify topic.** Match the files you'll edit against the path-glob table below. Pick the 1-3 topics that match. Do not pre-emptively pick "related" topics; pick only what the file paths actually match.

2. **Select ADRs by filename — the filename is the index.** Run `ls .actual/rules/`. Each filename is `<topic>-<aspect-slug>-<hash>.md`; the `<aspect-slug>` (middle segment) names the ADR's specific concern — e.g., `database-schema-defined`, `zod-input-validation`, `cache-key-format`.

   **Scan ALL filenames first, then pick only the ones whose aspect-slug directly names a noun or verb in your task.** Select by filename; never read a body to decide relevance. **Hard cap: read at most 5 ADR files total.** If more than 5 look relevant, you are over-matching — keep the 5 most specific.

   **If the path-glob table below is a single `**/*` → `cross-cutting-` row** (one big bucket, no per-area topics), this filename scan is your ONLY filter. Do **not** read the bucket exhaustively — treat the filenames as a menu, match aspect-slugs to your task, read ≤5, and ignore the rest. Reading every ADR in the bucket is the exact failure this directive exists to prevent.

3. **Locate insertion points (one read per file, max 3 files).** You may read source files ONLY to (a) find where to add code (which directory, which barrel export to update) or (b) look up an exact identifier you must import. **Do not read source files as pattern examples — the ADRs already encode the pattern.** If you find yourself reading a file because "I want to see how X is done elsewhere," stop. The ADR you already read tells you how.

4. **Implement.** Write the code following the rule statements verbatim. If two ADRs seem to conflict, follow the more specific one (longer topic prefix wins).

5. **Verify after implementing.** Only after the code is written, re-read the `verify_commands` or `accept_criteria` sections of the ADRs you applied and check your work against them. Run the verify commands if any.

## Anti-patterns to avoid

- Reading the first N rules alphabetically because they're cheap. Filter by aspect-slug first, then read only the relevant ones.
- Reading >5 ADR files for a single feature. If you're tempted, you're over-scoping the topic match.
- Reading the entire `cross-cutting-` bucket because "every rule is always active." Selection is by filename (step 2); you apply the ≤5 you selected, not all of them.
- Reading existing similar features to "see the pattern" — the ADRs encode the pattern. Trust them.
- Re-reading the same ADR multiple times. Cache it mentally.
- Continuing to browse the codebase after step 3. By step 4 you should be writing, not reading.

Each rule file at `.actual/rules/<topic>-<aspect>-<hash>.md` contains the full ADR with rule statements, verify commands, and accept criteria.

## Verification Protocol

These rules are ALWAYS ACTIVE. Apply every rule **from the ADRs you selected in step 2** that governs the files you touch — to all code generation, modification, and review. "Always active" does **not** mean read every ADR: you apply the handful you selected by filename, within the read cap above.

Every rule follows a **Verify → Fix → Repeat** loop. After generating or modifying code for any rule you MUST:

1. **RUN** the rule's `### Verify` command(s).
2. **CAPTURE** the full output (stdout + stderr).
3. **EVALUATE** the output against the rule's **Accept when** criteria.
4. **IF FAILING:** diagnose the root cause, apply a fix, and re-run from step 1.
5. **IF PASSING:** keep the passing output as evidence before moving on.
6. **MAX ITERATIONS:** 5 attempts per rule. If still failing after 5 attempts, STOP and report the failure with all captured output.

Compliance is not optional. Do not skip verification, assume correctness, or defer it to a later task. Every change to a governed area must be accompanied by a passing verification run.

## Mandatory Dependency Grounding

Before writing or modifying implementation code that uses an external dependency:

1. Identify every affected external dependency.
2. Locate the repository's manifest and lock or resolution artifact.
3. Determine the exact repository-resolved version from the lock artifact.
4. Verify that the active environment matches that version.
5. Verify each API being introduced or changed against evidence applicable to that exact version (official documentation or public API reference).
6. Produce a dependency-grounding record.
7. Stop if any version, environment, or API cannot be verified.

Do not begin implementation until dependency grounding has passed.

The repository lock or resolution artifact is authoritative. A manifest range or model recollection is not sufficient.

### Integrated workflow

1. Stabilize the workspace.
2. Inspect the task and relevant architecture decisions.
3. Identify affected dependencies.
4. Run dependency grounding.
5. Produce the implementation plan.
6. Implement the change.
7. Validate grounding coverage, build, types, lint, and tests.
8. Report evidence, assumptions, and blockers.

## Path glob → topic

| You're editing | Topic prefix |
|---|---|
| `e2e/test-app/**` + `examples/with-cte/**` + `examples/with-mrrt/**` + `examples/with-next-intl/**` + `examples/with-passkeys/**` + `examples/with-passwordless-db/**` + `examples/with-passwordless/**` + `examples/with-shadcn/**`<br>`e2e/test-app/pages/api/pages-router/get-session/**` + `examples/with-cte/app/api/cte/**` + `examples/with-passkeys/**` + `examples/with-passwordless-db/components/**`<br>`e2e/test-app/app/**` + `examples/with-mrrt/app/**` + `examples/with-next-intl/app/**` + `examples/with-shadcn/app/**`<br>`e2e/test-app/pages/pages-router/server/**` + `examples/with-ipsie-session-expiry/app/**` + `examples/with-mrrt/app/**`<br>`e2e/test-app/app/app-router/api/**` + `examples/with-ipsie-session-expiry/app/api/**` + `examples/with-mrrt/**`<br>`examples/with-dpop/lib/**` + `src/server/**` + `src/utils/**`<br>`src/server/**` + `src/types/**` + `src/utils/**`<br>`e2e/test-app/app/app-router/client/**` + `examples/with-dpop/lib/**`<br>`src/server/**` + `src/utils/**`<br>`src/**/*` + `tests/**/*`<br>`**/*` | `cross-cutting-` _(57 ADRs)_ |
| `examples/with-dpop/**` | `examples-with-dpop-` _(32 ADRs)_ |
| `examples/with-cte/app/**` + `examples/with-enterprise-connect/app/**` + `examples/with-ipsie-session-expiry/app/**` + `examples/with-next-intl/app/**` + `examples/with-passkeys/app/**` + `examples/with-passwordless-db/app/**` + `examples/with-passwordless/app/**`<br>`examples/with-cte/app/api/stt/**` + `examples/with-dpop/lib/**` + `examples/with-mrrt/lib/**`<br>`examples/with-cte/**` + `examples/with-dpop/**` + `examples/with-mrrt/**`<br>`examples/with-enterprise-connect/lib/**` + `examples/with-passwordless/app/server-passwordless/**`<br>`examples/with-passkeys/components/**` + `examples/with-passwordless/app/server-passwordless/**` | `examples-` _(30 ADRs)_ |
| `docs/assets/**` | `docs-assets-` _(15 ADRs)_ |
| `src/server/**` | `server-` _(11 ADRs)_ |
| `src/client/**` | `client-` _(10 ADRs)_ |
| `examples/with-next-intl/app/**` | `examples-with-next-intl-app-` _(6 ADRs)_ |
| `src/utils/**` | `utils-` _(6 ADRs)_ |
| `src/server/session/**` | `server-session-` _(6 ADRs)_ |
| `src/errors/**` | `errors-` _(5 ADRs)_ |
<!-- actual-ai:adr-governance:end -->

# AGENTS.md

**SDK:** `@auth0/nextjs-auth0`  
**Purpose:** Auth0 authentication for Next.js (App Router + Pages Router)  
**Runtime:** Node 20+, ESM, TypeScript

---

## Quick Commands

| Task | Command |
|------|---------|
| Install | `pnpm install` |
| Build | `pnpm run build` |
| Test unit | `pnpm test:unit` |
| Test e2e | `pnpm test:e2e` |
| Lint + typecheck | `pnpm run lint` |
| Generate docs | `pnpm run docs` |

---

## Package Exports

| Import Path | Contents |
|-------------|----------|
| `@auth0/nextjs-auth0` | Client: `useUser`, `getAccessToken`, `Auth0Provider`, `withPageAuthRequired` |
| `@auth0/nextjs-auth0/server` | Server: `Auth0Client`, `AbstractSessionStore`, `TransactionStore` |
| `@auth0/nextjs-auth0/errors` | Error classes: `SdkError`, `AccessTokenError`, `AuthorizationError`, etc. |
| `@auth0/nextjs-auth0/types` | TypeScript types only: `SessionData`, `User`, `TokenSet` |
| `@auth0/nextjs-auth0/testing` | Test utilities: `generateSessionCookie` |

---

## Architecture

```
src/
├── client/           # React hooks, Auth0Provider, client getAccessToken
│   ├── hooks/        # useUser
│   ├── helpers/      # getAccessToken, withPageAuthRequired
│   └── providers/    # Auth0Provider
├── server/           # Auth0Client (public API), AuthClient (internal)
│   ├── session/      # Stateless (cookie) + Stateful (external store)
│   ├── helpers/      # withPageAuthRequired, withApiAuthRequired
│   ├── client.ts     # Auth0Client - main public class
│   └── auth-client.ts # Internal route handling + OAuth flows
├── errors/           # SdkError hierarchy (catch by error.code)
├── types/            # SessionData, User, TokenSet, AuthorizationParameters
├── utils/            # Internal: dpop, paths, scopes, urls
└── testing/          # generateSessionCookie for test session setup
```

---

## Data Flows

Legend: `→` flow, `↔` bidirectional, `[]` storage, `{}` transform

| Flow | Path |
|------|------|
| Login | Browser→`/auth/login`→Auth0`/authorize`→`/auth/callback`→{tokenSet}→[session cookie]→redirect |
| Logout | Browser→`/auth/logout`→[clear session]→Auth0`/oidc/logout`→redirect |
| getSession | [cookie]→{decrypt}→SessionData |
| getAccessToken | [session]→?expired→Auth0`/oauth/token`→{refresh}→[session update]→token |
| getAccessToken (client) | Browser→`/auth/access-token`→[session]→token |
| useUser | Browser→`/auth/profile`→[session]→User |
| Stateful session | [cookie:sid]↔[external store:SessionData] |

See [EXAMPLES.md](EXAMPLES.md) for detailed flow implementations.

---

## Key Patterns

### Public API Surface

| Class/Function | Location | Purpose |
|----------------|----------|---------|
| `Auth0Client` | `./server` | Main SDK entry, instantiate once per app |
| `useUser()` | `./client` | React hook for authenticated user |
| `getAccessToken()` | `./client` | Client-side token retrieval |
| `Auth0Provider` | `./client` | Context provider wrapping app |
| `withPageAuthRequired` | `./client` or `./server` | Page protection HOC |

### Session Storage

| Mode | Implementation | When |
|------|----------------|------|
| Stateless (default) | Encrypted cookie | No external deps |
| Stateful | Custom `SessionDataStore` | Large sessions, server-side revocation |

### Multi-Resource Refresh Tokens (MRRT)

- Multiple access tokens stored per audience in `session.accessTokens[]`
- Automatic token refresh per audience

### DPoP (Demonstrating Proof-of-Possession)

- Optional, requires `dpop.enabled: true` + key pair config
- Tokens bound to cryptographic proof

### Hooks

| Hook | Trigger |
|------|---------|
| `beforeSessionSaved` | Before session persisted, modify session data |
| `onCallback` | After OAuth callback, customize redirect/session |

---

## Error Handling

Base class: `SdkError` with `code: string` property.

| Error Class | Code | Cause |
|-------------|------|-------|
| `AccessTokenError` | `access_token_error` | Token fetch/refresh failure |
| `AuthorizationError` | `authorization_error` | OAuth authorize failure |
| `InvalidConfigurationError` | `invalid_configuration` | Bad SDK config |
| `DiscoveryError` | `discovery_error` | OIDC discovery failed |
| `OAuth2Error` | varies | Auth0 callback error (may contain user input) |

**Pattern:** Catch by `error.code`, not `instanceof`.

---

## Environment Variables

### Required

| Variable | Purpose |
|----------|---------|
| `AUTH0_DOMAIN` | Auth0 tenant domain |
| `AUTH0_CLIENT_ID` | Application client ID |
| `AUTH0_CLIENT_SECRET` | Application client secret |
| `AUTH0_SECRET` | Session encryption key (min 32 chars) |
| `APP_BASE_URL` | Application base URL |

### Optional

| Variable | Purpose |
|----------|---------|
| `AUTH0_COOKIE_*` | Cookie configuration overrides |
| `AUTH0_DPOP_*` | DPoP configuration |
| `NEXT_PUBLIC_*_ROUTE` | Custom route paths |

---

## Testing

### Unit Tests

- Framework: Vitest, co-located `*.test.ts` in `src/`
- Run: `pnpm test:unit`

### Flow Tests (`*.flow.test.ts`)

Black-box tests. MSW mocks HTTP only, SDK called normally. No other mocks unless required.

---

## CI/Validation Pipeline

```bash
pnpm run test:coverage && pnpm run prepack && pnpm run lint:fix
```

E2E runs separately, requires credentials.

---

## Peer Dependencies

| Package | Versions |
|---------|----------|
| `next` | ^14.2.35 \|\| ~15.x \|\| ^16.0.10 |
| `react` | ^18.0.0 \|\| ~19.x |
| `react-dom` | ^18.0.0 \|\| ~19.x |

---

## File Conventions

| Pattern | Purpose |
|---------|---------|
| `*.test.ts` | Unit test, co-located with source |
| `*.flow.test.ts` | Integration/flow tests |
| `*.msw.test.ts` | Tests using MSW mocking |

---

## Key Files

| File | Purpose |
|------|---------|
| [src/server/client.ts](src/server/client.ts) | `Auth0Client` implementation |
| [src/server/auth-client.ts](src/server/auth-client.ts) | Internal OAuth/route handling |
| [src/client/hooks/use-user.ts](src/client/hooks/use-user.ts) | `useUser` hook |
| [src/errors/index.ts](src/errors/index.ts) | All error class definitions |
| [EXAMPLES.md](EXAMPLES.md) | Usage patterns and code samples |

---

## Anti-Patterns

- ❌ Importing from internal paths (`src/server/auth-client.ts`)
- ❌ Using `instanceof` for error handling (use `error.code`)
- ❌ Storing sensitive data in client-accessible session fields
- ❌ Calling `getAccessToken()` without checking user authentication first
