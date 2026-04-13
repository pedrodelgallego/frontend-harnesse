# fe-web-ui-forms

Without a shared UI and forms contract, forms submit without duplicate protection, validation only fires on submit, loading states cause layout jumps, and destructive actions offer no confirmation. This harness defines the decisions once — UI state completeness, validation ownership, submission lifecycle, error association, destructive action guards, and input formatting — and applies them everywhere.

## Who should use it

Any team building a web frontend with forms, multi-state UI surfaces, or user actions with irreversible consequences. Framework agnostic; compose with `react-web-blueprint` or `nextjs-web-blueprint` for implementation guidance.

## How to use it

Reference this harness in a framework blueprint or feature spec. The violations table — 6 ERROR — maps to code review criteria and CI policy checks.

## What it contains

- **UI states** — loading, empty, error, success, and partial-data states defined for every user-visible surface; layout stable during loading where practical; no dead-end states without a recovery path
- **Forms** — validation ownership defined (client, server, or both); validation before submission when rules are client-available; server validation surfaced back to fields or form summary; user input preserved on recoverable failures; duplicate submission prevented; pending state exposed on submit actions; keyboard submission supported where semantically appropriate
- **Validation UX** — required fields, constraints, and irreversible effects clear before submit; field-level errors shown near the relevant control; form-level errors for cross-field or server failures; resolved errors cleared when inputs become valid
- **Destructive and irreversible actions** — confirmation, undo, or equivalent safety mechanism required when user harm is material; destructive actions visually distinct; default focus not on destructive confirmation when safer alternatives exist
- **Formatting and masking** — display formatting separated from submitted value; user input normalized before validation when safe and expected; input masks do not trap cursor movement or block valid paste behavior
