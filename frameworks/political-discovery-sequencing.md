# Political-First Discovery Sequencing

## The problem

Your first 30 days on a complex implementation set the tone for everything that follows. Three departments are competing for priority. Each believes their workflows should be configured first. The politically loudest one is often the most dangerous to prioritize — they'll extract commitments during discovery that constrain every downstream decision.

Most implementation teams sequence discovery on a first-come-first-served basis, or by whichever department is easiest to schedule. Both approaches surrender control of the scene to whoever pushes hardest.

The better move is to sequence discovery **politically**, not operationally.

## The pattern

Rank the departments by three criteria — none of them "which one talks the loudest":

**1. Isolation.** Which department has the least cross-departmental workflow entanglement? That department goes first. You get a clean environment to prove baseline architecture without dragging the political mess of the other departments into your first sprint.

**2. Regulatory sharpness.** Which department has the highest life-safety or regulatory stakes? That department goes second. Regulatory constraints need early architectural clarity — if you defer them, they surface later as design-breaking changes.

**3. Political heaviness.** Which department has the most executive access, the most public visibility, or the most connection to the go-live commitment? That department goes **last**. By the time you get to their discovery, you have wins from the first two departments, technical credibility, and momentum. That's leverage.

## Why the "loudest first" instinct is wrong

The politically loudest department almost always wants their workflows configured first because they know that first-mover position lets them shape the architecture in their favor. If you concede that, you spend the rest of the project constrained by design decisions optimized for one department's needs.

Entering their discovery last is not avoidance. It's positioning. You show up with:

- Evidence that the technical approach works (from the isolated first department)
- Regulatory patterns already understood (from the sharp-stakes second department)
- Political capital from two successful discoveries under your belt

Now the loudest department is negotiating with someone who has an established track record, not someone begging for permission to start.

## What this looks like in practice

**Week 1** — Meet with your own sales team before meeting the customer. Understand what was verbally promised to the politically heavy department that isn't in the signed statement of work. You need to know the delta before you walk in.

**Weeks 1-2** — Discovery with the isolated department first. Prove baseline data integration works. Prove routing patterns work. Get one department mapped completely.

**Weeks 2-3** — Discovery with the sharp-stakes regulatory department. Bring the architectural findings from the first department as context. Regulatory reviewers respect technical rigor.

**Weeks 3-4** — Discovery with the politically heavy department. You now have two departments mapped, a demonstrated approach, and technical credibility. Their loudest scope demands land differently when they can see what you've already delivered.

## The transferable insight

The move that makes this work is not the specific department order. It's the underlying principle:

**Sequence political engagements to build leverage, not to accommodate volume.**

Loud stakeholders extract commitments during discovery. Quiet stakeholders reveal architecture. Regulatory stakeholders enforce constraints. All three are legitimate, but they should not enter the room in the same order.

## Where this framework has limits

**When there's no politically loud stakeholder.** If the environment is genuinely collaborative, political sequencing is unnecessary overhead. Discover in whatever order makes operational sense.

**When the "isolated" department doesn't exist.** Some organizations have such tight cross-department integration that no department is truly isolated. In that case, sequence by regulatory sharpness first and accept that political sequencing will be harder to preserve.

**When the executive sponsor forces a specific order.** Sometimes the go-live commitment was made about specific workflows in a specific order. Then political sequencing is subordinate to the commitment. Adapt.

## Related frameworks

- [Argue About Authority, Not Scope](authority-not-scope.md) — for handling scope demands from the politically heavy department
- [Tiered Governance](tiered-governance.md) — for preventing verbal commitments from becoming disputes
- [Three-Option Framework for Scope Gaps Under Timeline Pressure](scope-gap-three-options.md) — for when politically-driven scope surfaces mid-project
