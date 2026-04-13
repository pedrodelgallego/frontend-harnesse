# Next.js Web Blueprint — Non-Negotiable Rules

## Scope
This file explains how to implement the `fe-web-*` policies in Next.js.

## Baseline
- MUST use Next.js 16 App Router for new applications unless an exception is documented. citeturn977204search1turn977204search7
- MUST use TypeScript strict mode.

## Violations
- browser-only logic executed in a Server Component path without boundary — ERROR
- sensitive server capability exposed to Client Components without review — ERROR
- client component used by default when a Server Component would suffice — ERROR
- cache or revalidation behavior left implicit for critical data path — ERROR
- middleware used for heavy business logic or per-request data fetching that belongs elsewhere — ERROR
- route handler duplicates backend domain logic that should live in a service tier — ERROR

## App Router Structure
- MUST organize by route segment and feature boundary.
- MUST treat Server Components as the default for renderable content that does not require client interactivity. citeturn977204search18
- MUST mark Client Components explicitly and narrowly.
- MUST keep client-only state and browser API use behind `'use client'` boundaries.

## Server and Client Boundaries
- MUST keep secrets and privileged server access in server-only code.
- MUST pass only the minimum required serializable data to Client Components.
- MUST avoid hoisting large client subtrees above the narrowest interactive boundary.
- MUST prevent hydration mismatch from time, randomness, locale, and browser-only state.

## Data Fetching and Caching
- MUST define caching and revalidation policy per data source.
- MUST avoid implicit duplicate fetching across server and client boundaries.
- MUST document when data is static, revalidated, dynamic, or user-specific.
- MUST use route-level loading and error boundaries.

## Mutations
- MUST keep mutations in approved boundaries such as server-side actions or route handlers, according to repository policy.
- MUST define pending, success, rollback, and failure UX for every mutation.
- MUST prevent duplicate submission.

## Routing
- MUST use App Router primitives for nested layouts, loading, error, and not-found handling.
- MUST keep route params and search params validated at the boundary.
- MUST preserve shareable state in `searchParams` when appropriate.

## Middleware and Edge
- MUST keep middleware minimal, deterministic, and low-latency.
- MUST use middleware for request shaping, redirects, locale, and lightweight auth gates only when appropriate.
- MUST not place heavy data fetching or complex business rules in middleware.
- MUST document when code targets Edge runtime versus Node runtime.

## Assets and Platform Features
- MUST use Next.js image, font, and metadata features when they materially improve performance or correctness.
- MUST load third-party scripts with explicit strategy and ownership.

## Styling
- If Tailwind is used, MUST keep it consistent with the React blueprint rules.
- MUST keep global CSS limited to app-wide concerns.
- MUST prefer colocated styles or utility composition over page-wide CSS leakage.

## Tooling Notes
- Turbopack is the default bundler in Next.js 16; exceptions MUST be documented. citeturn977204search19
- React Compiler support MAY be enabled only after repository validation because it is stable but not default. citeturn977204search13
