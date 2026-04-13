# fe-web-browser-platform

Without a browser platform contract, teams user-agent sniff instead of capability-detect, localStorage grows into an unversioned database, and SSR hydration breaks on locale or time mismatches. This harness defines the decisions once — support policy, progressive enhancement, platform API wrappers, storage ownership, offline strategy, and SSR safety.

## Who should use it

Any team building a web frontend that must handle browser diversity, offline scenarios, or server-side rendering. Framework agnostic; compose with `react-web-blueprint` or `nextjs-web-blueprint` for implementation guidance.

## How to use it

Reference this harness in a framework blueprint or feature spec. The violations table — 5 ERROR — maps to code review criteria and CI policy checks.

## What it contains

- **Browser support** — explicit browser and device class definitions; documented graceful degradation; critical journeys tested on supported browsers
- **Progressive enhancement** — capability detection over user-agent sniffing; core navigation and content available under degraded conditions; advanced behavior layered on a working baseline
- **Browser APIs** — browser-only APIs guarded behind capability and execution-context checks; centralized wrappers for platform APIs; permission denial handled gracefully
- **Storage and cookies** — ownership, schema, expiry, and migration defined for every persistent storage key; cookies justified by session, security, or interoperability needs; sensitive values not in long-lived storage without explicit approval
- **Offline and connectivity** — app classified as online-only, resilient-online, or offline-capable; connectivity loss surfaced when it affects user actions; offline action queuing only when conflict handling is defined
- **SSR and hydration safety** — server-rendered markup deterministic enough to hydrate safely; no browser-time, locale, or random-value divergence at first render unless intentionally isolated
