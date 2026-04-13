# Usage

## Referencing from a blueprint spec

Add the following line under the Performance section of your blueprint spec:

```markdown
Implements [fe-web-performance harness](../../fe-web-performance/spec/index.md).
```

Framework blueprints (`react-web-blueprint`, `nextjs-web-blueprint`) already declare this harness as a dependency. For custom stacks, reference it directly.

## What to implement

1. **Performance budgets** — define LCP, INP, and CLS targets per critical page before shipping; measure with Lighthouse CI or equivalent.
2. **Code splitting** — split by route and heavy feature boundary; lazy-load non-critical features and below-the-fold content; audit bundle size before adding heavy dependencies.
3. **Rendering** — virtualize unbounded lists; defer non-urgent updates; prevent unnecessary rerenders of large subtrees.
4. **Assets** — size and compress images for usage context; reserve dimensions with `width`/`height` or aspect-ratio CSS to prevent CLS; load fonts with `font-display: swap` and limit variant downloads; load third-party scripts with `defer` or `async` only when required.
5. **Animation** — prefer `transform` and `opacity` over layout-affecting properties; respect `prefers-reduced-motion`.
6. **Hydration** — avoid duplicate fetches across server/client boundaries; keep serialized state minimal; prefer server rendering for non-interactive content.

## Verifying compliance

Run Lighthouse CI against critical pages in your CI pipeline:

```bash
npx lhci autorun --config=lighthouserc.json
```

Check bundle composition before each release:

```bash
npx webpack-bundle-analyzer stats.json
# or: npx @next/bundle-analyzer (for Next.js)
```
