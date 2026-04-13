# Frontend Web Performance — Non-Negotiable Rules

## Scope
This file owns rendering efficiency, bundles, code splitting, asset loading, hydration cost, and runtime responsiveness.

## Violations
- route ships large non-critical code in initial bundle without justification — ERROR
- image or font strategy causes avoidable layout shift on core screens — ERROR
- long-running synchronous work blocks user interaction on main thread — ERROR
- large list rendered without pagination or virtualization when item count is unbounded — ERROR
- expensive animation uses layout-affecting properties when transform/opacity would suffice — ERROR
- same data fetched again after hydration without need — ERROR

## Budgets
- MUST define performance budgets for critical pages or journeys.
- MUST measure against user-centric metrics, not build output alone.
- MUST optimize for fast first useful paint, responsive interaction, and stable layout.

## Bundles and Code Loading
- MUST split code by route and heavy feature boundary.
- MUST lazy-load non-critical features and below-the-fold functionality when practical.
- MUST avoid importing heavy libraries into critical paths without review.
- MUST tree-shake dead code and unused locales/assets where possible.

## Rendering
- MUST keep render work proportional to visible UI.
- MUST prevent unnecessary rerenders of large subtrees.
- MUST virtualize or window large collections when bounded pagination alone is insufficient.
- MUST defer non-urgent updates when that improves responsiveness.

## Assets
- MUST size, compress, and format images for their usage context.
- MUST prevent layout shift by reserving image/media dimensions.
- MUST load fonts in a way that limits CLS and avoids excessive variant downloads.
- MUST load third-party scripts lazily and only when required.

## CSS and Motion
- MUST prefer transform and opacity for animation where possible.
- MUST avoid excessive selector complexity and style recalculation hotspots.
- MUST support reduced-motion behavior.

## Data and Hydration
- MUST avoid duplicate fetches across server/client boundaries when data can be reused safely.
- MUST keep hydration payloads minimal.
- MUST prefer server rendering or streaming for content that does not need client interactivity.
