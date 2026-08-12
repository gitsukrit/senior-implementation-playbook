# Pre-UAT Validation Gate

## The problem

User Acceptance Testing is supposed to be the final validation step before go-live — where the customer's staff exercises the system against real-world workflows and confirms it does what they need. In practice, UAT often becomes the phase where integration bugs surface for the first time, because nobody validated the integration end-to-end before turning the customer loose on it.

When UAT is the first real integration test, three things happen. The customer discovers bugs. The customer loses confidence in the system. The team scrambles to fix issues under launch pressure, in an environment where every fix ships to customer testers immediately.

The move is to establish a **pre-UAT validation gate**. UAT does not begin until integration testing has been done systematically in a staging environment, against real data flows, with documented pass criteria. We do not use the customer to find integration bugs.

## The pattern

A staged validation sequence in the months leading up to UAT. Each stage has a specific purpose and a hard pass/fail criteria. UAT is gated behind all stages passing.

**Month 1 — Proof of Connection.** Verify the vendor's system can securely connect to the counterparty's system and push a single test record round-trip. If this baseline fails, escalate immediately — nothing downstream can proceed until basic connectivity works.

**Month 2 — Data Contract.** Freeze the exact data mapping, security rules, and performance limits in writing with the counterparty. This document becomes the unbending standard that every subsequent test measures against. Not a spec that can change — a contract that requires formal renegotiation to modify.

**Months 2-3 — Internal Resilience Testing.** Test the vendor system's error handling internally. Simulate connection drops, timeouts, malformed responses, and partial failures. Confirm the retry queue holds data safely without crashing. This surfaces the failure modes that only appear under adverse conditions.

**Month 4 — Staging Alignment.** Connect to the counterparty's actual staging environment. This is where undocumented behavior surfaces — the counterparty's system doesn't quite match their written contract, edge cases produce unexpected responses, or documented endpoints behave differently in staging than in production. Better to find these in staging than in UAT.

**Months 5-6 — End-to-End Simulation.** Push a fully formatted, sanitized workflow record from the vendor system all the way through to the counterparty's staging map or destination. Verify the record plots correctly, the exact approved fields display, and the round-trip completes as expected.

**The Pre-UAT Gate itself.** Written checklist. UAT does not begin until the data contract is locked and the end-to-end staging simulation passes 100%. No exceptions for schedule pressure.

## Why "skip pre-UAT and go straight to UAT" is wrong

Three failure modes.

**The customer becomes the first line of QA.** When UAT is the first real integration test, the customer's staff are the ones discovering the failure modes. Their confidence in the system drops with every bug. Even if you fix the bugs quickly, the customer's memory of "the system didn't work in UAT" persists. Trust is expensive to rebuild.

**Fixes ship to customer testers immediately.** In UAT, every change you make is visible to the customer. There's no space to fix issues quietly. Every fix is a public event that reinforces the perception that the system isn't ready. This compresses the team's ability to fix things thoughtfully — every hour matters, so shortcuts get taken.

**Political pressure compounds technical pressure.** When UAT reveals integration issues, leadership on both sides gets involved. What was a technical challenge becomes a political situation. The team ends up managing the customer's leadership perception at the same time as fixing the actual bugs. Both suffer.

The pre-UAT gate exists to move all of this work into an earlier phase, where fixes happen out of the customer's view and the team has time to be thoughtful.

## What this looks like in practice

**The gate is a written checklist, not a status update.** A specific document with specific pass criteria. Every stage of the pre-UAT sequence has a line on the checklist. Every line has a signature or timestamp confirming pass. UAT scheduling references the checklist explicitly — "UAT begins after checklist item 6 is signed."

**The internal PM enforces the gate, not the customer PM.** The customer PM will feel pressure to start UAT on schedule regardless of whether the checklist is complete. Your internal PM is the one who holds the line. This is why the framework is written down — the internal PM needs an external authority to point to when the customer PM pushes to skip stages.

**Failure at any stage escalates, not deferred.** If the Proof of Connection fails in Month 1, that's not "we'll figure it out later." That's an immediate escalation to leadership on both sides. Every deferred failure at an earlier stage becomes a compounded failure at UAT.

**The gate protects the counterparty too.** Sometimes the pre-UAT validation reveals that the counterparty's system isn't as ready as they claimed. This is the moment to surface it — before UAT, when there's still time to renegotiate. If the counterparty's staging environment doesn't exist, or their documentation has drifted, better to know in Month 4 than Month 8.

**The signature move.** The specific line to have in your head, and to say out loud to your PM and to the customer if necessary: *"We do not use the customer to find integration bugs."* This is not just a discipline. It's a commitment about the kind of implementation team you are.

## The transferable insight

The gate is not a checkpoint. It's a **discipline**.

**Validation happens in the staging environment before the customer sees the system. Every deferred validation is a bug the customer discovers instead of the team.**

This applies to any implementation where the customer's staff will be exercising the system before go-live — enterprise software rollouts, healthcare platform migrations, financial system upgrades, government technology modernizations. The pattern of skipping validation to hit the schedule is the pattern that generates most late-project rescues.

**The team that validates rigorously in staging is the team that ships confidently in production. The team that uses UAT as validation is the team that never fully ships.**

## Where this framework has limits

**When the counterparty has no staging environment.** If the counterparty can't provide staging access, the pre-UAT sequence has to adapt — mocked responses in your own environment, contract-based validation against the written data contract, extra monitoring in the first hours of production. The gate still exists, but the specific checks change.

**When the timeline genuinely doesn't allow the sequence.** Some engagements are so time-constrained that the pre-UAT sequence has to be compressed. In that case, the gate becomes a formal risk acknowledgment — the customer's leadership signs a document accepting that UAT will function as first-line QA and that discovered bugs will be handled in a specific way. The gate is not skipped — it's replaced with an explicit risk contract.

**When the customer refuses to accept the gate.** Some customers see pre-UAT validation as vendor overhead and push to start UAT immediately. In that case, you either enforce the gate anyway (accepting the political cost) or you document that UAT is starting without pre-UAT validation and accept the risk. The framework can't force the customer's hand — but it can make the risk explicit.

## Related frameworks

- [Integration Readiness Questions](integration-readiness-questions.md) — for the precondition audit that precedes the gate
- [Tiered Governance](tiered-governance.md) — for the documentation discipline that enforces the gate
- [Family-Variant Architecture](family-variant-architecture.md) — for the configuration structure that pre-UAT tests against
