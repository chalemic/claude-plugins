---
name: write-apex
description: Apply when writing or modifying Apex classes (.cls) or triggers (.trigger)
---

# Write Apex

Apply these guidelines whenever writing or modifying Apex classes (`.cls`) or triggers (`.trigger`).

@./rules/apex_naming.md
@./rules/apex_dml.md
@./rules/apex_testing.md


- After writing or modifying Apex or LWC code, run `/salesforce-code-analysis` and resolve all identified issues before considering the task done.
- If an issue requires restructuring or refactoring to resolve, discuss the proposed changes before making them.
- After all code analysis issues are resuled, run `/deploy-to-salesforce` and resolve any errors before proceeding.
- After all code has deployed, run `/run-apex-tests` to execute the relevant unit tests. Update the Apex to fix failures, but NEVER modify the unit tests themselves without permission; assume the test is correct and the code is wrong.