# Task 5: Security Audit

## Executive Summary
The Subscription ROI Auditor Skill + Gmail connector present low overall
risk. The Skill itself is pure text-processing logic with no external calls;
the connector is scoped strictly read-only.

## Purpose
Audit subscriptions using real Gmail billing data; produce keep/cancel/
downgrade verdicts and savings estimates.

## Permissions Used
- Gmail: read-only search + message read (`gmail.readonly`)
- No send, delete, modify, contacts, or calendar access
- No credential storage — auth handled by the platform's OAuth flow, not
  stored or logged by the Skill itself

## Potential Risks
- Email bodies may contain adjacent PII (addresses, partial card digits) —
  mitigated by instructing the Skill to extract only service/amount/date and
  never restate other content
- A standing/background sync (if ever enabled) would expand the exposure
  window beyond a single session — currently not implemented
- Search keyword misses (bundled/parent-company brand names) could cause
  incomplete results — low severity, availability issue not a security one

## Risk Level: **Low**

## Recommended Improvements
- Add an explicit instruction in SKILL.md to never quote unrelated PII found in emails
- Scope connector access per-session rather than persistent by default
- Require a separate, explicit confirmation step before any future
  write-permission feature (e.g., drafting cancellation emails)

## Final Verdict
**Safe to enable** for read-only use as currently scoped. Any future
expansion to write permissions should be a separate, explicitly-approved step
— not bundled into this Skill's default behavior.
