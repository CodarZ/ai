# Input Template for DESIGN.md Generation

Use this template to prepare the context for the generator.

## Project state

- state: existing | partial | missing | idea-only
- project_name: ""
- product_type: ""
- target_users: ""
- summary: ""

## Evidence sources

- repo_path: ""
- readme_path: ""
- prd_path: ""
- existing_design_doc: "" # path to existing DESIGN.md (for incomplete-spec repair scenario)
- screenshots:
  - ""
- storybook_url: ""
- figma_url: ""
- reference_sites:
  - ""

## Existing system signals

- theme_files:
  - ""
- css_variables_file: ""
- tailwind_config: ""
- component_library: ""

## Constraints

- brand_keywords:
  - ""
- must_keep:
  - ""
- must_avoid:
  - ""
- accessibility_requirements:
  - ""

## Desired output behavior

- strict_spec_compliance: true
- conservative_inference: true
- preserve_existing_patterns: true
- omit_unsupported_sections: true
- fix_non_compliant_structure: false # true for incomplete-spec repair scenario

## Agent notes

- free_form_notes: "" # any additional context, constraints, or special instructions for the generator
