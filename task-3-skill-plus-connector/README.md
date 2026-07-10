# Task 3: Combined Workflow

**Sentence used:** "Pull my subscription emails from Gmail and audit them."

## Workflow
```
User Request
   ↓
Gmail connector searches/extracts receipt & renewal emails (read-only)
   ↓
Skill normalizes data (service, cost, cadence, renewal date)
   ↓
Skill calculates cost-per-use and assigns verdicts
   ↓
Final formatted audit table + recommended actions + savings estimate
```

## Reasoning
The whole point of the Skill is catching things people forget to reconsider
— pairing it with Gmail means the audit runs on real, current billing data
instead of the user's memory of what they signed up for.

## Validation Process
Spot-checked the Adobe CC line item's price and renewal date against the
actual source email before trusting the full table — matched exactly.

## Screenshots Needed
- The one-sentence request in chat
- The connector retrieving/listing matched emails
- The final formatted audit table

## Result
One plain-English sentence produced a complete, correctly formatted audit
with no manual data entry — no copy-pasting statements or typing subscription
lists by hand.
