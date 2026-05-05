# Rule: Apex DML Guidelines

**Description:** Enforce some best practices for DML operations.

**Applies to:** `**/*.cls` and `**/*.trigger`.

**Guidelines:**
- Avoid SOQL or DML inside `for` loops. Use Maps and Sets to bulkify logic.
- DML should be in user mode. For example: `insert as user` or `update as user`.
- Use `WITH USER_MODE` explicitly for SOQL queries.
- Never concatenate user input into dynamic SOQL strings — use bind variables to prevent SOQL injection. For example: `WHERE Name = :searchTerm` not `'WHERE Name = \'' + searchTerm + '\''`.
- Avoid hardcoded record IDs or hardcoded picklist values in queries.
- Wrap DML in try/catch blocks and surface errors meaningfully rather than swallowing exceptions silently.
- Prefer `Database.insert(records, false)` over plain `insert` in bulk contexts where partial success is acceptable; handle `Database.SaveResult` errors explicitly.
