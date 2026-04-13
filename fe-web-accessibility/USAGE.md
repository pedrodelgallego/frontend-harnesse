# Usage

## Referencing from a blueprint spec

Add the following line under the Accessibility section of your blueprint spec:

```markdown
Implements [fe-web-accessibility harness](../../fe-web-accessibility/spec/index.md).
```

Framework blueprints (`react-web-blueprint`, `nextjs-web-blueprint`) already declare this harness as a dependency. For custom stacks, reference it directly.

## What to implement

1. **Semantic HTML** — use native elements before ARIA; provide accessible names for every interactive control.
2. **Keyboard operation** — all interactive functionality operable by keyboard; logical tab order; visible focus indicator; no traps except intentional managed contexts (modal with escape).
3. **Focus management** — move focus intentionally after route changes, dialog opens/closes, and async UI swaps; restore focus on dismiss; no unexpected focus moves during typing or pointer interaction.
4. **Forms** — associate labels, descriptions, and errors with controls; indicate invalid state programmatically; provide error summary for long or multi-field forms.
5. **Dynamic content** — announce critical async state changes not obvious visually; manage live regions sparingly; ensure skeletons/spinners do not hide task progress.
6. **Motion, contrast, and targets** — respect `prefers-reduced-motion`; sufficient color contrast for text and interactive states; adequately sized targets; do not rely on color alone.

## Verifying compliance

Run an automated accessibility audit on critical user journeys:

```bash
# Using axe-core in your test suite
npx axe-cli https://your-app/critical-journey
```

Supplement automated checks with keyboard-only and screen reader manual testing. Automated tools catch ~30–40% of WCAG issues — manual verification is required for full sign-off.
