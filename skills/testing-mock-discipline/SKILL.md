---
name: testing-mock-discipline
description: Analyze and improve automated testing strategy with a DI-first approach and disciplined mock usage. Use when reviewing test suites that overuse `jest.mock`/`vi.mock`/module mocks/filesystem mocks, when refactoring code to remove global singletons, when deciding unit vs integration vs e2e balance, or when asked to increase runtime confidence from tests.
---

# Testing Mock Discipline

## Overview
Use this skill to evaluate test quality, reduce brittle over-mocking, and move teams toward high-confidence tests through dependency injection, realistic fakes, and integration coverage.

## Workflow

### 1. Map the System Under Test
Identify what behavior must be trusted in production, then list dependencies by type:
- Pure logic: deterministic transforms/calculations.
- Internal collaborators: domain services/repositories/adapters.
- IO boundaries: filesystem, DB, network, queues, clock, randomness.

State which dependencies are currently global singletons or imported directly.

### 2. Run a Mock Smell Audit
Flag test smells that usually indicate weak abstraction design:
- Heavy `jest.mock`/`vi.mock` at module level for core business flow.
- File system mocks replacing most behavior of storage code.
- Tests asserting call choreography more than business outcomes.
- Unit tests that break after harmless refactors (implementation-coupled).
- Multiple mocks with long setup for a simple behavior claim.

Use this quick rule:
- If most test code is mock wiring, confidence is probably in the mock, not in runtime behavior.

### 2.1 Evaluate Mocking Fidelity Risks (Vitest-Specific)
Treat these as explicit risk signals during review:
- `vi.mock` changes module loading semantics (hoisting + import transformation), so tests can drift from real runtime behavior.
- Behavior can differ across environments (Node module runner vs Browser native ESM), which can reduce test fidelity.
- Mock registry and transform layers add complexity, increasing the chance that tests pass under mocked wiring but fail in production.

### 2.2 PR Red-Flag Checklist (Quick Scan)
Run this 5-item checklist on every test PR:
- Does a single test require more than two module-level mocks (`vi.mock`/`jest.mock`)?
- Does the assertion mostly verify internal call choreography instead of business outcome/state?
- Would a harmless refactor (rename/split/internal reorder) likely break the test?
- Is a filesystem/network/database dependency fully mocked when a hermetic integration test is feasible?
- Does the test pass only because transformed/registered mocks replace real runtime wiring?

If two or more answers are "yes", recommend DI seam refactor and move coverage toward integration tests.

### 3. Refactor Toward DI Seams
Prefer explicit dependency seams over implicit module patching.

Function injection pattern:
```ts
export function buildReport(readFile: (p: string) => Promise<string>) {
  return async (path: string) => {
    const raw = await readFile(path)
    return parseReport(raw)
  }
}
```

Constructor injection pattern:
```ts
class PaymentService {
  constructor(private gateway: PaymentGateway) {}
  async charge(input: ChargeInput) {
    return this.gateway.charge(input)
  }
}
```

Require tests to inject:
- Real dependency for fast hermetic integration tests when possible.
- Fake implementation for richer behavior contracts.
- Mock/stub only when failure paths or edge conditions are hard to trigger otherwise.

### 4. Choose the Right Test Level
Use this selection matrix:
- Unit test: pure logic or narrow branching rules.
- Integration test: adapter + boundary behavior (DB/filesystem/http client).
- E2E test: critical user journey and wiring across subsystems.

Bias toward integration when module mocking would hide real wiring risks.

### 5. Enforce Assertions that Matter
Prioritize user-visible/domain outcomes:
- Returned values, persisted state, emitted events, observable side effects.
- Avoid asserting internal call order unless it is business-critical behavior.

### 6. Report Findings Clearly
For each finding include:
- Risk: what can pass in CI but fail in runtime.
- Evidence: concrete test snippet or pattern.
- Fix: DI refactor + recommended test level.
- Confidence impact: why the change improves signal.

## Heuristics
- Keep module mocks as a tactical last resort, not a default architecture.
- Prefer fake implementations over fragile module rewiring.
- If a boundary can be made hermetic locally, test it with the real boundary code.
- Minimize global state in production code to simplify test setup.

## Output Template
When asked to analyze a test suite, answer in this order:
1. Top risks from current mock strategy.
2. DI refactors with concrete before/after patterns.
3. Suggested target test portfolio (unit/integration/e2e split).
4. Minimal migration steps the team can apply this sprint.

## References
Use and cite:
- `references/testing-best-practices-2026.md` for source-backed principles.
