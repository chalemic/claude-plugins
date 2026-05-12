# Rule: Apex Testing Best Practices

**Description:** Enforce some best practices for unit testing.

**Applies to:** `**/*.cls` and `**/*.trigger`.

**Guidelines:**
- Test classes must use PascalCase and end with `Test` (For example: `AccountServiceTest`)
- Test method names should describe the test scenario clearly (For example: `testCalculateTaxWithValidInput`)
- When writing asserts, always use the `Assert` class instead of `System.assert`
- Always annotate the test class with `@isTest(seeAllData=false)` — never use `seeAllData=true`, as it couples tests to org data and causes flaky results
- Tests must create all required data themselves; never rely on existing org records
- Use a `@TestSetup` method to insert shared test data once per test class rather than repeating inserts in each test method
- Use `System.runAs(testUser)` for any test that exercises permission- or profile-sensitive logic
- Wrap the code under test with `Test.startTest()` and `Test.stopTest()` to reset governor limits and allow async operations (such as `@future` or queueable jobs) to complete
- Use test data generator/builder classes to create test records rather than constructing SObjects inline in test methods or `@TestSetup`.
