# Token Extraction Rules

Extract only the token groups supported by DESIGN.md: colors, typography, rounded, spacing, components.

## Colors

Capture semantic roles first:

- primary, secondary, background, surface, text, muted, border, accent
- success, warning, error

Prefer semantic names over raw hue names. Accept valid CSS color strings (hex, rgb, rgba, hsl, oklch, named).

## Typography

Capture: fontFamily, fontSize, fontWeight, lineHeight, letterSpacing, fontFeature, fontVariation.

Map to semantic roles:

- display, headline, body, label, caption, code

## Rounded

Use scale tokens: none, sm, md, lg, xl, full. Use the project's actual corner language.

## Spacing

Use a consistent scale: xs, sm, md, lg, xl, 2xl. Keep coherent with the project's existing spacing rhythm. Avoid inventing a full scale if only a few values are confirmed.

Common additional tokens:

- `section` — vertical padding between major page sections (typically 60-120px). Use when the project has consistent section-level spacing.
- `none` or `0` — explicit zero spacing for edge cases.

Only include tokens you can evidence. A project with 3 confirmed spacing values should define 3 tokens, not force-fit a 6-value scale.

## Components

Only use valid component properties (backgroundColor, textColor, typography, rounded, padding, size, height, width).

Common component names: button-primary, button-secondary, card, input, badge, navbar.

## Token Reference Syntax

Use `{path.to.token}` when a value derives from another token:

- `{colors.primary}`, `{colors.surface}`
- `{typography.body}`, `{rounded.md}`, `{spacing.md}`

Never duplicate a token value in prose if a token already exists.

## Validation Rule

Each token must answer:

- What is the value?
- Where was it observed?
- How confident are we?

If any answer is missing, do not promote the token to verified.
