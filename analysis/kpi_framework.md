# KPI Framework — Underwriter360

Proposed success measures if Underwriter360 were actually implemented. **These are not real results.** This portfolio concept has not been built, piloted, or measured — there is no employer data, no adoption rate, and no before/after comparison behind any number here. What follows is a framework for *how* the product's impact would be evaluated, not a report of impact that occurred.

For each KPI: what it measures, why it matters, how it could be calculated, and what business question it answers.

## Workflow Visibility & Speed

### 1. Median Days Outstanding (Open Book)
- **What it measures:** the midpoint of `Days_Outstanding` across all open items on a book, team, or region.
- **Why it matters:** this is the most direct measure of whether work is moving or stalling. A rising median signals growing backlog before it becomes a crisis.
- **How it could be calculated:** `MEDIAN(Days_Outstanding)` across open records, filterable by underwriter/team/region/occupancy type.
- **Business question it answers:** *Is our open work moving at a healthy pace, or backing up?*

### 2. % of Open Items Past Target Issuance Date
- **What it measures:** share of open items where the as-of date has passed `Target_Issuance_Date`.
- **Why it matters:** directly measures whether the team is meeting its own internal service expectations — the clearest "are we on track" signal available without external SLA data.
- **How it could be calculated:** `COUNT(open items where AsOfDate > Target_Issuance_Date) / COUNT(open items)`.
- **Business question it answers:** *How much of our current book has already missed its own target?*

### 3. Aging Distribution (0–5 / 6–10 / 11–15 / 16–30 / 30+ days)
- **What it measures:** the shape of the open book across aging buckets, not just an average.
- **Why it matters:** an average can hide a long tail of severely aged items. The distribution shows whether a backlog is broadly aging or concentrated in a few badly stuck accounts.
- **How it could be calculated:** count of open items per `Aging_Bucket`, viewable by team/underwriter.
- **Business question it answers:** *Is our backlog a few outliers, or a systemic slowdown?*

## Prioritization & Ownership

### 4. Attention Score Distribution (High / Medium / Low)
- **What it measures:** the proportion of the open book in each Attention Score band.
- **Why it matters:** tracks overall workload pressure over time, and — combined with KPI 6 below — is one of the inputs into validating whether the score itself is calibrated correctly.
- **How it could be calculated:** count of open items per `Priority` band, from the [Attention Score Model](attention_score_model.md).
- **Business question it answers:** *How much of our open work is genuinely urgent right now, versus routine?*

### 5. % of Open Items Where the Underwriter Is the Next-Action Owner
- **What it measures:** share of open items where `Next_Action_Owner` = Underwriter.
- **Why it matters:** distinguishes "I'm the bottleneck" work from "I'm waiting on someone else" work — a manager reviewing this can tell whether a backlog is an underwriter capacity problem or a broker/client responsiveness problem.
- **How it could be calculated:** `COUNT(Next_Action_Owner = "Underwriter") / COUNT(open items)`, by underwriter.
- **Business question it answers:** *Is our open work stuck with us, or stuck with someone else?*

### 6. Attention Score Override / Disagreement Rate *(requires a working pilot — not measurable from static data)*
- **What it measures:** how often a user manually reprioritizes an item away from its model-suggested rank.
- **Why it matters:** the single most important signal for whether the [Attention Score Model](attention_score_model.md) is actually trustworthy — a model users constantly override is a model that needs re-tuning, not a model users have adopted.
- **How it could be calculated:** `COUNT(manual overrides) / COUNT(items viewed)` over a rolling window, once the product supports the interaction.
- **Business question it answers:** *Do underwriters actually agree with what the model tells them to prioritize?*

## Renewal & Continuity

### 7. Renewals With an Open Blocker Inside the Look-Ahead Window
- **What it measures:** count of upcoming renewals (within e.g. 30 days) that also have a non-"None" `Outstanding_Item`.
- **Why it matters:** this is the highest-risk combination in the workflow — a renewal that could lapse or get delayed because of an unresolved blocker. It's the exact scenario the Renewal Radar concept exists to surface early.
- **How it could be calculated:** `COUNT(Renewal_Date within window AND Outstanding_Item != "None")`.
- **Business question it answers:** *Which upcoming renewals are actually at risk, not just approaching?*

## Team & Regional Distribution

### 8. Open Item Count and Aging by Underwriter/UA
- **What it measures:** workload distribution across a team.
- **Why it matters:** the single view a manager currently has to rebuild manually in Excel — a KPI here means eliminating that manual step, not producing a new number.
- **How it could be calculated:** count and average `Days_Outstanding` of open items, grouped by `Underwriter`/`Underwriting_Assistant`.
- **Business question it answers:** *Is work distributed evenly across the team, or concentrated on a few people?*

## What Is Deliberately Not Here

- **Any productivity, cost-savings, or time-savings figure.** No such figure exists for this concept, and none is estimated here — see the truthfulness note at the top of this file and in [README.md](../README.md).
- **Loss ratio, premium growth, or retention metrics.** These are legitimate underwriting business outcomes, but Underwriter360 is a workflow visibility tool, not a pricing or risk-selection tool (see [Account 360 IA — What Underwriter360 Is Not](../prototype/account_360_ia.md#what-underwriter360-is-not)). Attributing loss-ratio movement to a visibility dashboard would overstate what this kind of tool can plausibly claim credit for.
- **Adoption rate.** Genuinely important for a real rollout, but listed in [Risks & Constraints](../README.md#risks--constraints) as a risk to manage rather than a KPI to report before the product exists.
