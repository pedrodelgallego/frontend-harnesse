# Usage

## Referencing from a blueprint spec

Add the following line under the Data Fetching section of your blueprint spec:

```markdown
Implements [fe-web-data-fetching harness](../../fe-web-data-fetching/spec/index.md).
```

Framework blueprints (`react-web-blueprint`, `nextjs-web-blueprint`) already declare this harness as a dependency. For custom stacks, reference it directly.

## What to implement

1. **Data access layer** — centralize all network access in approved hooks, loaders, or server action boundaries; never fetch directly in component render.
2. **Timeouts and cancellation** — set explicit timeouts on all outbound requests; cancel in-flight requests when navigation or input makes the result irrelevant.
3. **Caching policy** — define freshness budget and invalidation strategy per resource before using a cache; revalidate after mutations; make optimistic updates reversible.
4. **Retries** — retry only transient failures (network errors, 429, 503) with bounded backoff and jitter; never auto-retry non-idempotent mutations without explicit backend contract.
5. **Pagination** — define one strategy per list (paged, cursor, infinite, or virtualized); keep paginated state in the URL when shareable; surface end-of-list, empty, and partial-failure states.
6. **Mutations** — define pending, success, rollback, and failure behavior before shipping any mutation; prevent duplicate submission; reconcile results with cached reads.

## Verifying compliance

Confirm a resource has a documented freshness policy before adding it to a cache. In code review, check every `fetch` / API client call for:
- Timeout set
- Cancellation on unmount or navigation
- Error, loading, and empty states handled
- Mutation result reconciled with cache
