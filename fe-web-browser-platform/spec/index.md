# Frontend Web Browser Platform — Non-Negotiable Rules

## Scope
This file owns browser support policy, progressive enhancement, storage APIs, cookies, feature detection, offline behavior, and safe use of browser-only APIs.

## Violations
- user-agent sniffing used as primary capability check — ERROR
- browser-only API accessed during server rendering path without guard — ERROR
- local storage used as a durable database without schema/version handling — ERROR
- unsupported browser gets a blank screen instead of degraded behavior or explicit message — ERROR
- app requires JavaScript for core content with no documented reason when progressive enhancement is feasible — ERROR

## Browser Support
- MUST define supported browsers and device classes explicitly.
- MUST document graceful degradation for unsupported capabilities.
- MUST test critical journeys on supported browsers.

## Progressive Enhancement
- MUST prefer capability detection over user-agent sniffing.
- MUST ensure core navigation and content remain available when practical under degraded conditions.
- MUST layer advanced behavior on top of a working baseline where feasible.

## Browser APIs
- MUST guard browser-only APIs behind capability checks and execution-context checks.
- MUST centralize wrappers for storage, clipboard, notifications, and other platform APIs.
- MUST handle permission denial gracefully.

## Storage and Cookies
- MUST define ownership, schema, expiry, and migration for local persistent storage.
- MUST use cookies only when justified by session, security, or interoperability needs.
- MUST avoid storing sensitive values in long-lived browser storage unless explicitly approved.

## Offline and Connectivity
- MUST define whether the app is online-only, resilient-online, or offline-capable.
- MUST surface connectivity loss when it affects user actions.
- MUST queue or retry user actions offline only when conflict handling is defined.

## SSR and Hydration Safety
- MUST keep server-rendered markup deterministic enough to hydrate safely.
- MUST avoid browser-time, locale, or random-value divergence at first render unless intentionally isolated.
