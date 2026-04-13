# fe-web-accessibility

Without a shared accessibility contract, every team makes different decisions about semantics, keyboard support, and focus management. Keyboard users hit traps, screen reader users miss announcements, and WCAG failures surface late in QA. This harness fixes the decisions once — baseline, violations, and per-domain rules — and applies them everywhere.

## Who should use it

Any team building a production web frontend that must meet WCAG 2.2 AA on supported user journeys. Framework agnostic; compose with `react-web-blueprint` or `nextjs-web-blueprint` for implementation guidance.

## How to use it

Reference this harness in a framework blueprint or feature spec. The violations table — 6 ERROR — maps to code review criteria and CI policy checks.

## What it contains

- **Baseline** — WCAG 2.2 AA for all supported user journeys
- **Semantics** — native HTML before ARIA; accessible names on every interactive control; headings, landmarks, lists, tables, and forms used according to meaning
- **Keyboard** — full keyboard operation; logical tab order; visible focus; no traps except intentional managed contexts with escapable exits
- **Focus management** — intentional focus moves after route changes, dialogs, drawers, and async UI swaps; focus restored on dismiss; no unexpected moves during typing or pointer use
- **Forms and errors** — labels, descriptions, and errors associated with controls; invalid state indicated programmatically; error summary for long or multi-field forms
- **Dynamic content** — critical async state changes announced; live regions used sparingly and correctly; skeletons and spinners do not hide task progress
- **Motion, contrast, and targets** — `prefers-reduced-motion` respected; sufficient contrast for text and interactive states; adequately sized targets; color not sole communicator of meaning
