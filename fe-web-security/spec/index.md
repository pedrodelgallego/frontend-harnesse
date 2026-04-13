# Frontend Web Security — Non-Negotiable Rules

## Scope
This file owns browser-side security decisions, untrusted content handling, token handling, storage rules, and frontend authorization boundaries.

## Violations
- secret embedded in client bundle — ERROR
- access token persisted in insecure browser storage against policy — ERROR
- untrusted HTML rendered without sanitization or trusted transformation — ERROR
- frontend treats hidden UI as authorization — ERROR
- user-controlled URL, HTML, or message event trusted without validation — ERROR
- cross-origin message accepted without origin validation — ERROR
- sensitive data exposed in client logs, analytics, or crash reports — ERROR

## Secrets and Configuration
- MUST treat all shipped frontend code and config as public.
- MUST NOT store server secrets, signing keys, or privileged credentials in the client.
- MUST use backend or platform proxies for privileged operations.

## Tokens and Credentials
- MUST follow the backend auth model exactly.
- MUST minimize token exposure in JavaScript-accessible storage.
- MUST NOT place tokens or credentials in URLs.
- MUST clear client-held credentials on logout and session invalidation.
- MUST handle expired credentials without revealing protected content.

## Authorization Boundaries
- MUST treat frontend authorization as UX guidance only.
- MUST NOT rely on the client to enforce data access.
- MUST hide unavailable actions when appropriate, but MUST still expect server enforcement.

## Untrusted Content
- MUST sanitize or transform untrusted HTML before rendering.
- MUST avoid dangerous HTML injection by default.
- MUST validate downloadable or previewable resource URLs before use.
- MUST treat markdown, CMS content, user-generated content, and third-party widgets as untrusted by default.

## Browser Messaging and Embeds
- MUST validate `postMessage` origin and payload shape.
- MUST restrict iframe/embed integrations to approved origins and capabilities.
- MUST not grant unnecessary browser permissions.

## Privacy in Telemetry and Storage
- MUST minimize PII in logs, analytics, and error reports.
- MUST redact or omit sensitive fields before sending telemetry.
- MUST define retention and expiry for client-side persisted sensitive-adjacent data.
