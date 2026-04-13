# fe-web-testing

Without a shared testing contract, the test pyramid inverts, component tests hit live APIs, snapshots become the primary assertion, and flaky retries hide nondeterminism instead of fixing it. This harness defines the decisions once — test pyramid, boundary rules, assertion style, data isolation, and coverage policy — and applies them everywhere.

## Who should use it

Any team building a production web frontend that needs a sustainable, reliable test suite. Framework agnostic; compose with `react-web-blueprint` or `nextjs-web-blueprint` for implementation guidance.

## How to use it

Reference this harness in a framework blueprint or feature spec. The violations table — 7 ERROR — maps to code review criteria and CI policy checks.

## What it contains

- **Pyramid** — layered strategy: unit → component → integration → end-to-end; more tests at lower layers than higher ones; pure logic tested without DOM or network; end-to-end reserved for critical journeys and environment wiring
- **Boundaries** — unit tests: pure functions, mappers, formatters, reducers, domain logic; component tests: UI with mocked network or approved test doubles; integration tests: routing, state, forms, and data layers together; end-to-end: production-like deployments or preview environments
- **Assertions** — visible behavior, accessibility semantics, navigation results, and network outcomes asserted; unhappy paths covered (invalid input, empty state, loading, timeout, server error, auth failure); brittle styling selectors avoided
- **Test data and isolation** — deterministic test data generated or seeded; every test independent; state reset between tests; no production data, shared accounts, or hardcoded secrets
- **Visual and accessibility testing** — automated accessibility checks for common regressions; visual regression only for stable surfaces where review burden is justified; automated scans do not substitute for full accessibility sign-off
- **Coverage and quality** — coverage thresholds defined by repository policy; justified exclusions documented; behavior and branch relevance prioritized over raw percentage
