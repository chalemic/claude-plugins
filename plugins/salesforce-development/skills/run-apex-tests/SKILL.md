---
name: run-apex-tests
description: Run Apex unit tests for recently modified classes with code coverage reporting
---

# Run Apex Tests

Run unit tests for recently modified Apex classes, synchronously, with code coverage reporting.

## Steps

### 1. Identify test classes

Derive the test class name(s) from the Apex classes written or modified in this conversation (e.g. `AccountService` → `AccountServiceTest`). If the user specifies different class names, use those instead.

### 2. Ensure output directory exists

Create `UnitTestResults/` in the project root if it does not already exist.

### 3. Run tests

```bash
sf apex run test --class-names <TestClass1,TestClass2> --code-coverage --result-format json --output-dir UnitTestResults -w 10
```

The `-w 10` flag waits up to 10 minutes for results synchronously.

### 4. Read and interpret results

Read the output JSON from `UnitTestResults/`, then report based on outcome:

**If any tests fail:**
- List each failure with: test method name, error message, and stack trace.
- Do not attempt to fix failures automatically — present them to the user to address.

**If all tests pass:**
- Report a brief summary: classes run and pass count.
- Report the overall code coverage percentage.
- If overall coverage is **below 75%**, treat this as a failure — report the percentage and identify which classes have the lowest individual coverage so the user knows where to focus.
