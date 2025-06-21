# Flaky Test Analyzer and Fixer - Custom Command for Claude Code

$ARGUMENTS

## Purpose
You are tasked with identifying, analyzing, and fixing flaky tests in a codebase. Your goal is to make intelligent decisions about whether to fix, refactor, or remove tests based on their value, coverage overlap, and focus on business logic.

Use multiple subagents to work in parallel
You can use GitHub action run history to evaluate historic flakiness

## Phase 1: Discovery and Analysis

### 1.1 Identify Flaky Tests
First, locate potentially flaky tests by looking for:
- Tests with random failures in CI/CD logs
- Tests using `setTimeout`, `setInterval`, or other timing-dependent code
- Tests that depend on external services or network calls without proper mocking
- Tests with race conditions or order dependencies
- Tests that use hardcoded dates/times without proper time freezing
- Tests that rely on specific system states or environmental conditions
- Look for patterns like retry mechanisms, flaky test annotations, or skip flags

### 1.2 Categorize Flakiness Patterns
Classify each flaky test by its root cause:
- **Timing Issues**: Race conditions, improper async handling, arbitrary waits
- **External Dependencies**: Network calls, file system, databases without proper isolation
- **Test Interdependence**: Tests that depend on execution order or shared state
- **Environmental**: Platform-specific, timezone-dependent, locale-dependent
- **Non-deterministic Code**: Random values, timestamps, UUIDs without mocking
- **Resource Constraints**: Memory leaks, port conflicts, file handle exhaustion

## Phase 2: Deep Analysis

### 2.1 Understand Test Intent
For each flaky test, determine:
- What business logic or behavior is being tested?
- Is this testing implementation details or actual business requirements?
- What is the value this test provides to the codebase?
- Could this be tested at a different level (unit vs integration vs e2e)?

### 2.2 Coverage Analysis
Check for redundancy:
- Search for similar test cases across the test suite
- Identify if the same business logic is tested elsewhere more reliably
- Look for overlapping integration tests that might cover the same scenarios
- Consider if multiple unit tests could replace a flaky integration test

### 2.3 Business Logic Focus Assessment
Evaluate if the test is focused on the right things:
- Is it testing business rules and requirements?
- Or is it testing implementation details that could change?
- Does it validate user-facing behavior or internal mechanics?
- Would a change to this test indicate a real regression?

## Phase 3: Strategic Decision Making

### 3.1 Decision Framework
For each flaky test, decide on one of these actions:

**FIX** - When the test:
- Covers unique, critical business logic
- Has no redundant coverage elsewhere
- Can be made reliable with reasonable effort
- Tests important edge cases or error scenarios

**REFACTOR** - When the test:
- Has value but is testing at the wrong level
- Could be split into more focused, deterministic tests
- Needs better isolation or mocking strategies
- Would benefit from a different testing approach

**REMOVE** - When the test:
- Is redundant with more reliable tests
- Tests implementation details rather than behavior
- Has low value relative to maintenance cost
- Cannot be made reliable without significant architectural changes

**REPLACE** - When the test:
- Has important coverage but poor implementation
- Could be better expressed as a different type of test
- Needs fundamental restructuring to be valuable

## Phase 4: Implementation Strategy

### 4.1 Fixing Patterns

**For Timing Issues:**
- Replace arbitrary waits with proper event waiting
- Use test utilities for async operations (waitFor, etc.)
- Mock time-dependent operations
- Ensure proper promise handling and async/await usage

**For External Dependencies:**
- Implement comprehensive mocking/stubbing
- Use test doubles for external services
- Create reliable test fixtures
- Ensure proper test isolation

**For Test Interdependence:**
- Add proper setup/teardown
- Isolate test data and state
- Remove shared variables between tests
- Ensure each test is self-contained

**For Non-deterministic Code:**
- Mock random value generators
- Freeze time for date-dependent tests
- Use deterministic test data
- Control all sources of randomness

### 4.2 Refactoring Guidelines

When refactoring tests:
1. **Extract shared setup** into well-named helper functions
2. **Use data-driven tests** for similar scenarios with different inputs
3. **Separate concerns** - one assertion per test when possible
4. **Improve naming** to clearly express what's being tested
5. **Add comments** explaining why certain approaches were taken

### 4.3 Documentation Requirements

For each change, document:
- Why the test was flaky (root cause)
- What approach was taken to fix it
- Any tradeoffs made in the solution
- Links to relevant issues or documentation

## Phase 5: Validation and Verification

### 5.1 Ensure Fix Effectiveness
- Run the test multiple times locally to verify stability
- Check that the test still catches the regressions it's meant to catch
- Verify the test fails when the tested code is broken
- Ensure the fix doesn't mask real issues

### 5.2 Performance Considerations
- Ensure fixes don't significantly slow down the test suite
- Consider parallelization impacts
- Monitor resource usage of fixed tests

## Output Format

For each flaky test identified, provide:

```markdown
### Test: [Test Name/Path]

**Flakiness Type**: [Category from 1.2]

**Root Cause**: 
[Detailed explanation of why the test is flaky]

**Business Value Assessment**:
- Coverage: [What business logic this tests]
- Uniqueness: [Is this covered elsewhere?]
- Importance: [Critical/High/Medium/Low]

**Recommendation**: [FIX/REFACTOR/REMOVE/REPLACE]

**Reasoning**:
[Detailed justification for the recommendation]

**Implementation Plan**:
[Step-by-step approach to implement the recommendation]

**Code Changes**:
[Specific code modifications needed]
```

## Key Principles to Remember

1. **Business Logic First**: Tests should focus on business requirements, not implementation details
2. **Reliability Over Coverage**: A smaller suite of reliable tests is better than a large flaky suite
3. **Maintainability**: Consider long-term maintenance cost of complex test fixes
4. **Test at the Right Level**: Unit tests for logic, integration tests for interactions, E2E for critical user paths
5. **Document Decisions**: Future developers should understand why changes were made

## Examples of Good Decisions

- **Good Fix**: Converting a test that waits 5 seconds for an API call to use proper mocking
- **Good Refactor**: Splitting a large integration test into focused unit tests with one E2E happy path
- **Good Removal**: Removing a test that checks if a button has a specific CSS class when another test already verifies the button's functionality
- **Good Replacement**: Converting a flaky UI test to a more stable API test when the business logic is in the backend

Begin by scanning the codebase for test files and identifying patterns that suggest flakiness. Focus on delivering maximum value with minimum complexity.