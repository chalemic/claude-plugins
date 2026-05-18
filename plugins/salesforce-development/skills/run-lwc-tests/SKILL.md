---
name: run-lwc-tests
description: Run LWC Jest unit tests for recently modified components with code coverage reporting
---

# Run LWC Jest Tests

Run Jest unit tests for recently modified LWC components, with code coverage reporting.

## Steps

### 1. Identify components under test

Derive the component name(s) from the LWC files written or modified in this conversation (e.g. `myComponent` → `--testPathPattern=myComponent`). If the user specifies different targets, use those instead.

### 2. Ensure output directory exists

Create `UnitTestResults/` in the project root if it does not already exist.

### 3. Run tests

```bash
npm run test:unit -- --coverage --json --outputFile=UnitTestResults/jest-results.json --coverageDirectory=UnitTestResults/coverage --testPathPattern=<componentName>
```

### 4. Run accessibility tests

Call `mcp__salesforce__run_lwc_accessibility_jest_tests`. This returns instructions for running Sa11y accessibility Jest tests — follow them to run accessibility tests on the modified components and report any failures alongside the Jest results.

### 5. Read and interpret results

Read `UnitTestResults/jest-results.json` and the coverage summary, then report based on outcome:

**If any tests fail:**
- List each failure with: test name, error message, and stack trace.
- Do not attempt to fix failures automatically — present them to the user to address.

**If all tests pass:**
- Report a brief summary: components tested and pass count.
- Report the overall code coverage percentage.
- If overall coverage is **below 75%**, treat this as a failure:
  - Report the percentage and identify which files have the lowest individual coverage.
  - Invoke `mcp__salesforce__orchestrate_lwc_component_testing` to get guidance on improving test coverage. This orchestrates `create_lwc_jest_tests` and `review_lwc_jest_tests` internally to analyze the component and generate suggested test cases.
  - Present the suggested tests to the user for review — do not write them automatically.
