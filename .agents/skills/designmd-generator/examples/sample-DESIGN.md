---
version: alpha
name: Atlas Billing
description: |
  A calm, precise billing dashboard for finance teams and operators. The system uses a restrained blue-led palette with neutral surfaces and strong text contrast, rendered in Inter across all text roles. Cards and sections sit on a light cream canvas with no decorative elevation — depth comes from spacing rhythm and subtle border separation rather than shadows. The interface prioritizes scanning density for invoice tables and usage charts while maintaining a trustworthy, enterprise-grade visual tone.
colors:
  primary: '#2563eb'
  secondary: '#64748b'
  background: '#ffffff'
  surface: '#f8fafc'
  text: '#0f172a'
typography:
  body:
    fontFamily: Inter
    fontSize: 16px
    fontWeight: 400
    lineHeight: 1.5
    letterSpacing: 0
  label:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: 500
    lineHeight: 1.4
    letterSpacing: 0.01em
rounded:
  sm: 4px
  md: 8px
  lg: 12px
spacing:
  xs: 4px
  sm: 8px
  md: 16px
  lg: 24px
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

Atlas Billing should feel calm, precise, and dependable. The interface supports finance workflows, so density is acceptable when it improves scanning and decision speed. The visual language favors clear information structure over decorative styling.

**Key Characteristics:**

- Inter used across all text roles — no display face, hierarchy built from weight and size contrast
- Restrained blue-led palette with neutral surfaces; primary blue carries action and emphasis only
- Cards read as organized containers, not floating objects — no decorative elevation
- Spacing rhythm is consistent across tables, forms, and summary panels
- Moderate radius values keep the interface modern without becoming soft or playful

## Colors

### Brand & Accent

- **Primary** (`{colors.primary}` — `#2563eb`): the brand's action color. Used for primary CTAs, active links, focus rings, and chart highlights. Chosen for trust and clarity in financial contexts.
- **Secondary** (`{colors.secondary}` — `#64748b`): muted neutral for secondary actions, metadata text, and chart gridlines.

### Surface

- **Background** (`{colors.background}` — `#ffffff`): page body, table backgrounds, form fields.
- **Surface** (`{colors.surface}` — `#f8fafc`): card backgrounds, sidebar fill, alternating row tint.

### Text

- **Text** (`{colors.text}` — `#0f172a`): headlines, body copy, table data. Near-black chosen for maximum legibility in dense financial layouts.

## Typography

### Font Family

**Inter** is used for all text roles — body, headings, labels, table data. The font was chosen for its tabular number support and strong legibility at small sizes, critical for invoice tables and usage charts.

### Hierarchy

| Token                | Size | Weight | Line Height | Letter Spacing | Use                                                      |
| -------------------- | ---- | ------ | ----------- | -------------- | -------------------------------------------------------- |
| `{typography.body}`  | 16px | 400    | 1.5         | 0              | Body copy, paragraph text, form labels                   |
| `{typography.label}` | 14px | 500    | 1.4         | 0.01em         | Table headers, navigation links, button labels, metadata |

### Principles

The hierarchy is deliberately flat: two sizes, two weights. Headings increase weight (700) rather than size to keep the interface compact. Labels use slightly tighter line-height (1.4) to maintain density in table headers and sidebar navigation.

## Layout

### Spacing System

- **Tokens:** `{spacing.xs}` (4px) · `{spacing.sm}` (8px) · `{spacing.md}` (16px) · `{spacing.lg}` (24px).
- **Section rhythm:** major content blocks separated by `{spacing.lg}` (24px); card internal padding uses `{spacing.lg}`.
- **Table rows:** compact vertical padding at `{spacing.sm}` (8px) to maximize data density.

### Grid & Container

- **Desktop:** two-column shell with persistent left sidebar (~240px) and scrollable content area.
- **Content max width:** ~960px for main panels.
- **Tables:** full-width within content area, no horizontal scroll at desktop breakpoints.

### Whitespace Philosophy

Whitespace is functional, not decorative. Gaps between elements signal grouping — related items sit closer together, unrelated items breathe. The sidebar and content area are separated by a 1px border, not by margin, to keep the layout tight.

## Elevation & Depth

| Level             | Treatment                    | Use                                        |
| ----------------- | ---------------------------- | ------------------------------------------ |
| 0 — Flat          | No border, no shadow         | Default for page body, table rows, sidebar |
| 1 — Border        | 1px solid `{colors.surface}` | Card edges, section dividers               |
| 2 — Subtle shadow | `0 1px 3px rgba(0,0,0,0.08)` | Dropdowns, modals, popovers                |

Depth is minimal. Cards use border-based separation, not shadow. The system stays flat to keep financial data readable and avoid visual noise.

## Shapes

### Border Radius Scale

| Token          | Value | Use                      |
| -------------- | ----- | ------------------------ |
| `{rounded.sm}` | 4px   | Buttons, inputs, badges  |
| `{rounded.md}` | 8px   | Cards, tables, panels    |
| `{rounded.lg}` | 12px  | Modals, large containers |

## Components

**`button-primary`** — the primary CTA. Background `{colors.primary}`, text `{colors.background}`, rounded `{rounded.md}`, padding `{spacing.md}`. Used for "Create Invoice", "Save Changes", "Export CSV".

**`card`** — the primary surface container. Background `{colors.surface}`, rounded `{rounded.lg}`, padding `{spacing.lg}`. Used for invoice summaries, usage charts, plan comparison panels. Cards should remain readable in dense states and should not rely on heavy borders for structure.

## Do's and Don'ts

### Do

- Keep hierarchy explicit — use weight contrast, not size jumps.
- Preserve strong text contrast for financial data legibility.
- Keep component spacing consistent across tables, forms, and cards.
- Use primary blue only for actions and emphasis, not for decorative elements.
- Maintain compact density in table-heavy views.

### Don't

- Introduce decorative gradients or playful color accents.
- Add unsupported visual flourishes beyond the existing token vocabulary.
- Change component behavior without evidence from the existing codebase.
- Use shadows for card separation — borders are the system's depth signal.
- Increase spacing beyond the established rhythm without justification.
- Use primary blue for decorative elements — it is reserved for actions and emphasis only.
