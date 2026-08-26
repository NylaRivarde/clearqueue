# Research & Source Log

Public sources used to establish industry context, underwriting terminology, and workflow facts referenced throughout this case study. My own professional observations establish the core business problem (see [README.md](../README.md)); these sources support the broader industry and technical context. Demonstration data, product requirements, and the Attention Score model are original analysis for this portfolio and are not drawn from any of these sources.

## Commercial Underwriting Operations & Digitization

- **Insurance Journal / Send Technology / Veridion / Baker Tilly — Underwriting technology trends (2024–2025).** Used to support the observation that commercial underwriters still rely heavily on manual, Excel-driven workflows despite available technology, and that submission triage speed is a recognized industry pain point.
  - [10 Insurance Underwriting Trends for 2025 — Send Technology](https://send.technology/resources/blog/top-10-insurance-industry-trends-underwriters-should-know-about-in-2025/)
  - [Insurance operations: Are you relying on outdated processes? — Baker Tilly](https://www.bakertilly.com/insights/insurance-operations-relying-on-outdated-processes-or-challenging-the-status-quo)
  - [Top 5 Challenges In Insurance Underwriting — Veridion](https://veridion.com/blog-posts/insurance-underwriting-challenges/)

- **McKinsey & Company — "How data and analytics are redefining excellence in P&C underwriting."** Used for industry context on digital transformation's impact on underwriting cycle time and issuance speed.
  - [mckinsey.com — data and analytics in P&C underwriting](https://www.mckinsey.com/industries/financial-services/our-insights/how-data-and-analytics-are-redefining-excellence-in-p-and-c-underwriting)

- **Deloitte Insights — "The future of insurance underwriting."** Used for industry context on operating-model modernization in underwriting.
  - [deloitte.com — future of insurance underwriting](https://www.deloitte.com/us/en/insights/industry/financial-services/future-of-insurance-underwriting.html)

- **Decerto — "What Is an Underwriting Workbench? The 2026 Guide for U.S. P&C Carriers."** Used as background on how "workbench" tools are positioned in the industry, relevant to why Underwriter360 is framed as a visibility layer that complements rather than replaces existing systems like a workbench.
  - [decerto.com — underwriting workbench guide](https://www.decerto.com/us/post/what-is-an-underwriting-workbench)

## Commercial Lines Market Context

- **Triple-I (Insurance Information Institute) — Facts + Statistics: Commercial Lines.** Used for high-level, publicly available market context on commercial lines performance. Not used as a source for any specific claim about product impact or ROI.
  - [iii.org — Commercial Lines facts and statistics](https://www.iii.org/fact-statistic/facts-statistics-commercial-lines)
  - [iii.org — Commercial property insurance market brief](https://www.iii.org/press-release/commercial-property-insurance-shows-signs-of-improvement-stable-growth-says-new-triple-i-brief-121924)

- **NAIC — Accelerated Underwriting.** Used for background on regulatory attention to underwriting technology and automation.
  - [content.naic.org — Accelerated Underwriting](https://content.naic.org/insurance-topics/accelerated-underwriting)

## Commercial Property Underwriting Terminology (COPE, Construction, Inspections, SOV/TIV)

These sources ground the property-specific fields in the synthetic dataset, dashboard, and Account 360 concept in real, standard industry terminology — not invented or employer-specific practices.

- **IRMI — "Construction, Occupancy, Protection, and Exposure (COPE)."** Definitional source for the COPE framework used throughout the data dictionary and Account 360 IA.
  - [irmi.com — COPE definition](https://www.irmi.com/term/insurance-definitions/construction-occupancy-protection-and-exposure)

- **Insurance Journal — "Understanding Commercial Property Underwriting and 'COPE'."** Practitioner-facing explanation of how COPE is used in real submissions.
  - [insurancejournal.com — COPE in commercial property underwriting](https://www.insurancejournal.com/news/national/2015/02/03/356085.htm)

- **IRMI — "Building Construction Categories (ISO)."** Source for the six ISO CLM construction classes (Frame, Joisted Masonry, Non-Combustible, Masonry Non-Combustible, Modified Fire-Resistive, Fire-Resistive) used as `Construction_Type` values in the synthetic dataset.
  - [irmi.com — ISO building construction categories](https://www.irmi.com/term/insurance-definitions/building-construction-categories-(iso))

- **CCPIA (Commercial Construction & Property Inspectors Association) — "Commercial Property Insurance Inspections."** Source for four-point inspection scope (roof, HVAC, electrical, plumbing) and its role in underwriting older buildings — the basis for the `Building_Age_Years`-driven "4-Point inspection required" outstanding item in the synthetic data.
  - [ccpia.org — commercial property insurance inspections](https://ccpia.org/commercial-property-insurance-inspections/)

- **Pibit.AI — "What Is Statement of Values (SOV)?" and "What Is Total Insured Value (TIV)?"** Source for how a Statement of Values rolls up into Total Insured Value, and for the standard SOV data fields (construction, occupancy, year built, square footage, protection class, sprinkler status, roof information, flood zone, elevation certificate) referenced in the `TIV_Band`, `Flood_Zone`, and related fields.
  - [pibit.ai — Statement of Values](https://pibit.ai/insurance-knowledge/statement-of-values-sov)
  - [pibit.ai — Total Insured Value](https://pibit.ai/insurance-knowledge/total-insured-value-tiv)

## What These Sources Were *Not* Used For

- No source above was used to justify any claim of productivity improvement, cost savings, or adoption outcome for Underwriter360 — this concept has no implementation and no measured results (see [README.md — My Role / Perspective](../README.md#my-role--perspective)).
- No source above describes any specific employer's internal systems, tools, or practices. Where this case study references tools like "Workbench," "SharePoint," or "Excel-based tracking," those are described generically, consistent with widely reported industry patterns in the sources above — not as a specific employer's proprietary configuration.

## Data Notice

Demonstration data used in this portfolio is synthetic and does not represent actual company, customer, policy, or performance data.
