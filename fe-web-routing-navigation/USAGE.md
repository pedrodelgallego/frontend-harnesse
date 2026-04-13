# Usage

## Referencing from a blueprint spec

Add the following line under the Routing section of your blueprint spec:

```markdown
Implements [fe-web-routing-navigation harness](../../fe-web-routing-navigation/spec/index.md).
```

Framework blueprints (`react-web-blueprint`, `nextjs-web-blueprint`) already declare this harness as a dependency. For custom stacks, reference it directly.

## What to implement

1. **URL as source of truth** — path segments for identity and hierarchy; query params for filters, sorting, pagination, tab selection, and bookmarkable view state; normalize invalid or unsupported values.
2. **Deep linking** — every navigable screen must support refresh and direct entry; canonical URLs for duplicate states.
3. **Route builders** — centralize dynamic route generation; encode/decode params consistently; validate route params at the boundary.
4. **Navigation behavior** — preserve back, forward, open in new tab, and copy link expectations; warn before discarding unsaved changes; avoid full reloads for same-app transitions; show pending state on slow navigations.
5. **Route guards** — resolve auth and authz before rendering protected content; redirect or deny consistently; never rely on route hiding as a security control.
6. **Error states** — provide not-found and route-level error states; map invalid route params to corrected URLs, not-found, or a clear validation state.

## Verifying compliance

Test that direct URL entry, refresh, and back/forward work correctly for every navigable screen. Confirm protected routes redirect to login when unauthenticated before any content renders:

```bash
curl -sI https://your-app/protected-route
# Should return a redirect to /login, not 200 with partial content
```
