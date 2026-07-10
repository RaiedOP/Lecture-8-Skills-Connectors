# Project Report: Subscription ROI Auditor

## Task 1 — Skill
**Objective:** Turn subscription spend review into a repeatable AI task.
**Problem:** Manual cross-referencing of statements vs. usage is tedious, so
it's rarely done consistently.
**AI tools used:** Claude, skill-creator
**Approach:** Built SKILL.md with a fixed table output, verdict logic (Keep/
Downgrade/Cancel/Investigate), and a one-clarifying-question-max rule.
**Prompt iterations:** Started generic ("audit my subscriptions"), refined
to add a strict table format and remove guilt-inducing tone after the first
test read as preachy.
**Testing:** 3 separate chats, different phrasing, consistent output confirmed.
**Challenges:** Initial version moralized too much ("you're wasting money on
this") — fixed by adding a neutral-tone instruction.
**Result:** A reliable, natural-language-triggered skill I'll keep using monthly.
**Why this skill:** Almost everyone has subscription creep; this closes a gap
no budgeting app currently reasons about — value, not just spend.

## Task 2 — Connector
**Objective:** Source real data instead of manual entry.
**Why Gmail:** Best coverage-to-risk ratio versus a bank API (too high-risk
for v1) or manual CSV (no connector value).
**Testing:** Verified 3 extracted line items against the real emails —
amounts and dates matched exactly.
**Challenges:** Some services used inconsistent sender display names,
requiring dedup logic in the extraction step.

## Task 3 — Combined Workflow
**Objective:** One sentence → full audit, no copy-paste.
**Result:** Achieved; spot-checked one line item for accuracy before
trusting the full output.

## Task 4 — Portability
**Objective:** Prove the Skill works outside its original chat.
**Result:** Ran identically in a fresh session with new sample data — no
re-explanation needed, same table format and verdict logic.

## Task 5 — Security Audit
**Objective:** A genuine risk review, not a rubber stamp.
**Result:** Low overall risk; documented the PII-exposure edge case and
recommended per-session scoping and a future write-permission gate as
improvements.

## Reflection
The hardest part was resisting scope creep on the Skill itself — early
versions tried to also give budgeting advice. Narrowing it back to
"audit only" made the output far more consistent and genuinely useful.

## Future Improvements
- Auto-draft cancellation emails (would require a separate, explicit
  write-permission opt-in)
- Track audits over time to show spend trend, not just a one-time snapshot
- Extend to bank statement data once a scoped, low-risk API option exists
