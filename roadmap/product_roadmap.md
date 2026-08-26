# Product Roadmap — Underwriter360

A proposed phasing, not a committed plan — there is no team, budget, or timeline behind this roadmap. It exists to show how the MVP reasoning in [MVP Prioritization](../analysis/mvp_prioritization.md) would extend over time, and to be explicit about what's deferred and why.

## Phase 1 — MVP: Answer "What Needs My Attention?"

**Goal:** a single underwriter can open one view and know what to work on next, and why, without checking another system or asking a colleague.

- My Attention Queue, scoped to one underwriter's book
- Attention Score (proposed v1 model) with a visible, plain-language "why" reason per item
- Data freshness indicator ("last updated")
- Role-scoped access (an underwriter sees only their own book)

**Exit criteria before moving to Phase 2:** the validation steps in [Attention Score Model — How This Would Be Validated](../analysis/attention_score_model.md#how-this-would-be-validated-with-real-underwriters) have actually happened with real underwriters, and the model/thresholds have been adjusted based on that feedback. Phase 2 should not be built on top of an unvalidated Phase 1.

## Phase 2 — Extend Visibility Up the Org

**Goal:** solve the manager and regional-leader version of the same problem, once the underlying per-item data and scoring are proven at the individual level.

- Team View (manager-level aggregation, by underwriter/UA)
- Regional Roll-Up (aggregation across teams)
- Renewal Radar (upcoming renewals cross-referenced with open blockers)
- Export to CSV/PDF for stakeholders not yet using the tool directly
- Change auditability (timestamped status/ownership changes)
- Begin historical trending (requires deliberately designing a data retention approach, not just turning on storage)

## Phase 3 — Account 360 and Deeper Decision Support

**Goal:** move from "what needs attention across my book" to "give me everything relevant when I choose to dig into one account."

- Build out Account 360 based on the [information architecture already defined](../prototype/account_360_ia.md) — Account Snapshot, Risk Characteristics (COPE Summary), Workflow Status, Next Action & Ownership, Renewal & Timeline Context
- Re-evaluate the Attention Score model based on real usage data and override patterns (see KPI 6 in the [KPI Framework](../analysis/kpi_framework.md))
- Evaluate whether a separate, explicit "account significance" sort/filter (distinct from the Attention Score itself) is worth adding, per the reasoning in the Attention Score model doc

## Future / Not Yet Scoped

Ideas that are plausible extensions but are intentionally not designed yet, because designing them now would be speculation without the validation data Phases 1–3 would produce:

- Deeper loss-history or prior-term context on renewals
- Broker-level performance or responsiveness signals feeding into prioritization
- Any proactive/predictive capability (e.g., flagging accounts likely to become blocked before they are)

**What stays constant across every phase:** Underwriter360 remains a workflow visibility and prioritization layer on top of existing systems of record — not a policy administration system, not a risk-selection or pricing tool. See [Account 360 IA — What Underwriter360 Is Not](../prototype/account_360_ia.md#what-underwriter360-is-not).
