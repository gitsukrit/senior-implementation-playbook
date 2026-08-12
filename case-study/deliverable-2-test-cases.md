# Deliverable 2: Test Case Library — Commercial TI Permit

## 1. Workflow Definition: Commercial Tenant Improvement (TI) / Change of Use

**Intake & Payment:** Applicant submits plans and pays application fees. Application moves to "Pending Payment" status until fees clear.

**Conditional Routing Determination:** Based on application data, the system determines which departments must review:
- Building review: always required for TI permits.
- Planning review: conditional — triggered by change of use, historic overlay location, or valuation over $50k.
- Fire review: conditional — triggered by occupancy classification change, square footage > 2,500, or assembly occupancy.

**Parallel Review:** The system simultaneously routes applications to all triggered departments. Parallel review starts an SLA countdown timer against the parent permit; the timer pauses during resubmission waits and resumes on resubmission.

**Resubmission Loop:** If any department marks the task "Revisions Required," the permit goes on hold, SLA pauses, and the applicant is asked to upload new plans. The system routes the first three attempts back to the reviewer. At attempt 4, routing locks and forces a supervisor override to prevent endless loops.

**Conditional Approval:** Departments may mark their task "Approved with Conditions" (e.g., "patio must close by 9 PM") and tag those conditions by category (e.g., 'Life Safety', 'Historic Preservation', 'Structural').

**Consolidation & Issuance:** When all reviews pass, the system consolidates the conditions. The system checks conditions against defined incompatibility rules (e.g., 'Life Safety' vs. 'Historic Preservation'). If there are no conflicts, final permit fees are calculated and the permit is issued. If conflicting conditions are found, the system moves the application for supervisor review.

**Inspections:** City inspectors visit during construction. Inspection failures return the permit to a defined status ("Inspection Failed - Correction Required").

**Final Sign-Off:** When all inspections pass, the system issues the Certificate of Occupancy.

## 2. Test Case Library

Execution ownership is assigned based on the type of judgment required to validate the test:

- **QA:** Validates deterministic paths fully defined by the spec. Anyone following the steps can execute pass/fail without needing domain judgment.
- **SA:** Validates backend architecture, database state, and API payloads. I execute these to ensure data contracts and system stability hold under the hood, where the UI doesn't tell the whole story.
- **Customer (City Staff UAT):** Validates operational workflows. The customer's own staff must verify that the system's behavior reflects real operational intent, not just matching what's written on paper.

---

### TC-01: Application Fee Gate & Integration Failure (Pending Payment Hold)

**Preconditions:** Applicant is on the public portal. Payment gateway integration is active.

**Steps:**
1. Complete the TI application form.
2. Submit the application without paying, OR simulate a payment gateway timeout error.
3. Check the application record and system error log.

**Expected Result:** The application moves to "Pending Payment" status. In the timeout scenario, the gateway error is logged. No review tasks are generated.

**Pass/Fail Criteria:** Pass if the system prevents routing before a successful payment clears and gracefully handles a gateway timeout without crashing or auto-routing.

**Execution Owner:** QA

---

### TC-02: E2E Happy Path (Building Only to CO Issuance)

**Preconditions:** Application is paid. Change of Use, occupancy classification change, historic overlay, and assembly use triggers are not met.

**Steps:**
1. Clear the payment to trigger application routing.
2. As a Building Reviewer, mark the Building task as "Approved."
3. As an Intake Clerk, execute "Issue Permit" (simulating fee payment).
4. As a Building Inspector, mark the Final Inspection task as "Pass."

**Expected Result:** Only the Building Review task generates. Upon plan approval, the permit advances to issuance. Upon final inspection pass, the Certificate of Occupancy is generated.

**Pass/Fail Criteria:** Pass if Planning and Fire tasks never generate, and the permit advances linearly from intake through CO issuance without supervisor intervention.

**Execution Owner:** QA

---

### TC-03: Conditional Routing (Isolated Triggers)

**Preconditions:** Application is paid. Distinct triggers (Change of Use OR Occupancy Classification) are met independently.

**Steps:**
1. Clear the payment to trigger application routing.
2. Check the generated tasks on the permit record.

**Expected Result:** The system dynamically generates the specific review task (Planning or Fire) tied to the trigger, while ignoring the untriggered department.

**Pass/Fail Criteria:** Pass if the required department task is active and the ignored department task is absent.

**Execution Owner:** QA

---

### TC-04: All Disciplines Triggered & SLA Initiation

**Preconditions:** Application is paid. Change of Use, occupancy classification change, and historic overlay are all present.

**Steps:**
1. Clear the payment to trigger application routing.
2. Check generated tasks and parent SLA timer.

**Expected Result:** Building, Planning, and Fire Review tasks all generate simultaneously. The parent SLA timer starts its countdown.

**Pass/Fail Criteria:** Pass if exactly three child tasks generate and the SLA timer transitions from null to active.

**Execution Owner:** QA

---

### TC-05: Resubmission Boundary (Attempt 4 Override)

**Preconditions:** Permit has completed three review attempts. The current Building Review task is active.

**Steps:**
1. Mark the Building task as "Revisions Required."
2. As the applicant, upload revised plans and submit (triggering attempt 4).
3. As a supervisor, execute the override action to allow routing.

**Expected Result:** After step 2, auto-routing is blocked and the permit routes to a supervisor queue. After step 3, the attempt-4 Building Review task generates and the override is recorded on the permit audit log.

**Pass/Fail Criteria:** Pass if auto-routing stops at attempt 4, and the manual override forces task generation and creates an audit trail entry.

**Execution Owner:** QA

---

### TC-06: Conditional Approval (No Conflict)

**Preconditions:** Building and Planning tasks are active.

**Steps:**
1. Mark Building as "Approved."
2. Mark Planning as "Approved with Conditions." Input "Patio closes at 9 PM" and tag as 'Standard.'
3. Check workflow state.

**Expected Result:** The system merges the condition onto the parent permit task and moves the file to the Issued state.

**Pass/Fail Criteria:** Pass if the file auto-advances to Issued and the exact condition text is attached to the parent record.

**Execution Owner:** Customer (City Staff UAT)

---

### TC-07: Conflicting Conditions (Supervisor Review)

**Preconditions:** Building, Planning, and Fire tasks are active.

**Steps:**
1. Mark Building as "Approved."
2. Mark Planning as "Approved with Conditions," input "Retain original wooden doors," and tag it as 'Historic Preservation.'
3. Mark Fire as "Approved with Conditions," input "Replace wooden doors with steel fire doors," and tag it as 'Life Safety.'
4. Check workflow state.

**Expected Result:** The system flags the incompatible category tags ('Historic Preservation' and 'Life Safety'). Consolidation stops and a supervisor review task generates.

**Pass/Fail Criteria:** Pass if the system blocks auto-issuance and moves the application to a supervisor queue to resolve the tagged conflict.

**Execution Owner:** QA

---

### TC-08: Outbound Integration Payload (GIS Map Sync)

**Preconditions:** Permit has reached the "Issued" state. API connection to the external GIS endpoint is active.

**Steps:**
1. Trigger final permit issuance.
2. Intercept the outbound JSON payload in the middleware/API gateway.
3. Inspect the data structure against the vendor data contract.

**Expected Result:** The workflow successfully generates the outbound payload. Unapproved fields (PII, applicant financials) are stripped before transmission.

**Pass/Fail Criteria:** Pass if the JSON structure conforms to the external API specification and zero unapproved data is transmitted.

**Execution Owner:** SA

---

## 3. Distinguishing a Defect from a Scope Gap

When issues arise during UAT, I try to eliminate guesswork and debate by applying a strict triage framework based on specification alignment and rule ownership:

- **Configuration Defect:** The system deviates from the written requirements.
  - *Action:* Resolve the issue immediately at no cost.
- **Specification Defect:** The system matches the specification perfectly, but the underlying requirement is incorrect or inconsistent. This triggers a secondary analysis:
  - **Scope Gap:** The business team clearly owns the domain, but a new or corrected rule is required.
    - *Action:* Route the update through formal change control.
  - **Responsibility Gap:** The rule is missing and domain authority is unclear.
    - *Action:* Escalate directly to client leadership to assign a business owner before making system modifications.

## 4. Communicating the Distinction Without Renegotiation

UAT surfaces different kinds of communication challenges, and how I handle each depends on where the tension actually lives.

### Case 1: Authority Ambiguity

When I communicate a scope gap to a customer, I never start by arguing about contracts or what is "out of scope." That just makes people defensive and invites a renegotiation. Instead, I frame the conversation entirely around authority. As the implementation team, we are not city planners or fire marshals; we do not have the regulatory authority to define city policy. If an unwritten requirement surfaces, I tell the client that I don't qualify to make that policy decision on their behalf. I ask them to have an authorized department head define the rule. If they push back and tell us to "just figure it out," I escalate to their project sponsor, framing it as a liability risk: we cannot configure software to enforce a city ordinance that the city itself hasn't formally defined.

**Example:** "My team doesn't have the Fire Code authority to decide what is considered a life-safety risk — if the Fire Marshal wants to lower the threshold, we need it in writing."

### Case 2: Scope Gap Under Timeline Pressure

When a legitimate, approved requirement surfaces too late for the remaining timeline to absorb, the math simply doesn't work. My job isn't to unilaterally defer the work or volunteer an extended launch date. Those decisions are above my paygrade. My job is to surface the objective tradeoffs to the PM and executive sponsor by presenting three explicit paths:

- **Option 1 — Defer to Phase 2.** Hold the go-live date, accept a functional gap at launch, and track the requirement for post-production delivery.
- **Option 2 — Extend the Launch Window.** Preserve full scope, but push the timeline out by the required build duration (requires sponsor and council notification).
- **Option 3 — Interim Workaround.** Deploy a temporary manual process at go-live, then deliver the automated configuration in Phase 2 to manage technical debt.

I present these tradeoffs in writing. Once leadership makes a determination, we document the choice and configure accordingly. My role is to make the options visible and defensible; their role is to make the call.

**Example:** State-mandated CO field surfaces in Month 7. The three options with cost and impact go to the Mayor's office. They decide; we configure to their decision.
