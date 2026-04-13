# Usage

## Referencing from a blueprint spec

Add the following line under the Browser Platform section of your blueprint spec:

```markdown
Implements [fe-web-browser-platform harness](../../fe-web-browser-platform/spec/index.md).
```

Framework blueprints (`react-web-blueprint`, `nextjs-web-blueprint`) already declare this harness as a dependency. For custom stacks, reference it directly.

## What to implement

1. **Browser support declaration** — document supported browsers and device classes; define graceful degradation for unsupported capabilities.
2. **Capability detection** — use feature detection (e.g., `'serviceWorker' in navigator`), never user-agent sniffing, as the primary capability check.
3. **Platform API wrappers** — centralize storage, clipboard, notifications, and other browser APIs behind wrappers that guard against missing support and SSR context.
4. **Storage ownership** — define schema, expiry, and migration strategy for every `localStorage` / `sessionStorage` / `IndexedDB` key before use.
5. **Offline strategy** — classify the app as online-only, resilient-online, or offline-capable; surface connectivity loss when it affects user actions.
6. **SSR/hydration safety** — avoid time, locale, and randomness divergence at first render; guard browser-only APIs behind execution-context checks.

## Verifying compliance

Check that browser-only APIs are guarded in SSR paths:

```bash
# Grep for unguarded window/document usage in server-rendered files
grep -rn "window\." src/app --include="*.tsx" | grep -v "typeof window"
```

Run critical journeys in a browser compatibility matrix (BrowserStack or equivalent) against your defined support matrix.
