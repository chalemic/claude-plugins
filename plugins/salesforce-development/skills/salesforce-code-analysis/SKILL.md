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

### 3. Run the CLI analyzer

Run the following command, replacing `<targets>` with the space-separated list of target files:

```bash
sf code-analyzer run --target <targets> --output-file CodeAnalysis/results.json
```

### 4. Run MCP analysis (in parallel with or immediately after Step 3)

#### For Apex files (`.cls`)

For each `.cls` file in the target list, call `mcp__salesforce__scan_apex_class_for_antipatterns`:
- `className`: derived from the filename (e.g., `AccountService` from `AccountService.cls`)
- `apexFilePath`: absolute path to the `.cls` file
- `directory`: the project root directory
- `usernameOrAlias`: call `mcp__salesforce__get_username` first if the default org is not known

This detects performance antipatterns the CLI does not cover: `Schema.getGlobalDescribe()` usage, SOQL without `WHERE`/`LIMIT` clauses, and SOQL queries with unused fields.

#### For LWC files (`.js`, `.html`)

Call `mcp__salesforce__validate_and_optimize` with:
- `suite: "core-lwc"`
- `targetPaths`: list of absolute paths to the LWC files being analyzed

This returns a runbook — follow it exactly. The runbook will instruct you to call validators and `mcp__salesforce__score_issues` after each validator and again in aggregate. The final output includes a readiness score (0–100) and quality grade (`draft`, `prototype`, or `review-for-production`).

### 5. Merge and group all findings

Combine violations from the CLI results (`CodeAnalysis/results.json`) and all MCP findings into a single table grouped by severity:

| Severity | Label    | Action                          |
|----------|----------|---------------------------------|
| 1        | Critical | Discuss with user before fixing |
| 2        | High     | Discuss with user before fixing |
| 3        | Moderate | Discuss with user before fixing |
| 4        | Low      | Fix automatically               |
| 5        | Info     | Fix automatically               |

For LWC files, also report the readiness score and quality grade from `mcp__salesforce__score_issues`.

### 6. Apply automatic fixes (severity 4–5)

For each Low and Info violation:
- Read the affected file.
- Apply the fix directly.
- Briefly note what was changed and why.

### 7. Discuss before fixing (severity 1–3)

For each Critical, High, and Moderate violation, present a summary to the user:
- File and line number
- Rule name and severity
- Description of the issue
- Recommended fix

Wait for explicit user approval before making any changes for these severities.

### 8. Re-run to verify

After all automatic fixes are applied, re-run the CLI analyzer on the same target files to confirm no regressions or new violations were introduced.
