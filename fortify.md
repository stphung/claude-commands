# Test Coverage and Quality Analyzer

# Input
$ARGUMENTS

## Purpose
You are tasked with comprehensively analyzing and improving the test suite of a codebase. Your goal is to identify gaps in coverage, improve test quality, fix flaky tests, optimize performance, and ensure the test suite effectively validates business logic while remaining maintainable.

Use multiple subagents to work in parallel
Leverage CI/CD history, coverage reports, and codebase analysis for data-driven decisions

## Phase 1: Comprehensive Test Suite Analysis

### 1.1 Coverage Assessment
Analyze the current state of test coverage:
- **Quantitative Coverage**: Line, branch, function, and statement coverage percentages
- **Qualitative Coverage**: Critical business logic paths covered vs uncovered
- **Coverage Gaps**: Identify untested files, functions, and code paths
- **Coverage Distribution**: Balance between unit, integration, and E2E tests
- **Edge Cases**: Identify missing boundary conditions and error scenarios

### 1.2 Test Quality Evaluation
Assess the quality of existing tests:
- **Test Focus**: Are tests validating behavior or implementation details?
- **Assertion Quality**: Are assertions meaningful and comprehensive?
- **Test Clarity**: Are test names descriptive and intentions clear?
- **Test Independence**: Can tests run in isolation?
- **Mock Usage**: Are mocks used appropriately without over-mocking?

### 1.3 Flaky Test Identification
Locate and categorize unreliable tests:
- Tests with inconsistent pass/fail rates in CI/CD
- Timing-dependent tests (setTimeout, race conditions)
- Tests with external dependencies lacking proper isolation
- Order-dependent tests or those with shared state
- Environment-specific failures

### 1.4 Performance Analysis
Evaluate test suite efficiency:
- **Execution Time**: Identify slowest tests and bottlenecks
- **Resource Usage**: Memory leaks, unclosed connections
- **Parallelization**: Tests that can't run in parallel
- **Setup/Teardown Overhead**: Expensive repeated operations

### 1.5 Test Organization Review
Examine test structure and maintainability:
- **File Organization**: Logical grouping and naming conventions
- **Code Duplication**: Repeated setup, assertions, or test logic
- **Helper Utilization**: Proper use of test utilities and shared code
- **Documentation**: Test purpose and special requirements documented

## Phase 2: Strategic Analysis

### 2.1 Business Logic Coverage Mapping
Create a comprehensive map of business requirements to tests:
- Identify critical user journeys and their test coverage
- Map business rules to specific test cases
- Find gaps where important business logic lacks tests
- Prioritize based on business impact and risk

### 2.2 Test Pyramid Evaluation
Assess the distribution of test types:
```
     /\      E2E Tests (Critical User Journeys)
    /  \     
   /    \    Integration Tests (Component Interactions)
  /      \   
 /        \  Unit Tests (Business Logic, Algorithms)
/----------\
```
- Is the pyramid appropriately shaped for the application?
- Are tests at the appropriate level of abstraction?
- Is there redundant coverage across levels?

### 2.3 Risk-Based Priority Assessment
Prioritize improvements based on:
- **Business Criticality**: Impact on core functionality
- **Change Frequency**: How often the code changes
- **Defect History**: Areas with frequent bugs
- **Complexity**: Complex logic needing thorough testing

## Phase 3: Improvement Strategy

### 3.1 Coverage Gap Remediation
For each identified gap, determine:
- **Priority**: Critical/High/Medium/Low based on risk assessment
- **Test Type**: Unit, integration, or E2E test needed
- **Implementation Approach**: TDD for new tests, specific scenarios to cover
- **Success Criteria**: What constitutes adequate coverage

### 3.2 Test Quality Improvements
For existing tests needing improvement:

**ENHANCE** - When tests:
- Cover important functionality but lack comprehensive assertions
- Need better error scenarios or edge case coverage
- Would benefit from clearer naming or documentation
- Could validate more business rules with minimal changes

**REFACTOR** - When tests:
- Have value but poor implementation
- Contain significant duplication
- Test at the wrong level of abstraction
- Need better organization or structure

**OPTIMIZE** - When tests:
- Take excessive time to run
- Use resources inefficiently
- Can be parallelized but aren't
- Have expensive setup that could be shared

**FIX** (for flaky tests) - When tests:
- Cover unique, critical functionality
- Can be made reliable with reasonable effort
- Have no stable alternative coverage

**REMOVE** - When tests:
- Are redundant with better tests
- Test implementation details that change frequently
- Have low value relative to maintenance cost
- Cannot be made valuable with reasonable effort

### 3.3 New Test Implementation Guidelines

**For Unit Tests:**
- Focus on business logic and algorithms
- Test edge cases and error conditions
- Keep tests fast and isolated
- Use descriptive test names following: `should_[expectedBehavior]_when_[condition]`

**For Integration Tests:**
- Test component interactions
- Verify data flow between systems
- Use test containers or in-memory databases when needed
- Focus on contract testing between services

**For E2E Tests:**
- Cover critical user journeys only
- Focus on happy paths and key error scenarios
- Implement retry mechanisms for UI interactions
- Use page object patterns for maintainability

## Phase 4: Implementation Plan

### 4.1 Test Writing Patterns

**Arrange-Act-Assert (AAA) Pattern:**
```javascript
test('should calculate discount when customer is premium', () => {
  // Arrange
  const customer = { type: 'premium', purchases: 1000 };
  
  // Act
  const discount = calculateDiscount(customer);
  
  // Assert
  expect(discount).toBe(100);
});
```

**Data-Driven Tests:**
```javascript
test.each([
  [input1, expected1],
  [input2, expected2],
  [input3, expected3],
])('should handle %s correctly', (input, expected) => {
  expect(processData(input)).toBe(expected);
});
```

### 4.2 Coverage Improvement Techniques

1. **Branch Coverage**: Ensure all conditional paths are tested
2. **Exception Testing**: Verify error handling and edge cases
3. **Boundary Testing**: Test limits and boundaries of inputs
4. **State Testing**: Verify behavior across different states
5. **Interaction Testing**: Ensure proper component communication

### 4.3 Performance Optimization Strategies

1. **Parallelize Independent Tests**: Configure test runner for parallel execution
2. **Share Expensive Setup**: Use beforeAll for costly operations
3. **Mock External Services**: Replace slow external calls with fast mocks
4. **Optimize Database Operations**: Use transactions and cleanup strategies
5. **Profile Test Execution**: Identify and optimize bottlenecks

## Phase 5: Quality Assurance and Monitoring

### 5.1 Validation Checklist
Before considering improvements complete:
- [ ] All new tests pass consistently (run 10+ times)
- [ ] Coverage metrics improved for critical paths
- [ ] Test execution time acceptable
- [ ] Tests fail appropriately when code is broken
- [ ] Documentation updated for complex scenarios

### 5.2 Continuous Monitoring
Establish ongoing quality metrics:
- Track coverage trends over time
- Monitor test execution times
- Flag new flaky tests quickly
- Review test-to-code ratio
- Measure mean time to test failure detection

## Output Format

Provide a comprehensive analysis with:

```markdown
# Test Suite Analysis Report

## Executive Summary
- Current Coverage: X%
- Critical Gaps: [List key uncovered business logic]
- Flaky Tests: X found
- Performance Issues: [List major bottlenecks]
- Recommended Priority Actions: [Top 5 improvements]

## Detailed Findings

### Coverage Analysis
#### Uncovered Critical Paths
1. [Path/Feature]: [Why it's critical] - Priority: [High/Medium/Low]

#### Test Distribution
- Unit Tests: X% of suite
- Integration Tests: Y% of suite  
- E2E Tests: Z% of suite
- Recommendation: [Adjust pyramid shape if needed]

### Quality Issues

#### Flaky Tests
[For each flaky test, provide the analysis format from the original document]

#### Poor Quality Tests
[Test Name]: 
- Issue: [What makes it low quality]
- Impact: [Why it matters]
- Recommendation: [ENHANCE/REFACTOR/REMOVE]

#### Performance Bottlenecks
[Test/Suite Name]:
- Current Time: Xs
- Issue: [Why it's slow]
- Optimization: [Proposed solution]

### Missing Test Scenarios
[Feature/Component]:
- Missing: [What scenarios aren't covered]
- Risk: [What could go wrong]
- Implementation: [Proposed test approach]

## Implementation Roadmap

### Phase 1: Critical Fixes (Week 1-2)
[List immediate actions for critical gaps and flaky tests]

### Phase 2: Coverage Expansion (Week 3-4)
[List new tests for important uncovered paths]

### Phase 3: Quality Improvements (Week 5-6)
[List refactoring and optimization tasks]

### Success Metrics
- Coverage target: X% → Y%
- Flaky test reduction: X → 0
- Test execution time: X min → Y min
- Business logic coverage: X% → 100%
```

## Key Principles

1. **Business Value First**: Prioritize tests that validate business requirements
2. **Right Level Testing**: Test at the lowest level that provides confidence
3. **Maintainable Over Complete**: Better to have fewer, high-quality tests
4. **Fast Feedback**: Optimize for quick test execution without sacrificing value
5. **Living Documentation**: Tests should clearly document system behavior
6. **Continuous Improvement**: Test quality is an ongoing process

## Tools and Integrations

Leverage available tools:
- **Coverage Tools**: Jest coverage, nyc, Istanbul
- **Flaky Test Detection**: Test retry reports, CI failure patterns
- **Performance Profiling**: Test execution time reports
- **Static Analysis**: ESLint rules for test quality
- **Mutation Testing**: Verify test effectiveness

Begin by performing a comprehensive scan of the test suite, analyzing coverage reports, and identifying patterns across all test quality dimensions.