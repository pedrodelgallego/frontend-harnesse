# Usage

## Referencing from a blueprint spec

Add the following line under the State Management section of your blueprint spec:

```markdown
Implements [fe-web-state-management harness](../../fe-web-state-management/spec/index.md).
```

Framework blueprints (`react-web-blueprint`, `nextjs-web-blueprint`) already declare this harness as a dependency. For custom stacks, reference it directly.

## What to implement

1. **State classification** — before adding state, classify it: local UI, shared client, server, route, or persisted; choose the appropriate owner and mechanism.
2. **Single source of truth** — define one writable owner per state slice; never store the same value in two writable locations; compute derived state instead of duplicating it.
3. **Global state discipline** — use shared/global state only for cross-route or cross-feature coordination; keep global state minimal; forms, transient loading flags, and server caches do not belong in global state by default.
4. **Persistence** — version persisted structures from the start; implement schema migration and graceful handling of invalid persisted data; define expiry or eviction for persisted state.
5. **Concurrency** — implement last-writer-wins or intent-based conflict resolution for rapid user actions; prevent stale async results from overwriting newer state.
6. **Form state** — keep form state owned by the form boundary unless the workflow explicitly requires sharing it.

## Verifying compliance

In code review, check any new state addition for:
- Classification documented (where does this state live and why?)
- One writable owner
- Derived values computed, not stored separately
- Persisted structures versioned with migration plan
