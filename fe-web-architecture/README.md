# fe-web-architecture

Without a shared architecture contract, UI components accumulate network calls, business logic migrates into presentational layers, and module graphs grow circular. Feature flags live forever without owners. This harness defines the decisions once — dependency direction, composition model, configuration, feature flag discipline, error isolation, and async governance.

## Who should use it

Any team building a production web frontend that needs clear separation of concerns, maintainable dependency direction, and disciplined release controls. Framework agnostic; compose with `react-web-blueprint` or `nextjs-web-blueprint` for implementation guidance.

## How to use it

Reference this harness in a framework blueprint or feature spec. The violations table — 7 ERROR — maps to code review criteria and CI policy checks.

## What it contains

- **Architecture** — separation of UI, state orchestration, data access, and domain rules; one dependency direction: `platform → app shell → routes/pages → features → domain → shared`; third-party SDKs isolated behind adapters; cross-cutting singletons documented
- **Composition** — one primary responsibility per component; presentational components receive data through explicit props; domain utilities deterministic and testable without DOM or network; shared UI primitives never import feature code
- **Configuration** — runtime config from explicit environment or server-injected config; hard fail on missing required config; no hardcoded secrets or environment-specific URLs; all client-exposed config treated as public
- **Feature flags** — release controls with defined owner, purpose, rollout scope, fallback, and expiry; kill-switch flags evaluated before expensive work; no nested flag trees; client-only evaluation cannot gate sensitive data or authorization
- **Error boundaries** — app-level isolation; narrower boundaries prevent single widget failures from crashing the application; recoverable fallback UI with retry
- **Async and background work** — user-visible background work is observable; obsolete work cancelled on navigation or ownership change; stale async results cannot overwrite newer state
