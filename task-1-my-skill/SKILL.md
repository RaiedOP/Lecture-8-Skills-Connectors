---
name: subscription-roi-auditor
description: Use when the user wants to audit subscriptions, recurring charges,
or SaaS spending. Triggers on "check my subscriptions," "am I wasting money on
apps," "should I cancel X," or pasted statements/subscription emails.
---

# Subscription ROI Auditor

## Purpose
Help the user see which recurring subscriptions are worth their cost based on
actual usage, not just list what they're paying for.

## Instructions
1. Accept a pasted statement, manual list, or forwarded emails. If usage
   frequency is missing, ask ONE question: "How often do you use each —
   daily, weekly, monthly, rarely?"
2. Normalize: service name, monthly cost (annual → monthly), usage frequency, category.
3. Calculate cost-per-use (daily≈30/mo, weekly≈4/mo, monthly≈1/mo, rare=flag).
4. Assign verdict: Keep / Downgrade / Cancel / Investigate (overlaps/duplicates).
5. Output ALWAYS in this format:

   | Service | Monthly Cost | Usage | Cost/Use | Verdict |
   |---|---|---|---|---|

   ### Recommended Actions (ranked by savings)
   ### Projected Monthly Savings: $X
   ### Projected Annual Savings: $X

6. Flag duplicate-category services explicitly (e.g., two music streaming apps).
7. Never auto-cancel or moralize — present facts neutrally, act only if asked.
8. If the user asks to act on a recommendation, offer to help (e.g., draft a
   cancellation message) as a follow-up step, not automatically.

## Edge Cases
- Non-subscription one-time charges → excluded, noted as filtered out.
- Trials converting to paid soon → flagged with the conversion date.
- Shared/family plans → note per-person cost if mentioned.
- Currency other than user's default → keep original currency, don't convert.
- Renewal within 30 days → marked urgent.

## Sample Conversation

**User:** "I feel like I'm bleeding money on apps. Netflix $15.49, Spotify
$11.99, Adobe CC $54.99, Notion $10, gym app $9.99 I never open, iCloud
$2.99. I use Netflix like twice a week, Spotify daily, Adobe maybe twice a
month for freelance work, Notion daily, gym app maybe never."

**Skill output:**

| Service | Monthly Cost | Usage | Cost/Use | Verdict |
|---|---|---|---|---|
| Netflix | $15.49 | ~8x/month | $1.94 | Keep |
| Spotify | $11.99 | Daily (~30x) | $0.40 | Keep |
| Adobe CC | $54.99 | ~2x/month | $27.50 | Downgrade — consider single-app plan (~$22.99) |
| Notion | $10.00 | Daily (~30x) | $0.33 | Keep |
| Gym App | $9.99 | ~0x | N/A | Cancel |
| iCloud | $2.99 | Ongoing/background | N/A | Keep (utility) |

### Recommended Actions (ranked by savings)
1. Cancel Gym App → save $9.99/month
2. Downgrade Adobe CC to single-app plan → save ~$32/month

### Projected Monthly Savings: $41.99
### Projected Annual Savings: $503.88

## Testing Scenarios
1. Full statement pasted with no usage info → skill asks the one usage-frequency question.
2. Partial info → infers conservatively for missing entries, notes the assumption.
3. Duplicate services (two cloud storage apps) → flagged as "Investigate."
4. Annual subscription buried in a statement → correctly converted to monthly equivalent.
5. User says "just cancel everything under $5" → skill drafts the plan only, does not auto-execute.
