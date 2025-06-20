# /refine - Codebase Quality Improvement Analysis

## Phase 1: Test Coverage Analysis
Analyze the codebase to identify untested business logic:

1. **Scan for Testing Gaps**
   - Identify all business logic functions/methods lacking tests
   - Flag critical paths (payment processing, data validation, authentication)
   - Note complex algorithms or calculations without test coverage
   - Skip UI rendering logic unless it contains business rules

2. **Prioritize by Risk**
   - HIGH: Core business logic, data transformations, financial calculations
   - MEDIUM: API endpoints, service integrations, validation logic
   - LOW: Simple getters/setters, UI formatting helpers

3. **Output Format**
   For each untested component provide:
   - File path and function/class name
   - Risk level (HIGH/MEDIUM/LOW)
   - Estimated test complexity (1-5)
   - Brief description of what tests would verify

## Phase 2: Refactoring Opportunities

1. **Code Duplication Analysis**
   - Identify repeated code blocks (>10 lines)
   - Find similar patterns that could be abstracted
   - Look for copy-paste violations across files
   - Pay special attention to files >300 lines

2. **Evaluate Each Opportunity**
   For each refactoring candidate, assess:
   - Lines of code reduction (estimate)
   - Risk level: LOW (cosmetic) / MEDIUM (logic change) / HIGH (architectural)
   - Test coverage: FULL / PARTIAL / NONE
   - Dependencies affected (count)
   - Implementation effort (hours estimate)

3. **Output Format**
   Group opportunities by type:
   - **Extract Method**: [locations, LoC saved, risk, coverage]
   - **Extract Class**: [locations, LoC saved, risk, coverage]
   - **Consolidate Duplicate Logic**: [locations, LoC saved, risk, coverage]
   - **Simplify Complex Conditions**: [locations, complexity reduction, risk]

## Phase 3: Actionable Recommendations

1. **Quick Wins** (Low risk, high value)
   - Can be done in <2 hours
   - Has existing test coverage
   - Reduces >20 lines of code

2. **Strategic Improvements** (Medium risk, high value)
   - Requires 2-8 hours
   - May need test updates
   - Improves maintainability significantly

3. **Technical Debt Items** (Higher risk, long-term value)
   - Major refactoring needed
   - Requires comprehensive testing first
   - Architecture-level improvements

## Analysis Approach
- Start with the most critical business logic files
- Use static analysis to find code smells
- Consider both immediate value and future maintenance burden
- Flag any security or performance concerns discovered
- Note patterns that could prevent future duplication

## Expected Deliverable
Provide a structured report with:
1. Executive summary of findings
2. Detailed test coverage gaps table
3. Refactoring opportunities ranked by ROI
4. Recommended implementation order
5. Specific next steps for top 3 items