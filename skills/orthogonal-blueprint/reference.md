# Orthogonal blueprint — reference

Use when domain context or pushback scripts help the user more than the core protocol alone.

## Domain-specific orthogonal lenses

### Fintech

- Treat regulation as design input, not post-hoc paint.
- Separate layers orthogonally: settlement vs ledger vs risk—independent where possible.
- Myopic trap: coupling core transaction logic to a single payment-provider SDK.

### System / infrastructure

- Orthogonal split: control plane vs data plane.
- Myopic trap: scaling out hardware before fixing architecture or failure domains.
- Adversarial: operator-as-attacker (misconfig, insider, compromised credentials).

### Network / hardware

- Orthogonal: firmware vs hardware—can you upgrade behavior without silicon changes?
- Myopic trap: assuming today’s throughput forever.
- Temporal: behavior at ~100× traffic or failure rates.

### Web / mobile product

- Inversion: can the feature be removed instead of built?
- Myopic trap: optimizing for today’s user mental model vs underlying goal.
- Abstraction: UX symptom vs missing or wrong data model.

## Anti-patterns to refuse

Do not let these pass unchallenged:

1. **"We need microservices"** — Does team size and actual scale justify the operational cost?
2. **"We need AI/ML"** — Would a simpler rule-based or deterministic approach suffice first?
3. **"We need real-time"** — What delay does the user or SLA actually tolerate?
4. **"We need horizontal scaling"** — Have vertical limits been hit with evidence?
5. **"Everyone uses X"** — Assumption inheritance, not verified reasoning.
