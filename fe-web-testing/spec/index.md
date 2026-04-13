# Frontend Web Testing — Non-Negotiable Rules

## Scope
This file owns frontend test strategy, layers, mocking boundaries, data setup, and flake control.

## Violations
- test pyramid inverted — ERROR
- end-to-end tests used to cover basic pure logic that belongs in unit tests — ERROR
- component test depends on live network or shared external environment — ERROR
- test asserts implementation detail instead of user-visible behavior where behavior testing is possible — ERROR
- snapshot used as the primary assertion for critical behavior — ERROR
- tests share mutable state or depend on order — ERROR
- flaky retry hides nondeterminism instead of fixing the cause — ERROR

## Pyramid
- MUST follow a layered strategy: unit -> component -> integration -> end-to-end.
- MUST keep more tests at lower layers than higher ones.
- MUST test pure logic without DOM or network when possible.
- MUST test user-visible behavior at component and integration layers.
- MUST reserve end-to-end coverage for critical journeys and environment wiring.

## Boundaries
- Unit tests MUST isolate pure functions, mappers, formatters, reducers, and domain logic.
- Component tests MUST render UI with mocked network or approved test doubles.
- Integration tests MUST cover realistic composition across routing, state, forms, and data layers.
- End-to-end tests MUST run against production-like deployments or preview environments.

## Assertions
- MUST assert visible behavior, accessibility semantics, navigation results, and network outcomes as relevant.
- MUST cover unhappy paths: invalid input, empty state, loading, timeout, server error, and authorization failure where applicable.
- MUST avoid brittle selectors tied to styling structure.

## Test Data and Isolation
- MUST generate or seed deterministic test data.
- MUST keep every test independent.
- MUST reset test state between tests.
- MUST NOT depend on production data, shared accounts, or hardcoded secrets.

## Visual and Accessibility Testing
- SHOULD use automated accessibility checks for common regressions.
- SHOULD use visual regression only for stable surfaces where review burden is justified.
- MUST NOT treat automated accessibility scans as full accessibility sign-off.

## Coverage and Quality
- MUST define coverage thresholds by repository policy.
- MUST document any justified exclusion.
- MUST prioritize behavior and branch relevance over raw percentage.
