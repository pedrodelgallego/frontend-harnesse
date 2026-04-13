# Usage

## Referencing from a blueprint spec

Add the following line under the Security section of your blueprint spec:

```markdown
Implements [fe-web-security harness](../../fe-web-security/spec/index.md).
```

Framework blueprints (`react-web-blueprint`, `nextjs-web-blueprint`) already declare this harness as a dependency. For custom stacks, reference it directly.

## What to implement

1. **Secrets** — treat all shipped frontend code and config as public; never include server secrets, signing keys, or privileged credentials; proxy privileged operations through backend or platform.
2. **Token handling** — follow the backend auth model exactly; minimize token exposure in JavaScript-accessible storage; never put tokens in URLs; clear credentials on logout; handle expired credentials without revealing protected content.
3. **Authorization** — frontend authz is UX guidance only; always expect server enforcement; hide unavailable actions when appropriate but never treat UI hiding as a security control.
4. **Untrusted content** — sanitize or transform untrusted HTML before rendering (DOMPurify or equivalent); validate resource URLs before download or preview; treat markdown, CMS, user-generated content, and third-party widgets as untrusted.
5. **Browser messaging** — validate `postMessage` origin and payload shape before acting; restrict iframe/embed integrations to approved origins; avoid granting unnecessary browser permissions.
6. **Telemetry privacy** — minimize PII in logs, analytics, and error reports; redact sensitive fields before sending; define retention and expiry for persisted sensitive-adjacent data.

## Verifying compliance

Scan the client bundle for secrets:

```bash
grep -rn "secret\|token\|api_key\|password" dist/ --include="*.js" | grep -v "placeholder\|example"
```

Review CSP headers and `postMessage` handler origin checks before each release.
