# Data Dictionary — Synthetic Commercial Property Policy Tracker

**File:** [`synthetic_policy_tracker.csv`](synthetic_policy_tracker.csv)
**Records:** 145 fictional Commercial Property policy transactions
**Snapshot / "as-of" date:** 2026-08-17 (a fixed reference date used to calculate aging, deadlines, and the Attention Score — treat it as "today" when reading the data)

> **This data is 100% synthetic.** Account names, underwriters, dates, risk characteristics, and scores were generated programmatically for demonstration purposes. It does not represent any real company, customer, policy, employee, or performance data.

## Why Commercial Property Specifically

ClearQueue's Version 1 concept is scoped to a **Commercial Property underwriter's** book of business, not commercial lines generally. Every record in this file is a Commercial Property submission or policy. The risk fields below (construction, occupancy, protection, exposure) reflect **COPE** — the standard framework property underwriters use to evaluate a risk — plus the property-specific workflow steps (four-point inspections, elevation certificates, wind mitigation reports) that actually drive delays in property issuance. See [Research & Source Log](../research/source_log.md) for the public sources behind these terms.

## Column Reference

| Column | Type | Description |
|---|---|---|
| `Policy_ID` | Text | Unique fictional submission/policy identifier (e.g., `CPU-210001`). |
| `Account_Name` | Text | Fictional insured business name. Generated from random name fragments — any resemblance to a real company is coincidental. |
| `Occupancy_Type` | Category | How the building is used — the "O" in COPE. One of: Manufacturing/Industrial, Warehouse & Distribution, Office, Retail/Mercantile, Habitational (Multifamily), Restaurant/Hospitality, Self-Storage. |
| `Construction_Type` | Category | The "C" in COPE — ISO's six building construction classes, least to most fire-resistive: Frame, Joisted Masonry, Non-Combustible, Masonry Non-Combustible, Modified Fire-Resistive, Fire-Resistive. |
| `Protection_Class` | Integer (1–10) | Simplified ISO Public Protection Classification — the "P" in COPE. Lower numbers indicate better fire protection (closer/better-resourced fire department, hydrants, etc.); 10 indicates essentially unprotected. |
| `Sprinklered` | Category | Yes / Partial / No — a primary fire protection feature underwriters weigh heavily. |
| `Building_Age_Years` | Integer | Age of the structure. Drives whether a four-point inspection (roof, HVAC, electrical, plumbing) is typically required — insurers commonly require one for buildings over ~20 years old. |
| `TIV_Band` | Category | Banded Total Insured Value (building + contents + business income), rolled up from a submission's Statement of Values (SOV): `$1M-$5M` through `$100M+`. Banded, not exact, to keep the demonstration data non-sensitive. |
| `Account_Significance` | Category | Standard / Notable / Significant — derived from `TIV_Band`. Shown in the queue and Account 360 as a separate badge, deliberately kept out of the Attention Score calculation. See [Attention Score Model — Account Significance Is Deliberately Excluded](../analysis/attention_score_model.md#account-significance-is-deliberately-excluded-from-the-score) for why workflow urgency and account size are treated as two different signals rather than one blended number. |
| `Wind_Hail_Exposure` | Category | Low / Moderate / High — the "E" (exposure) in COPE, specific to wind/hail/named-storm risk. Correlated with region in this synthetic set (Southeast and South Central skew higher, matching real CAT geography). |
| `Flood_Zone` | Category | Simplified FEMA-style flood zone: `Zone X - Minimal`, `Zone A - Moderate`, `Zone AE - High-Risk`, `Zone VE - Coastal High-Risk`. Drives whether an elevation certificate becomes a required outstanding item. |
| `Region` | Category | Book-of-business region: Northeast, Southeast, Midwest, South Central, West. |
| `Transaction_Type` | Category | New Business, Renewal, or Endorsement. |
| `Underwriter` | Text | Fictional Commercial Property underwriter of record. |
| `Underwriting_Assistant` | Text | Fictional Underwriting Assistant (UA) handling issuance tasks for the transaction. |
| `Submission_Date` | Date | Date the submission entered the underwriting workflow. |
| `Target_Issuance_Date` | Date | Internally expected issuance date (14–45 days from submission). A service-level expectation, not a contractual deadline. |
| `Actual_Issuance_Date` | Date or blank | Date the policy was actually issued. Blank for anything still open. |
| `Policy_Status` | Category | Current workflow stage — see **Status Values** below. |
| `Days_Outstanding` | Integer | Calendar days from `Submission_Date` to the as-of date (open items) or to `Actual_Issuance_Date` (closed items). |
| `Aging_Bucket` | Category | `Days_Outstanding` grouped: `0-5 days`, `6-10 days`, `11-15 days`, `16-30 days`, `30+ days`. |
| `Outstanding_Item` | Text | The specific property-underwriting blocker holding the transaction up — see **Outstanding Item Catalog** below, or "None". |
| `Next_Action_Owner` | Category | Who the ball is in the court of: Underwriter, Underwriting Assistant, Broker/Agent, Client, Loss Control/Inspector, or None (closed items). |
| `Recommended_Next_Action` | Text | A short, specific suggested next step tied to the current status/outstanding item (e.g., "Order 4-point inspection; hold for results before binding"). This is what turns a status list into an action list. |
| `Renewal_Date` | Date | Upcoming renewal date. |
| `Attention_Score` | Integer (0–100) | Transparent, rule-based prioritization score. See [Attention Score Model](../analysis/attention_score_model.md) for the full, documented rubric (0 for closed items). |
| `Priority` | Category | Derived label from `Attention_Score`: High (≥65), Medium (35–64), Low (<35), or N/A for closed items. |
| `Score_Driver` | Text | The single most decision-relevant reason behind the score (e.g., "Hard blocker: elevation certificate needed (flood zone)") — what the queue displays instead of raw points. |

## Status Values (`Policy_Status`)

These span two distinct lifecycle stages, and the distinction matters for where this case study says the fragmentation problem actually lives:

**Underwriting decision stage** — the underwriter is the one doing the work, so visibility here is already largely intact. These statuses are included in the queue for completeness (an underwriter wants one place to see everything on their book), not because this is where the observed pain point occurs.

| Status | Meaning |
|---|---|
| Submitted - Awaiting Review | Received, not yet picked up by underwriting |
| In Underwriting Review | Underwriter actively assessing the risk |
| Quoted - Awaiting Response | Quote issued, waiting on broker/client decision |

**Issuance execution stage** — ownership shifts to the Underwriting Assistant once a risk is bound. This is where the real-world fragmentation this project is about actually occurs: day-to-day status moves into a UA's own tracking method, outside the underwriter's direct view.

| Status | Meaning |
|---|---|
| Bound - Pending Issuance | Coverage bound, issuance paperwork not started/complete |
| Issuance In Progress | Issuance actively being processed, typically by the UA |
| On Hold - Missing Information | Blocked on an outstanding item — can occur at either stage, but most consequential post-bind |

**Closed** — `Issued` and `Cancelled/Declined`.

## Outstanding Item Catalog

Grounded in how commercial property submissions are actually underwritten (see [Source Log](../research/source_log.md)):

| Outstanding Item | Typically Triggered By | Typical Owner |
|---|---|---|
| Statement of Values (SOV) incomplete | Any submission — the SOV drives TIV and pricing | Broker/Agent |
| 4-Point inspection required (roof/HVAC/electrical/plumbing) | Building age > ~20 years | Loss Control/Inspector |
| Loss control inspection pending | Any submission needing a physical risk survey | Loss Control/Inspector |
| Elevation certificate needed (flood zone) | Flood Zone AE or VE | Broker/Agent |
| Wind mitigation report pending | High wind/hail exposure (credit eligibility) | Broker/Agent |
| Updated appraisal/valuation needed | Any submission with a stale valuation | Client |
| Roof condition documentation pending | Older buildings | Broker/Agent |
| Broker confirmation of sprinkler/protective safeguards | Any submission | Broker/Agent |
| Signed application pending | Any submission | Broker/Agent |
| Payment / down payment pending | Bound items awaiting funds | Client |

## Known Snapshot Characteristics

Descriptive facts about *this generated file* — not industry benchmarks or real performance claims:

- 145 total records; 90 open/outstanding, 55 closed.
- Attention Score on open records ranges roughly 12–89 (mean ≈ 50).
- Priority split on open records: roughly 25 High, 41 Medium, 24 Low.

## Data Notice

Demonstration data used in this portfolio is synthetic and does not represent actual company, customer, policy, or performance data.
