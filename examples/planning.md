# Example: Planning

Task given to the agent: *"Add rate limiting to our API."*

## Bad plan

```
Plan:
1. Research rate limiting best practices
2. Implement rate limiting middleware
3. Add configuration
4. Test everything
5. Update documentation

I'll start by adding a rate limiter to the API. Should I use Redis or
in-memory? What limits do you want? Should it apply to all endpoints?
Do you want per-user or per-IP? Let me know and I'll get started!
```

**Why it fails:** No code was read before planning -- this could be written for any repo on earth. Steps are labels, not actions ("implement middleware", "test everything" -- verifiable how?). Every question asked is answerable from the codebase (is Redis already a dependency? is there existing middleware? are users authenticated?). No risks, no done-when. And it ends by blocking on the user instead of proceeding (violates `07` section 1.1 and Constitution Art. VII).

## Good plan

```
Read: src/middleware/ (auth.ts shows the middleware chain pattern),
src/config/index.ts, docker-compose.yml (Redis already runs for sessions),
src/routes/ (14 routes; 3 are unauthenticated: /login, /signup, /health).

Plan -- add rate limiting to the public API:

Scope IN: per-user limits on authenticated routes, per-IP on /login and
/signup. Scope OUT: /health (monitoring would trip it), admin routes
(internal network only), and any UI for limit configuration.

1. Add sliding-window limiter backed by the existing Redis instance
   (new src/middleware/rateLimit.ts, following auth.ts's middleware shape).
   Verify: unit tests for window math, including clock-edge cases.
2. Wire into the chain after auth (so user ID is available), with per-route
   config in src/config. Verify: integration test -- 429 after N requests,
   Retry-After header present, window resets.
3. Fail-open on Redis outage, with a warn log. Rationale: availability
   over strictness for this product; flag if you'd rather fail closed.
   Verify: test with Redis stopped.

Risks: shared Redis -- limiter keys get their own prefix + TTL so session
data can't collide; login limiter must count failures per-IP+username to
blunt credential stuffing without letting one IP lock out a shared office.

Done when: integration tests pass, /health unlimited, README's API section
documents the limits and 429 contract.

Assumption (proceeding, reversible): default 100 req/min per user, 10/min
per IP on auth endpoints -- easily changed in config if you want different
numbers.
```

**Why it works:** Reading came first, and it shows -- the plan cites the actual middleware pattern, the existing Redis, the real route inventory. Every step carries its own verification. Scope is bounded in both directions. Risks are specific to *this* codebase. The one genuine judgment call (fail-open vs. fail-closed) is flagged rather than hidden, and the guessable parameter is taken as a stated reversible assumption instead of a blocking question (`07` section 1.4).
