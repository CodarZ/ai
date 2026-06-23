# Sample Input: Incomplete Spec Repair

## Project state

- state: partial
- project_name: Acme Dashboard
- product_type: Internal admin tool
- target_users: Operations team
- summary: An internal dashboard for managing orders, inventory, and customer support tickets. Has an existing DESIGN.md that covers colors and typography but is missing component specs, spacing tokens, and responsive behavior.

## Evidence sources

- repo_path: ./apps/admin
- readme_path: ./README.md
- existing_design_doc: ./DESIGN.md
- screenshots:
  - ./screenshots/orders-list.png
  - ./screenshots/ticket-detail.png
  - ./screenshots/inventory-grid.png

## Existing system signals

- theme_files:
  - ./src/theme.ts
- css_variables_file: ./src/styles/tokens.css
- tailwind_config: ./tailwind.config.js
- component_library: custom (no external lib)

## Existing DESIGN.md issues

- Missing: spacing tokens, rounded tokens, component definitions
- Missing: Elevation & Depth section, Shapes section
- Contains: Colors section (but uses non-standard token names like `brand-blue` instead of `primary`)
- Contains: Typography section (but no fallback stack documented)
- Contains: Do's and Don'ts (but items are generic, not specific to the project)
- Non-compliant: front matter has `confidence` labels on tokens (should be in audit only)
- Non-compliant: section order is Overview → Typography → Colors (wrong order)

## Constraints

- brand_keywords:
  - efficient
  - clear
  - no-nonsense
- must_keep:
  - existing table density
  - current color scheme
- must_avoid:
  - playful design elements
  - unnecessary animations
- accessibility_requirements:
  - keyboard navigable
  - WCAG AA contrast

## Desired output behavior

- strict_spec_compliance: true
- conservative_inference: true
- preserve_existing_patterns: true
- omit_unsupported_sections: true
- fix_non_compliant_structure: true
