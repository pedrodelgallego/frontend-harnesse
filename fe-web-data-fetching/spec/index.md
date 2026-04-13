# Frontend Web Data Fetching — Non-Negotiable Rules

## Scope
This file owns client/server fetch policy, caching, revalidation, retries, cancellation, and server-state mutation behavior.

## Violations
- fetch initiated directly inside render path — ERROR
- duplicate requests issued for the same resource without deduplication or reason — ERROR
- request continues after owning view becomes irrelevant and can still update state — ERROR
- retry applied to unsafe mutation without explicit idempotency protection — ERROR
- stale response overwrites fresher state — ERROR
- timeout omitted for outbound request — ERROR
- cache used without freshness or invalidation policy — ERROR

## Ownership
- MUST centralize network access in an approved data access layer or server action boundary.
- MUST keep transport concerns separate from presentation.
- MUST define per-resource caching and invalidation policy.

## Requests
- MUST set explicit timeouts on outbound requests.
- MUST cancel obsolete requests when navigation or input invalidates the result.
- MUST deduplicate equivalent in-flight requests when practical.
- MUST classify requests as one of: critical blocking, deferred, background refresh, or prefetch.
- MUST handle loading, empty, error, and success states explicitly.

## Caching and Revalidation
- MUST define cache ownership and staleness policy per resource.
- MUST revalidate after mutations when cached data becomes stale.
- MUST prevent stale data from silently persisting past its documented freshness budget.
- MUST prefer background refresh over blocking refetch when UX allows.
- MUST make optimistic updates reversible.

## Retries
- MUST retry only transient failures.
- MUST use bounded retry with backoff and jitter.
- MUST honor `Retry-After` when present.
- MUST NOT retry non-idempotent mutations unless the backend contract explicitly supports it.

## Pagination and Incremental Loading
- MUST keep pagination state in the URL when user-shareable.
- MUST define one strategy per list: paged, cursor, infinite scroll, or virtualized window.
- MUST prevent duplicate or skipped items during incremental loading.
- MUST expose end-of-list, empty, and partial-failure states clearly.

## Mutations
- MUST define pending, success, rollback, and failure behavior for every mutation.
- MUST prevent duplicate submission when the same action is in flight unless parallel execution is intended.
- MUST reconcile mutation results with cached reads consistently.

## API Consumption
- MUST validate assumptions at the boundary when the backend contract is untrusted or partially typed.
- MUST tolerate additive response fields.
- MUST NOT depend on undocumented backend behavior.
