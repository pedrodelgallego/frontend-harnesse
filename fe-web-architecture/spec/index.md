# Frontend Web Architecture — Non-Negotiable Rules

## Scope
This file owns frontend structure, responsibility boundaries, release controls, and dependency direction.

## Violations
- UI component performs direct network I/O outside an approved data layer — ERROR
- business rules embedded in presentational components — ERROR
- module imports create circular dependency across app layers — ERROR
- feature flag used as permanent branching with no owner or expiry — ERROR
- permission logic implemented only in the UI without server enforcement — ERROR
- page-level code depends on browser-only APIs during server execution path — ERROR
- shared component imports app-specific service or route module — ERROR

## Architecture
- MUST separate UI, state orchestration, data access, and domain rules.
- MUST keep business rules outside presentational components.
- MUST define one dependency direction: `platform -> app shell -> routes/pages -> features -> domain -> shared`.
- MUST keep shared modules framework-agnostic unless the file is explicitly framework-bound.
- MUST prefer composition over inheritance.
- MUST keep side effects at boundaries, never inside pure formatting or mapping utilities.
- MUST make feature boundaries visible in the directory structure.
- MUST isolate third-party SDK wrappers behind internal adapters.
- MUST document every cross-cutting singleton.

## Composition
- Components MUST have one primary responsibility.
- Container/orchestration components MAY coordinate data, permissions, and state.
- Presentational components MUST receive data and callbacks through explicit props.
- Domain utilities MUST be deterministic and testable without DOM or network.
- Shared UI primitives MUST NOT import feature code.

## Configuration
- MUST load runtime configuration from explicit environment or server-injected config.
- MUST fail fast when required config is missing.
- MUST NOT hardcode secrets, tokens, or environment-specific URLs in frontend code.
- MUST treat all client-exposed config as public.

## Feature Flags and Progressive Delivery
- MUST treat feature flags as release controls, not long-term architecture.
- MUST define for every flag: owner, purpose, rollout scope, fallback, and expiry/removal date.
- MUST keep permission checks separate from experiment flags.
- MUST evaluate kill-switch and safety flags before expensive work when feasible.
- MUST define deterministic defaults when flag resolution fails.
- MUST remove stale flags after rollout or rollback is complete.
- MUST NOT create nested flag trees that make behavior untraceable.
- MUST document whether a flag is server-evaluated, edge-evaluated, or client-evaluated.
- Client-only evaluation MUST NOT gate sensitive data or authorization.

## Error Boundaries
- MUST define app-level error isolation boundaries.
- MUST prevent one route or widget failure from crashing the whole application when a narrower boundary is appropriate.
- MUST provide a recoverable fallback UI for user-triggered retry when safe.

## Async and Background Work
- MUST make user-visible background work observable through explicit UI state.
- MUST cancel obsolete work when navigation, input, or ownership changes make results irrelevant.
- MUST prevent stale async results from overwriting newer state.

## Documentation
- MUST document app shell, feature boundaries, shared layers, and release controls.
- MUST document each intentional exception to this file.
