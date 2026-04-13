# fe-web-performance

Without a shared performance contract, routes ship non-critical code in initial bundles, images cause layout shift, unbounded lists render without virtualization, and post-hydration duplicate fetches re-do server work. This harness defines the decisions once — budgets, code splitting, rendering, assets, CSS, and hydration — and applies them everywhere.

## Who should use it

Any team building a production web frontend with performance requirements tied to user-centric metrics (Core Web Vitals, interaction responsiveness). Framework agnostic; compose with `react-web-blueprint` or `nextjs-web-blueprint` for implementation guidance.

## How to use it

Reference this harness in a framework blueprint or feature spec. The violations table — 6 ERROR — maps to code review criteria and CI policy checks.

## What it contains

- **Budgets** — performance budgets defined per critical page or journey; measurement against user-centric metrics, not build output alone; optimization targets fast first useful paint, responsive interaction, and stable layout
- **Bundles and code loading** — code split by route and heavy feature boundary; non-critical features and below-the-fold functionality lazy-loaded; heavy libraries reviewed before inclusion in critical paths; dead code and unused locales tree-shaken
- **Rendering** — render work proportional to visible UI; unnecessary rerenders of large subtrees prevented; large collections virtualized when bounded pagination alone is insufficient; non-urgent updates deferred
- **Assets** — images sized, compressed, and formatted for usage context; dimensions reserved to prevent layout shift; fonts loaded with limited CLS and minimal variant downloads; third-party scripts loaded lazily and only when required
- **CSS and motion** — transform and opacity preferred for animation; excessive selector complexity avoided; reduced-motion behavior supported
- **Data and hydration** — duplicate fetches across server/client boundaries avoided when data can be reused; hydration payloads minimal; server rendering or streaming preferred for non-interactive content
