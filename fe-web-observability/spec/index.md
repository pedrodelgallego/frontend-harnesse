# Frontend Web Observability — Non-Negotiable Rules

## Scope
This file owns frontend logs, errors, metrics, RUM, journey telemetry, trace correlation, and experiment telemetry.

## Violations
- client error swallowed without capture path — ERROR
- telemetry event contains raw secrets, tokens, or prohibited PII — ERROR
- high-cardinality value used as a metric dimension without review — ERROR
- event names differ across screens for the same user action — ERROR
- feature flag exposure not attributable to variant and request context — ERROR
- backend trace correlation headers discarded when correlation is required — ERROR

## Signals
- MUST emit error telemetry, user-journey telemetry, and user-experience metrics from supported applications.
- MUST define a canonical event naming scheme.
- MUST attach stable context fields consistently, for example environment, app version, route, and request correlation identifiers.
- MUST avoid unbounded-cardinality dimensions.

## Error Monitoring
- MUST capture unhandled render, async, and route-level failures.
- MUST include enough context to debug without leaking secrets or prohibited PII.
- MUST deduplicate noisy repeated client failures where possible.

## RUM and Performance Metrics
- MUST collect browser performance metrics for critical journeys.
- MUST measure real-user performance for route transitions and interaction responsiveness where tooling allows.
- MUST correlate frontend request context with backend traces when supported.

## Product and Journey Events
- MUST define event contracts for key user journeys.
- MUST keep event names stable.
- MUST separate product analytics from operational telemetry when retention or access rules differ.
- MUST not emit duplicate events for one user action without explicit reason.

## Feature Flags and Progressive Delivery Telemetry
- MUST emit flag exposure or assignment events when flags materially affect UX, metrics, or experiment analysis.
- MUST include flag key, evaluated variant, and evaluation context sufficient for debugging.
- MUST distinguish exposure from conversion or outcome events.
- MUST avoid sending raw targeting attributes unless approved.

## Logging
- MUST use structured client logs where logs are collected.
- MUST sample noisy informational events.
- MUST keep console-only debugging out of production telemetry flows.
