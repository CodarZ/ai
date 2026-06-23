# Sample Input: Missing Spec — First-Pass Design

## Project state

- state: existing
- project_name: Pulse Analytics
- product_type: SaaS analytics dashboard
- target_users: Product managers and data analysts
- summary: A real-time analytics dashboard with charts, funnel views, and cohort tables. Has a mature UI codebase with Tailwind CSS and React components but no design documentation whatsoever.

## Evidence sources

- repo_path: ./apps/web
- readme_path: ./README.md
- screenshots:
  - ./screenshots/dashboard.png
  - ./screenshots/funnel.png
  - ./screenshots/cohort.png
  - ./screenshots/settings.png

## Existing system signals

- theme_files:
  - ./src/theme/colors.ts
  - ./src/theme/typography.ts
- css_variables_file: ./src/styles/variables.css
- tailwind_config: ./tailwind.config.ts
- component_library: custom + Radix UI primitives

## Constraints

- brand_keywords:
  - data-driven
  - clean
  - professional
- must_keep:
  - current chart color palette (used in all dashboards)
  - existing table row density
- must_avoid:
  - skeuomorphic design
  - heavy borders
- accessibility_requirements:
  - keyboard navigable
  - screen reader compatible
  - WCAG AA contrast for data visualization

## Desired output behavior

- strict_spec_compliance: true
- conservative_inference: true
- preserve_existing_patterns: true
- omit_unsupported_sections: true

## Notes for the agent

- The chart color palette is critical — it's used across all data visualizations and users have built reports around it
- Typography choices were deliberate for data density — don't suggest "improvements"
- Dark mode exists but is rarely used — document it if evidence supports it, omit if not
