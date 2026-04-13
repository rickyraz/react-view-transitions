---
name: react-view-transitions
description: Use when working with React View Transitions, including the ViewTransition component, view-transition-name, startViewTransition, enter/exit/share/gesture transitions, Suspense constraints, list reordering behavior, animation debugging, and React internals related to view transitions.
---

# React View Transitions

Use this skill to help implement, debug, explain, or review React View Transitions.

## Workflow

1. Identify the layer of the problem first:
   - App usage: component placement, names, CSS pseudo-elements, callbacks, list items, Suspense, or browser support.
   - React internals: commit phase ordering, pairing, auto-naming, gesture clones, resource blocking, or lane eligibility.
   - Browser View Transitions API: `document.startViewTransition`, snapshots, pseudo-elements, or compositing behavior.

2. For app-level implementation:
   - Wrap the smallest stable visual unit that should animate.
   - Use explicit, stable names for shared elements, for example `name={"item-" + id}`.
   - Give each reordered list item its own `ViewTransition`; a boundary around the whole list animates the subtree as one layer.
   - Treat `className="none"` or a resolved class of `"none"` as an opt-out.
   - Keep urgent input updates outside view-transition-eligible work when keyboard or pointer responsiveness matters.

3. For debugging:
   - Confirm the old and new elements have matching `view-transition-name` values when expecting a share transition.
   - Check whether the element is outside the viewport; React may revert names for an exiting offscreen element.
   - Distinguish layout-only movement from content updates. React uses the `Update` flag as a proxy and has known rough edges here.
   - For list reordering, verify each child gets a unique transition name rather than relying on DOM-order matching.
   - For Suspense or streaming behavior, remember that browser view transitions are atomic and cannot animate partially revealed intermediate states.

4. For React internals:
   - Read [the architecture reference](references/react-view-transitions-architecture.md) before making claims about commit phase ordering, callbacks, gesture clones, resource blocking, or lane gates.
   - Prefer the exact names and constants from the reference when explaining internals.
   - If inspecting source, start with `ReactFiberCommitViewTransitions.js`, then follow into `ReactFiberViewTransitionComponent.js`, `ReactFiberConfigDOM.js`, `ReactFiberApplyGesture.js`, and `ReactFiberWorkLoop.js`.

## Quick Rules

- `startViewTransition()` wraps the mutation phase; old-state setup happens before mutation and new-state setup happens after.
- Explicit `props.name` wins unless the name is `"auto"`; auto names are assigned lazily at commit time.
- Matching entering and exiting transition names produce share transitions; unmatched entering produces enter and unmatched exiting produces exit.
- Native view transitions operate at the compositing layer, so userland FLIP libraries cannot fully reproduce them for Canvas, WebGL, or browser pseudo-elements.
- React may cancel or restore update transitions when measurement shows nothing actually moved.
