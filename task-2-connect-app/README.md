# Task 2: Gmail Connector (Read-Only)

**App chosen:** Gmail

**Why Gmail (and not alternatives):**
- **Bank/card API (e.g., Plaid)** — richer data, but requires linking a
  financial account directly; too high-risk a permission for a v1 tool.
- **Manual CSV upload** — zero connector value, defeats the purpose of Task 2.
- **Calendar** — some services put renewal reminders there, but coverage is
  inconsistent and unreliable as a primary source.

Gmail was chosen because nearly every subscription service sends a
confirmation, receipt, or renewal-reminder email — the most complete,
universally available signal without touching financial accounts.

## Permission Scope
- **Access level:** Read-only (`gmail.readonly`)
- **What is accessed:** Search results and message bodies matching
  subscription-related queries ("receipt," "your subscription," "renewal,"
  "payment confirmation") within a bounded window (last 90 days)
- **What is NOT accessed:** Send, delete, or modify permissions; contacts;
  attachments beyond what's needed to extract price/date text

## How the AI Retrieves Meaningful Information
1. Search Gmail for defined subscription-signal keywords within the lookback window.
2. Extract: sender/service name, amount, billing frequency, next renewal date.
3. Deduplicate — multiple emails from the same service collapse into one
   line item, keeping the most recent charge and next renewal date.
4. Pass the normalized list into the Subscription ROI Auditor Skill.

## Test Cases
| # | Scenario | Expected Result |
|---|---|---|
| 1 | Inbox has clear receipts from 5 known services | All 5 correctly extracted |
| 2 | Same service under two display names | Deduplicated into one line item |
| 3 | Email mentions a price but it's a one-time purchase | Excluded, noted as filtered out |
| 4 | No qualifying emails found | Skill reports "none found," doesn't fabricate |
| 5 | Promotional email uses subscription-like language | Correctly excluded via sender/amount validation |

## Verification Process
Cross-checked 3 extracted line items against the actual Gmail messages
side-by-side — amounts and dates matched exactly before trusting the full audit.

## Security Implications
- Read-only limits blast radius — no risk of sending/deleting/altering email.
- Email bodies may contain adjacent PII (addresses, partial card digits) —
  Skill should extract only service/amount/date, nothing else.
- Access should be session-scoped, not a standing background sync.
- Revocable anytime via the user's Google Account permissions page.

## Potential Failure Cases
- Bundled brand names under a parent company may be missed by keyword search.
- Emails outside the lookback window are missed, understating subscription count.
- Forwarded (vs. original) emails may lack structured pricing data.

**One-sentence access summary:** *I gave the AI read-only access to search
and read my Gmail for billing-related emails — it cannot send, delete, or
change anything.* Write access would only ever be needed for a future,
separately-approved "draft a cancellation email" feature.
