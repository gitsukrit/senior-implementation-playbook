# Integration Readiness Questions

## The problem

Integrations fail in a small number of predictable ways. The failure modes don't require sophisticated analysis to surface — they require asking the right questions before writing a single line of specification. Most implementation teams skip that step, either because the questions feel like they should be someone else's job or because there's pressure to start building.

The result is what everyone in this line of work has seen too many times: an integration that looked technically feasible turns out to be architecturally impossible because a precondition was never verified. The team discovers this during UAT, when there's no time to recover.

The move is to treat integration risk as a set of **verifiable preconditions** — specific questions with specific answers that either exist or don't. If any of them don't exist, the integration is unspecifiable in its current form, and the timeline needs to reflect that reality before build begins.

## The pattern

Five questions to ask before writing any integration specification. Each question has a concrete answer — a yes/no, a name, or a date. Vague responses mean the precondition isn't in place.

**1. Dependency.** Do we have a funded, scheduled technical contact at the counterparty right now? Not a name in a directory. A real person with allocated time to work with us on the integration. If that person doesn't exist or isn't scheduled, the integration is a fiction.

**2. Documentation.** By what date will the counterparty provide the technical specification we need to evaluate feasibility? What is their commitment to notifying us of changes to the specification before go-live? A one-time document is not enough — integrations exist in a moving environment, and we need commitment to change notification.

**3. Sandbox.** Does the counterparty have an isolated staging environment we can test against without affecting production? "We'll test in production" is not a viable answer. If there's no sandbox, we're either testing on live users or we're not testing.

**4. Security.** Has the customer's internal IT or security team approved the authentication protocols for the connection? Not "we plan to" or "we've submitted the request." Approved. If approval hasn't happened, the integration timeline needs to include the approval process, which is often months.

**5. Authority.** If the counterparty's system can't technically support the promised functionality — data volume, latency, uptime — who has the authority to modify the go-live commitment? If nobody has that authority, the integration timeline is not a plan, it's a hope.

The questions are ordered by dependency. If Question 1 has no answer, the others are premature. If Question 5 has no answer, the earlier answers don't matter — the integration is politically undefended.

## Why "start building and see what breaks" is wrong

Two failure modes.

**Silent precondition failure.** You start the build assuming the preconditions exist. Halfway through, you discover the counterparty's technical contact was never actually assigned, or the API documentation was accurate at some point in the past but has drifted, or the sandbox doesn't actually exist. Now you have partially-built work you can't finish, and you're negotiating for what should have been secured at the start.

**Political precondition failure.** Even if the technical preconditions are in place, the political precondition — who has the authority to change the commitment if the integration can't be delivered as promised — is often missing. When the delivery pressure hits, nobody knows who can make the call to reduce scope or extend the timeline. The integration ships broken because the political structure to handle failure was never established.

The five questions are designed to surface both failure modes before the build begins. If any question can't be answered concretely, the integration risk is not "we might have some issues" — it's "this precondition doesn't exist yet, and until it does, the specification is premature."

## What this looks like in practice

**Ask the questions before drafting the spec, not after.** The natural instinct is to draft a specification and then flag risks. This inverts the order — the questions come first, the specification comes after the questions have real answers.

**Get answers in writing.** Verbal answers to these questions are worse than no answers, because they create a false sense of confidence. "Yes, we have a technical contact" from a project manager who hasn't actually confirmed with the counterparty's technical team doesn't count. The answer has to come from someone with direct knowledge, in writing.

**Escalate concrete gaps to leadership immediately.** If you learn that Question 4 has no answer — the customer's security team hasn't approved authentication protocols — that's not a technical issue to resolve later. That's a leadership decision about whether to proceed with the integration in scope. Surface it in writing to the customer PM and the internal PM the same day you learn it.

**Distinguish between counterparty risks and customer-owned risks.** Some of these questions are the counterparty's problem to answer (Documentation, Sandbox). Others are the customer's problem to answer (Security approval, Authority for scope changes). Route the questions to the right owners and don't let the customer or counterparty offload their questions onto each other.

**Time-box the answers.** Give the customer and counterparty a specific deadline to provide the answers. Two weeks is reasonable for most environments. If the answers aren't in by then, the integration is at material risk, and the risk needs to be surfaced formally in the integration risk assessment.

## The transferable insight

Integration risk is not a technical assessment. It's a **precondition audit**.

**Every integration failure mode has a corresponding precondition. Surface the preconditions, verify them, and refuse to build until they're in place.**

This applies to any system-to-system integration where the counterparty is outside your direct control — vendor APIs, government data services, third-party payment processors, legacy system connectors, partner platforms. The specific preconditions vary. The pattern of verifying them upfront doesn't.

**The alternative — building without verified preconditions — is not a risk-taking strategy. It's a way of guaranteeing failure at the least convenient moment.**

## Where this framework has limits

**When the counterparty is inside your organization.** For internal integrations, most of these preconditions are already in place implicitly. Asking them formally feels like process for its own sake. Judgment call — but bias toward asking anyway if the integration crosses team boundaries.

**When the counterparty refuses to answer.** Some counterparties refuse to answer precondition questions until they're contractually required to. In that case, the answers are a leverage question — you need the customer to require the answers as part of their agreement with the counterparty. Escalate the leverage question to leadership.

**When the answers change during build.** Preconditions verified at the start can degrade over time — the technical contact leaves, the sandbox goes offline, the documentation drifts. Re-verify preconditions at key milestones — end of design, before build starts, before UAT begins. Preconditions are not one-time checks.

## Related frameworks

- [Pre-UAT Validation Gate](pre-uat-validation-gate.md) — for the validation discipline that follows precondition verification
- [Tiered Governance](tiered-governance.md) — for the documentation discipline around counterparty commitments
- [Three-Option Framework for Scope Gaps Under Timeline Pressure](scope-gap-three-options.md) — for handling precondition failures that surface late
