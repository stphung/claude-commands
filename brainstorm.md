# /brainstorm - Feature Implementation Exploration

## Input
Feature to build: $ARGUMENTS

## Analysis Process

### Phase 1: Understanding the Feature
1. Parse the feature requirements
2. Identify core user needs
3. Determine success criteria
4. List key constraints

### Phase 2: Implementation Approaches

Generate 3-5 different approaches, considering:
- **Minimal approach** - Bare essentials
- **Standard approach** - Industry common patterns  
- **Innovative approach** - Creative/cutting-edge solution
- **Modular approach** - Highly extensible design
- **Quick-win approach** - Fastest to market

### Phase 3: Detailed Analysis

For each approach, provide:

#### Approach Name & Description
Brief overview of the implementation strategy

#### Technical Architecture
- Core technologies/patterns used
- Data flow and storage approach
- Integration points
- Scale considerations

#### Implementation Details
- Estimated effort (dev-weeks)
- Technical complexity (1-10)
- Team expertise required
- Major milestones

#### Pros ✅
- User experience benefits
- Technical advantages
- Business value
- Development efficiency
- Maintenance benefits
- Scalability advantages
- Cost effectiveness
- Time to market

#### Cons ❌
- Technical limitations
- User experience drawbacks
- Implementation challenges
- Maintenance burden
- Scalability concerns
- Hidden complexities
- Technical debt introduced
- Opportunity costs

#### Risks & Mitigations 🚨
- Key risks identified
- Mitigation strategies
- Fallback options

### Phase 4: Comparison Matrix

| Approach | Time to Market | Technical Complexity | User Value | Scalability | Maintenance | Total Score |
|----------|---------------|-------------------|------------|-------------|-------------|-------------|
| [Approach 1] | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ | XX/25 |
| [Approach 2] | ... | ... | ... | ... | ... | XX/25 |

### Phase 5: Recommendations

1. **Recommended Approach**: [Name] 
   - Why this approach wins
   - Key success factors
   - Watch-outs

2. **Alternative if constraints change**:
   - If time is critical: [Approach]
   - If scale is critical: [Approach]
   - If cost is critical: [Approach]

3. **Hybrid possibilities**:
   - Can we combine approaches?
   - Phased rollout options

### Phase 6: Next Steps
1. Prototype recommendations
2. Validation experiments needed
3. Key decisions required
4. Information gaps to fill

---

## Example Output Format:

**Feature**: $ARGUMENTS

### 🎯 Approach 1: [Name]
*Brief description of approach*

**How it works:**
- Technical implementation summary
- Key components and flow

**Pros ✅**
- Fastest time to market (2 weeks)
- Leverages existing infrastructure
- Minimal new dependencies
- Easy to A/B test
- Low risk rollback

**Cons ❌**
- Limited flexibility for future features
- May hit performance limits at 10k users
- Requires manual processes initially
- Some code duplication

**Risk Assessment 🚨**
- Main risk: Performance at scale
- Mitigation: Add caching layer in Phase 2

**Complexity**: ⭐⭐⭐ (3/10)
**Effort**: 2-3 dev weeks
**Best for**: Quick validation, MVP

[Continue for other approaches...]

### 📊 Decision Matrix
[Comparison table]

### 💡 Recommendation
Start with Approach 2 because...

---

This brainstorming provides multiple perspectives to make informed product and technical decisions.