# fe-web-routing-navigation

Without a shared routing contract, route state lives only in memory and breaks on refresh, URLs are built by string concatenation, protected routes flash content before auth resolves, and back/forward breaks user task flows. This harness defines the decisions once — URL shape, deep linking, navigation behavior, route guards, and error handling — and applies them everywhere.

## Who should use it

Any team building a web frontend with multiple routes, auth-protected screens, or URL-driven navigation state. Framework agnostic; compose with `react-web-blueprint` or `nextjs-web-blueprint` for implementation guidance.

## How to use it

Reference this harness in a framework blueprint or feature spec. The violations table — 6 ERROR — maps to code review criteria and CI policy checks.

## What it contains

- **URLs** — stable, shareable, and meaningful; URL as source of truth for route identity; path segments for identity and hierarchy; query params for bookmarkable view state (filters, sorting, pagination, tab selection); no secrets, PII, or tokens in URLs; invalid query values normalized
- **Deep linking** — refresh and direct entry supported for every navigable screen; meaningful route state preserved across reloads; canonical URLs for duplicate states
- **Navigation behavior** — browser expectations (back, forward, open in new tab, copy link) preserved; explicit user warning before navigation discards unsaved changes; no full reloads for same-app transitions; pending navigation visible when latency is noticeable
- **Route guards** — auth and authz resolved before protecting content is revealed; unauthorized access redirected or denied consistently; route hiding not relied upon as a security control
- **Errors and missing routes** — not-found route; route-level error state for loader/render failure; invalid route params mapped to corrected URLs, not-found, or clear validation state
- **Route builders** — dynamic route generation centralized; route params consistently encoded and decoded; params validated at the boundary
