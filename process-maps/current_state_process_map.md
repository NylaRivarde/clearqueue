# Current-State Workflow: Policy Issuance & Visibility

This map reflects a generalized commercial underwriting policy issuance workflow, informed by professional experience working inside commercial underwriting operations. It is written to illustrate a **common industry pattern**, not any single employer's proprietary process, and it deliberately stays at the level of roles and handoffs rather than system-specific steps.

## Workflow

```mermaid
flowchart TD
    A["Broker/Agent submits business\n(new business, renewal, or endorsement)"] --> B["Underwriter reviews & assesses risk"]
    B --> C{Quote issued?}
    C -- "Declined" --> Z["Closed / Declined\n(tracked separately, low visibility once closed)"]
    C -- "Quoted" --> D["Broker/Client responds"]
    D -- "Not bound" --> Z
    D -- "Bound" --> E["Underwriter hands off to\nUnderwriting Assistant (UA) for issuance"]
    E --> F["UA processes issuance tasks:\ndocument prep, data entry, endorsements,\noutstanding items follow-up"]
    F --> G{Anything outstanding?\ne.g. loss runs, signed app,\nSOV/COPE, inspection}
    G -- "Yes" --> H["UA follows up with broker/client\n(manual email/phone, tracked in\npersonal notes or a spreadsheet)"]
    H --> G
    G -- "No" --> I["Policy issued in system of record"]

    subgraph VIS["Visibility layer (fragmented)"]
        direction TB
        V1["Underwriter checks status\nad hoc — asks UA directly,\nor checks Workbench/system"]
        V2["UA maintains own tracking\n(spreadsheet or personal notes)\nof what's outstanding"]
        V3["Manager periodically pulls\ndata into Excel to see\nteam-wide outstanding items"]
        V4["Manager manually distributes\nExcel summary to regional\nleaders by email"]
        V3 --> V4
    end

    F -.status not\ncentrally visible.-> V1
    F -.status lives in\nUA's own tracking.-> V2
    V2 -.rolled up manually,\nnot in real time.-> V3
```

## Roles in This Workflow

| Role | What they do | What they need to see |
|---|---|---|
| **Broker/Agent** | Submits business, responds to quotes, supplies outstanding items | Status of their submission (largely external to this case study) |
| **Underwriter** | Assesses risk, quotes, binds, hands off to UA, remains accountable for the account relationship | What's still outstanding on their book; what needs their decision or attention today |
| **Underwriting Assistant (UA)** | Executes issuance tasks, chases outstanding items, processes endorsements | Their own queue, prioritized by aging and deadline |
| **Underwriting Manager** | Oversees a team of underwriters/UAs, reports up on team performance | Team-wide outstanding volume, aging, and bottlenecks |
| **Regional Leader** | Oversees multiple teams/managers, wants portfolio-level visibility | Roll-up of outstanding work and risk across teams/regions |

## Where Visibility Breaks Down

The transaction itself moves through a fairly standard path (submit → quote → bind → issue). The friction is not in the underwriting decision — it's in **knowing where every open item stands without asking someone or rebuilding a report by hand**:

1. **The underwriter can't see UA-managed issuance status in one place.** Once a policy is bound and handed to the UA, day-to-day status often lives in the UA's own tracking method, not a shared, real-time view.
2. **The UA's tracking is personal, not standardized.** Different UAs may track outstanding items differently, making it hard to roll up consistently across a team.
3. **Team- and region-level visibility requires manual work.** A manager assembling an outstanding-items view for regional leaders typically pulls data into Excel and distributes it — a snapshot that is stale the moment it's sent.
4. **There is no shared definition of "what needs attention."** Aging, priority, and outstanding-item status are judgment calls made informally, not a consistent, visible standard.

This is the gap ClearQueue is designed to close — see the [Future-State Workflow](future_state_process_map.md).
