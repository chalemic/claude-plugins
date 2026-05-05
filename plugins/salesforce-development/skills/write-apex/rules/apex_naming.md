# Rule: Apex Naming Conventions

**Description:** Enforce some guidelines for naming conventions.

**Applies to:** `**/*.cls` and `**/*.trigger`.

**Guidelines:**
- Class names must be PascalCase (For example: `AccountService`)
- Method names must be camelCase
- Constants must be UPPER_SNAKE_CASE
- Variable names must be camelCase and descriptive (For example: `accountList` or `isClosed`)
- Boolean variable names should start with `is`, `has`, or `can` (For example: `isActive` or `hasAccess`)
- Use plural names for collections (For example: `contacts` or `accountsMap`)
- Avoid abbreviations and single-letter variables (For example: `account`, not `acc`)
- Interfaces should be prefixed with `I` (For example: `IAccountService`); implementing classes use the name without the prefix (For example: `AccountService`)
- Inner classes should be PascalCase and named to reflect their role relative to the outer class (For example: `AccountService.Request` or `AccountService.Result`)
- Enums should be PascalCase with UPPER_SNAKE_CASE values (For example: `enum Status { ACTIVE, INACTIVE }`)
