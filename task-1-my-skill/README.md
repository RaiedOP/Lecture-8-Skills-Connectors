# Task 1: Subscription ROI Auditor Skill

**Problem:** People pay for subscriptions they don't use, but auditing this
requires manually cross-referencing statements against memory — nobody does
it regularly.

**Target user:** Anyone with 4+ recurring subscriptions (professionals, small
business owners, students).

**Why existing methods fail:** Bank statements show charges, not usage. No
single view connects "what I'm paying" to "what I'm actually getting value
from." Budgeting apps total spend but don't reason about worth.

**Why AI helps:** Requires judgment (cost-per-use math, flagging overlaps,
tiered verdicts) — not just formatting a list.

**Prompts used:**
1. Initial: "Build a skill that audits my subscriptions against usage and
   tells me what to cancel."
2. Refined: added a fixed table format, verdict categories, and a
   no-moralizing constraint after the first test output felt preachy
   ("you're wasting money on this").

**Testing:** Ran with a real 6-subscription list (see sample conversation in
SKILL.md). Confirmed consistent table format and verdict logic across 3
separate chats using different phrasing ("check my subs" / "am I wasting
money on apps" / a pasted statement) — screenshots in this folder.

**Result:** Triggers reliably from natural phrasing, no special command
needed, and produces a consistent, decision-ready table every time. This is
a skill I'll keep using monthly.
