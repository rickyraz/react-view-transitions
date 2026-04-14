# react-view-transitions


 implement, debug, and explain React View Transitions, including Stable vs Canary/Experimental constraints.


## Repository Layout

```text
/SKILL.md
/agents/openai.yaml
/references/react-view-transitions-architecture.md


```

## Install Skill

via `skills` CLI by skill name

```bash
npx skills add https://github.com/rickyraz/skills --skill react-view-transitions

```

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
