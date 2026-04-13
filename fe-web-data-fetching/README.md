# fe-web-data-fetching

Without a shared data fetching contract, components fire requests in render paths, caches lack freshness policy, retries run against non-idempotent mutations, and stale responses overwrite fresh state. This harness defines the decisions once — ownership, timeouts, caching, retries, pagination, and mutation lifecycle — and applies them everywhere.

## Who should use it

Any team building a web frontend that fetches data from APIs or server boundaries. Framework agnostic; compose with `react-web-blueprint` or `nextjs-web-blueprint` for implementation guidance.

## How to use it

Reference this harness in a framework blueprint or feature spec. The violations table — 7 ERROR — maps to code review criteria and CI policy checks.

## What it contains

- **Ownership** — network access centralized in an approved data layer; transport concerns separated from presentation; per-resource caching and invalidation policy defined
- **Requests** — explicit timeouts; obsolete requests cancelled on navigation or input change; equivalent in-flight requests deduplicated; requests classified as critical blocking, deferred, background refresh, or prefetch; all four states handled (loading, empty, error, success)
- **Caching and revalidation** — cache ownership and staleness policy per resource; post-mutation revalidation; background refresh preferred over blocking refetch when UX allows; optimistic updates reversible
- **Retries** — only transient failures retried; bounded retry with backoff and jitter; `Retry-After` honored; non-idempotent mutations not retried without explicit backend contract
- **Pagination** — strategy defined per list (paged, cursor, infinite scroll, or virtualized window); shareable state in URL; no duplicate or skipped items during incremental loading; end-of-list, empty, and partial-failure states surfaced
- **Mutations** — pending, success, rollback, and failure behavior defined for every mutation; duplicate submission prevented; mutation results reconciled with cached reads
- **API consumption** — boundary validation when backend contract is untrusted; additive response fields tolerated; no dependency on undocumented backend behavior
