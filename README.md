# Senior Implementation Playbook

A set of frameworks for approaching complex regulated implementations — the kind where legacy infrastructure, competing stakeholders, fixed political deadlines, and ambiguous scope all collide.

I developed these frameworks while working through a highly constrained, multi-department modernization initiative. The scenario had legacy infrastructure, competing stakeholders, fixed political deadlines, and ambiguous scope — the kind of environment where technical decisions and political decisions are the same decision.

I'm publishing the frameworks because they're portable. The scenario was regulated-industry implementation work under political constraint — same shape as healthcare payer projects, financial services compliance rollouts, utility modernizations, and any environment where multiple stakeholders with legitimate authority disagree about priorities under a fixed clock.

---

## The Frameworks

Each framework stands alone. Read whichever one is relevant to what you're working on.

**[Political-First Discovery Sequencing](frameworks/political-discovery-sequencing.md)**
How to order your first 30 days of discovery across competing departments — starting with the department that gives you political cover, not the one making the most noise.

**[Family-Variant Architecture](frameworks/family-variant-architecture.md)**
Configuring 50+ workflow variants without building 50 different configurations. Grouping by routing pattern, not by domain or department.

**[Infrastructure-First Phasing](frameworks/infrastructure-first-phasing.md)**
Sequencing implementation waves by database integration complexity rather than business value. When to accept short-term political cost to protect the timeline.

**[Tiered Governance](frameworks/tiered-governance.md)**
How to document decisions in proportion to what's at stake. Preventing verbal decisions from becoming disputes without turning every conversation into a formal negotiation.

**[Argue About Authority, Not Scope](frameworks/authority-not-scope.md)**
The communication pattern that lets you handle scope gaps without opening a renegotiation. Reframing "out of scope" conversations as authority conversations.

**[Three-Option Framework for Scope Gaps Under Timeline Pressure](frameworks/scope-gap-three-options.md)**
When a legitimate scope gap surfaces late in the project, how to route the decision to the right authority instead of absorbing it silently.

**[Integration Readiness Questions](frameworks/integration-readiness-questions.md)**
The five questions to ask before writing a single line of an integration specification — turning integration risk into verifiable preconditions.

**[Pre-UAT Validation Gate](frameworks/pre-uat-validation-gate.md)**
Staging validation so you're not using the customer to find integration bugs. The discipline that separates a clean go-live from a rescue project.

---

## The Case Study

For anyone who wants to see how the frameworks emerged from the scenario, the full deliverables are here:

- [The Scenario](case-study/scenario.md)
- [Deliverable 1: Solution Design & Phasing Summary](case-study/deliverable-1-solution-design.md)
- [Deliverable 2: Test Case Library](case-study/deliverable-2-test-cases.md)
- [Deliverable 3: Integration Risk Assessment](case-study/deliverable-3-integration-risk.md)

---

## Reflection

[What worked, where the reasoning had blind spots, what I'd do differently](reflection.md)

---

## About

I'm Sukrit Chakravarty. I've spent 14 years doing configuration analysis and implementation work in healthcare — Epic Radiant at Scripps, QNXT at TriZetto, and D-SNP claims and utilization management at San Francisco Health Plan. The frameworks here reflect what I've learned about doing this kind of work in regulated environments where technology decisions are always also political decisions.

Currently building AI-forward tools for implementation and regulatory work — the same kind of complexity these frameworks address, but with the leverage of modern AI applied where it actually helps.

- LinkedIn: [linkedin.com/in/sukrit-chakravarty-549016156](https://www.linkedin.com/in/sukrit-chakravarty-549016156/)
- GitHub: [github.com/gitsukrit](https://github.com/gitsukrit)
- Email: sukritchakravarty@gmail.com
