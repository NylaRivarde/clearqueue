# Attention Score Model (Proposed v1 — Unvalidated)

**Status: a product hypothesis, not a validated instrument.** Every weight in this document is a reasoned starting point, not a calibrated result. No underwriter has reviewed this model, no real workflow data has informed it, and it has not been tested against actual outcomes. Treat it the way you'd treat a first draft of a scoring rubric in a requirements review: worth debating, not worth trusting blindly.

**Purpose:** answer "what should I work on first?" with a score the underwriter can audit — because they can see exactly how it was built, and can say "that's wrong" about a specific, named part of it. That auditability is the point, more than the specific numbers.

## Why a Score At All

A flat priority label (High/Medium/Low) hides the reasoning behind it. Two "High" items can require very different handling — one is overdue, another is blocked on a third party. An underwriter juggling a full queue needs to know not just *that* something is urgent, but *why*, so they can decide whether to act personally, delegate, or chase someone else.

## The Four Factors

| Factor | Points | Logic |
|---|---|---|
| **Aging** | 0–30 | How long the item has been outstanding. `0–5 days`=0, `6–10`=8, `11–15`=15, `16–30`=22, `30+`=30. Mirrors the aging buckets used elsewhere in the product so views never disagree with each other. |
| **Deadline Pressure** | 0–30 | Position relative to the internally expected target issuance date. Overdue=30, due within 5 days=22, due within 6–15 days=12, otherwise 0. Catches urgency that pure aging misses — a new submission with an aggressive target date can need attention soon even if it isn't "old" yet. |
| **Blocking Item Severity** | 0–25 | Not all outstanding items are equal. Items requiring a third party or physical inspection that can materially delay binding — a Statement of Values, a 4-point inspection, a loss control inspection, an elevation certificate, a wind mitigation report — score 25 ("hard blockers"). Paperwork/confirmation items score 15. A pending payment scores 6. No blocker scores 0. |
| **Next-Action Ownership** | 0–15 | Whether the next step sits with the underwriter personally (15), an external party — broker, client, or loss control/inspector (10), or is already delegated to the Underwriting Assistant (8). |

**Total: 0–100.** Priority label: **High ≥ 65 · Medium 35–64 · Low < 35.**

## Why Each Factor Was Selected

- **Aging** is the baseline signal every current-state tracking method already uses informally ("how long has this been sitting"). It had to be in the model or the score wouldn't be recognizable as an improvement on what people already do.
- **Deadline pressure** exists because aging alone under-weights new-but-urgent work. A submission that arrived yesterday with a 15-day target cycle is a different problem than one that arrived yesterday with a 45-day cycle, and pure aging can't tell them apart.
- **Blocking severity** exists because "outstanding" isn't one thing. An item waiting on a scheduled physical inspection behaves completely differently from one waiting on a signature. Treating them the same would make the score less useful than an underwriter's own judgment, not more.
- **Ownership** exists because the same fact ("something is blocking this") implies a different action depending on who's holding it. An underwriter needs to know when *they* are the bottleneck, separately from knowing when someone else is.

## Why These Initial Weights (and Not Others)

The weights were chosen by engineering judgment to reflect a rough intuition — aging and deadline pressure matter most because they're time-based and compound the longer they're ignored; blocking severity matters because a hard blocker changes what "attention" even means (you can't underwrite your way past a missing inspection); ownership matters least of the four because it changes *who* acts, not *whether* something is urgent. That ordering (aging ≈ deadline > severity > ownership) is a defensible starting hypothesis, not a derived result. A different, equally defensible team could reasonably weight severity higher than aging, on the theory that a hard blocker is a harder stop than time pressure alone.

## Assumptions Being Made

- That underwriters would broadly agree with the *relative* ordering above, even before reaching agreement on exact point values.
- That "days outstanding" and "days to target" are both meaningful and worth treating as separate factors rather than collapsing into one.
- That the outstanding-item severity tiers (hard/medium/low) are correctly categorized — this is itself a judgment call worth challenging with real underwriters who know which blockers actually cause the longest real-world delays.
- That a single score per item is more useful than, say, a small set of tags ("overdue," "blocked," "your action needed") without a combined number. The scored approach was chosen because it makes a long queue sortable at a glance — but this is a hypothesis, not a proven UX preference.

## Account Significance Is Deliberately Excluded From the Score

An earlier version of this model included account size (Total Insured Value) as a fifth factor, on the theory that a larger account's delays matter more to the business. On review, that was cut. Reasoning:

- **A larger account does not make its outstanding item more urgent.** A $100M account waiting on a routine signature is not more time-critical than a $2M account that's overdue and blocked on a flood elevation certificate. Blending exposure size into the same number as workflow urgency would let a large-but-easy account outrank a small-but-genuinely-stuck one — the opposite of what a triage tool should do.
- **Workflow urgency and account significance are different questions**, and collapsing them into one opaque number would make the score *less* explainable, not more — which cuts against the entire premise of this model.
- Instead, account significance is shown as a **separate, clearly labeled signal** — a "Significant Account" badge next to the account name in the queue (driven by TIV band), with full detail in [Account 360](../prototype/account_360_ia.md). It is visible, but it never changes the Attention Score or the sort order.

This is documented here specifically because it was a real design decision, not an oversight — a plausible product could go the other way, and a future iteration might reintroduce exposure as a *separate* sort/filter option (e.g., "show me my most urgent items among my largest accounts") without ever re-merging it into the score itself.

## Displayed "Why" Reason

The queue shows one human-readable reason per item, not four raw numbers. It's selected by a fixed precedence so the most decision-relevant fact surfaces first: **overdue/near-term deadline → hard blocker → significant aging → approaching deadline → owned by the underwriter personally → moderate blocker → routine.** This precedence favors telling the underwriter what to *do* (chase a blocker, hit a deadline) over restating a number they've already seen.

## Worked Example

> **Ironwood Industries** — Bound – Pending Issuance, submitted 2026-07-12, 36 days outstanding as of the 2026-08-17 snapshot, target issuance date 2026-08-23 (6 days away — not yet overdue), blocked on an elevation certificate, owned by Broker/Agent.
>
> - Aging: 36 days → `30+ days` bucket → **30**
> - Deadline: 6 days to target (falls in the 6–15 day band, not yet overdue) → **12**
> - Blocking severity: elevation certificate = hard blocker → **25**
> - Ownership: Broker/Agent (external) → **10**
>
> **Score = 30 + 12 + 25 + 10 = 77 → High.** Displayed reason: *"Hard blocker: elevation certificate needed (flood zone)"* — of the four contributing factors, the hard blocker is what the precedence rule surfaces, because it's the most actionable fact: the underwriter immediately knows this needs a broker follow-up, not underwriting time, regardless of the exact point total.

## Deliberate Design Choices

- **No machine learning.** Every input and weight is visible and documented here. If the model misranks something, the fix is a rule change anyone can review — not a retraining exercise.
- **Ownership counts, and internal ownership counts highest.** An item sitting on the underwriter's own desk is scored *higher* than one waiting on a broker, on the theory that "only I can act on this" deserves more of my attention than "I'm waiting on someone else" — even though both may need follow-up.
- **The thresholds (65/35) are a starting proposal**, not a validated cutoff. They were tuned only so the demonstration dataset produces a plausible High/Medium/Low split.

## How This Would Be Validated With Real Underwriters

This model should not move beyond "proposed" without:

1. **Blind ranking comparison.** Take a sample of real (de-identified) open items from an underwriter's actual book. Have the underwriter rank them by gut instinct on "what would you work on first," independently of the tool. Compare that ranking to the model's output. Large disagreements are the most useful data point this process could produce.
2. **Structured factor review.** Walk through the four factors and their weights with several underwriters and a manager, specifically asking: which factor should matter more? Which outstanding items are miscategorized in severity? Is ownership weighted right, or does it not matter as much as assumed?
3. **Override tracking, if piloted.** If the tool were piloted, track how often users manually reprioritize or ignore the suggested ranking. A high override rate tied to a specific factor (e.g., users consistently bumping up items the model rates low) is a direct signal that factor's weight is wrong.
4. **Outcome tracking over time.** Once enough history exists, check whether high-scored items that got timely attention actually saw better outcomes (faster issuance, fewer escalations) than low-scored items — the real test of whether "urgent" as defined by the model matches "urgent" in practice.

## How Weighting Could Change

The weights are stored as named, isolated constants specifically so they can change without redesigning the product. Plausible outcomes of validation:

- Rebalancing point values among the four factors (e.g., if underwriters consistently say blocking severity should dominate, its share of the 100-point total could increase at aging's expense).
- Splitting "blocking item severity" into a more granular scale if three tiers proves too coarse.
- Reintroducing a size/significance dimension as a *separate sort option* rather than a score input, if users specifically ask to see it blended after using the separated version.
- Discovering the score should be replaced entirely by a simpler ranked-tag system, if the blind-ranking validation step above shows the numeric score doesn't actually match underwriter intuition any better than a simpler scheme would.

None of this can be resolved from a desk — it requires the validation steps above with real users and real workflow data, which this portfolio concept explicitly does not have access to.

## What Would Need to Happen Before This Is "Real"

Summarizing the above: underwriters and managers reviewing the ranked order against their own judgment on real (anonymized) accounts, adjustment of point values/thresholds based on that feedback, and an explicit decision about whether additional factors (e.g., broker relationship tier, prior loss history, CAT season timing) belong in the model — deliberately excluded from v1 to keep the logic auditable. See [Risks & Constraints](../README.md#risks--constraints) for how this fits into the broader set of things that would need validation before any real implementation.
