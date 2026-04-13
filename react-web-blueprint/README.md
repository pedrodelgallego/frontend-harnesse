# react-web-blueprint

Without a shared React implementation contract, side effects creep into render, hooks get called conditionally, components mix orchestration with domain logic, and route handlers reach directly into transport clients. This blueprint maps all `fe-web-*` harness policies to concrete React 19 implementation rules.

## Who should use it

Any team building a production web frontend with React 19 and TypeScript strict mode. This is the implementation layer — it depends on all `fe-web-*` domain harnesses and defines how those rules apply in React specifically.

## How to use it

Install this blueprint as a dependency in a feature spec or compose it with a Next.js blueprint. The violations table — 6 ERROR — maps to code review criteria and CI policy checks.

## What it contains

- **Components** — presentational components separated from data/orchestration; one primary reason to change per component; explicit props over hidden shared mutable state; controlled components for complex or validated form flows
- **Hooks** — hooks pure in signature and explicit in ownership; custom hooks for reusable stateful behavior; `useEffect` only for synchronization with external systems; memoization only for measured or likely rerender cost; no effect chains simulating imperative workflows
- **State** — local UI state with `useState`/`useReducer` by default; state lifted only to nearest common owner; server data not copied into ad hoc local mirrors without a synchronization strategy
- **Error handling** — React error boundaries for render-time isolation; recoverable fallbacks where retry is safe
- **Data and async UX** — data access through dedicated hooks, loaders, or framework boundaries; obsolete async work cancelled; race conditions from stale closures or overlapping requests prevented; transitions for non-urgent UI updates where appropriate
- **Forms** — form ownership inside the form boundary or explicit workflow container; server validation propagated back into field/form UI consistently
