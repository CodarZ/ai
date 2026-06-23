# DESIGN.md Specification Reference

A DESIGN.md file is a self-contained, plain-text design system contract.

## File Structure

Two layers:

1. Optional YAML front matter at the top
2. Markdown body made of `##` sections

Front matter must start and end with a line containing exactly `---`.

## Token Schema

Allowed top-level token groups:

- `version`
- `name`
- `description`
- `colors`
- `typography`
- `rounded`
- `spacing`
- `components`

## Token Types

- **Color:** any valid CSS color string (hex, rgb(), rgba(), hsl(), oklch(), named)
- **Dimension:** number with unit (e.g., `16px`, `1.5`, `0`)
- **Token reference:** `{path.to.token}` — use when one value derives from another
- **Typography object:** fontFamily, fontSize, fontWeight, lineHeight, letterSpacing, fontFeature, fontVariation

## Section Order

Sections that appear in the body must follow this order:

1. `## Overview`
2. `## Colors`
3. `## Typography`
4. `## Layout`
5. `## Elevation & Depth`
6. `## Shapes`
7. `## Components`
8. `## Do's and Don'ts`

Sections may be omitted, but relative order must stay the same.

## Section Aliases

When they better match project terminology:

- Overview → Brand & Style
- Layout → Layout & Spacing
- Elevation & Depth → Elevation

For strict output, prefer the canonical headings.

## Component Token Properties

Valid properties for component tokens:

- `backgroundColor`
- `textColor`
- `typography`
- `rounded`
- `padding`
- `size`
- `height`
- `width`

## Validation Criteria

A correct file should be:

- Parseable as YAML + Markdown
- Grounded in project evidence
- Internally consistent (all token references resolve)
- Free from fabricated token values
- Free from extra sections outside the spec (except documented project-specific sections)

## Project-Specific Sections

After the 8 canonical sections, these additional sections may appear when evidence supports them:

- `## Responsive Behavior` — breakpoints, touch targets, collapsing strategy
- `## Iteration Guide` — developer workflow for maintaining the design system
- `## Known Gaps` — documented limitations, missing evidence, open questions

These are optional and must NOT appear unless there is concrete evidence to document. They are appended after `## Do's and Don'ts`, never inserted between canonical sections.

## Description Field

The `description` token in front matter must be a rich paragraph (3-5 sentences), not a single sentence. It should capture: the dominant visual characteristic, the palette approach, the typographic identity, the depth/elevation approach, and the overall feel. This is the first thing an agent reads — it defines the system's identity at a glance.
