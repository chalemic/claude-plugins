---
name: salesforce-code-analysis
description: Run Salesforce Code Analyzer against recently modified Apex or LWC files and fix violations
---

# Salesforce Code Analysis

Run the Salesforce Code Analyzer against recently modified files, automatically fix low-severity issues, and discuss higher-severity issues before making changes.

## When to use this skill

Use this skill after writing or modifying any Apex (`.cls`, `.trigger`) or LWC (`.js`, `.html`) files.

## Steps

### 1. Identify target files

- **Default:** Use only the Apex and LWC files written or modified in this conversation.
- **If the user specifies a scope** (e.g., a directory, a component name, or "all files"), use that instead.

### 2. Prepare output directory

Ensure `CodeAnalysis/` exists in the project root. Create it if it does not.

### 3. Run the analyzer

Run the following command, replacing `<targets>` with the space-separated list of target files:

```bash
sf code-analyzer run --target <targets> --output-file CodeAnalysis/results.json
```

### 4. Read and parse results

Read `CodeAnalysis/results.json` and group all violations by severity:

| Severity | Label    | Action                          |
|----------|----------|---------------------------------|
| 1        | Critical | Discuss with user before fixing |
| 2        | High     | Discuss with user before fixing |
| 3        | Moderate | Discuss with user before fixing |
| 4        | Low      | Fix automatically               |
| 5        | Info     | Fix automatically               |

### 5. Apply automatic fixes (severity 4–5)

For each Low and Info violation:
- Read the affected file.
- Apply the fix directly.
- Briefly note what was changed and why.

### 6. Discuss before fixing (severity 1–3)

For each Critical, High, and Moderate violation, present a summary to the user:
- File and line number
- Rule name and severity
- Description of the issue
- Recommended fix

Wait for explicit user approval before making any changes for these severities.

### 7. Re-run to verify

After all automatic fixes are applied, re-run the analyzer on the same target files to confirm no regressions or new violations were introduced.
