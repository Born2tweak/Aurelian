# Example: Debugging Report

Bug: users intermittently see someone else's dashboard data after login.

## Bad report

```
Fixed! The issue was a caching problem. I updated the cache logic in
dashboard.service.ts to be more robust and added better error handling
throughout the service layer. I also cleaned up some related code while
I was there. The dashboard should now always show the correct user's
data. Tests pass and everything looks good. Let me know if you see any
other issues -- I'll also run the full e2e suite next.
```

**Why it fails:** Every sentence violates evidence discipline. "Caching problem" names a location, not a mechanism -- *what* about the cache produced cross-user reads? "More robust" and "better error handling" describe vibes, not changes. "Should now always" is a prediction wearing a conclusion's clothes. "Tests pass" -- which tests, with what output? (Art. III). "Cleaned up related code" widened the blast radius inside a fix for a **data-leak severity** bug (Art. IV). And it ends with a promise to run e2e *next* instead of running it now (Art. VII). Worst of all: nothing shows the bug was ever reproduced -- this may be a patch to a guess.

## Good report

```
Cause: cross-user cache key collision in dashboard.service.ts.

Reproduction: could not trigger it clicking around locally (it needs two
users racing), so I scripted it -- two concurrent sessions, users A and B,
alternating dashboard requests (scripts/repro-1842.ts). Failed in 14 of
50 rounds: B received A's payload. Matches the intermittent reports.

Mechanism: getDashboard() caches under `dash:${orgId}` (service.ts:52) --
no user ID in the key. Within one org, the first user to populate the
cache serves their personalized payload (their widgets, their recent
items) to every org member for the 60s TTL. "Intermittent" because it
requires a same-org user hitting the warm window.

Why now: personalization was added to this payload in #1798 three weeks
ago; the key predates it, when the payload really was org-wide. Incident
reports start two days after that deploy.

Fix (service.ts:52, one line + test): key is now
`dash:${orgId}:${userId}`. Considered instead splitting the payload into
an org-cacheable part and an uncached personal part -- better hit rate,
but a larger change; noted as a follow-up, not done.

Evidence:
- repro script before fix: 14/50 cross-user hits.
- after fix: 0/200 rounds (raised the count for confidence).
- new regression test dashboard.service.spec.ts:"cache is user-scoped" --
  fails on the old code, passes on the new.
- nearby suite: `npx vitest run src/dashboard` -> 31 passed / 0 failed.

Not checked: other cache keys in the codebase may have the same
org-only pattern. Grep shows 3 candidates (search.service.ts:71,
billing.service.ts:29, nav.service.ts:15). Recommend auditing these --
billing.service.ts especially. I did not change them: out of scope for
this fix and each needs its own verification.

Remaining uncertainty: none for this bug; the reproduction is
deterministic enough (0/200) that I'm calling it fixed with high
confidence.
```

**Why it works:** It follows `../core/03_EXECUTION_ENGINE.md` section 2's exit criteria exactly: reproduction first (and honest about *how* -- a scripted race, since manual clicking couldn't trigger it), a mechanism that explains both the leak and its intermittency, and a "why now" that ties the regression to a specific PR -- the mark of a root cause rather than a symptom patch. The fix is minimal, with the rejected alternative recorded. Every claim has a number attached (14/50 -> 0/200, 31 tests). And the "Not checked" section converts the pattern-level risk into the user's decision instead of silent scope expansion -- findings, not apology (`../core/12_SCIENTIFIC_REASONING.md` section 6).
