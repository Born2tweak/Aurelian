# Example: Code Review

PR under review: "Add password reset via email" (+412 / -18, touches auth routes, mailer, user model).

## Bad review

```
LGTM overall, nice work! success

A few nits:
- line 34: prefer const over let
- the function name `sendResetMail` could be `sendResetEmail` for consistency
- maybe add a comment explaining the token logic?
- consider extracting the email template to its own file

Approving, feel free to address in a follow-up.
```

**Why it fails:** It reviewed the *style* of a security-critical diff and approved it. Nothing about token generation, expiry, or invalidation; nothing about enumeration; nothing about rate limiting -- on a password reset flow, these are the entire review (`../core/03_EXECUTION_ENGINE.md` section 7.2 puts security immediately after correctness). "Maybe add a comment explaining the token logic" reveals the reviewer didn't understand the token logic -- which is precisely the moment to dig, not to shrug. Approval with unexamined risk is the "vague approval" the Reviewer skill forbids.

## Good review

```
Findings, by severity:

BLOCKER -- auth/reset.ts:41 -- reset token is Math.random().toString(36).
Not cryptographically secure; tokens are guessable. Use
crypto.randomBytes(32) and store only a hash of the token (treat it like
a password -- a DB read replica leak currently yields valid reset links).

BLOCKER -- auth/reset.ts:67 -- token has no expiry and survives use.
Add expires_at (<=1h) and delete on successful reset. Also invalidate all
outstanding tokens on password change, or an old email link can undo a
user's recovery.

MAJOR -- routes/auth.ts:88 -- response differs for unknown emails ("no
account found" vs "email sent"). Account enumeration. Return the same
response and status either way; do the existence check silently.

MAJOR -- routes/auth.ts:82 -- no rate limit on the request endpoint. One IP
can flood a victim's inbox and burn mailer quota. The middleware from
src/middleware/rateLimit.ts fits here (per-IP + per-target-email).

MINOR -- mailer/templates.ts:12 -- reset URL built by string concat with
user-supplied redirect param; validate against an allowlist or drop the
param (open-redirect via reset email).

CONSIDER -- user.model.ts:104 -- resetToken lives on the user row; a
separate table would let you keep an audit trail and expire in bulk.
Fine either way for now.

Verified: read the full diff plus routes/auth.ts and the mailer; ran the
new tests (11 pass) -- note none cover expiry or reuse; blockers above
need tests demonstrating both.

Must fix before merge: the two blockers + both majors. The rest at your
discretion.
```

**Why it works:** Findings first, severity-ordered, every one grounded in file:line with the concrete break *and* a suggestion (`../skills/05_SKILLS_LIBRARY.md` Reviewer output format). It reviewed the diff **and its context** -- the rate-limit middleware suggestion comes from knowing the surrounding codebase. Threat reasoning is specific (read-replica leak, inbox flooding, open redirect), not generic "improve security." It states what was actually verified -- including the gap in the submitted tests -- and draws a clean must-fix/consider line so the author knows exactly what blocks the merge.
