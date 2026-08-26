# Account 360 — Information Architecture (Concept)

**Status:** Information architecture only. Not yet wired into the dashboard mockup beyond an entry-point link ("Account 360 →") on each queue row. Deliberately not designed as a full screen yet — see [Refine Underwriter360](../README.md) for why: the goal at this stage is to decide *what belongs here and why*, before designing pixels.

## Why This Screen Exists — and Why the Product Is Named After It

**My Attention Queue** answers "what needs my attention across my whole book?" It is intentionally thin — one row per account, just enough to triage.

Once an underwriter clicks into a specific account, they need the opposite: everything relevant about *that one account*, assembled in one place, instead of pulled from the submission file, the SOV, an inspection report, prior correspondence, and the issuance tracker separately. That consolidation — one account, every system's worth of relevant status, one screen — is the "360" the product is named for. My Attention Queue is the triage layer; Account 360 is where the actual decision gets made.

## Design Principle

Every section on this screen has to answer one of:
1. What is this risk? (COPE / property characteristics)
2. Where does it stand right now? (workflow status)
3. What's blocking it and who owns the next move?
4. What's coming up that I need to plan around?

If a candidate field doesn't answer one of those four questions for *this specific account*, it doesn't belong on Account 360 — it either belongs in the source system of record, or it doesn't belong in Underwriter360 at all.

## Proposed Sections

### 1. Account Snapshot (header)
Account name, occupancy type, region, underwriter/UA of record, transaction type (new business/renewal/endorsement), current Attention Score with its factor breakdown (not just the number — see [Attention Score Model](../analysis/attention_score_model.md)), and Account Significance (TIV band) shown as its own labeled figure next to — never merged into — the score. This is where the "two separate signals" principle from the Attention Score model is most visible: urgency and business significance sit side by side, not blended.
*Answers: what is this, how urgent is the open work, and how significant is the account — as two separate answers, not one.*

### 2. Risk Characteristics (COPE Summary)
Construction type, occupancy detail, protection class, sprinkler status, building age, TIV band, wind/hail exposure tier, flood zone. Presented as a compact summary, not a full copy of the submission file — enough for the underwriter to recall the risk without reopening the original submission.
*Answers: what is this risk, at a glance, without re-reading the file.*

### 3. Workflow Status
Current policy status, days outstanding, target vs. actual issuance date, and — critically — the specific outstanding item and its recommended next action (the same fields already surfaced in the queue, shown in full here rather than truncated).
*Answers: where does this stand, and what happens next.*

### 4. Next Action & Ownership
Who owns the next step (underwriter, UA, broker/agent, client, or loss control/inspector), with a way to see how long it's been sitting with that owner. This is where a manager reviewing an escalated account would look first.
*Answers: who do I need to follow up with, and have they had it too long.*

### 5. Renewal & Timeline Context
Renewal date (if applicable) and how it relates to the current outstanding work — e.g., a renewal 7 days out that still has an open blocker is a materially different situation than a renewal with nothing outstanding. This is the same cross-reference the Renewal Radar panel already surfaces at the queue level; Account 360 is where it's shown in full context for one account.
*Answers: what's coming up that changes how urgently I should act.*

## Explicitly Deferred (Not in Account 360 v1)

These were considered and set aside for this version — not rejected, just not justified yet without real user validation:

- **Full document viewer** (SOV files, inspection reports, correspondence) — valuable, but a much larger integration problem than a status/visibility layer should take on first. Underwriter360 links out to the system of record rather than replacing it.
- **Loss history / prior term detail** — genuinely useful for renewals, but requires a data source this concept hasn't assumed access to. Flagged as a Phase 2 candidate in the [Roadmap](../roadmap/product_roadmap.md).
- **Broker relationship / performance data** — interesting context, but out of scope until the core visibility problem is solved.

## What Underwriter360 Is Not

Because Account 360 surfaces COPE risk characteristics (construction, occupancy, protection, exposure), it's worth being explicit about a boundary: **Underwriter360 is not a risk-selection or pricing tool.** It does not score risk quality, recommend accept/decline decisions, calculate premium, or enforce underwriting guidelines. COPE fields appear here for exactly one reason — they give the underwriter enough context to recall *what this risk is* while acting on a workflow item, the same way glancing at a submission's cover sheet would. If a field doesn't serve that recall purpose, it doesn't belong here, no matter how standard it is in property underwriting generally. Every COPE field kept in the synthetic dataset was checked against this test — see the field-by-field reasoning in [data_dictionary.md](../data/data_dictionary.md).

## Relationship to the Rest of the Product

| Screen | Scope | Core Question |
|---|---|---|
| My Attention Queue | Every open item across one underwriter's book | What needs my attention today, across everything I own? |
| Team View | Every open item across a manager's team | Where are the bottlenecks on my team? |
| Regional Roll-Up | Every open item across a region | What does the region need to know, live? |
| Renewal Radar | Upcoming renewals, cross-referenced with open blockers | What's coming up that I need to get ahead of? |
| **Account 360** | **Everything relevant to one account** | **What's the full picture on this one account, and what should happen next?** |
