# fe-web-state-management

Without a shared state management contract, server state gets copied into global stores, derived state is manually synchronized in multiple places, and persisted state accumulates without versioning or expiry. This harness defines the decisions once — state classification, ownership, sources of truth, persistence, and concurrency safety — and applies them everywhere.

## Who should use it

Any team building a web frontend with shared state across components, server-fetched data managed on the client, or user-facing persistent state. Framework agnostic; compose with `react-web-blueprint` or `nextjs-web-blueprint` for implementation guidance.

## How to use it

Reference this harness in a framework blueprint or feature spec. The violations table — 6 ERROR — maps to code review criteria and CI policy checks.

## What it contains

- **State classification** — every state classified as local UI, shared client, server, route, or persisted; server state kept out of generic global stores; ephemeral UI state local by default; route state for URL-shareable view state
- **Sources of truth** — one writable owner per state slice; derived state computed instead of duplicated; no bidirectional synchronization between independent stores; every persisted state key documented with lifecycle
- **Global state** — shared/global state only for cross-route or cross-feature coordination with clear ownership; global state minimal and explicit; forms, transient loading flags, and server caches not in global state by default
- **Persistence** — only user-value state persisted across refresh; persisted structures versioned; schema migration and invalid data handled safely; expiry or eviction defined where relevant
- **Concurrency** — stale async updates prevented from overwriting current intent; race conditions handled for rapid user actions creating competing state transitions
- **Forms** — form state owned by the form boundary unless explicitly shared for a workflow
