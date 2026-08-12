# Deliverable 1: Solution Design & Phasing Summary

## Context

This engagement isn't a straightforward technical implementation. The council-mandated 9-month timeline sits on top of three fighting stakeholders: a Planning Director operating outside project governance, an IT team defending legacy infrastructure they didn't choose to replace, and a city-side PM whose verbal-decision pattern creates undocumented risk. The design decisions below are constructed to navigate those political constraints, not just technical ones.

## 1. Discovery Approach (First 30 Days)

Discovery will be structured politically to control the scene before competing parties derail the timeline.

**Week 1 (Internal):** Before meeting the client, I will meet our Sales team and check what was promised informally to the Planning Director and where those promises deviate from the SOW. It is needed so I don't go in blind and be prepared.

**Weeks 1-2 (Workflow Mapping):** We do not run discovery on a first-come-first-served basis. We map workflows by department:

1. **Business Licensing:** Selected for isolation, not simplicity. It bypasses cross-departmental turf wars, giving us a siloed environment to prove our baseline database integration.
2. **Fire:** Highest risk. Life-safety routing needs early architectural clarity.
3. **Planning:** Highest political stakes. By entering this session last, we will have our wins from the previous two departments as a base, giving us maximum leverage.

**Weeks 2-3 (IT Peer Engagement):** IT is under the assumption that we are replacing them. We plan their engagement in a way that shows them we are in this together, and its their expertise that will guide us in creating a stable and excellent extraction strategy. Our Wave 1 "read-only" integration strategy buys IT the first two months to build write-pipelines without holding up our configuration.

**Weeks 3-4 (Decision Governance):** We decide how we document things based on what's at stake.
- Routine items go into meeting minutes.
- Anything impacting scope, timeline, or cost requires a go-ahead from the City Sponsor.
- When the IT team gives us a technical constraint, I send a quick note summarizing our path forward. This makes sure we're aligned without turning every chat into a contract negotiation.

**Note:** Given our tight 9-month clock, we have to lock requirements early. Any new feature requests after that point are tracked for Phase 2 to keep our launch date safe.

## 2. Proposed Architecture & Phasing Strategy

50+ permits in 9 months is a humongous task, especially with a dependency on MS Access and IT stonewalling us. The best foot forward is to group permits into similar groups/families.

Configuration will be built at the family level — permits that share intake shape and routing skeleton — with individual permit types as front-end variants of their family. This is the only realistic path to 50+ types in 9 months. Building family-first also means the routing engine gets stressed once, not fifty times.

Each family's specific departmental routing is determined during discovery per permit type. The family taxonomy captures configuration structure, not organizational assignment.

**Family 1 — Rules-Driven Issuance:** for high-volume, low-risk permits requiring no human review.
- *Flow:* Portal Intake → Automated Rule Validation → Fee Assessment → Payment → Auto-Issue.
- *Config:* No workflow tasks generated. Configuration relies entirely on front-end logic and automated fee calculations.

**Family 2 — Over-the-Counter:** for minor projects that need human eyes from only one or two disciplines. Routing is strictly linear.
- *Flow:* Intake → Desk Review (Dept A) → [Optional: Desk Review Dept B] → Corrections Loop → Payment → Issue.
- *Config:* Linear task generation with strict precedence. A task must be closed before the next one opens.

**Family 3 — Concurrent Plan Review (The Heavyweights):** the most complex template. Used for major construction where multiple departments must review the same documents simultaneously.
- *Flow:* Intake → Parallel Routing (Building, Planning, Fire, Public Works active simultaneously) → Consolidate Comments → Resubmission Loop → Final Approval → Issue.
- *Config:* Requires parent/child workflow task dependencies. The workflow cannot advance to "Approved" until all parallel child tasks reach a "Pass" status.

**Family 4 — Event-Driven:** dictated by calendars, public noticing periods, and external board votes rather than internal staff review times.
- *Flow:* Intake → Staff Review → Public Notice → Hearing/Vote → Resolution/Issuance.
- *Config:* Calendar-driven timing (public notice periods, board schedules) rather than internal review SLAs. Outcomes are custom (e.g., "Approved with Conditions") rather than simple Pass/Fail.

**Family 5 — Recurring:** for permits that live indefinitely and require ongoing, scheduled actions.
- *Flow:* Intake/Approval → Issue → Annual Trigger → Renewal Invoice/Inspection → Updated Certificate.
- *Config:* Uses automated batch tasks to trigger renewals and inspections, keeping the system clean and preventing duplicate records.

### Wave Sequencing & The IT Bottleneck

Treating MS Access as a real-time transactional database for 50 concurrent permit types will cause it to choke. We will likely need to advocate for a middleware layer — a staging database (SQL Server Express or PostgreSQL) that handles the real-time permitting traffic and syncs to the legacy Access DB via nightly batch jobs.

Because of this IT dependency, we cannot sequence waves based purely on business value; we have to sequence based on database integration complexity to give IT time to build stable pipelines.

- **Wave 1 (Months 1–2) — Bare Bones:**
  - Goal: Families 1 & 2 (read-only). Includes a Small Business Zoning permit — gives the Mayor a win without creating cross-dept risk.
  - QA: Validate database read-access.
- **Wave 2 (Months 3–4) — Complex Routing:**
  - Goal: Single-threaded writes for Families 2 & 4.
  - QA: Test task engine and SLA timers to make sure workflow moves as expected.
- **Wave 3 (Months 5–6) — Heavyweights:**
  - Goal: Family 3 parallel routing and parent/child logic.
  - QA: Validate workflow gating and dependencies so the system doesn't get stuck.
- **Wave 4 (Month 7) — Lifecycle & Batch:**
  - Goal: Family 5 operations.
  - QA: Time-skip testing; verify renewal triggers fire and prevent duplicate records.
- **Wave 5 (Months 8–9) — Hardening:**
  - Goal: Cross-dept integration testing, load-testing the Access bottleneck, and staff UAT.
  - QA: Stress-testing routing logic against actual day-to-day workflows.

## 3. Key Assumptions

1. **Assumption:** SOW is enforceable as the true scope, not Sales' informal commitments to the Planning Director.
   - *Validated:* Week 1 Sales reconciliation.
2. **Assumption:** Business Licensing is decoupled enough from other departments to serve as an early standalone win.
   - *Validated:* Weeks 1-2 department mapping.
3. **Assumption:** IT can support read pipelines immediately, buying time to figure out write-pipelines.
   - *Validated:* Weeks 2-3 IT peer sessions.
4. **Assumption:** The target platform natively supports our family/variant configuration without requiring per-permit custom code.
   - *Validated:* Wave 1 golden-path proof.

## 4. Open Questions

**Requires a Written Answer (SOW Amendment or Executive Memo):**
- What is the defined technical fallback if MS Access fails concurrent write-testing in Month 3?
- How will life-safety regulatory gaps discovered after the hard scope-freeze date be handled?
- What is the direct escalation path if the City PM refuses to route scope, timeline, or cost decisions to the City Sponsor for written sign-off?

**Requires Verbal Alignment (Logged as Formal Project Assumptions):**
- For Family 3 Concurrent Plan Reviews, who holds the ultimate tie-breaking authority when Building, Fire, and Planning disagree on a shared workflow step?
- What is the exact criteria for a "Phase 1 go-live blocker" versus a "post-go-live defect"?
