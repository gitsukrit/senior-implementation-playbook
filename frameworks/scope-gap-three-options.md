# Three-Option Framework for Scope Gaps Under Timeline Pressure

## The problem

Sometimes a scope gap surfaces late in the project — Month 7 of a 9-month timeline, for example — and there's no authority ambiguity to redirect around. The customer's business team owns the domain, the rule is legitimate, and it needs to be built. But the timeline can't absorb the additional work without breaking something.

The naive move is to make the call yourself. Either "we'll fit it in" (silently absorbing scope you can't deliver) or "sorry, too late for this phase" (unilaterally deferring what the customer might have decided differently if given the choice).

Both are failure modes. The first breaks delivery. The second breaks the relationship. Neither respects that this is a decision belonging to the customer's authorized leadership, not to the implementation team.

The move is to surface the trade-offs as three concrete options and route the decision to the sponsor.

## The pattern

Present three options in writing to the customer's PM and executive sponsor. Each option has a different trade-off profile. The implementation team's role is to make the trade-offs visible and defensible — the leadership's role is to make the call.

**Option 1 — Defer to Phase 2.** Hold the go-live date. Accept a capability gap at launch. Track the requirement for post-launch delivery. Preserves timeline, sacrifices completeness at launch.

**Option 2 — Extend the launch window.** Preserve full scope. Timeline slips by the duration required to build the requirement. Requires executive sponsor and — if the go-live is a public commitment — communication to the political leadership that set the deadline.

**Option 3 — Interim workaround.** Deliver a partial or manual version at go-live so the workflow isn't broken. Full automated implementation ships in Phase 2. Accepts technical debt in exchange for preserving both timeline and workflow continuity.

Each option is complete on its own. Each has clear costs. The customer sponsor picks one — or asks for a hybrid — and the implementation team executes.

## Why "just decide unilaterally" is wrong

Two failure modes, mirror images of each other.

**Silently absorbing scope.** You commit to fitting the requirement into the existing timeline. Your team eats the extra work. The launch either slips anyway (breaking the commitment) or ships buggy (breaking downstream stability). Either way, the customer's leadership never had a chance to make an informed decision about the trade-off, and now they get to blame you for the outcome. This is the failure mode that ends careers.

**Unilaterally deferring.** You tell the customer "sorry, too late for this phase" without giving them options. The customer's leadership finds out about the deferral through their PM, not through you. Depending on who's told and how, this reads as vendor arrogance or vendor failure. The customer's political leadership may reverse the decision anyway, and now you've damaged the relationship and still have to build the requirement.

Both failure modes come from the same root cause: the implementation team made a decision that wasn't theirs to make. The three-option framework prevents this by forcing the decision back to the authority that owns it.

## What this looks like in practice

**Present in writing, not verbally.** The three options go in an email or a formal document to the sponsor and PM. Verbal presentations get remembered wrong and disputed later. The written record locks the options and the trade-offs so nobody can revise their memory later.

**Include cost, timeline impact, and risk for each option.** Not just "defer" or "extend" — actual numbers. Option 1: capability gap at launch, X features unavailable, deferred to Phase 2 estimated Q3 of next year. Option 2: launch date moves from Month 9 to Month 11, requires council notification. Option 3: manual workaround requires 40 hours of ongoing operator effort per month until Phase 2 automation ships. The specifics are what let the sponsor make a real decision.

**Do not recommend a preferred option unless asked.** Your job is to make the trade-offs visible. The sponsor's job is to weigh them against political and strategic priorities the implementation team doesn't fully see. If the sponsor asks for your recommendation, give one — but don't lead with it. Present the options neutrally first.

**Force closure with a deadline.** The written presentation includes a decision deadline. "Please confirm which option by end of week so we can adjust the build plan." Without a deadline, sponsors defer decisions indefinitely and the implementation team ends up making the call by default.

**Once the decision is made, execute it cleanly.** Document the decision in the project record. Adjust the build plan to reflect the chosen option. Don't relitigate. The sponsor made their call; your job now is to make their call work.

## The transferable insight

The move is to make scope decisions someone else's job — the right someone else's.

**Present options with trade-offs. Force the decision to the authority that owns it. Execute what they decide.**

This applies anywhere an implementation team gets pulled into decisions that properly belong to program leadership — enterprise software rollouts, healthcare configurations, financial systems, regulatory technology projects. The pattern of "just decide unilaterally" is tempting because it feels efficient. It's actually the pattern that generates the majority of late-project blowups.

**Never accept authority you weren't given. Never surrender authority that is yours.**

## Where this framework has limits

**When the customer sponsor is unavailable.** If the sponsor is out of pocket or unreachable, the framework depends on either waiting or escalating to whoever's above them. In some cases, the delay is worse than a unilateral decision. Judgment call — but bias toward waiting whenever possible.

**When the trade-offs are unclear.** Sometimes you genuinely don't know what the impact of each option is. In that case, the framework becomes: "Here are the three shapes of options. I need Week X to estimate the costs before presenting them formally. Can we schedule the decision for Week Y?" Don't present options without real numbers behind them.

**When the customer refuses to accept that a trade-off exists.** Some customers respond to the three-option framework by demanding "all three — deliver everything, on time, with no compromises." That's not a decision, that's a demand for magic. You surface it as impossible, document the ask, and route it to the sponsor's sponsor. The framework doesn't work if the customer refuses to engage with the reality of trade-offs.

## Related frameworks

- [Argue About Authority, Not Scope](authority-not-scope.md) — for scope requests where authority ambiguity exists
- [Tiered Governance](tiered-governance.md) — for the documentation discipline that makes this framework enforceable
- [Infrastructure-First Phasing](infrastructure-first-phasing.md) — for the phasing structure that Phase 2 refers back to
