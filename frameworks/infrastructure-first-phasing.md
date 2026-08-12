# Infrastructure-First Phasing

## The problem

Once you've grouped workflow variants into families, you have to decide the order in which to build them. The tempting move is to sequence by business value — build the workflows the customer cares most about first. This maximizes early visibility and gives the customer wins to point to.

Business-value sequencing collapses when the underlying infrastructure isn't ready to support it. And in most legacy modernizations, the infrastructure is a real constraint — legacy databases with concurrency limits, resistant IT teams building pipelines, integration counterparties on their own schedules.

If you sequence by business value first and infrastructure isn't ready, you either delay the launches (breaking the go-live commitment) or ship on top of unstable infrastructure (breaking everything else).

The better move is to sequence phases by **database and integration complexity**, not by business value. Accept short-term political cost to protect the timeline.

## The pattern

Order the phases so that each wave requires slightly more infrastructure capability than the previous one. The IT team builds pipelines in the background while your team configures the workflows that need those pipelines.

The rough shape:

**Wave 1 — Read-only workflows.** Configurations that only read from the legacy database. No writes back, no integrations. Build in Months 1-2 while IT works on write pipelines.

**Wave 2 — Single-threaded writes.** Configurations with linear task generation and simple database writes. Build in Months 3-4 as write pipelines come online.

**Wave 3 — Parallel writes and complex routing.** Configurations with concurrent processing, parent/child dependencies, and heavy write patterns. Build in Months 5-6 once infrastructure is fully mature.

**Wave 4 — Lifecycle and batch operations.** Configurations that trigger on schedules, generate recurring records, or run as batch jobs. Build in Month 7.

**Wave 5 — Hardening, load-testing, and UAT.** Break the system on purpose in the months before go-live. Load-test the database bottleneck, cross-department integration testing, hands-on UAT with real staff.

Each wave respects a specific infrastructure boundary. Wave 1 doesn't ask IT to do anything they haven't already done. Wave 2 requires the first write capability. Wave 3 stresses the write layer. Wave 5 stresses everything.

## Why "business value first" is wrong

Business-value sequencing feels right because it aligns with customer priorities. Give the customer what they care about most, first. That's how you show progress.

The problem is that the workflows a customer cares about most are usually the most infrastructure-heavy. In this specific scenario, the heavyweight concurrent-review workflows are the most business-valuable and also the most infrastructure-demanding — parallel database writes, complex parent/child task dependencies, cross-department consolidation.

If you build the heavyweights in Wave 1, one of two things happens:

**One** — IT hasn't built the write pipelines yet, so you're blocked. The launch delays and the "we prioritized business value" story reverses into "we prioritized business value and it derailed the timeline."

**Two** — IT rushes to build pipelines under pressure, ships something unstable, and every downstream wave inherits the instability. Wave 5 UAT becomes a disaster because the infrastructure is the bug, not the workflow configuration.

Infrastructure-first sequencing accepts that Wave 1 will feel less impressive to the customer. The trade-off is protecting the delivery of the higher-value waves later.

## What this looks like in practice

**A political containment move in Wave 1.** Include one high-visibility workflow from a politically heavy department in Wave 1, even though the department itself isn't fully addressed until later. This gives the politically loud executive a visible win without dragging their department's complex workflows into the first phase. It buys political cover while infrastructure ripens.

**A middleware recommendation for the database bottleneck.** If the legacy database can't handle expected concurrent load, propose a staging layer — a modern database that handles real-time transactional traffic and syncs to the legacy system via nightly batch. This is not a Phase 1 requirement; it's a Phase 1 recommendation surfaced early so the customer's IT team has time to evaluate and approve. Don't decide unilaterally.

**A hard scope freeze late in the phasing.** Any new workflow requests after a defined date go to Phase 2. This is enforced through governance discipline, not by refusing to talk about them. See [Tiered Governance](tiered-governance.md).

**QA overlap in every wave.** Every wave has both a build focus and a QA focus. Wave 1 QA validates read access. Wave 2 QA validates single-thread writes. Wave 3 QA validates parallel routing. QA is not a phase — it's a discipline running across every wave.

## The transferable insight

The move is to sequence by what constrains you, not by what motivates you.

**Business value tells you what matters. Infrastructure tells you what's possible. Sequence by the constraint, not the motivation.**

This applies in any environment where technical dependencies gate downstream work — data platform migrations, financial system consolidations, ERP replacements, healthcare payer configurations. The customer's priority list is real information, but it's not a build sequence.

Protect the timeline by building what you can build now, not what you wish you could build now.

## Where this framework has limits

**When infrastructure is genuinely ready.** If the underlying infrastructure has been prepared in advance and isn't a constraint, sequence by business value. Infrastructure-first is a response to a constraint — if the constraint isn't there, don't invent it.

**When the customer explicitly refuses infrastructure sequencing.** Sometimes the customer's political commitment is to specific high-value workflows shipping first. If they've publicly committed and can't be moved, you sequence by their priorities and accept the elevated timeline risk. Then document the risk aggressively.

**When infrastructure complexity is unpredictable.** In new domains where you haven't seen the infrastructure patterns before, you might sequence based on the wrong complexity estimate. Build the first wave, learn what actually breaks, and re-sequence the later waves based on what you learned.

## Related frameworks

- [Family-Variant Architecture](family-variant-architecture.md) — for the grouping that this framework sequences
- [Tiered Governance](tiered-governance.md) — for enforcing scope freezes late in the phasing
- [Three-Option Framework for Scope Gaps Under Timeline Pressure](scope-gap-three-options.md) — for handling scope requests that surface late in the sequencing
