# Frontend Web State Management — Non-Negotiable Rules

## Scope
This file owns local state, shared state, server state boundaries, persistence, and derived state.

## Violations
- server state copied into global client state without reason — ERROR
- same source of truth stored in multiple writable locations — ERROR
- derived state manually synchronized instead of computed — ERROR
- global state used for route-local or component-local concerns — ERROR
- persisted state used for sensitive data without explicit approval — ERROR
- state mutation bypasses ownership boundary — ERROR

## State Classification
- MUST classify state as one of: local UI state, shared client state, server state, route state, or persisted client state.
- MUST keep server state out of generic global state unless there is a clear synchronization need.
- MUST keep ephemeral UI state local by default.
- MUST use route state for URL-shareable view state.

## Sources of Truth
- MUST define one writable owner for each piece of state.
- MUST compute derived state instead of duplicating it.
- MUST avoid bidirectional synchronization between independent stores.
- MUST document every persisted state key and its lifecycle.

## Global State
- MUST use shared/global state only for cross-route or cross-feature coordination with clear ownership.
- MUST keep global state minimal and explicit.
- MUST NOT place forms, transient loading flags, or server caches in global state by default.

## Persistence
- MUST persist only state that survives refresh for user value.
- MUST version persisted structures.
- MUST handle schema migration and invalid persisted data safely.
- MUST define expiry or eviction for persisted state where relevant.

## Concurrency
- MUST prevent stale async updates from overwriting current intent.
- MUST handle race conditions where rapid user actions create competing state transitions.

## Forms
- Form state MUST remain owned by the form boundary unless explicitly shared for a workflow.
