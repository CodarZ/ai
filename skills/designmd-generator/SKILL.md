---
name: designmd-generator
description: Use when a project needs a DESIGN.md file — for existing projects missing design docs, projects with incomplete or inconsistent design specs, or new projects that need a first-pass design contract from available evidence
---

# DESIGN.md Generator

Generate a strict, spec-compliant DESIGN.md grounded in project evidence.

**Core principle:** DESIGN.md is a design narrative, not a token dump. The prose explains _why_ decisions were made, describes how the system feels, and documents the constraints that make it coherent. Tokens are the appendix; the prose is the contract.

## When to Use

- Existing project has no DESIGN.md and needs one
- Existing DESIGN.md is incomplete, inconsistent, or non-compliant
- New project needs a design contract from PRD/brief/screenshots
- AI coding agent needs a design spec to follow

**Do NOT use for:** Projects that already have a complete, compliant DESIGN.md (unless asked to audit it).

## Project State Classification

Before generating, classify the project:

| State         | Description                               | Inference aggressiveness                      |
| ------------- | ----------------------------------------- | --------------------------------------------- |
| **existing**  | Codebase with UI, no DESIGN.md            | Conservative — extract from code              |
| **partial**   | Some design docs or tokens exist          | Moderate — fill gaps from evidence            |
| **missing**   | Codebase exists but zero design artifacts | Conservative — minimal defensible system      |
| **idea-only** | No code, only brief/PRD/references        | Most conservative — explicit constraints only |

This classification drives how much you may infer vs. must leave as unknowns.

## Required Workflow

### Phase 1: Audit

Collect evidence BEFORE writing anything. Inspect in priority order:

1. CSS variables / theme files
2. Tailwind config / design token files
3. Component source code
4. Rendered UI / screenshots
5. Storybook / Figma exports
6. README / PRD / issue text
7. Competitive references (idea-only)

Write `design-audit.json` with:

- `project_state` (existing | partial | missing | idea-only)
- `confidence_summary` (overall: high | medium | low + reason)
- `evidence` (sources, colors, typography, spacing, rounded, components, layout, accessibility)
- `inferences` (list of inferred conclusions)
- `assumptions` (list of assumptions with rationale)
- `missing_information` (gaps that block a complete DESIGN.md)
- `recommended_next_steps`

### Phase 2: Extract Tokens

Populate ONLY the official DESIGN.md token groups:

- `version`, `name`, `description`, `colors`, `typography`, `rounded`, `spacing`, `components`

Use `{path.to.token}` syntax for references (e.g., `{colors.primary}`, `{rounded.md}`).

**Description field:** Write a rich paragraph (3-5 sentences) that captures the design system's identity at a glance. Include: the dominant visual characteristic, the palette approach, the typographic identity, the depth/elevation approach, and the overall feel. This is the first thing an agent reads — make it count.

### Phase 3: Compose DESIGN.md

Produce the file with:

1. Optional YAML front matter (tokens as machine-readable YAML)
2. Markdown body with `##` sections

**Canonical section order** (omit unsupported, never reorder):

1. `## Overview`
2. `## Colors`
3. `## Typography`
4. `## Layout`
5. `## Elevation & Depth`
6. `## Shapes`
7. `## Components`
8. `## Do's and Don'ts`

**Allowed aliases:** Overview → Brand & Style, Layout → Layout & Spacing, Elevation & Depth → Elevation

**Project-specific sections** may be appended AFTER the canonical sections when evidence supports them:

- `## Responsive Behavior` — breakpoints, touch targets, collapsing strategy
- `## Iteration Guide` — developer workflow for maintaining the design system
- `## Known Gaps` — documented limitations, missing evidence, open questions

### Phase 4: Validate

Before finishing, verify ALL of:

- [ ] Front matter starts and ends with `---`
- [ ] YAML parses correctly
- [ ] `description` is a rich paragraph, not a single sentence
- [ ] Body uses only `##` sections (subsections use `###`)
- [ ] Section order matches spec
- [ ] Token names are consistent (no duplicates, no invented names)
- [ ] All token references `{...}` resolve to defined tokens
- [ ] Component properties use only valid keys: backgroundColor, textColor, typography, rounded, padding, size, height, width
- [ ] Every component defined in front matter has prose in the Components section
- [ ] No fabricated values (every value has evidence in audit)
- [ ] Audit completeness: every token in DESIGN.md front matter has a corresponding entry in design-audit.json
- [ ] No extra sections outside the spec (except documented project-specific sections)
- [ ] Do's count is 5-7, Don'ts count is 6-8
- [ ] Typography hierarchy table includes Letter Spacing column
- [ ] No prose before or after the file
- [ ] No code fences around the output

## Prose Depth Rules

The body prose is the primary contract. Follow these rules:

### Overview

- 2-4 paragraphs covering: the dominant visual characteristic, the palette approach, the typographic identity, the depth philosophy, and the overall feel
- Include a **Key Characteristics** subsection as bullet points summarizing the system's defining traits
- Reference specific token values inline (e.g., `{colors.canvas}` — `#fdfcfc`)

### Colors

- Group by role: Brand & Accent, Surface, Text, Semantic
- For each color: token name, hex value, and a sentence explaining its role and why it exists
- Document hover/active variants for semantic colors
- Note the source pages audited

### Typography

- Document the font family with full fallback stack
- Hierarchy table with columns: Token, Size, Weight, Line Height, Letter Spacing, Use
- Include concrete use examples in the Use column (e.g., "Hero headline ('The open source AI coding agent')")
- Add a **Principles** subsection explaining how the hierarchy works (weight vs. size contrast, line-height rationale)
- Optionally add a **Font Substitutes** note for commercial fonts

### Layout

- Document the spacing system with all tokens
- Grid & container rules with specific widths
- Add a **Whitespace Philosophy** subsection explaining how spacing creates structure

### Elevation & Depth

- Table with Level, Treatment, Use columns
- Add a **Decorative Depth** subsection describing non-CSS visual elements (ASCII art, mockups, charts)

### Shapes

- Border radius scale table
- Add a **Photography Geometry** subsection if the system uses non-standard visual elements

### Components

- **Every component defined in front matter must have prose** — no exceptions
- For each: background, text color, typography token, padding, radius, and a description of where it's used
- Document variant states (active, disabled, focused) with their differences
- Group by category: Buttons, Inputs, Cards & Containers, Navigation, Footer, Inline
- Add a policy note at the top if hover states are not documented

### Do's and Don'ts

- 5-7 Do items covering what the system IS
- 6-8 Don't items covering what would BREAK the system
- Each item should be specific and actionable, not generic

## Evidence Rules

| Confidence   | Meaning                                  | Example                                   |
| ------------ | ---------------------------------------- | ----------------------------------------- |
| **verified** | Directly observable in source            | `--color-primary: #2563eb` in CSS         |
| **inferred** | Strongly supported by multiple signals   | Card shadow consistent across screenshots |
| **assumed**  | Conservative hypothesis, limited support | Mobile breakpoint behavior unclear        |

**Never present inferred or assumed as verified.** Prefer omission over fabrication.

## Scenario Handling

### Existing project — compliance check

**When:** Project has UI code but no DESIGN.md, or has one that's outdated.

1. Audit the codebase thoroughly — CSS variables, theme files, component source, screenshots
2. Extract all verifiable tokens with source locations
3. Build the DESIGN.md from evidence, not from the existing (possibly broken) design docs
4. In the audit: flag any patterns that contradict each other (e.g., two different primary colors in different parts of the app)
5. In `missing_information`: list design decisions that are ambiguous or inconsistent across the codebase

**Key risk:** The codebase may have accumulated inconsistencies over time. The DESIGN.md should document the _dominant_ pattern, not every variation. Record contradictions in the audit.

### Missing spec — first-pass design

**When:** Project has code/UI but zero design documentation. Need to reverse-engineer a design system.

1. Audit available evidence — CSS variables, Tailwind config, component source, screenshots
2. Extract only what's verifiable — never guess values
3. Build a minimal defensible system: every token has a source, every component has evidence
4. All non-explicit choices marked as inferred/assumed in audit
5. In `recommended_next_steps`: list what the team should verify or decide (e.g., "Confirm dark mode support", "Define hover states for buttons")

**Key risk:** Without source code access, you can only infer from rendered output. Document this limitation in the audit's `confidence_summary`. A DESIGN.md built from screenshots alone is inherently lower confidence than one built from CSS variables.

### Incomplete spec — repair

**When:** Project has a DESIGN.md but it's incomplete, inconsistent, or non-compliant with the spec.

1. Audit both the existing spec AND the codebase
2. For each existing section: check if it has evidence support from the codebase. If not, flag it
3. For each codebase pattern: check if it's represented in the spec. If not, add it with confidence label
4. Identify non-compliant content:
   - Sections outside the canonical order → reorder
   - Tokens not in the official groups → remove or map to valid groups
   - `confidence` labels in front matter → move to audit only
   - Fabricated values (no evidence) → remove, record in audit
   - Generic filler prose → replace with evidence-grounded descriptions
5. Result: strict subset that's both spec-compliant and evidence-grounded

**Key risk:** The existing spec may contain decisions the team relies on but can't verify from code. Don't silently remove these — flag them in `missing_information` and ask the team to confirm.

### External website — reverse-engineer from rendered output

**When:** Target is a live website (no source code access). Need to infer the design system from rendered HTML/CSS.

1. Fetch multiple pages (homepage, key subpages, blog) to capture the full visual range
2. Attempt to access CSS files directly — look for `/_next/static/css/`, `assets/*.css`, or inline `<style>` tags
3. If CSS files are accessible: extract exact values (hex colors, font declarations, spacing, radius)
4. If CSS files are NOT accessible (most common): infer from rendered structure, HTML semantics, and visual patterns
5. Mark ALL values as `inferred` in the audit — never present rendered-output observations as `verified`
6. Document the verification limitation in `confidence_summary.reason`

**Verification strategies for external sites:**

- **Browser DevTools**: If the user can open the site, suggest inspecting computed styles for exact values
- **CSS file probing**: Try common paths (`/css/app.css`, `/_next/static/css/`, `/assets/css/`) — Next.js, Vite, and CRA have predictable patterns
- **GitHub source**: If the site is open-source, clone the repo and extract from source
- **Multiple page comparison**: Cross-reference values across pages — if a color appears consistently on 3+ pages, confidence increases
- **Font identification**: Check `<link>` tags for Google Fonts, inspect `font-family` in computed styles, or use font identification tools

**Key risk:** Without source code, all values are approximations. The DESIGN.md should explicitly state this limitation. Prefer conservative ranges (e.g., "48-64px") over false precision (e.g., "52px") when exact values are unverifiable.

## Output Contract

When writing a full result, output ONLY:

- `design-audit.json`
- `DESIGN.md`

No commentary around the files. No code fences. No preamble.

## Common Mistakes

| Mistake                                | Fix                                                                             |
| -------------------------------------- | ------------------------------------------------------------------------------- |
| Invented token values                  | Omit the token; record gap in audit                                             |
| Wrong section order                    | Follow canonical order exactly                                                  |
| `confidence` in DESIGN.md front matter | Confidence lives in audit only                                                  |
| Token ref `{colors.primary.value}`     | Use `{colors.primary}` (no `.value`)                                            |
| Generic filler in body sections        | Every sentence must reference evidence                                          |
| Missing `design-audit.json`            | Always produce audit first                                                      |
| Single-sentence description            | Write 3-5 sentence paragraph capturing system identity                          |
| Components without prose               | Every front matter component needs a prose entry                                |
| Missing subsections                    | Add Principles, Whitespace Philosophy, Decorative Depth where evidence supports |
| Abbreviated Do's and Don'ts            | 5-7 Do items, 6-8 Don't items, each specific and actionable                     |

## Supporting Files

| File                                                           | Purpose                                                                          |
| -------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| [rules/designmd-spec.md](rules/designmd-spec.md)               | Full DESIGN.md specification reference (token schema, section order, validation) |
| [rules/token-extraction.md](rules/token-extraction.md)         | Token extraction rules per group (colors, typography, spacing, etc.)             |
| [templates/DESIGN_TEMPLATE.md](templates/DESIGN_TEMPLATE.md)   | DESIGN.md output template with placeholders                                      |
| [templates/AUDIT_TEMPLATE.json](templates/AUDIT_TEMPLATE.json) | design-audit.json structure template                                             |
| [templates/INPUT_TEMPLATE.md](templates/INPUT_TEMPLATE.md)     | Input context gathering template                                                 |
| [examples/sample-input.md](examples/sample-input.md)           | Example: prepared input for a partial project                                    |
| [examples/sample-audit.json](examples/sample-audit.json)       | Example: completed audit for a partial project                                   |
| [examples/sample-DESIGN.md](examples/sample-DESIGN.md)         | Example: final DESIGN.md output                                                  |

Load the spec reference when unsure about allowed tokens, section order, or component properties. Use templates as structural starting points. Use examples to calibrate output quality.
