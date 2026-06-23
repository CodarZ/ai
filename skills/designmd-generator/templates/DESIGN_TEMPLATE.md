---
version: alpha
name: '{{PROJECT_NAME}}'
description: |
  {{RICH_DESCRIPTION_3_TO_5_SENTENCES}} — Capture the dominant visual characteristic, the palette approach, the typographic identity, the depth/elevation approach, and the overall feel. This is the first thing an agent reads.
colors:
  primary: '{{PRIMARY_COLOR}}'
  secondary: '{{SECONDARY_COLOR}}'
  surface: '{{SURFACE_COLOR}}'
  background: '{{BACKGROUND_COLOR}}'
  text: '{{TEXT_COLOR}}'
typography:
  heading-hero:
    fontFamily: '{{FONT_FAMILY}}'
    fontSize: '{{HERO_SIZE}}'
    fontWeight: '{{HERO_WEIGHT}}'
    lineHeight: '{{HERO_LINE_HEIGHT}}'
  heading-section:
    fontFamily: '{{FONT_FAMILY}}'
    fontSize: '{{SECTION_SIZE}}'
    fontWeight: '{{SECTION_WEIGHT}}'
    lineHeight: '{{SECTION_LINE_HEIGHT}}'
  body:
    fontFamily: '{{FONT_FAMILY}}'
    fontSize: '{{BODY_FONT_SIZE}}'
    fontWeight: '{{BODY_FONT_WEIGHT}}'
    lineHeight: '{{BODY_LINE_HEIGHT}}'
    letterSpacing: '{{BODY_LETTER_SPACING}}'
  label:
    fontFamily: '{{FONT_FAMILY}}'
    fontSize: '{{LABEL_FONT_SIZE}}'
    fontWeight: '{{LABEL_FONT_WEIGHT}}'
    lineHeight: '{{LABEL_LINE_HEIGHT}}'
rounded:
  sm: '{{RADIUS_SM}}'
  md: '{{RADIUS_MD}}'
  lg: '{{RADIUS_LG}}'
spacing:
  xs: '{{SPACING_XS}}'
  sm: '{{SPACING_SM}}'
  md: '{{SPACING_MD}}'
  lg: '{{SPACING_LG}}'
components:
  button-primary:
    backgroundColor: '{colors.primary}'
    textColor: '{colors.background}'
    rounded: '{rounded.md}'
    padding: '{spacing.md}'
  card:
    backgroundColor: '{colors.surface}'
    rounded: '{rounded.lg}'
    padding: '{spacing.lg}'
---

## Overview

{{OVERVIEW_2_TO_4_PARAGRAPHS}}

### Key Characteristics

- {{CHARACTERISTIC_1}}
- {{CHARACTERISTIC_2}}
- {{CHARACTERISTIC_3}}
- {{CHARACTERISTIC_4}}
- {{CHARACTERISTIC_5}}

## Colors

### Brand & Accent

- **Primary** (`{colors.primary}` — `{{PRIMARY_HEX}}`): {{PRIMARY_ROLE_DESCRIPTION}}
- **Secondary** (`{colors.secondary}` — `{{SECONDARY_HEX}}`): {{SECONDARY_ROLE_DESCRIPTION}}

### Surface

- **Background** (`{colors.background}` — `{{BACKGROUND_HEX}}`): {{BACKGROUND_ROLE_DESCRIPTION}}
- **Surface** (`{colors.surface}` — `{{SURFACE_HEX}}`): {{SURFACE_ROLE_DESCRIPTION}}

### Text

- **Text** (`{colors.text}` — `{{TEXT_HEX}}`): {{TEXT_ROLE_DESCRIPTION}}

## Typography

### Font Family

**{{FONT_FAMILY}}** is used for all text roles. {{FONT_RATIONALE}}.

### Hierarchy

| Token                          | Size             | Weight             | Line Height             | Letter Spacing             | Use                                    |
| ------------------------------ | ---------------- | ------------------ | ----------------------- | -------------------------- | -------------------------------------- |
| `{typography.heading-hero}`    | {{HERO_SIZE}}    | {{HERO_WEIGHT}}    | {{HERO_LINE_HEIGHT}}    | {{HERO_LETTER_SPACING}}    | Hero headline ("{{HERO_EXAMPLE}}")     |
| `{typography.heading-section}` | {{SECTION_SIZE}} | {{SECTION_WEIGHT}} | {{SECTION_LINE_HEIGHT}} | {{SECTION_LETTER_SPACING}} | Section titles ("{{SECTION_EXAMPLE}}") |
| `{typography.body}`            | {{BODY_SIZE}}    | {{BODY_WEIGHT}}    | {{BODY_LINE_HEIGHT}}    | {{BODY_LETTER_SPACING}}    | Body copy, descriptions                |
| `{typography.label}`           | {{LABEL_SIZE}}   | {{LABEL_WEIGHT}}   | {{LABEL_LINE_HEIGHT}}   | {{LABEL_LETTER_SPACING}}   | Navigation, buttons, metadata          |

### Principles

{{TYPOGRAPHY_PRINCIPLES}}

## Layout

### Spacing System

- **Tokens:** `{{SPACING_TOKENS_LIST}}`.
- **Section rhythm:** {{SECTION_RHYTHM}}.
- **Card internal padding:** {{CARD_PADDING}}.

### Grid & Container

- **Max content width:** {{MAX_WIDTH}}.
- **Layout pattern:** {{LAYOUT_PATTERN}}.

### Whitespace Philosophy

{{WHITESPACE_PHILOSOPHY}}

## Elevation & Depth

| Level      | Treatment             | Use             |
| ---------- | --------------------- | --------------- |
| 0 — Flat   | {{LEVEL_0_TREATMENT}} | {{LEVEL_0_USE}} |
| 1 — Border | {{LEVEL_1_TREATMENT}} | {{LEVEL_1_USE}} |

{{ELEVATION_PROSE}}

## Shapes

### Border Radius Scale

| Token           | Value               | Use               |
| --------------- | ------------------- | ----------------- |
| `{rounded.sm}}` | {{RADIUS_SM_VALUE}} | {{RADIUS_SM_USE}} |
| `{rounded.md}`  | {{RADIUS_MD_VALUE}} | {{RADIUS_MD_USE}} |
| `{rounded.lg}`  | {{RADIUS_LG_VALUE}} | {{RADIUS_LG_USE}} |

{{SHAPES_PROSE}}

## Components

<!-- Add a policy note here if hover states are not documented -->

**`button-primary`** — {{BUTTON_PRIMARY_DESCRIPTION}}. Background `{colors.primary}`, text `{colors.background}`, rounded `{rounded.md}`, padding `{spacing.md}`.

**`card`** — {{CARD_DESCRIPTION}}. Background `{colors.surface}`, rounded `{rounded.lg}`, padding `{spacing.lg}`.

## Do's and Don'ts

### Do

- {{DO_1}}
- {{DO_2}}
- {{DO_3}}
- {{DO_4}}
- {{DO_5}}

### Don't

- {{DONT_1}}
- {{DONT_2}}
- {{DONT_3}}
- {{DONT_4}}
- {{DONT_5}}
- {{DONT_6}}
