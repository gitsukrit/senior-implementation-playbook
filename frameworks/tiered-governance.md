# Tiered Governance

## The problem

Every complex implementation accumulates decisions. Some are trivial — which day the weekly meeting happens. Some are consequential — whether a new workflow gets added to Phase 1 scope. Most are somewhere in between.

If you treat every decision with the same governance weight, the project slows to a crawl. Every conversation becomes a formal negotiation. Momentum dies.

If you treat every decision as informal, verbal decisions accumulate and become disputes later. A customer PM says "yes, we agreed to that in Tuesday's call" three months after the fact. The vendor team says "that was never a decision, we were exploring options." Now the project has a fight instead of a launch.

The move is to match documentation formality to the weight of the decision — not because it's more polite, but because it's the only sustainable discipline for a long engagement.

## The pattern

Three tiers, each with different documentation requirements:

**Tier 1 — Routine.** Everyday operational choices. Meeting schedules, minor process adjustments, task ordering. Captured in standard meeting minutes distributed after the session. No formal sign-off required. Silence is acceptable consent because nothing at stake requires more.

**Tier 2 — Scope, timeline, or cost.** Any decision that affects what's being built, when it launches, or how much it costs. Requires explicit written confirmation from the customer's executive sponsor before it takes effect. Verbal "yes" from the customer PM is not sufficient. Silence is not consent.

**Tier 3 — Verbal technical constraints from external parties.** When an IT team, vendor, or contractor communicates a technical limit or design constraint verbally, capture it in a follow-up email that summarizes the constraint and confirms your team is designing to it. Something like: *"Confirming our design aligns with the 50 requests-per-minute limit discussed today. Let me know if this needs adjustment."* This creates a written trail of a verbal decision without turning the conversation into a formal negotiation.

Each tier has a specific purpose. Tier 1 preserves momentum. Tier 2 prevents scope creep. Tier 3 protects against verbal-decision drift.

## Why "one governance level for everything" is wrong

Two failure modes.

**Heavy governance everywhere.** Every conversation requires a formal decision log, every choice requires executive sign-off, every technical exchange becomes a contract negotiation. Nobody wants to talk to your team because talking to your team is expensive. Decisions get made outside your presence and land as surprises. You're not preventing disputes — you're just not in the room when they get formed.

**Light governance everywhere.** Every decision lives in verbal memory. When memories diverge — which they always do — you have no way to reconstruct what actually happened. The customer PM who characterizes verbal conversations as decisions when convenient will do exactly that, and you have nothing to point to. The vendor team who assumes verbal exploration doesn't count will find themselves surprised by a scope commitment they don't remember making.

Tiered governance is the middle path. It moves fast where speed matters and slows down where accuracy matters.

## What this looks like in practice

**Establish the tiers early.** Weeks 3-4 of the engagement is the right window. Late enough that you understand the customer's decision patterns. Early enough that no consequential decisions have accumulated undocumented.

**Communicate the tiers to the customer PM explicitly.** Not as a policy imposed on them, but as a shared discipline that protects both sides. "For routine items, minutes are enough. For scope, timeline, or cost, I need the sponsor's written sign-off before we act. For technical constraints from your IT team, I'll send a quick confirmation email. This way we can move fast without losing accuracy."

**Enforce the tiers in real time.** When the customer PM tries to move a scope decision through informal channels, don't refuse — redirect. "That sounds like a scope change. I'll draft the summary and send it to the sponsor. Once we have written confirmation, we'll add it to the build queue."

**Lock the scope freeze date.** Include a hard date in the governance framework beyond which new scope requests move to Phase 2. This is enforced through Tier 2 discipline — the sponsor can approve late scope changes if they want to accept the timeline impact, but the default is Phase 2.

**Documentation of verbal constraints.** For Tier 3, send the confirmation email within 24 hours of the conversation. Copy the customer PM even if they weren't in the technical conversation. This creates cross-visibility so verbal decisions don't get siloed inside a single relationship.

## The transferable insight

Governance is a spectrum, not a mode.

**Match documentation weight to decision weight. Fast where nothing's at stake. Formal where the outcome matters. Written where memory will fail.**

This applies to any long-running engagement with multiple stakeholders — implementation projects, program management, cross-functional initiatives, vendor relationships. The rule holds whether the "verbal decisions" come from a customer PM, a vendor account rep, or a peer on your own team.

Governance that scales with weight is governance that gets used. Uniform governance is governance that gets ignored.

## Where this framework has limits

**When the customer PM refuses to route Tier 2 decisions to the sponsor.** Some PMs guard access to the sponsor and refuse to escalate. You have to escalate anyway — your governance discipline is only as strong as your direct relationship with the party who can enforce it. Establish sponsor access early or the framework collapses.

**When the sponsor is politically weak.** Even with sponsor sign-off, if the sponsor can't enforce their own decisions internally, Tier 2 discipline doesn't stick. In that case, tiered governance shifts from enforcement to evidence — you're documenting decisions for the post-mortem, not preventing disputes in real time.

**When there's no scope freeze commitment.** The framework depends on the shared understanding that late scope requests default to Phase 2. If the customer refuses to accept a scope freeze date, Tier 2 discipline becomes negotiation instead of governance.

## Related frameworks

- [Political-First Discovery Sequencing](political-discovery-sequencing.md) — for the discovery phase that establishes the sponsor relationship the framework depends on
- [Argue About Authority, Not Scope](authority-not-scope.md) — for handling scope requests without opening renegotiation
- [Three-Option Framework for Scope Gaps Under Timeline Pressure](scope-gap-three-options.md) — for when Tier 2 decisions surface late in the project
