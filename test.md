# Smart Code Coverage Analyzer - Custom Command for Claude Code

# Input
Additional instructions: $ARGUMENTS

## Purpose
You are tasked with intelligently improving code coverage by identifying gaps, prioritizing business logic, and adding high-value tests. Your goal is to increase meaningful coverage while avoiding redundant tests, implementation detail tests, and test bloat.

## Phase 1: Coverage Analysis and Discovery

### 1.1 Identify Coverage Gaps
Analyze the codebase to find:
- Uncovered files and modules
- Functions/methods with zero coverage
- Untested branches and conditional logic
- Error handling and edge cases without tests
- Critical business logic paths lacking coverage
- Public APIs and interfaces without tests

### 1.2 Generate Coverage Report
If available, use coverage tools to:
- Run existing test suite with coverage enabled
- Identify specific line-by-line gaps
- Note branch coverage vs line coverage
- Find files with < 80% coverage (or project threshold)
- Look for patterns in what's not tested

### 1.3 Categorize Uncovered Code
Classify uncovered code into:
- **Core Business Logic**: Domain rules, calculations, validations
- **Integration Points**: API calls, database operations, external services
- **User Interactions**: UI handlers, form processing, user flows
- **Error Handling**: Exception cases, validation failures, edge conditions
- **Utilities**: Helper functions, data transformations, formatters
- **Configuration/Setup**: Initialization, config parsing, bootstrapping
- **Generated/Vendor Code**: Should typically be excluded

## Phase 2: Strategic Prioritization

### 2.1 Business Value Assessment
For each coverage gap, evaluate:
- **Revenue Impact**: Does this code directly affect money/transactions?
- **User Impact**: How many users would be affected by bugs here?
- **Risk Level**: What's the consequence of failures?
- **Change Frequency**: How often is this code modified?
- **Complexity**: How error-prone is this code?
- **Regulatory/Compliance**: Are there legal requirements?

### 2.2 Coverage Priority Matrix
Prioritize based on:

**CRITICAL** - Test immediately:
- Core business logic with high complexity
- Payment/financial calculations
- Security-related functions
- Data integrity operations
- User authentication/authorization

**HIGH** - Test soon:
- Primary user workflows
- API endpoints and contracts
- Data validation logic
- Integration boundaries
- Error recovery paths

**MEDIUM** - Test when possible:
- Secondary features
- UI interaction logic
- Data formatting/display
- Non-critical utilities

**LOW** - Consider skipping:
- Simple getters/setters
- Pure configuration code
- Logging/debugging code
- Code scheduled for removal
- Trivial wrappers

### 2.3 Test Level Decision Framework
Determine the appropriate test level:

**Unit Tests** for:
- Pure functions and algorithms
- Business rule validation
- Data transformations
- Isolated component behavior
- Complex conditional logic

**Integration Tests** for:
- API endpoint behavior
- Database operations
- Service interactions
- Cross-component workflows
- External service communication

**E2E Tests** for:
- Critical user journeys
- Multi-step workflows
- Full-stack scenarios
- Smoke tests for deployments

## Phase 3: Test Design Strategy

### 3.1 Test Quality Principles
Each test should:
- **Focus on behavior**, not implementation
- **Test one concept** per test
- **Be deterministic** and repeatable
- **Run quickly** (milliseconds for unit tests)
- **Have clear names** that describe the scenario
- **Avoid testing framework code** or language features

### 3.2 What NOT to Test
Avoid adding tests for:
- Third-party library internals
- Simple property assignments
- Framework-provided functionality
- Code that will be refactored soon
- Implementation details that don't affect behavior
- Generated code (unless customized)

### 3.3 Edge Case Identification
For each function/module, consider:
- Null/undefined inputs
- Empty collections or strings
- Boundary values (0, -1, MAX_INT)
- Invalid input types
- Concurrent access scenarios
- Resource exhaustion cases
- Network/service failures

## Phase 4: Implementation Guidelines

### 4.1 Test Structure Template
```javascript
describe('[Module/Feature Name]', () => {
  describe('[Function/Behavior]', () => {
    it('should [expected behavior] when [condition]', () => {
      // Arrange: Set up test data and dependencies
      // Act: Execute the code being tested
      // Assert: Verify the expected outcome
    });

    it('should [handle edge case] when [edge condition]', () => {
      // Edge case test
    });
  });
});
```

### 4.2 Test Data Strategies
- **Test Builders**: For complex objects
- **Fixtures**: For reusable test data
- **Factories**: For generating test variations
- **Minimal Data**: Use only what's needed for the test
- **Realistic Data**: Reflect production scenarios

### 4.3 Mocking and Isolation
Guidelines for dependencies:
- Mock external services and APIs
- Use test doubles for databases
- Isolate time-dependent code
- Mock only at boundaries
- Prefer real objects when possible
- Keep mocks simple and focused

## Phase 5: Coverage Improvement Plan

### 5.1 Batch Organization
Group tests by:
1. **Risk Mitigation**: Start with highest-risk gaps
2. **Feature Areas**: Keep related tests together
3. **Developer Assignment**: Based on code ownership
4. **Complexity**: Simple tests first for quick wins
5. **Dependencies**: Test foundations before features

### 5.2 Incremental Approach
- Set realistic coverage targets (not 100%)
- Focus on trending upward, not absolute numbers
- Measure coverage delta, not just total
- Track meaningful coverage (business logic)
- Exclude non-testable code from metrics

## Output Format

For each identified coverage gap:

```markdown
### Module: [Module/File Path]

**Current Coverage**: [X%] line coverage, [Y%] branch coverage

**Priority**: [CRITICAL/HIGH/MEDIUM/LOW]

**Business Value**:
- Function: [What this code does]
- Impact: [Who/what is affected by bugs]
- Risk: [Consequences of failure]

**Test Strategy**:
- Level: [Unit/Integration/E2E]
- Approach: [How to test effectively]
- Key Scenarios: [List of test cases needed]

**Implementation Plan**:
1. [Specific test to add]
2. [Edge cases to cover]
3. [Dependencies to mock]

**Example Test Case**:
```[language]
[Sample test code demonstrating the approach]
```

**Estimated Effort**: [Time estimate]
```

## Key Principles

1. **Quality Over Quantity**: 80% coverage of critical code > 100% coverage with poor tests
2. **Business Focus**: Prioritize tests that prevent real user issues
3. **Maintainability**: Tests should be easy to understand and update
4. **Performance**: Fast tests encourage frequent running
5. **Independence**: Each test should run in isolation
6. **Documentation**: Tests serve as living documentation

## Anti-Patterns to Avoid

❌ **Testing Implementation Details**
```javascript
// Bad: Tests private method names and internal structure
expect(object._privateMethod).toHaveBeenCalled();
expect(object.internalState).toBe('specific');
```

❌ **Redundant Tests**
```javascript
// Bad: Multiple tests for the same behavior
it('returns 5 when adding 2 and 3');
it('gives 5 as the sum of 2 and 3');
it('calculates 2 + 3 as 5');
```

❌ **Brittle Tests**
```javascript
// Bad: Depends on exact string formatting
expect(output).toBe('User: John, Age: 30, Status: Active');
// Good: Tests the important parts
expect(output).toContain('John');
expect(output).toContain('30');
```

❌ **Test Coupling**
```javascript
// Bad: Tests depend on execution order
it('test 1', () => { globalState.value = 5; });
it('test 2', () => { expect(globalState.value).toBe(5); });
```

## Success Metrics

Track improvement through:
- Coverage percentage increase in critical modules
- Reduction in production bugs
- Confidence in refactoring
- Deployment frequency
- Time to identify regressions
- Developer satisfaction with test suite

Begin by analyzing the current coverage report or scanning for untested files. Focus on delivering maximum risk reduction with minimum test overhead.