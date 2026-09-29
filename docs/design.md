# Design system

**Status:** Initial direction only. No UI existed in the audited workspace; tokens below are proposals to validate during implementation.

## Direction

Infrastructure-grade reliability: precise, calm, information-dense developer tooling. Use observability and financial infrastructure products as quality references without copying their interfaces. Avoid generic AI gradients, excessive glass, neon, decoration, and motion that obscures operational state.

## Tokens (provisional)

- **Typography:** system sans-serif for interface; tabular numerals for metrics; monospace for IDs, payload metadata, and code. Select and bundle fonts only after checking licensing and loading impact.
- **Color:** neutral slate surfaces and text; one restrained blue/indigo primary accent; semantic success green, warning amber, error red, pending slate, processing blue, unknown gray. Pair every color with a text label/icon.
- **Spacing:** 4px base rhythm; compact controls and dense tables, with larger section spacing for page hierarchy.
- **Shape/elevation:** restrained 6–10px control/card radii, subtle borders, minimal shadow. Avoid nested card-on-card treatment.
- **Motion:** short, purposeful transitions; honor `prefers-reduced-motion`; no essential information depends on animation.

These values are a starting point, not a measured contrast or final brand decision. Verify contrast and mobile behavior during implementation.

## Components and patterns

- **Navigation:** responsive sidebar/drawer for the authenticated application; clear active item, keyboard operation, skip link, and persistent page context.
- **Buttons/forms:** one primary action per context; visible focus, disabled/loading/success/error states, labels and server-side validation feedback.
- **Cards/metrics:** clear labels, period/source, and provenance; never imply simulated values are live production metrics.
- **Tables:** sortable only where useful, accessible headings, responsive overflow or mobile row cards, explicit status text, and authorized search.
- **Badges/alerts:** semantic text plus icon/shape; include severity and actionable explanation.
- **Timeline/graph:** readable textual timeline is always available alongside any event relationship visualization.
- **Modals:** keyboard focus management, escape/close behavior, explicit confirmation for consequential actions, and no hidden critical details.
- **Charts:** labeled axes/units, useful textual summary, accessible colors, and responsive sizing.

## Themes and responsive behavior

Treat light and dark themes as separately designed surface hierarchies; do not invert blindly. Suggested breakpoints: 320–767px mobile, 768–1023px tablet, 1024px+ desktop, with content constraints at wide widths. Validate 320, 375, 390, 768, 1024, and 1440px; avoid horizontal page overflow and preserve reachable incident actions.

## Accessibility and states

Use semantic HTML, labels, keyboard navigation, visible focus, sufficient verified contrast, reduced motion, and status text beyond color. Every view should define useful loading, empty, error, and success states. Errors explain what happened, what to do next, and a request ID when available without exposing internals. Print incident and reconciliation reports without navigation or controls.

## Landing page direction

One clear CTA, concise problem statement, lightweight event-flow visualization, reliability/idempotency/retry capabilities, reconciliation, evidence-led investigation, provider-neutral ecosystem, FAQ, and final CTA. Dashboard clarity and operational workflows take priority over marketing effects.
