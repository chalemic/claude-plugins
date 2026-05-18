---
name: write-lwc
description: Apply when writing or modifying Lightning Web Components (.js, .html)
---

# Write LWC

Apply these guidelines whenever writing or modifying Lightning Web Components (`.js`, `.html`).

@./rules/lwc.md

## Before writing any code

Determine whether this is a new component or a modification to an existing one:

- **New component:** Call `mcp__salesforce__orchestrate_lwc_component_creation` to get step-by-step creation guidelines. If a PRD or spec document is present in the conversation, use `mcp__salesforce__create_lwc_component_from_prd` instead, passing the PRD content as the `prd` parameter.
- **Modifying an existing component:** Call `mcp__salesforce__orchestrate_lwc_component_optimization` to get optimization guidance.

Follow the returned workflow before proceeding to write or modify code.

## Writing guidelines

- UI should use responsive designs
- UI should follow WCAG best practices
- UI should use SLDS elements and best practices when possible

## After writing code

1. Call `mcp__salesforce__guide_component_accessibility` with `mode: "fix"` to automatically fix any accessibility issues in the written or modified files. If the component includes images, also pass `hasImages: true` to enable Vision AI accessibility guidelines.
2. Run `/salesforce-code-analysis` and resolve all identified issues before considering the task done. If an issue requires restructuring or refactoring, discuss the proposed changes before making them.
3. After all code analysis issues are resolved, run `/deploy-to-salesforce` and resolve any errors before proceeding.
4. After all code has deployed, run `/run-lwc-tests` to execute the relevant Jest unit tests.
