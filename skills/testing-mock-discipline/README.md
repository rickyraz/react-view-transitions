# testing-best-practice

A reusable AI skill repository for reviewing test strategy quality, reducing harmful over-mocking, and migrating toward DI-first testing with a balanced unit/integration/e2e portfolio.

## Repository Layout

This repository currently contains one skill:

```text
skills/testing-mock-discipline/SKILL.md
skills/testing-mock-discipline/agents/openai.yaml
skills/testing-mock-discipline/references/testing-best-practices-2026.md
skills/testing-mock-discipline/README.md
```

## Install Skill

Option 1: via `skills` CLI from repository URL

```bash
npx skills add https://github.com/rickyraz/testing-best-practice --skill testing-mock-discipline
```

Option 2: install from direct skill path in repository URL

```bash
npx skills add https://github.com/rickyraz/testing-best-practice/tree/main/skills/testing-mock-discipline
```

Option 3: clone repo, then copy only the skill folder into your tool's skill directory

```bash
git clone https://github.com/rickyraz/testing-best-practice /tmp/testing-best-practice
mkdir -p ~/.codex/skills
cp -R /tmp/testing-best-practice/skills/testing-mock-discipline ~/.codex/skills/testing-mock-discipline
```

## Verify Installation

In a new AI assistant session, try:

```text
Use $testing-mock-discipline to audit this test suite. Focus on overuse of jest.mock/vi.mock,
propose DI refactors, and recommend a realistic unit/integration/e2e strategy.
```

If the skill is detected, the assistant will load:
- `skills/testing-mock-discipline/SKILL.md`
- `skills/testing-mock-discipline/references/testing-best-practices-2026.md`

Common local skill directories by tool:
- Codex: `~/.codex/skills/`
- Claude Code: `~/.claude/skills/`
- Generic local setup: `~/.skills/`

## What This Skill Covers

- Over-mocking smell audit (`jest.mock`, `vi.mock`, module mocks, filesystem mocks)
- DI seam refactors (function injection and constructor injection)
- Assertion quality guidance (outcome-focused vs implementation-focused)
- Test-level decision support (unit vs integration vs e2e)
- Incremental migration plan for existing brittle test suites

## Official References

- https://testing.googleblog.com/2013/05/testing-on-toilet-dont-overuse-mocks.html
- https://vitest.dev/api/vi.html
- https://jestjs.io/docs/manual-mocks
- https://testing-library.com/docs/guiding-principles
- https://martinfowler.com/articles/practical-test-pyramid.html

## Notes

- For local-only usage, you can skip CLI install and reference the absolute skill path directly.
