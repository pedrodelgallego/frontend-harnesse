# Changelog

## 0.1.0

- Initial release.
- Stack: Next.js 16 App Router, TypeScript strict mode, Turbopack (default bundler).
- Violations table: 6 ERROR covering browser-only logic in Server Component path, sensitive server capability exposed to Client Components, client component used when server component suffices, implicit cache/revalidation on critical data path, middleware with heavy business logic, and route handlers duplicating backend domain logic.
- Sections: App Router Structure, Server and Client Boundaries, Data Fetching and Caching, Mutations, Routing, Middleware and Edge, Assets and Platform Features, Styling.
- Dependencies: react-web-blueprint and all 11 fe-web-* domain harnesses.
