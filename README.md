# react-view-transitions

A reusable AI skill for implementing, debugging, and explaining React View Transitions, including React release-channel constraints (Stable vs Canary/Experimental).

## Repository Layout

This repository uses a cross-tool multi-skill layout:

```text
skills/react-view-transitions/SKILL.md
skills/react-view-transitions/agents/openai.yaml
skills/react-view-transitions/references/react-view-transitions-architecture.md
```

## Install Skill

Option 1: via `skills` CLI

```bash
npx skills add https://github.com/rickyraz/react-view-transitions --skill react-view-transitions
```

Option 2: install from direct skill path in the repo

```bash
npx skills add https://github.com/rickyraz/react-view-transitions/tree/main/skills/react-view-transitions
```

Option 3: clone repo, then copy only the skill folder into your tool's skill directory

```bash
git clone git@github.com:rickyraz/react-view-transitions.git /tmp/react-view-transitions
cp -R /tmp/react-view-transitions/skills/react-view-transitions ~/.skills/react-view-transitions
```

## Verify Installation

In a new AI assistant session, try:

```text
Use $react-view-transitions to debug why my list reorder animation becomes a cross-fade.
```

If the skill is detected, the assistant will use `skills/react-view-transitions/SKILL.md` and `skills/react-view-transitions/references/react-view-transitions-architecture.md`.

Common local skill directories by tool:

- Claude Code: `~/.claude/skills/`
- Codex: `~/.codex/skills/`
- Generic local setup: `~/.skills/`

## React Canary Notes (April 2026)

- `<ViewTransition />` and `addTransitionType` are currently available in Canary/Experimental channels, not in stable React 19.x.
- React docs for `<ViewTransition />` are still marked as `Canary`.
- The latest stable docs currently show React `19.2`.

To try the React View Transition API:

```bash
npm install react@canary react-dom@canary
```

Make sure `react` and `react-dom` are on the same channel (do not mix stable with canary/experimental).

If your project stays on stable React, use the browser API `document.startViewTransition()` directly.

## Check React Versions in a Project

```bash
npm ls react react-dom
```

## Official References

- https://react.dev/reference/react/ViewTransition
- https://react.dev/blog/2025/04/23/react-labs-view-transitions-activity-and-more
- https://react.dev/versions
- https://react.dev/community/versioning-policy
