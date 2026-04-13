# Frontend Web Routing and Navigation — Non-Negotiable Rules

## Scope
This file owns URL shape, deep linking, route state, navigation behavior, and guarded navigation.

## Violations
- route state stored only in memory when it must survive refresh/share — ERROR
- navigation triggered with raw string concatenation instead of route builder — ERROR
- query params used for secrets or tokens that belong in headers or cookies — ERROR
- back/forward navigation breaks user task flow or loses unsaved state without warning — ERROR
- protected route rendered before auth state is resolved when sensitive content can flash — ERROR
- invalid route param accepted without normalization or fallback — ERROR

## URLs
- MUST make URLs stable, shareable, and meaningful.
- MUST treat the URL as the source of truth for route identity and user-shareable state.
- MUST use path segments for identity and hierarchy.
- MUST use query parameters for filters, sorting, pagination, tab selection, and other bookmarkable view state.
- MUST NOT place secrets, PII, or tokens in URLs.
- MUST normalize invalid or unsupported query values.

## Deep Linking
- MUST support refresh and direct entry for every navigable screen.
- MUST preserve meaningful route state across reloads and share links.
- MUST produce canonical URLs for duplicate states where appropriate.

## Navigation Behavior
- MUST preserve browser expectations for back, forward, open in new tab, and copy link.
- MUST provide explicit user warning before navigation that would discard unsaved changes.
- MUST avoid full reloads for same-app transitions unless intentionally required.
- MUST make pending navigation visible when latency is noticeable.

## Route Guards
- MUST resolve authentication and authorization before revealing protected content.
- MUST redirect or render denial state consistently for unauthorized access.
- MUST NOT rely on route hiding as a security control.

## Errors and Missing Routes
- MUST provide a not-found route or screen.
- MUST provide a route-level error state for loader/render failure.
- MUST map invalid route params to either corrected URLs, not-found, or a clear validation state.

## Route Builders
- MUST centralize route generation for dynamic routes.
- MUST encode and decode route params consistently.
- MUST validate route params at the boundary.
