# Underwriter360

**A workflow visibility and prioritization concept for commercial property underwriting, built as a Business Analyst / Product portfolio case study.**

> Fragmented underwriting workflows make it hard to know what needs attention. Underwriter360 consolidates workflow signals into a prioritized attention queue, explains *why* an item is ranked, names who owns the next action, and offers a deeper account view when you need it.

This is a proposed concept, not a shipped product. I designed it independently, drawing on my own experience in commercial underwriting operations — it was never built or piloted at an employer, and there's no usage data or ROI to report. Everything here — the data, requirements, dashboard, and scoring model — is my own analysis for this portfolio. Where something below is a design assumption rather than an observed fact, I've said so, most explicitly in the [Attention Score Model](analysis/attention_score_model.md).

## Contents

[Business Problem](#business-problem) · [Users & Stakeholders](#users--stakeholders) · [Current State](#current-state) · [Root Cause](#root-cause) · [Requirements](#requirements) · [Proposed Solution](#proposed-solution) · [The Attention Score](#the-attention-score) · [MVP & Prioritization](#mvp--prioritization) · [Success Measures](#success-measures) · [Roadmap](#roadmap) · [Risks & Constraints](#risks--constraints) · [Next Steps](#next-steps) · [Repository Guide](#repository-guide)

## My Perspective

I'm an underwriting professional finishing an MBA (Data Analytics focus) and moving toward Business Analyst / Product Analyst / APM roles. My edge on this project is domain knowledge — I've worked inside the environment these users operate in, so the problem below is one I've watched happen, not one I researched secondhand.

## Business Problem

Underwriters need to know what's outstanding on their book and what needs attention. That used to be visible through a tracker; as tools and processes evolved and issuance execution shifted to Underwriting Assistants, that visibility fragmented.

**The two halves of the lifecycle matter here.** While an underwriter is reviewing and quoting a risk, they own that work and can see it fine — no fragmentation problem there. The problem starts **after bind**, once a policy moves into UA-managed issuance: status now lives in the UA's own tracking method, and any team- or region-level view means a manager manually rebuilding an Excel summary. Underwriter360's queue includes both stages for a single-pane-of-glass view, but the pain it's solving is specifically the post-bind handoff.

The tools to fix this already exist — Power BI, Excel, SharePoint, underwriting workbenches. The gap isn't technology. It's that no single view answers *what needs attention, why, and who owns the next step* without someone reassembling it by hand.

## Users & Stakeholders

| Role | Basis | Need |
|---|---|---|
| **Commercial Property Underwriter** | Observed directly | One prioritized, explainable view of their own outstanding book |
| **Underwriting Assistant (UA)** | Observed directly | A shared way to track outstanding items, instead of a personal method |
| **Underwriting Manager** | Reasonable assumption | Team-wide bottleneck visibility without manual Excel pulls |
| **Regional Leader** | Reasonable assumption | A live roll-up instead of a periodic emailed spreadsheet |
| **Broker/Agent, Client, Loss Control** | Observed as workflow participants | Frequently hold the next action on an item (shown as `Next_Action_Owner` in the data, not direct users of the tool) |

## Current State

A submission moves underwriter → quote → bind → UA-managed issuance. The friction isn't the underwriting decision — it's that once work is handed to the UA, status lives in a personal tracker rather than a shared view, and any rollup above that is manual. Diagram and full detail: [current_state_process_map.md](process-maps/current_state_process_map.md).

**Pain points:** fragmented visibility across systems and people · non-standardized UA tracking that doesn't roll up cleanly · manual, stale-on-arrival Excel reporting · no shared definition of "needs attention" · status that says *what* but never *why* or *what's next*.

## Root Cause

"Too many spreadsheets" is the symptom. The actual cause: no system owns the job of answering *what needs attention* — systems of record capture transactional state, they don't synthesize it into a ranked, explained action list. So every role builds its own workaround. That's why the fix here isn't "put more data in one dashboard" (still just a bigger spreadsheet) — it's a layer that synthesizes signals into something ranked and explained. That's the job of the Attention Score below.

## Requirements

Full matrix (Business/User/Functional/Non-Functional/Data, MoSCoW-prioritized) and 8 user stories with acceptance criteria: [requirements_matrix.md](requirements/requirements_matrix.md) · [user_stories.md](requirements/user_stories.md).

Worth flagging: **every prioritization signal has to be explainable, not a black box** (UR-06/FR-08) — this single requirement is what drove the Attention Score design. And account size is required to display as a *separate* signal, never blended into urgency (FR-10) — see [The Attention Score](#the-attention-score).

## Proposed Solution

Underwriter360 sits on top of existing systems — it doesn't replace them. Two levels of information, matched to two different jobs:

| Screen | Job |
|---|---|
| **My Attention Queue** | Minimal and prioritized — "what do I work on next?" |
| **Account 360** | Full context on one account, once you've chosen to dig in |

Each pain point above maps to a specific response: fragmented visibility → one queue per underwriter, one data model; inconsistent tracking → shared `Outstanding_Item` / `Next_Action_Owner` fields; manual reporting → live Team/Regional views (Phase 2); no shared urgency definition → the Attention Score; flat status → a `Recommended_Next_Action` on every item.

Future-state diagram: [future_state_process_map.md](process-maps/future_state_process_map.md).

## Product Concept

**[Open the dashboard mockup](prototype/dashboard_mockup.html)** in a browser. It's scoped to one Commercial Property underwriter's queue, ranked by Attention Score — each item shows the score, a plain-language reason, status, days outstanding, and next action with owner. A "Significant Account" badge appears separately when relevant (see below for why it's not part of the score).

Account 360 — the account-level drill-down the product is named for — is deliberately scoped as information architecture only at this stage, not a built screen: [account_360_ia.md](prototype/account_360_ia.md).

## The Attention Score

This is the concept's main differentiator, and it's presented as **an unvalidated v1 hypothesis** — full reasoning, worked example, and validation plan in [attention_score_model.md](analysis/attention_score_model.md).

Four transparent factors: aging, deadline pressure, blocking-item severity, and next-action ownership. Account size (TIV) is deliberately *excluded* — a large account waiting on a routine signature isn't more urgent than a small one that's overdue and genuinely blocked, so blending the two would make the score less trustworthy, not more. Account significance shows up as its own separate badge instead.

The model doc also spells out how this would actually get validated before anyone should trust it: blind-ranking comparisons against real underwriter judgment, structured factor review with underwriters and a manager, and (if piloted) tracking how often users override the suggested ranking.

## MVP & Prioritization

Full reasoning: [mvp_prioritization.md](analysis/mvp_prioritization.md)

MVP answers one question for one underwriter: *what needs my attention today, and why?* — the Attention Queue, the score with its visible reason, a freshness indicator, and role-scoped access. Team View, Regional Roll-Up, Renewal Radar, and Account 360 are all genuinely valuable, but each answers a different question, so they wait for Phase 2/3 rather than bloating the MVP.

## Success Measures

Full framework: [kpi_framework.md](analysis/kpi_framework.md)

Proposed KPIs: median days outstanding, % of items past target date, Attention Score distribution, % of items where the underwriter is the next-action owner, and — if piloted — the Attention Score override rate as the real test of whether the model matches human judgment.

## Roadmap

**Phase 1 (MVP):** Attention Queue + Attention Score for one underwriter. **Phase 2:** Team View, Regional Roll-Up, Renewal Radar, export, auditability. **Phase 3:** Account 360 build-out, plus re-validating the Attention Score against real usage. Phase 1 shouldn't lead to Phase 2 until that validation actually happens — detail in [product_roadmap.md](roadmap/product_roadmap.md).

## Risks & Constraints

- **Data availability** — assumes the underlying status/ownership data already exists somewhere; that needs checking against real source systems.
- **Integration** — pulling live data from a policy system, a UA's tracker, and a workbench is real technical work not modeled here.
- **Access design** — who sees own-book vs. team vs. region needs real organizational input.
- **Trust in the score** — an unvalidated model that doesn't match underwriter judgment gets ignored, not corrected, without the validation steps above.
- **Ownership** — unclear who'd build/maintain this (ops, BI, IT) — needs resolving before real scoping.
- **Change management** — replacing personal tracking habits is a behavior problem as much as a technology one.

## Next Steps

Before this goes anywhere real: discovery interviews with actual underwriters/UAs/managers to pressure-test the pain points and the score's weights; a real data-source assessment; the blind-ranking validation described in the Attention Score doc (the most important one — the model's credibility depends on it); ownership alignment; and usability testing before any build investment.

## Repository Guide

```
Underwriter360/
├── README.md
├── data/         — synthetic dataset + data dictionary
├── requirements/ — requirements matrix + user stories
├── process-maps/ — current-state and future-state diagrams
├── prototype/    — dashboard mockup + Account 360 IA
├── analysis/     — Attention Score model, KPI framework, MVP prioritization
├── roadmap/      — phased roadmap
└── research/     — public source log
```

All data in [`/data`](data/synthetic_policy_tracker.csv) is synthetic, generated for this portfolio — see [data_dictionary.md](data/data_dictionary.md) for field definitions.
