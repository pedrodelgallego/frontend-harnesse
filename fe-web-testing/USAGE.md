# Usage

## Referencing from a blueprint spec

Add the following line under the Testing section of your blueprint spec:

```markdown
Implements [fe-web-testing harness](../../fe-web-testing/spec/index.md).
```

Framework blueprints (`react-web-blueprint`, `nextjs-web-blueprint`) already declare this harness as a dependency. For custom stacks, reference it directly.

## What to implement

1. **Test pyramid** — more unit tests than component tests, more component tests than integration tests, more integration tests than end-to-end tests; pure logic tested without DOM or network.
2. **Boundary rules** — component tests use mocked network or approved test doubles; integration tests cover realistic routing, state, form, and data layer composition; end-to-end tests run against production-like deployments.
3. **Assertions** — assert visible behavior and accessibility semantics, not implementation details; cover unhappy paths; avoid brittle styling selectors.
4. **Test isolation** — generate or seed deterministic test data; reset state between tests; never depend on production data, shared accounts, or hardcoded secrets.
5. **Coverage** — define coverage thresholds by repository policy; document any justified exclusion; prioritize behavior and branch relevance over raw percentage.
6. **Accessibility checks** — run automated a11y checks for common regressions (axe-core integration); do not treat automated scans as full accessibility sign-off.

## Verifying compliance

Run the full test suite and coverage report:

```bash
# Example with Vitest
npx vitest run --coverage

# Example with Playwright for e2e
npx playwright test
```

Check coverage thresholds fail CI when below policy minimums. Review flaky test retries weekly — retries that consistently mask failures should be fixed, not increased.
