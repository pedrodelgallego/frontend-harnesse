# nextjs-web-blueprint

Without a shared Next.js contract, browser-only logic runs in Server Components, client components get used by default when server components would suffice, caching policy is left implicit, and middleware accumulates business logic it doesn't belong to. This blueprint maps all `fe-web-*` harness policies to concrete Next.js 16 App Router implementation rules.

## Who should use it

Any team building a production web frontend with Next.js 16 App Router and TypeScript strict mode. This is the implementation layer — it depends on `react-web-blueprint` and all `fe-web-*` domain harnesses, and defines how those rules apply in Next.js specifically.

## How to use it

Install this blueprint as a dependency in a feature spec. The violations table — 6 ERROR — maps to code review criteria and CI policy checks.

## What it contains

- **App Router structure** — organized by route segment and feature boundary; Server Components as the default for renderable content without client interactivity; Client Components marked explicitly and narrowly; client-only state and browser API use behind `'use client'` boundaries
- **Server and client boundaries** — secrets and privileged server access in server-only code; minimum required serializable data passed to Client Components; hydration mismatches prevented
- **Data fetching and caching** — caching and revalidation policy defined per data source; no implicit duplicate fetching across server and client boundaries; data classified as static, revalidated, dynamic, or user-specific; route-level loading and error boundaries used
- **Mutations** — mutations in approved boundaries (server actions or route handlers per repository policy); pending, success, rollback, and failure UX defined; duplicate submission prevented
- **Routing** — App Router primitives for nested layouts, loading, error, and not-found handling; route and search params validated at boundary; shareable state in `searchParams` when appropriate
- **Middleware and edge** — minimal, deterministic, and low-latency middleware; restricted to request shaping, redirects, locale, and lightweight auth gates; no heavy data fetching or business rules in middleware; Edge vs. Node runtime documented
- **Assets and platform** — Next.js image, font, and metadata features used when they improve performance or correctness; third-party scripts loaded with explicit strategy and ownership
