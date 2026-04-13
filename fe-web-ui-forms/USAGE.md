# Usage

## Referencing from a blueprint spec

Add the following line under the UI and Forms section of your blueprint spec:

```markdown
Implements [fe-web-ui-forms harness](../../fe-web-ui-forms/spec/index.md).
```

Framework blueprints (`react-web-blueprint`, `nextjs-web-blueprint`) already declare this harness as a dependency. For custom stacks, reference it directly.

## What to implement

1. **UI states** — define loading, empty, error, success, and partial-data states for every user-visible surface before implementation; reserve space during loading to prevent layout shift.
2. **Validation ownership** — decide upfront whether validation lives on the client, server, or both; validate before submission when rules are client-available; surface server validation back to fields or form summary.
3. **Submission lifecycle** — disable or show pending state on submit actions; prevent duplicate submission; preserve user input on recoverable failures; support keyboard submission where semantically appropriate.
4. **Error association** — attach field-level errors near their control; provide form-level errors for cross-field or server failures; clear resolved errors when inputs become valid.
5. **Destructive actions** — require confirmation, undo, or an equivalent safety mechanism when user harm is material; make destructive actions visually distinct from safe ones.
6. **Formatting** — separate display formatting (e.g., phone number masks, currency symbols) from the submitted value; normalize input before validation; avoid masks that trap cursor movement or block valid paste.

## Verifying compliance

For every form, verify in code review:
- Submit button shows pending state and is disabled while in-flight
- All four states handled: loading, empty, error, success
- Field errors are associated programmatically (via `aria-describedby` or equivalent)
- Destructive actions have confirmation or undo with material risk
