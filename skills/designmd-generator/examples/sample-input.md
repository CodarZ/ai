# Sample Input

## Project state

- state: partial
- project_name: Atlas Billing
- product_type: B2B SaaS dashboard
- target_users: finance teams and operators
- summary: A billing portal with invoices, usage charts, plan management, and a support inbox.

## Evidence sources

- repo_path: ./apps/web
- readme_path: ./README.md
- prd_path: ./docs/prd.md
- screenshots:
  - ./artifacts/home.png
  - ./artifacts/billing.png
- reference_sites:
  - https://getdesign.md/stripe/design-md
  - https://getdesign.md/notion/design-md

## Existing system signals

- theme_files:
  - ./src/theme.ts
- css_variables_file: ./src/styles/globals.css
- tailwind_config: ./tailwind.config.ts
- component_library: shadcn/ui

## Constraints

- brand_keywords:
  - calm
  - precise
  - trustworthy
- must_keep:
  - existing invoice table layout
  - current plan comparison flow
- must_avoid:
  - flashy gradients
  - dense copy blocks
- accessibility_requirements:
  - keyboard navigable
  - WCAG AA contrast for text

## Desired output behavior

- strict_spec_compliance: true
- conservative_inference: true
- preserve_existing_patterns: true
- omit_unsupported_sections: true
