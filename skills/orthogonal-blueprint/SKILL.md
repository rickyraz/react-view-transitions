---
name: orthogonal-blueprint
description: Applies orthogonal thinking to stress-test product ideas, draft system blueprints, and escape tunnel vision via boring-first gates, six perspective axes, orthogonality checks, reversibility maps, pre-mortems, and falsification criteria. Use when blueprinting a product, grilling or validating an idea, designing architecture, challenging assumptions, or when the user mentions orthogonal thinking, non-myopic design, or idea stress-testing.
disable-model-invocation: true
---

# Orthogonal Blueprint

## When to use

Apply when the user wants to: blueprint a product idea; grill, validate, or stress-test an idea; design system architecture; break tunnel vision; or challenge assumptions (any domain).

## Core premise

> Myopic = trapped on one axis. Orthogonal = move to a different axis entirely.

Myopic thinkers improve the existing path. Orthogonal thinkers find a different path. The goal is not to think harder—it is to think from a perpendicular dimension.

## Protocol

### Phase 0 — Boring solution gate (mandatory)

Before any axis shift:

> "What is the most boring, obvious solution that could possibly work?"

- State it explicitly.
- Can it be ruled out? If not—build it and stop.
- Continue only if the boring solution is genuinely insufficient.

Skipping this phase makes later analysis premature.

### Phase 1 — Decompose the problem

Extract:

1. **Surface problem** — what they say they want to fix
2. **Assumed solution** — what they already lean toward
3. **Underlying need** — what remains if the assumed solution disappears

Example:

```
Surface:    "Server is slow"
Assumed:    "Upgrade CPU"
Underlying: "Response time for users is unacceptable"
```

Reframe around the underlying need, not the surface symptom.

### Phase 2 — Six-axis shift

Rotate through these axes (each is a 90° shift from the default view).

**Axis 1 — Inversion:** What if we removed the problem instead of solving it? Can the need be eliminated? Is it caused by a reversible design choice?

**Axis 2 — Abstraction level:** Are we solving at the wrong layer? Step up (business vs tech) or down (hardware, network, protocol vs app).

**Axis 3 — Constraint reframing:** List assumed constraints; challenge each—is it real or inherited?

**Axis 4 — Temporal:** At 10x scale? At 0.1x? In ~5 years? The solution must survive at least one temporal view that is not "now."

**Axis 5 — Adversarial / red team:** If someone wanted this to fail, where would they attack? Weakest link? Second-order failure? What attacker, competitor, or regulator sees that builders miss?

**Axis 6 — Cross-domain pollination:** Strip domain jargon—what is the abstract shape? What field already solved that shape (biology, logistics, manufacturing, etc.)? Borrow the **mechanism**, not a loose metaphor.

### Phase 3 — Module independence (orthogonality test)

| Question | Pass |
|----------|------|
| Change this module without touching others? | Yes → orthogonal |
| Single clear responsibility? | Yes |
| Does interface change break internals? | No → separated |
| Composable via clean interface? | Yes |
| Hidden side effects? | No → orthogonal |

If a module fails 2+ checks, decompose it.

### Phase 3.5 — Reversibility classification

| Type | Meaning | Scrutiny |
|------|---------|----------|
| **Type 1 — Irreversible** | Undo is costly (data model, protocol, public API) | Full orthogonal analysis |
| **Type 2 — Reversible** | Cheap to change later (internal impl, tooling) | Best judgment, proceed |

Rules: Never treat Type 1 like Type 2. If unsure—Type 1. List Type 1 decisions explicitly in the blueprint. Reversibility changes with scale.

### Phase 4 — Myopia audit

- **Symptom patching:** Adding more of the same (RAM, instances, retries) often patches symptoms, not root cause.
- **Local optimization:** Fast module in a slow pipeline—still broken end-to-end.
- **Now-centric:** Valid only today? Team, volume, regulation, behavior change?
- **Assumption inheritance:** Constraints nobody verified—often the riskiest.
- **Solution-first:** Solution chosen before problem understood—return to Phase 1.

### Phase 4.5 — Pre-mortem and falsification

**Pre-mortem:** Assume the product failed in ~2 years. What killed it? Document top 3 **internal** failure modes (distinct from external adversarial axis).

**Falsification gate:** What observation would prove the core assumption wrong? How measured? By when? If none, the idea is not ready to blueprint.

Example:

```
Core assumption: "Users will pay $20/month for this feature"
Falsification:   "<5% of beta users upgrade after 30 days free"
Measurement:     Stripe conversion at day 30
Deadline:        Within 60 days of launch
```

## Blueprint output template

Use this structure after analysis:

```
## Problem (Reframed)
[Underlying need, not surface symptom]

## Boring Solution Considered
[Obvious path—and why ruled out, or why building it]

## Rejected Assumptions
[Constraints challenged and dropped]

## Axes Explored
- Inversion: [...]
- Abstraction shift: [...]
- Constraint reframe: [...]
- Temporal: [...]
- Adversarial: [...]
- Cross-domain: [...]

## Proposed Modules
[Each module: responsibility + orthogonality status]

## Reversibility Map
- Type 1 (irreversible): [...]
- Type 2 (reversible): [...]

## Composition Plan
[Interfaces: API, events, pipes, etc.]

## Pre-mortem Scenarios
[Top 3 internal failures ~2 years out]

## Falsification Condition
[Invalidating observation, metric, deadline]

## Known Risks (Non-Myopic)
[Second-order effects]

## What We Deliberately Chose NOT to Build
[Scope exclusions and why]
```

## Sign-off checklist

- [ ] Boring solution considered or chosen (explicit)
- [ ] Problem reframed to underlying need
- [ ] All six axes explored
- [ ] Modules pass orthogonality test
- [ ] Reversibility map; Type 1 listed
- [ ] Myopia audit (five traps)
- [ ] Pre-mortem: top 3 internal failures
- [ ] Falsification: condition, measure, deadline
- [ ] Rejected assumptions documented
- [ ] Second-order risks noted
- [ ] Explicit non-goals (what not to build)

## More depth

- Domain lenses (fintech, infra, hardware, web/mobile) and phrases to challenge: [reference.md](reference.md)
