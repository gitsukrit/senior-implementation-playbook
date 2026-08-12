# Argue About Authority, Not Scope

## The problem

Somewhere in every implementation, a customer tester or stakeholder surfaces a request that isn't in the specification. The natural instinct is to reach for the contract — "that's out of scope, we didn't sign up for that." Sometimes that's technically correct. It's almost always the wrong opening move.

The moment you frame the conversation around scope, you've invited a scope renegotiation. The customer starts thinking about what they thought they'd get versus what they're getting. Sales gets pulled into it. The lawyers eventually show up. What was a small request becomes a relationship-damaging fight.

Worse, a lot of these requests aren't really scope requests. They're **responsibility gaps** — moments where the customer is asking the vendor to make a policy or regulatory decision the vendor has no authority to make. Framing those as scope conversations misses the point entirely.

The move is to frame the conversation around **authority**, not scope.

## The pattern

When a request surfaces during testing or configuration that isn't clearly in the spec, run it through a three-question triage:

**Configuration defect.** The system deviates from the written spec. Fix immediately at no cost. This is your team's problem to solve.

**Specification defect.** The system matches the spec exactly, but the underlying requirement is wrong. The spec itself needs correction. This triggers a secondary analysis.

Under specification defect, two sub-cases:

**Scope gap.** A new or corrected rule is required, and the customer's business team clearly owns the domain. Route through formal change control. The customer decides how to fund and schedule the correction.

**Responsibility gap.** A rule is missing and it's unclear who has the authority to define it. Escalate directly to client leadership to assign an owner. Don't touch the system until authority is assigned.

The distinction between scope gap and responsibility gap is the whole game. Scope gaps go through change control. Responsibility gaps go to authority assignment.

## Why "arguing about scope" is wrong

Two failure modes:

**When you argue scope, you make everyone defensive.** The customer feels like they're being told they're wrong. They start defending the request. Sales gets called in. The conversation escalates because everyone's positioning around whether the request should have been included, rather than around how to handle it now.

**When you argue scope, you accept responsibility for policy decisions you can't make.** If a customer tester says "the system should trigger a review when X happens" and you argue that X isn't in the spec, you're implicitly accepting that this is your call to make. It isn't. Regulatory rules, compliance thresholds, policy decisions — these belong to the customer's authorized owners, not to the vendor's implementation team.

Reframing around authority sidesteps both failure modes. You're not saying "we won't do this." You're saying "we can't decide this — the person with authority needs to define the rule and put it in writing. Once they do, we'll configure it."

## What this looks like in practice

**The specific communication move.** When a scope gap surfaces, don't start by referencing the contract. Start by naming who has the authority to make the decision.

Example language:

*"My team doesn't have the authority to decide what constitutes an acceptable risk in this domain. If your subject-matter expert wants to change the rule, we need that decision in writing from them. Once they've made the policy decision, we'll adjust the configuration."*

The vendor isn't refusing. The vendor is redirecting the decision to the authorized owner. That's a different conversation.

**When the customer pushes back with "just figure it out."** Some customers respond to authority framing by trying to hand the decision back to you. Don't accept it.

*"We can't configure software to enforce a rule that hasn't been formally defined by an authorized owner. That creates strict liability exposure for both of us. Let me help you identify who should own this decision internally, and we'll wait until they've defined the rule."*

You've escalated the conversation from "will you do this?" to "who is authorized to decide this?" That's a much healthier fight.

**The Fire Marshal example.** In this specific scenario, a tester surfaces a request that a regulatory review should trigger under a different threshold than what's configured. Instead of arguing about the SOW, you say: *"My team doesn't have Fire Code authority to decide what constitutes a life-safety risk. We built the threshold based on the original spec. If the Fire Marshal wants to officially lower the threshold, they need to provide that updated rule in writing. Once the department makes that policy decision, we'll adjust the configuration."*

You've turned a scope fight into an authority conversation. The customer's team now has to figure out who has authority. That's their problem, not yours.

## The transferable insight

The move is to reframe the conversation before responding to it.

**Scope conversations invite renegotiation. Authority conversations invite ownership.**

This applies wherever an implementation team is asked to make decisions that properly belong to the customer's regulated owners — healthcare configurations, financial rule engines, compliance workflows, safety systems. The vendor doesn't have the authority to define the customer's rules. Making that explicit protects both sides.

**Never let the vendor become the de facto policy-maker for the customer's regulated environment. Escalate the authority question every time.**

## Where this framework has limits

**When you actually are configuring a scope gap.** Sometimes the request is genuinely a scope conversation — the customer wants a new feature that requires new work, and the authority to decide is clearly theirs. In that case, authority framing is misdirection. Route through change control directly.

**When the customer's internal authority is genuinely unclear.** Some organizations don't have clear ownership of policy decisions. If nobody at the customer knows who owns the rule, authority framing surfaces the ambiguity but doesn't resolve it. You have to work with customer leadership to establish the ownership before you can configure the rule.

**When the vendor actually is the authority.** In some domains — vendor-defined best practices, product capabilities, technical implementation choices — the vendor legitimately does have the authority. Don't punt these to the customer. Own them cleanly.

## Related frameworks

- [Three-Option Framework for Scope Gaps Under Timeline Pressure](scope-gap-three-options.md) — for scope gaps where authority is clear but timeline is the constraint
- [Tiered Governance](tiered-governance.md) — for the documentation discipline around authority decisions
- [Political-First Discovery Sequencing](political-discovery-sequencing.md) — for surfacing authority ambiguities during discovery
