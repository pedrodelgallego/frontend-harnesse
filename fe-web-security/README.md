# fe-web-security

Without a shared security contract, secrets end up in client bundles, tokens go in URLs, untrusted HTML gets rendered without sanitization, and cross-origin messages are accepted without validation. Frontend authorization gets mistaken for enforcement. This harness defines the decisions once — secrets, tokens, authz boundaries, untrusted content, browser messaging, and telemetry privacy — and applies them everywhere.

## Who should use it

Any team building a production web frontend that handles authentication tokens, user-generated content, third-party embeds, or sensitive data. Framework agnostic; compose with `react-web-blueprint` or `nextjs-web-blueprint` for implementation guidance.

## How to use it

Reference this harness in a framework blueprint or feature spec. The violations table — 7 ERROR — maps to code review criteria and CI policy checks.

## What it contains

- **Secrets and configuration** — all shipped frontend code and config treated as public; no server secrets, signing keys, or privileged credentials client-side; privileged operations proxied through backend or platform
- **Tokens and credentials** — backend auth model followed exactly; token exposure in JavaScript-accessible storage minimized; no tokens or credentials in URLs; credentials cleared on logout and session invalidation; expired credentials handled without revealing protected content
- **Authorization boundaries** — frontend authz is UX guidance only; client never enforces data access; unavailable actions hidden when appropriate but server enforcement always expected
- **Untrusted content** — untrusted HTML sanitized or transformed before rendering; dangerous HTML injection avoided by default; downloadable or previewable resource URLs validated; markdown, CMS content, user-generated content, and third-party widgets treated as untrusted
- **Browser messaging and embeds** — `postMessage` origin and payload shape validated; iframe/embed integrations restricted to approved origins and capabilities; unnecessary browser permissions not granted
- **Privacy in telemetry and storage** — PII minimized in logs, analytics, and error reports; sensitive fields redacted or omitted before telemetry; retention and expiry defined for client-side persisted sensitive-adjacent data
