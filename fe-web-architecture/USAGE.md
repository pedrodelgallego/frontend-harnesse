# Usage

## Referencing from a blueprint spec

Add the following line under the Architecture section of your blueprint spec:

```markdown
Implements [fe-web-architecture harness](../../fe-web-architecture/spec/index.md).
```

Framework blueprints (`react-web-blueprint`, `nextjs-web-blueprint`) already declare this harness as a dependency. For custom stacks, reference it directly.

## What to implement

1. **Dependency direction** — enforce `platform → app shell → routes/pages → features → domain → shared`; no circular imports across layers.
2. **Responsibility boundaries** — keep business rules out of presentational components; isolate third-party SDK wrappers behind internal adapters; document every cross-cutting singleton.
3. **Configuration** — load runtime config from environment or server-injected config; hard fail on missing required config; never hardcode secrets or environment-specific URLs.
4. **Feature flags** — define owner, purpose, rollout scope, fallback, and expiry for every flag; remove stale flags after rollout or rollback; never nest flag trees or use client-only evaluation for sensitive data.
5. **Error boundaries** — define app-level isolation boundaries; provide recoverable fallback UI; prevent one widget failure from crashing the application when a narrower boundary is appropriate.
6. **Async work** — make user-visible background work observable; cancel obsolete work on navigation; prevent stale async results from overwriting newer state.

## Verifying compliance

Check module dependency direction in CI:

```bash
# Using dependency-cruiser
npx depcruise --config .dependency-cruiser.cjs src
```

Review feature flag registry for entries missing owner or expiry fields before each release.
