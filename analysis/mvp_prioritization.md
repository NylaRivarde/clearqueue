# MVP Prioritization — ClearQueue

Using **MoSCoW** (already applied per-requirement in the [Requirements Matrix](../requirements/requirements_matrix.md)), this document explains the *reasoning* behind what belongs in an MVP versus later phases — not just the label.

## MVP Definition: What "Minimum" Means Here

The MVP is scoped to answer one question well: ***what needs my attention today, and why?*** for a single underwriter. Everything in the MVP either directly answers that question or is required infrastructure to make the answer trustworthy (data freshness, correct scoping to the right user). Everything else — team/regional aggregation, renewal look-ahead, account drill-down — is valuable, but is a *second* question, and bundling every valuable idea into "MVP" is how visibility tools become the next fragmented dashboard nobody trusts.

## In the MVP

| Capability | Why It's MVP, Not Later |
|---|---|
| **My Attention Queue** (FR-01, FR-03) | This is the core product. Without it, there is no product — every other view is an extension of "what needs attention," and this is where that question gets answered first, for the person who needs it most urgently: the underwriter themselves. |
| **Attention Score with visible "why" reason** (FR-08) | The differentiator that separates this from "a filtered spreadsheet." Deferring it would ship a product indistinguishable from existing manual tracking with a nicer UI — the exact outcome the original business problem (fragmented, low-trust visibility) is trying to escape. |
| **Data freshness indicator** (NFR-01) | Without a visible "last updated," any stale data undermines trust in everything else the product does. This is cheap to build and expensive to skip. |
| **Role-scoped access** (NFR-02) | An underwriter must only ever see their own book by default. This isn't a nice-to-have permission model — showing the wrong data to the wrong person is a trust-destroying failure mode, not a missing feature. |

## Should-Have (Fast Follow, Not MVP)

| Capability | Why It Waits |
|---|---|
| **Team View** (FR-04) | Valuable to managers, but the manager's problem (manual Excel rollups) is a *downstream* consequence of the underwriter-level visibility problem. Solve the root first; the team rollup becomes straightforward once the underlying per-item data model and scoring already work. |
| **Regional Roll-Up** (FR-05) | Same logic as Team View, one level further removed from the daily user. Also carries more organizational complexity (who has access to which region) that shouldn't block the core product from shipping. |
| **Renewal Radar** (FR-06) | Genuinely useful, but it's a specialized *view* of data the MVP already has to collect (renewal date, outstanding item). Once My Attention Queue exists, Renewal Radar is mostly a different sort/filter on the same data — low-risk to add second. |
| **Account 360** (FR-09) | Deliberately scoped as information-architecture-only in this version (see [Account 360 IA](../prototype/account_360_ia.md)) specifically *because* it's valuable enough to deserve real design work, not a bolt-on. Building it prematurely — before validating what the queue itself gets right or wrong — risks designing the wrong drill-down screen. |

## Could-Have

| Capability | Why It's Optional |
|---|---|
| **Export to CSV/PDF** (FR-07) | Useful bridge for stakeholders not yet using the tool directly, but it's a workaround for incomplete adoption, not a core capability. If the tool is trusted, export need matters less over time. |
| **Change auditability / timestamps** (NFR-04) | Valuable for process analysis and trust, but not required to deliver the core "what needs attention" value on day one. |

## Won't-Have (This Version)

| Capability | Why It's Explicitly Out |
|---|---|
| **Historical trending** (DR-03) | Requires a data retention/history strategy this concept hasn't designed. Point-in-time visibility solves the immediate problem; trending is a legitimate Phase 2 ask once the retention approach is deliberately designed rather than bolted on. |
| **Any risk-selection, pricing, or underwriting-guideline feature** | Explicitly out of scope for the product as a whole, not just this version — see [Account 360 IA — What ClearQueue Is Not](../prototype/account_360_ia.md#what-clearqueue-is-not). Adding these would change what kind of product this is. |
| **Attention Score auto-tuning / machine learning** | The model is deliberately rule-based and transparent (see [Attention Score Model](attention_score_model.md)). Introducing ML would trade explainability — the entire point of the model — for a marginal accuracy gain that hasn't even been shown to be needed yet. |

## The One-Sentence Test

Every "in MVP" row above passes this test: *if we shipped only this, would an underwriter's daily "what do I work on" question be meaningfully easier to answer than it is today, using existing fragmented tools?* Team View, Regional Roll-Up, Renewal Radar, and Account 360 are all "yes, and" additions — genuinely valuable, but each answers a *different* question than the one the MVP is scoped to answer first.
