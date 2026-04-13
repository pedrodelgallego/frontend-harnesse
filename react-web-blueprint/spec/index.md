# React Web Blueprint — Non-Negotiable Rules

## Scope
This file explains how to implement the `fe-web-*` policies in React.

## Baseline
- MUST use React 19.x. citeturn977204search9turn977204search0
- MUST use TypeScript strict mode.

## Violations
- side effects run during render — ERROR
- hook called conditionally or outside React rules — ERROR
- component mixes orchestration, domain logic, and presentation without clear boundary — ERROR
- `useEffect` used for pure derivation that belongs in render or memoized calculation — ERROR
- uncontrolled prop-to-state mirroring without ownership reason — ERROR
- route/page component imports low-level transport client directly — ERROR

## Components
- MUST separate presentational components from data/orchestration components.
- MUST keep components small enough to have one primary reason to change.
- MUST prefer explicit props over hidden shared mutable state.
- MUST use controlled components for complex or validated form flows unless uncontrolled inputs materially improve performance and remain safe.

## Hooks
- MUST keep hooks pure in signature and explicit in ownership.
- MUST use custom hooks for reusable stateful behavior and side-effect coordination.
- MUST NOT hide network mutations or navigation side effects in low-level presentational hooks.
- MUST avoid effect chains that simulate imperative workflows.
- MUST use `useEffect` only for synchronization with external systems.
- MUST use memoization only when it addresses measured or likely rerender cost.

## State
- MUST keep local UI state with `useState`/`useReducer` by default.
- MUST lift state only to the nearest common owner that needs it.
- MUST not copy server data into ad hoc local mirrors without a synchronization strategy.

## Error Handling
- MUST use React error boundaries for render-time isolation.
- MUST provide recoverable fallbacks where retry is safe.

## Data and Async UX
- MUST implement data access through dedicated hooks, loaders, or framework boundaries rather than ad hoc fetches in components.
- MUST cancel obsolete async work where the underlying client supports it.
- MUST prevent race conditions from stale closures or overlapping requests.
- MAY use transitions for non-urgent UI updates where that improves responsiveness. citeturn977204search0

## Forms
- MUST keep form ownership inside the form boundary or explicit workflow container.
- MUST propagate server validation back into field/form UI consistently.

## Styling
- If Tailwind is used, MUST treat it as an implementation detail of the blueprint, not a design-system substitute.
- Tailwind usage MUST prefer reusable component variants over unbounded inline utility growth.
- MUST centralize conditional class composition with a standard helper.
- MUST keep global CSS minimal and reserved for resets, tokens, and app-wide primitives.
- MUST avoid runtime CSS solutions that materially increase render or hydration cost without need.

## Testing
- MUST use React-focused component testing for user-visible behavior.
- MUST test hooks either through components or dedicated hook harnesses, never by reaching into internals.
