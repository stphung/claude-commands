# Strategic Refactoring Advisor - Custom Command for Claude Code

# Input
Additional instructions: $ARGUMENTS

## Purpose
You are tasked with identifying, prioritizing, and executing refactoring opportunities to improve code maintainability, readability, and structure. Your goal is to make strategic decisions that reduce technical debt while minimizing risk and maximizing long-term value.

## Phase 1: Code Analysis and Smell Detection

### 1.1 Identify Code Smells
Scan the codebase for common issues:

**Bloaters**
- Long methods (>20-30 lines)
- Large classes (>200-300 lines)
- Long parameter lists (>3-4 parameters)
- Primitive obsession (overuse of primitives)
- Data clumps (repeated groups of parameters)

**Object-Orientation Abusers**
- Switch statements (type checking)
- Temporary fields
- Refused bequest (unused inheritance)
- Alternative classes with different interfaces

**Change Preventers**
- Divergent change (class changes for many reasons)
- Shotgun surgery (change requires many small edits)
- Parallel inheritance hierarchies

**Dispensables**
- Lazy classes (classes that don't do enough)
- Duplicate code
- Dead code
- Speculative generality (unused flexibility)
- Comments explaining bad code

**Couplers**
- Feature envy (method uses another class excessively)
- Inappropriate intimacy (classes know too much about each other)
- Message chains (long chains of method calls)
- Middle man (class only delegates)

### 1.2 Complexity Metrics
Measure and identify:
- **Cyclomatic Complexity**: >10 needs attention, >20 is critical
- **Cognitive Complexity**: Mental effort to understand
- **Depth of Inheritance**: >4 levels is concerning
- **Class Coupling**: >8-10 dependencies is high
- **Method Length**: >30 lines needs review
- **File Length**: >300 lines consider splitting

### 1.3 Maintainability Indicators
Look for signs of poor maintainability:
- Frequent bug fixes in the same area
- Developers avoiding certain code
- Long onboarding time for new team members
- Difficulty adding new features
- Test complexity or absence
- Inconsistent patterns within modules

## Phase 2: Impact and Risk Assessment

### 2.1 Change Frequency Analysis
Identify hot spots by analyzing:
- Git history for frequently modified files
- Files with high churn rate
- Code modified by multiple developers
- Areas with frequent merge conflicts
- Bug fix concentration

### 2.2 Business Impact Evaluation
For each refactoring candidate, assess:
- **Feature Velocity Impact**: Will this speed up future development?
- **Bug Risk**: Does this area produce frequent bugs?
- **Team Productivity**: How many developers work here?
- **Customer Impact**: User-facing vs internal code
- **Performance**: Current bottlenecks or inefficiencies
- **Compliance**: Regulatory or security requirements

### 2.3 Refactoring Risk Matrix

**LOW RISK - High Confidence**
- Well-tested code
- Isolated modules
- Clear boundaries
- Non-critical path
- Single responsibility

**MEDIUM RISK - Moderate Confidence**
- Some test coverage
- Moderate coupling
- Active development area
- Multiple consumers
- Business logic

**HIGH RISK - Low Confidence**
- No/poor tests
- High coupling
- Critical path
- Complex logic
- External dependencies

## Phase 3: Refactoring Strategy

### 3.1 Refactoring Priority Framework

**URGENT - Refactor Immediately**
- Blocking new features
- Causing production issues
- Security vulnerabilities
- Extreme complexity in critical path
- Preventing team productivity

**HIGH - Next Sprint**
- High-change frequency areas
- Significant tech debt
- Performance bottlenecks
- Missing abstractions
- Inconsistent patterns

**MEDIUM - This Quarter**
- Moderate complexity
- Some duplication
- Minor performance issues
- Style inconsistencies
- Documentation needs

**LOW - As Time Permits**
- Cosmetic issues
- Nice-to-have improvements
- Stable, working code
- Low-traffic areas
- Personal preferences

### 3.2 Refactoring Patterns Catalog

**Method-Level Refactorings**
- Extract Method (for long methods)
- Inline Method (for unnecessary indirection)
- Extract Variable (for complex expressions)
- Replace Temp with Query
- Remove Assignments to Parameters
- Substitute Algorithm

**Class-Level Refactorings**
- Extract Class (for large classes)
- Inline Class (for lazy classes)
- Move Method/Field
- Extract Interface
- Pull Up/Push Down Method
- Replace Inheritance with Delegation

**Data-Level Refactorings**
- Replace Magic Numbers with Constants
- Encapsulate Field
- Replace Array with Object
- Replace Data Value with Object
- Change Value to Reference

**Conditional Logic Refactorings**
- Decompose Conditional
- Consolidate Conditional Expression
- Replace Conditional with Polymorphism
- Introduce Null Object
- Replace Nested Conditional with Guard Clauses

**API Refactorings**
- Rename Method/Variable
- Add/Remove Parameter
- Separate Query from Modifier
- Parameterize Method
- Replace Parameter with Method Call

### 3.3 Safety Practices

**Pre-Refactoring Checklist**
- [ ] Comprehensive tests exist or are added
- [ ] Current behavior is documented
- [ ] Performance baseline is measured
- [ ] Backup/rollback plan exists
- [ ] Team is informed of changes

**During Refactoring**
- Make one change at a time
- Run tests after each change
- Commit frequently with clear messages
- Keep refactoring separate from features
- Maintain backwards compatibility when needed

## Phase 4: Implementation Approach

### 4.1 Incremental Refactoring Strategy

**Step 1: Establish Safety Net**
```javascript
// Add characterization tests if missing
describe('Current behavior', () => {
  it('preserves existing functionality', () => {
    // Capture current behavior
  });
});
```

**Step 2: Small, Safe Changes**
- Start with automated refactorings (IDE support)
- Rename for clarity
- Extract obvious methods
- Remove dead code
- Fix linting issues

**Step 3: Structural Improvements**
- Extract classes/modules
- Introduce abstractions
- Reduce coupling
- Improve cohesion
- Establish clear boundaries

**Step 4: Pattern Implementation**
- Apply design patterns where appropriate
- Standardize approaches
- Create reusable components
- Document decisions

### 4.2 Code Organization Principles

**Single Responsibility**
- Each class/module has one reason to change
- Methods do one thing well
- Clear, focused interfaces

**Dependency Management**
- Depend on abstractions, not concretions
- Inject dependencies
- Minimize coupling
- Clear dependency graph

**Consistency**
- Naming conventions
- File organization
- Error handling patterns
- Testing approaches

## Phase 5: Validation and Metrics

### 5.1 Success Metrics
Track improvements in:
- **Code Complexity**: Cyclomatic/Cognitive scores
- **Test Coverage**: Especially for refactored code
- **Build Time**: Compilation and test execution
- **Code Duplication**: DRY principle adherence
- **Developer Velocity**: Feature delivery speed
- **Bug Frequency**: Defect density in refactored areas
- **Code Review Time**: Ease of understanding

### 5.2 Quality Gates
Ensure refactoring maintains/improves:
- All tests still pass
- Performance benchmarks met
- No new linting errors
- Documentation updated
- API contracts preserved
- Security scan results

## Output Format

For each refactoring opportunity:

```markdown
### Target: [File/Module/Class Name]

**Identified Issues**:
- Code Smell: [Specific smell type]
- Complexity: [Metrics that exceed thresholds]
- Maintainability Impact: [How this affects development]

**Priority**: [URGENT/HIGH/MEDIUM/LOW]

**Risk Assessment**:
- Risk Level: [LOW/MEDIUM/HIGH]
- Test Coverage: [Current coverage %]
- Dependencies: [Number of consumers]
- Change Frequency: [Commits in last 6 months]

**Refactoring Plan**:
1. [First refactoring step]
2. [Second refactoring step]
3. [Additional steps as needed]

**Specific Techniques**:
- Pattern: [Extract Method/Class/etc.]
- Approach: [Incremental/Big Bang]
- Safety: [How to ensure no regressions]

**Example Transformation**:
```[language]
// Before
[Current problematic code]

// After
[Refactored clean code]
```

**Expected Benefits**:
- Complexity reduction: [From X to Y]
- Improved testability: [How tests become easier]
- Future changes: [How this helps new features]

**Migration Notes**:
[Any special considerations for existing code/APIs]
```

## Key Principles

1. **Boy Scout Rule**: Leave code better than you found it
2. **Incremental Progress**: Small improvements compound over time
3. **Test-Driven Refactoring**: Never refactor without tests
4. **Behavior Preservation**: Refactoring doesn't change functionality
5. **Team Alignment**: Refactoring decisions affect everyone
6. **Economic Thinking**: Balance cost of refactoring vs future savings

## Anti-Patterns to Avoid

❌ **Big Bang Refactoring**
- Attempting massive rewrites
- Months-long refactoring projects
- Breaking working systems

❌ **Premature Optimization**
- Refactoring without clear need
- Over-engineering solutions
- Adding unnecessary abstractions

❌ **Refactoring During Feature Work**
- Mixing refactoring with new functionality
- Unclear commits and reviews
- Difficult rollbacks

❌ **Ignoring Team Context**
- Not communicating changes
- Changing style unilaterally
- Ignoring team conventions

## Decision Framework

Ask these questions before refactoring:

1. **Is it broken?** If not, does it need fixing?
2. **Will we touch this code soon?** If not, maybe wait
3. **Do we understand it fully?** Don't refactor what you don't understand
4. **Can we test it?** No refactoring without tests
5. **What's the ROI?** Time spent vs time saved
6. **Who else is affected?** Coordinate with team

## Common Refactoring Scenarios

**Scenario 1: Long Method**
- Extract cohesive blocks into well-named methods
- Replace comments with method names
- Reduce cyclomatic complexity

**Scenario 2: Duplicate Code**
- Extract common functionality
- Create shared utilities
- Use template methods or strategies

**Scenario 3: Large Class**
- Identify distinct responsibilities
- Extract collaborator classes
- Maintain clear interfaces

**Scenario 4: Complex Conditionals**
- Extract condition checks to methods
- Use polymorphism for type checks
- Implement guard clauses

Begin by analyzing the codebase for high-impact refactoring opportunities. Focus on code that will provide the most value when improved, considering both technical debt reduction and future development velocity.