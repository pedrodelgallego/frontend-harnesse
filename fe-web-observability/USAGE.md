# Usage

## Referencing from a blueprint spec

Add the following line under the Observability section of your blueprint spec:

```markdown
Implements [fe-web-observability harness](../../fe-web-observability/spec/index.md).
```

Framework blueprints (`react-web-blueprint`, `nextjs-web-blueprint`) already declare this harness as a dependency. For custom stacks, reference it directly.

## What to implement

1. **Error capture** — instrument unhandled render, async, and route-level failures with an error monitoring client (Sentry, Datadog RUM, or equivalent); include route and correlation context.
2. **Event naming scheme** — define a canonical naming convention (e.g., `<noun>_<verb>`: `checkout_started`) and enforce it across all screens; keep names stable once shipped.
3. **Context fields** — attach stable fields to every event: environment, app version, route, and request correlation ID.
4. **RUM metrics** — instrument Core Web Vitals and route transition latency for critical journeys; correlate frontend request spans with backend traces where supported.
5. **Feature flag telemetry** — emit exposure events on flag evaluation when flags materially affect UX or experiment outcomes; include flag key, evaluated variant, and evaluation context.
6. **Logging** — use structured logs where collected; sample noisy events; keep console-only debugging out of production telemetry pipelines.

## Verifying compliance

Confirm error capture is wired up for unhandled rejections and React error boundaries:

```bash
# Trigger a test error and verify it appears in your monitoring platform
# Check that the event includes: environment, appVersion, route, correlationId
```

Review telemetry schemas for PII before each release. Confirm high-cardinality values are not used as metric dimensions.
