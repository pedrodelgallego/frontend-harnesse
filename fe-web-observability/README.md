# fe-web-observability

Without a shared observability contract, client errors get swallowed, events get named inconsistently across screens, telemetry leaks PII, and backend traces lose their frontend leg. This harness defines the decisions once — error capture, RUM, event naming, telemetry standards, feature flag exposure, and structured logging — and applies them everywhere.

## Who should use it

Any team building a production web frontend that emits errors, analytics, or RUM signals to an observability platform. Framework agnostic; compose with `react-web-blueprint` or `nextjs-web-blueprint` for implementation guidance.

## How to use it

Reference this harness in a framework blueprint or feature spec. The violations table — 6 ERROR — maps to code review criteria and CI policy checks.

## What it contains

- **Signals** — error telemetry, user-journey telemetry, and user-experience metrics emitted from supported applications; canonical event naming scheme; stable context fields (environment, app version, route, correlation ID); bounded-cardinality dimensions
- **Error monitoring** — unhandled render, async, and route-level failures captured; enough context to debug without leaking secrets or PII; noisy repeated failures deduplicated where possible
- **RUM and performance metrics** — browser performance metrics collected for critical journeys; real-user performance measured for route transitions and interaction responsiveness; frontend requests correlated with backend traces
- **Product and journey events** — event contracts defined for key user journeys; event names stable; product analytics separated from operational telemetry when retention or access rules differ; no duplicate events per user action without explicit reason
- **Feature flag telemetry** — exposure/assignment events emitted when flags materially affect UX, metrics, or experiments; flag key, evaluated variant, and evaluation context included; exposure distinguished from conversion events; raw targeting attributes not sent without approval
- **Logging** — structured client logs where collected; noisy informational events sampled; console-only debugging kept out of production telemetry flows
