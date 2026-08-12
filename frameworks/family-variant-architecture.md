# Family-Variant Architecture

## The problem

You're staring at 50+ workflow variants and a 9-month timeline. The naive read is that this means 50+ configurations, 50+ testing efforts, 50+ places for bugs to hide. The math doesn't work.

Most implementation teams either commit to the impossible ("we'll configure all 50 in parallel") or gut the scope ("we'll only ship 15 in Phase 1"). Both are failure modes. The first collapses under its own weight. The second turns the launch into a disappointment.

The real move is to recognize that 50+ variants doesn't mean 50 workflows. It means 50 variations on a much smaller number of underlying routing patterns.

## The pattern

Group the variants by their **routing behavior**, not by their business domain, department, or category. Each group is a "family." Each family has a shared workflow skeleton and a set of configuration drivers. Individual variants are built as front-end variants of their family — same routing engine, different fields, fees, and rules.

The families I identified in this specific scenario:

**Family 1 — Rules-Driven Issuance.** High-volume, low-risk workflows requiring no human review. Front-end validation, automated fee calculation, auto-issue.

**Family 2 — Over-the-Counter.** Minor workflows needing single or dual-department review. Linear task generation, sequential precedence.

**Family 3 — Concurrent Review (Heavyweights).** Complex workflows where multiple departments review the same submission simultaneously. Parent/child task dependencies, gated advancement.

**Family 4 — Event-Driven.** Workflows driven by external calendars — public notice periods, board votes. Temporal triggers, custom outcomes.

**Family 5 — Recurring.** Workflows with ongoing scheduled lifecycle actions — annual renewals, periodic inspections. Batch triggers, duplicate-record prevention.

Any workflow variant falls into exactly one family. Configuring at the family level means the routing engine gets stressed once, not fifty times.

## Why "configure each variant separately" is wrong

The instinct to configure each variant as its own unit feels safer because it isolates risk — if one variant has a bug, it doesn't affect the others. In practice, this instinct multiplies work rather than isolating risk.

Configuring 50 variants separately means:

- The routing engine gets tested 50 times, each time with slight variations that make debugging harder
- Common patterns get re-implemented slightly differently each time, creating maintenance nightmares
- Testing coverage is shallow because there's no time to go deep on each variant
- A bug in the routing engine surfaces in 50 different-looking ways, making root-cause analysis a mess

Family-first configuration inverts all of this. The routing engine is built once, tested deeply, and every variant inherits its stability. When a routing bug appears, it appears in the family — not in one variant.

## What this looks like in practice

For each family, you build:

**A routing skeleton.** The sequence of task states, decision points, and transitions that define the family's workflow behavior. Same skeleton across all variants in the family.

**Configuration drivers.** The specific settings that differentiate variants within the family — task types, SLA timers, approver roles, fee schedules, custom fields, output formats.

**A golden-path variant.** One fully-configured variant per family, built end-to-end. This variant proves the family's architecture works and becomes the template for all other variants.

**A variant checklist.** The specific configuration steps required to stamp out a new variant from the family template. Once the checklist is stable, new variants can be configured in hours, not days.

Configuration effort scales with families, not variants. Five families with well-defined skeletons can produce 50 variants faster than 50 individually configured workflows can produce 15.

## The transferable insight

The move is to build for the pattern, not the specific.

**Fifty workflows doesn't mean fifty engines. It means one engine, run in fifty configurations.**

This applies wherever you're facing a large surface area with underlying similarity — healthcare benefit plans across multiple product lines, financial products across market segments, compliance rules across jurisdictions, retail policies across store formats. The specific variants matter to users. The underlying pattern matters to architecture.

Build the pattern once. Stamp the variants from it.

## Where this framework has limits

**When variants don't share underlying patterns.** If your 50 workflows genuinely have 50 different routing behaviors, family grouping won't emerge. In that case, you're not looking at variants — you're looking at 50 distinct systems, and the family approach adds no leverage.

**When variant behaviors diverge over time.** A family that started coherent can drift if individual variants get customized aggressively. Sometimes what starts as Family 3 becomes a new family unto itself. Recognize the drift early and split, don't patch.

**When the platform doesn't support inheritance-style configuration.** Family-variant architecture assumes the underlying platform can efficiently reuse skeletons across configured instances. If the platform requires custom code per variant, the architecture doesn't gain the expected leverage.

## Related frameworks

- [Infrastructure-First Phasing](infrastructure-first-phasing.md) — for sequencing which families to build first
- [Political-First Discovery Sequencing](political-discovery-sequencing.md) — for surfacing the family patterns during discovery
- [Pre-UAT Validation Gate](pre-uat-validation-gate.md) — for testing family-level behavior before scaling to variants
