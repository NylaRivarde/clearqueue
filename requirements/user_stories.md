# User Stories & Acceptance Criteria — ClearQueue

Representative proposed user stories tied to the requirements in the [Requirements Matrix](requirements_matrix.md). Each maps to a specific pain point identified in the current-state workflow.

---

### US-01 — Underwriter: See what needs my attention today

**As an** underwriter
**I want** a single view of every open item on my book, ranked by Attention Score
**So that** I can decide what to work on first without checking multiple systems or asking my UA

**Acceptance Criteria**
- Given I open ClearQueue, when the page loads, then I see only transactions where I am the underwriter of record.
- Given a transaction is overdue against its target issuance date or has a hard blocker (e.g., an outstanding 4-point inspection), when I view my queue, then its Attention Score reflects that and it sorts near the top.
- Given I want to focus on one line of business or region, when I apply a filter, then the queue updates without a page reload or manual re-export.
- Given the data was last refreshed at a specific time, when I view the queue, then I can see that timestamp on screen.

*Related requirements: UR-01, FR-01, FR-03, FR-08, NFR-01*

---

### US-02 — Underwriting Assistant: Manage my workload in one place

**As an** Underwriting Assistant
**I want** to log and update outstanding items for the transactions I'm processing
**So that** I stop maintaining a separate personal tracker that no one else can see

**Acceptance Criteria**
- Given I am processing an issuance task, when something is blocking it (e.g., missing loss runs), then I can record the outstanding item and who owns the next action (broker, client, underwriter, me).
- Given I resolve an outstanding item, when I update its status, then it is reflected in the underwriter's and manager's views without any additional manual step.
- Given I have multiple accounts in progress, when I open my own queue, then I see them sorted by aging, not in the order I happened to add them to a spreadsheet.

*Related requirements: UR-02, FR-02, FR-03*

---

### US-03 — Manager: Understand team-wide bottlenecks without a manual pull

**As an** underwriting manager
**I want** a live summary of outstanding volume and aging across my team
**So that** I can identify where to rebalance work or step in, without rebuilding an Excel report

**Acceptance Criteria**
- Given my team has multiple underwriters and UAs, when I open the Team View, then I see counts of open items broken out by person, status, and aging bucket.
- Given I need to share this with a regional leader, when I export the view, then the export reflects exactly what's on screen at that moment (no separate manual reconciliation step).
- Given one underwriter or UA has a disproportionate share of High-priority aged items, when I view the team summary, then that concentration is visually obvious without me needing to build a pivot table.

*Related requirements: UR-03, BR-01, FR-04, FR-07*

---

### US-04 — Regional Leader: See the same live data instead of a periodic email

**As a** regional leader
**I want** a live roll-up of outstanding work across the teams in my region
**So that** I know what requires attention without waiting for someone to compile and send a spreadsheet

**Acceptance Criteria**
- Given multiple teams report into my region, when I open the Regional Roll-Up, then I see an aggregated view across those teams with the ability to drill into any one team.
- Given the underlying data changes, when I check the roll-up again, then I'm seeing current data, not a static snapshot from whenever it was last emailed.

*Related requirements: UR-04, BR-01, FR-05*

---

### US-05 — Underwriter: Avoid being surprised by an upcoming renewal

**As an** underwriter
**I want** to see which of my policies are approaching renewal
**So that** I can start renewal work proactively instead of reactively when a broker calls

**Acceptance Criteria**
- Given a policy's renewal date falls within a configurable look-ahead window (default 30 days), when I view the Renewal Radar, then that policy appears in the list.
- Given a renewal is also currently flagged as an open outstanding item, when I view the Renewal Radar, then I can see both the renewal timing and the outstanding item together, not in two separate places.

*Related requirements: UR-05, FR-06*

---

### US-07 — Underwriter: Understand *why* something is ranked urgent

**As an** underwriter
**I want** to see the specific reason behind an item's Attention Score, not just a High/Medium/Low label
**So that** I know whether to act myself, delegate, or chase a third party — and can trust the ranking enough to act on it

**Acceptance Criteria**
- Given an item appears in my queue, when I view its score, then I also see a single plain-language reason (e.g., "Hard blocker: elevation certificate needed (flood zone)") explaining why it's ranked where it is.
- Given I want to understand the model itself, when I look for it, then the scoring rules (aging, deadline pressure, blocking severity, ownership, exposure size, and their point values) are documented and visible — not a black box.
- Given two items have the same Attention Score, when I compare their displayed reasons, then I can see they may need different kinds of action (e.g., one needs me to do the underwriting, the other needs a broker follow-up).

*Related requirements: UR-06, FR-08*

---

### US-08 — Underwriter: See the full picture on one account

**As an** underwriter
**I want** to open a single account and see its risk characteristics, current status, and next action together
**So that** I don't have to reassemble that picture from the submission file, the SOV, and the tracker separately

**Acceptance Criteria**
- Given I select an account from my queue, when Account 360 opens, then I see its COPE risk summary (construction, occupancy, protection, exposure), current workflow status, outstanding item and owner, and renewal timing together on one screen.
- Given the account has an approaching renewal and an open blocker at the same time, when I view Account 360, then both facts are visible together, not in separate views I have to cross-reference myself.

*Related requirements: UR-07, FR-09*

---

### US-06 — Any user: Trust that the data is current

**As any** ClearQueue user
**I want** to know when the data was last refreshed
**So that** I can trust the view enough to act on it instead of double-checking with a person

**Acceptance Criteria**
- Given I open any view in ClearQueue, when the page loads, then a "last updated" timestamp is visible.
- Given the refresh cadence is, for example, hourly, when more than one refresh cycle has passed without an update, then the tool visibly flags the data as stale rather than silently showing old data as current.

*Related requirements: NFR-01*
