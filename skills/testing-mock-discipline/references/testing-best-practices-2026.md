# Testing Best Practices (Source-Backed)

## 1) Avoid overusing mocks
Source: Google Testing Blog, "Testing on the Toilet: Don’t Overuse Mocks"  
Link: https://testing.googleblog.com/2013/05/testing-on-toilet-dont-overuse-mocks.html

Key points:
- Overusing mocks can reduce readability and maintainability.
- Behavior-heavy mocks leak implementation details into tests.
- Mock-based tests can diverge from real runtime behavior.
- Prefer local hermetic servers or fakes when possible for stronger fidelity.

## 2) Mock modules carefully in Vitest
Source: Vitest API (`vi.mock`)  
Link: https://vitest.dev/api/vi.html

Key points:
- `vi.mock` is hoisted and rewires module behavior at load time.
- Vitest notes module mocking limitations and recommends dependency injection in same-file/internal-call cases that cannot be safely mocked.
- Treat module mocking as a powerful but high-coupling tool.

## 3) Manual module mocks are explicit and structural
Source: Jest docs, "Manual Mocks"  
Link: https://jestjs.io/docs/manual-mocks

Key points:
- Manual mocks require dedicated `__mocks__` structure and explicit calls.
- They are useful for speed/stability, but can make tests dependent on mocked module behavior rather than real integrations.
- Use deliberately and keep scope narrow.

## 4) Confidence comes from tests resembling real usage
Source: Testing Library Guiding Principle  
Link: https://testing-library.com/docs/guiding-principles

Key points:
- The more tests resemble real usage, the more confidence they provide.
- Favor observable behavior over implementation details.

## 5) Balanced portfolio beats single test style
Source: Martin Fowler, "The Practical Test Pyramid"  
Link: https://martinfowler.com/articles/practical-test-pyramid.html

Key points:
- Use a mix of unit, integration, and higher-level tests.
- Avoid relying only on one layer.
- Keep terminology consistent in the team and optimize for fast, reliable feedback.

## Practical synthesis
- DI improves test seam clarity and reduces pressure for module-level mocks.
- Integration tests validate wiring risks that module mocks often hide.
- Keep mock usage intentional: narrow scope, explicit reason, and short lifetime.
