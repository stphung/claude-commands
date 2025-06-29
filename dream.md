# Feature design and exploration

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

### Phase 3: Mockup Explorations 🎨

For each implementation approach, provide 2-3 distinct mockup variations:

#### Approach [Name] - Visual Concepts

**Mockup A: [Descriptive Name]**
- Layout description
- Key UI elements and placement
- Interaction patterns
- Visual style notes
- User flow highlights
- Accessibility considerations

**Mockup B: [Descriptive Name]**
- Alternative layout approach
- Different interaction model
- Visual differentiation
- Trade-offs vs Mockup A

**Mockup C: [Descriptive Name]**
- Experimental/innovative take
- Unique UI patterns
- Future-forward design elements

Include for each mockup:
- Screen layout descriptions
- Component hierarchy
- Navigation patterns
- Mobile/responsive considerations
- Key interaction states (hover, active, error)
- Animation/transition suggestions

### Phase 4: Detailed Analysis

For each approach, provide:

#### Approach Name & Description
Brief overview of the implementation strategy

#### Selected Mockup Rationale
- Why this visual approach best supports the implementation
- User experience advantages
- Technical feasibility

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

### Phase 5: Comparison Matrix

| Approach | Time to Market | Technical Complexity | User Value | Scalability | Maintenance | Visual Impact | Total Score |
|----------|---------------|-------------------|------------|-------------|-------------|---------------|-------------|
| [Approach 1] | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ | XX/30 |
| [Approach 2] | ... | ... | ... | ... | ... | ... | XX/30 |

### Phase 6: Recommendations

1. **Recommended Approach & Mockup**: [Name] with [Mockup Variant]
   - Why this combination wins
   - Key success factors
   - Watch-outs

2. **Alternative if constraints change**:
   - If time is critical: [Approach] with [Mockup]
   - If scale is critical: [Approach] with [Mockup]
   - If cost is critical: [Approach] with [Mockup]

3. **Hybrid possibilities**:
   - Can we combine approaches?
   - Mix-and-match mockup elements
   - Phased rollout options

### Phase 7: Next Steps
1. Prototype recommendations
2. User testing priorities for mockups
3. Validation experiments needed
4. Key decisions required
5. Information gaps to fill

---

## Example Output Format:

**Feature**: $ARGUMENTS

### 🎯 Approach 1: [Name]
*Brief description of approach*

#### 🎨 Mockup Variations

**Mockup 1A: Clean Minimal**
- Single-column layout with card-based components
- Primary action button floating at bottom
- Subtle shadows and 8px border radius
- Sans-serif typography, high contrast
- Swipe gestures for quick actions
- Tab navigation for sections

**Mockup 1B: Information Dense**
- Two-column layout on desktop, stacked on mobile
- Inline actions within each row
- Compact spacing, smaller typography
- Sidebar navigation with nested items
- Hover states reveal additional options

**Mockup 1C: Conversational UI**
- Chat-like interface with message bubbles
- Progressive disclosure of options
- Voice input capability
- Animated transitions between states
- Mobile-first design approach

**Selected: Mockup 1A** - Best balance of simplicity and functionality for MVP

**How it works:**
- Technical implementation summary
- Key components and flow

**Pros ✅**
- Fastest time to market (2 weeks)
- Clean, intuitive interface
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
[Comparison table including visual impact scores]

### 💡 Recommendation
Start with Approach 2 + Mockup 2B because...

---

This brainstorming provides multiple perspectives on both implementation and visual design to make informed product and technical decisions.