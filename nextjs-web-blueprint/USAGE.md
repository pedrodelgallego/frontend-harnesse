# Usage

## Referencing from a feature spec

Add the following line under the Framework section of your feature spec to pull in Next.js implementation rules, the React blueprint, and all `fe-web-*` domain harnesses:

```markdown
Implements [nextjs-web-blueprint](../../nextjs-web-blueprint/spec/index.md).
```

## What to implement

1. **Server vs. Client Components** — default to Server Components for renderable content that does not need interactivity; mark Client Components explicitly and narrowly with `'use client'`; keep secrets and privileged server access in server-only code.
2. **Data fetching and caching** — define caching and revalidation policy (`force-cache`, `no-store`, `revalidate: N`) per data source; document whether data is static, revalidated, dynamic, or user-specific; use route-level `loading.tsx` and `error.tsx`.
3. **Mutations** — implement mutations as server actions or route handlers per repository policy; define pending, success, rollback, and failure UX; prevent duplicate submission.
4. **Routing** — use App Router primitives for nested layouts, parallel routes, intercepting routes, and not-found/error handling; validate route params and search params at the boundary.
5. **Middleware** — keep middleware minimal, deterministic, and low-latency (redirects, locale selection, lightweight auth gates only); document Edge vs. Node runtime choice.
6. **Assets** — use `next/image` for images, `next/font` for fonts, and `next/script` with explicit strategy for third-party scripts.

## Verifying compliance

Run Next.js build to check for Server/Client Component boundary violations:

```bash
npx next build
```

Check for implicit cache behavior on critical data paths — any `fetch` without an explicit `cache` option defaults to `force-cache` in Next.js App Router. Review `next.config.js` for bundle analyzer output before each release.
