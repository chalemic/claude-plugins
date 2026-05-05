# Rule: LWC Best Practices

**Description:** Maintain consistent structure and safe patterns in LWC components.

**Applies to:** `**/*.html`, `**/*.js`

**HTML Guidelines:**
- Wrap all content in a root `<template>` tag
- Use a top-level `<div class="component-name">` block
- Use `lwc:if`, `lwc:elseif`, and `lwc:else` for conditional rendering (preferred over the legacy `if:true`/`if:false` syntax)
- Group conditional rendering elements together
- Include a comment block before each major section

**JavaScript Guidelines:**
- Name custom events in `kebab-case` and dispatch them with `CustomEvent` (For example: `this.dispatchEvent(new CustomEvent('record-saved', { detail: result }))`)
- Public `@api` properties must be primitive types or plain objects; never expose complex class instances
- Use `@wire` adapters for declarative data fetching; avoid imperative Apex calls unless reactive behavior is needed
- Never use `innerHTML` or dynamic code execution functions — both are XSS vectors that bypass Locker Service protections
- Do not directly manipulate the DOM via `document.querySelector`; use `this.template.querySelector` instead

**Accessibility:**
- Interactive elements must have descriptive ARIA labels or visible label text
- Ensure keyboard navigability for all custom interactive components
- Toast messages should use `mode: 'sticky'`