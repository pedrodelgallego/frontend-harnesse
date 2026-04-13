# Usage

## Referencing from a feature spec

Add the following line under the Framework section of your feature spec to pull in React implementation rules and all `fe-web-*` domain harnesses:

```markdown
Implements [react-web-blueprint](../../react-web-blueprint/spec/index.md).
```

The Next.js blueprint (`nextjs-web-blueprint`) already depends on this blueprint. Reference it directly only for pure React apps without Next.js.

## What to implement

1. **Component boundaries** — separate presentational components from data/orchestration components; one primary reason to change per component; explicit props over hidden shared mutable state.
2. **Hooks** — hooks pure in signature and explicit in ownership; custom hooks for reusable stateful behavior and side-effect coordination; `useEffect` only for synchronization with external systems; no effect chains simulating imperative workflows; memoization only for measured rerender cost.
3. **State** — `useState`/`useReducer` by default; lift state to nearest common owner only; never copy server data into ad hoc local mirrors without a synchronization strategy.
4. **Error handling** — React error boundaries for render-time isolation; recoverable fallbacks where retry is safe.
5. **Data and async** — data access through dedicated hooks, loaders, or framework boundaries; cancel obsolete async work; prevent race conditions from stale closures or overlapping requests; use transitions for non-urgent updates.
6. **Forms** — form state owned by the form boundary or explicit workflow container; server validation propagated back into field/form UI consistently.

## Verifying compliance

Enable React's strict mode to catch side effects in render and double-invoke lifecycle methods:

```tsx
// src/main.tsx
<React.StrictMode>
  <App />
</React.StrictMode>
```

Run TypeScript with `strict: true` in `tsconfig.json`. Hook rule violations are caught by `eslint-plugin-react-hooks` — ensure it is enabled in CI.
