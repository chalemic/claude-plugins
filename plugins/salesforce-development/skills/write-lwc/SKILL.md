---
name: write-lwc
description: Apply when writing or modifying Lightning Web Components (.js, .html)
---

# Write LWC

Apply these guidelines whenever writing or modifying Lightning Web Components (`.js`, `.html`).

@./rules/lwc.md

- UI should use responsive designs
- UI should follow WCAG best practices
- UI should use SLDS elements and best practices when possible
- After writing or modifying LWC code, run `/salesforce-code-analysis` and resolve all identified issues before considering the task done.
- If an issue requires restructuring or refactoring to resolve, discuss the proposed changes before making them.
- After all code analysis issues are resolved, run `/deploy-to-salesforce` and resolve any errors before proceeding.
- After all code has deployed, run `/run-lwc-tests` to execute the relevant Jest unit tests.
