# Frontend Web Accessibility — Non-Negotiable Rules

## Scope
This file owns accessibility requirements for semantics, keyboard use, focus, naming, announcements, motion, and contrast.

## Baseline
- MUST meet WCAG 2.2 AA for supported user journeys. citeturn977204search2turn977204search8

## Violations
- clickable non-semantic element used instead of appropriate native control without full keyboard and semantics support — ERROR
- form control missing accessible name — ERROR
- dialog without focus trap or restore — ERROR
- keyboard focus hidden or removed without equivalent visible indicator — ERROR
- auto-advancing carousel or animation ignores reduced-motion preference — ERROR
- status update not announced when required for task completion — ERROR

## Semantics
- MUST prefer native HTML semantics before ARIA.
- MUST provide an accessible name for every interactive control.
- MUST use headings, landmarks, lists, tables, and form elements according to meaning.
- MUST NOT use ARIA to override correct native semantics unnecessarily.

## Keyboard
- MUST support full keyboard operation for all interactive functionality.
- MUST preserve logical tab order.
- MUST provide visible focus indication.
- MUST avoid keyboard traps except within intentional managed contexts such as modals, where exit must remain possible.

## Focus Management
- MUST move focus intentionally after route changes, dialogs, drawers, and async UI swaps when user context would otherwise be lost.
- MUST restore focus when dismissing temporary surfaces where appropriate.
- MUST not move focus unexpectedly during typing or pointer interaction.

## Forms and Errors
- MUST associate labels, descriptions, and errors with controls.
- MUST indicate invalid state programmatically.
- MUST provide an error summary for long or multi-field forms when useful.

## Dynamic Content
- MUST announce critical async state changes when they are not obvious visually.
- MUST manage live regions sparingly and correctly.
- MUST ensure skeletons, spinners, and delayed content do not hide task progress.

## Motion, Contrast, and Targets
- MUST respect `prefers-reduced-motion`.
- MUST preserve sufficient color contrast for text and interactive states.
- MUST provide adequately sized interaction targets for supported platforms.
- MUST not use color alone to communicate required meaning.
