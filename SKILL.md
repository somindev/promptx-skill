---
name: promptx
description: Intelligently match user inquiries to the most appropriate prompt framework from 57 curated frameworks. Use when users ask about prompt engineering, framework selection, structured prompting, or need guidance on AI interaction patterns.
---

# PromptX: Intelligent Prompt Framework Matching

## Overview

PromptX is an intelligent framework matching system that analyzes user requirements and recommends the most suitable prompt engineering framework from a curated collection of 57 frameworks. Using multi-dimensional scoring across domain, task type, keywords, and complexity, PromptX identifies optimal matches and guides users through applying the selected framework.

**Framework Coverage:** 57 frameworks across 6 categories:
- **Prompt Engineering** (25 frameworks): BAB, CRISPE, RODES, SPARK, TAG, etc.
- **Decision Making** (8 frameworks): Pros and Cons, RICE, Six Thinking Hats, etc.
- **Problem Solving** (12 frameworks): Chain of Thought, Tree of Thought, SCAMPER, etc.
- **Content Creation** (10 frameworks): RELIC, BLOG, Hamburger Model, etc.
- **Creative & Brainstorming** (15 frameworks): How Might We, Imagine, What If, etc.
- **Technical Analysis** (12 frameworks): PEE, CIDI, GRADE, TRACE, etc.

## When to Use PromptX

### Trigger Phrases
- "Help me optimize a prompt for..."
- "What framework should I use for..."
- "How should I structure my prompt for..."
- "Need a framework for..."
- "Best approach for..."
- "Create a prompt for..."
- "Improve my prompt about..."

### Ideal Scenarios
✅ User needs structured prompting strategies
✅ Complex task requiring systematic approach
✅ Analytical work needing clear methodology
✅ Decision-making requiring framework
✅ Content creation needing structure
✅ Problem-solving requiring technique

### When NOT to Use
❌ Simple factual queries ("What is X?")
❌ Direct code generation ("Write a function that...")
❌ Single-step requests ("Summarize this text")
❌ Routine conversations ("How are you?")

## Workflow

```mermaid
graph TB
    Start([User Request]) --> Analyze[Extract: Domain, Task, Complexity, Keywords]
    Analyze --> Score[Score all 57 frameworks]
    Score --> Rank{Top score > 80?}
    Rank -->|Yes| Single[Present 1 framework]
    Rank -->|No, scores 60-80| Multiple[Present top 3 with comparison]
    Rank -->|No, score < 60| Clarify[Ask clarification questions]
    Clarify --> Score
    Single --> Apply[Guide application]
    Multiple --> Select[User chooses]
    Select --> Apply
    Apply --> End([Complete])
```

## Framework Categories

### 1. Prompt Engineering Frameworks
**Purpose:** Structure and optimize AI interactions
**Examples:** BAB (Background, Ask, Benefit), CRISPE (Capacity, Role, Identity, etc.), TAG (Topic, Action, Goal)
**Best for:** Improving AI response quality, structuring complex queries

### 2. Decision Making Frameworks
**Purpose:** Systematic evaluation and choice
**Examples:** Pros and Cons, RICE (Reach, Impact, Confidence, Effort), Six Thinking Hats
**Best for:** Business decisions, feature prioritization, strategic choices

### 3. Problem Solving Frameworks
**Purpose:** Break down and resolve complex issues
**Examples:** Chain of Thought, Tree of Thought, SCAMPER (Substitute, Combine, etc.)
**Best for:** Analytical tasks, troubleshooting, systematic analysis

### 4. Content Creation Frameworks
**Purpose:** Structure written content
**Examples:** RELIC (Role, Event, Location, etc.), Hamburger Model, BLOG
**Best for:** Articles, reports, stories, marketing copy

### 5. Creative & Brainstorming Frameworks
**Purpose:** Generate innovative ideas
**Examples:** How Might We (HMW), Imagine, What If, Brainstorming
**Best for:** Ideation, innovation, creative thinking

### 6. Technical Analysis Frameworks
**Purpose:** Deep analytical examination
**Examples:** PEE (Point, Evidence, Explanation), CIDI, GRADE
**Best for:** Research, analysis, evaluation, assessment

## Scoring Algorithm

**Score Formula:**
```
Score = (Domain_Match × 0.30) + (Task_Match × 0.25) + (Keyword_Match × 0.20) + (Complexity_Match × 0.15) + (Examples_Bonus × 0.10)
```

**Component Breakdown:**

1. **Domain Match (30%)**: Jaccard similarity between user domains and framework domains
   - Calculates intersection over union of domain sets
   - Domains: education, business, creative, technical, decision, problem
   - Score: 0-100

2. **Task Match (25%)**: Exact task type matches
   - 50 points per matching task type
   - Task types: prompt_engineering, decision_making, problem_solving, content_creation, analysis, brainstorming
   - Score: 0-100

3. **Keyword Match (20%)**: Overlap between user keywords and framework keywords
   - 20 points per matching keyword, capped at 100
   - Keywords extracted from user query and framework metadata
   - Score: 0-100

4. **Complexity Match (15%)**: Alignment of complexity levels
   - 100 points if exact match
   - 50 points if adjacent (simple ↔ medium ↔ complex)
   - 0 points if far apart
   - Complexity determined by query length, specific terms, and question type

5. **Examples Bonus (10%)**: Framework has examples
   - 10 points if framework has 1+ examples
   - 0 points if no examples
   - Encourages frameworks with practical applications

**Tie-Breaking:**
1. Higher examples count
2. Higher flexibility (high > medium > low)
3. Fewer components (simpler frameworks preferred)
4. Lower ID (earlier in collection)

## Red Flags

| Thought | Reality |
|---------|---------|
| "This is just a simple prompt question" | Users asking about prompts likely need framework guidance. Check PromptX. |
| "I can recommend a framework quickly" | Framework selection requires systematic analysis. Use the scoring algorithm. |
| "Any framework will work" | Poor framework matches reduce effectiveness. Score properly. |
| "User didn't explicitly ask for a framework" | Implicit need for structure is common. Analyze the task type. |
| "I'll just give them a popular one" | Popularity ≠ relevance. Match to their specific use case. |
| "The query is too short to score" | Short queries still have domains and keywords. Score what you have. |
| "They need examples, not frameworks" | Examples are part of frameworks. Present both together. |

## Quality Checklist

Before presenting a framework recommendation:

- [ ] Extracted user's domain, task type, complexity, and keywords
- [ ] Scored all 57 frameworks using the algorithm
- [ ] Verified top score makes sense for the query
- [ ] Checked for ties and applied tie-breaking rules
- [ ] Loaded framework details from index.json
- [ ] Read actual framework file for examples if score > 60
- [ ] Prepared response matching the appropriate template
- [ ] Included rationale for the recommendation
- [ ] Offered to help apply the framework

## Presentation Templates

### Single Clear Match (Score > 80)

```markdown
## Recommended Framework: [Framework Name]

**Match Score:** [Score]/100

**Why this framework:** [2-3 sentence rationale based on scoring]

**Quick Overview:** [Description from index]

**Framework Components:**
1. **[Component 1]**: [Brief explanation from framework file]
2. **[Component 2]**: [Brief explanation from framework file]
3. **[Component 3]**: [Brief explanation from framework file]

**Best For:**
- [Use case 1 from optimal_for]
- [Use case 2 from optimal_for]

**Strengths:**
✅ [Strength 1]
✅ [Strength 2]
✅ [Strength 3]

**Considerations:**
⚠️ [Relevant weakness if applicable]

**Example Application:**
[Relevant example from framework file, adapted if needed]

Would you like me to help you apply this framework to your specific task?
```

### Multiple Matches (Scores 60-80)

```markdown
## Top 3 Framework Recommendations

I found multiple frameworks that could work well for your task. Here are your best options:

### 1. [Framework Name] - Score: [Score]/100

**Best for:** [Primary use case from optimal_for]
**Why it fits:** [Rationale based on domain/task match]
**Complexity:** [Level]
**Components:** [Component 1], [Component 2], [Component 3]

### 2. [Framework Name] - Score: [Score]/100

**Best for:** [Primary use case]
**Why it fits:** [Rationale]
**Complexity:** [Level]
**Components:** [Component 1], [Component 2], [Component 3]

### 3. [Framework Name] - Score: [Score]/100

**Best for:** [Primary use case]
**Why it fits:** [Rationale]
**Complexity:** [Level]
**Components:** [Component 1], [Component 2], [Component 3]

## Quick Comparison

| Aspect | Option 1 | Option 2 | Option 3 |
|--------|----------|----------|----------|
| Complexity | [Level] | [Level] | [Level] |
| Flexibility | [Level] | [Level] | [Level] |
| Examples | [Count] | [Count] | [Count] |
| Best Domain | [Domain] | [Domain] | [Domain] |

**My Recommendation:** Start with **[Framework 1]** because [specific reason related to their query].

Which framework would you like to explore further?
```

### Ambiguous Input (Score < 60)

```markdown
I'd love to help you find the right framework! To recommend the best fit, I need to understand your situation better.

**Quick Questions:**

1. **What are you trying to accomplish?**
   - Create effective AI prompts?
   - Make a business decision?
   - Solve a complex problem?
   - Generate content?
   - Analyze information?

2. **What domain are you working in?**
   - Business/Marketing
   - Education/Learning
   - Creative/Design
   - Technical/Engineering
   - Personal/General

3. **How complex is your task?**
   - Simple (straightforward, single step)
   - Medium (multiple factors to consider)
   - Complex (many variables, deep analysis needed)

Once I know more, I can match you with the perfect framework from our collection of 57 options!
```

## Examples

### Example 1: Clear Match

**User:** "Help me optimize a prompt for analyzing customer feedback"

**Analysis:**
- Domain: business, technical (feedback analysis)
- Task: analysis
- Complexity: medium
- Keywords: analyze, feedback, customer

**Top Match:** PEE Framework (Point, Evidence, Explanation) - Score: 88/100

**Response:**
```markdown
## Recommended Framework: PEE Framework

**Match Score:** 88/100

**Why this framework:** The PEE Framework (Point, Evidence, Explanation) is ideal for analytical tasks like customer feedback analysis. It provides a structured approach to making claims supported by evidence and thorough explanation.

**Quick Overview:** A framework for building analytical responses through structured arguments.

**Framework Components:**
1. **Point**: Make a clear claim or assertion about the feedback
2. **Evidence**: Support the point with specific examples from the feedback data
3. **Explanation**: Explain how the evidence supports the point and its implications

**Best For:**
- Analytical writing and responses
- Evidence-based conclusions
- Structured evaluation of data

**Strengths:**
✅ Encourages evidence-based reasoning
✅ Creates clear, structured responses
✅ Improves analytical depth

**Example Application:**

For customer feedback analysis:
- **Point**: "Users report that the new interface improves productivity by 40%"
- **Evidence**: "Based on 127 survey responses mentioning 'faster workflow' and 'time savings'"
- **Explanation**: "The consistent mention of time efficiency across responses indicates the interface redesign successfully addresses user workflow pain points"

Would you like me to help you apply this framework to your specific customer feedback analysis?
```

### Example 2: Multiple Matches

**User:** "I need to make a decision about which features to build next"

**Analysis:**
- Domain: business, technical
- Task: decision_making
- Complexity: medium
- Keywords: decision, features, build

**Top Matches:**
1. RICE Framework - Score: 78/100
2. Pros and Cons Analysis - Score: 75/100
3. Six Thinking Hats - Score: 72/100

**Response:**
```markdown
## Top 3 Framework Recommendations

I found multiple frameworks that could work well for your feature prioritization decision.

### 1. RICE Framework - Score: 78/100

**Best for:** Prioritizing features based on quantitative scoring
**Why it fits:** Specifically designed for product decisions, RICE provides a numerical approach to compare features objectively
**Complexity:** Medium
**Components:** Reach, Impact, Confidence, Effort

### 2. Pros and Cons Analysis - Score: 75/100

**Best for:** Evaluating multiple options systematically
**Why it fits:** Classic decision-making approach that's versatile and easy to apply
**Complexity:** Simple
**Components:** Listing advantages and disadvantages for each option

### 3. Six Thinking Hats - Score: 72/100

**Best for:** Comprehensive decision exploration from multiple perspectives
**Why it fits:** Ensures you consider emotional, creative, and critical aspects of the decision
**Complexity:** Medium
**Components:** Six distinct thinking perspectives (facts, feelings, caution, benefits, creativity, process)

## Quick Comparison

| Aspect | RICE | Pros and Cons | Six Thinking Hats |
|--------|------|---------------|-------------------|
| Complexity | Medium | Simple | Medium |
| Flexibility | Medium | High | High |
| Examples | 1 | 1 | 1 |
| Best Domain | Business | Decision | Decision |

**My Recommendation:** Start with **RICE Framework** because it's specifically designed for feature prioritization and provides quantitative scores that make comparison objective.

Which framework would you like to explore further?
```

### Example 3: Ambiguous Input

**User:** "I need a framework"

**Analysis:**
- Domain: None specified
- Task: None specified
- Complexity: Unknown
- Keywords: framework (too generic)

**Top Score:** 45/100 (no clear match)

**Response:**
```markdown
I'd love to help you find the right framework! To recommend the best fit, I need to understand your situation better.

**Quick Questions:**

1. **What are you trying to accomplish?**
   - Create effective AI prompts?
   - Make a business decision?
   - Solve a complex problem?
   - Generate content?
   - Analyze information?

2. **What domain are you working in?**
   - Business/Marketing
   - Education/Learning
   - Creative/Design
   - Technical/Engineering
   - Personal/General

3. **How complex is your task?**
   - Simple (straightforward, single step)
   - Medium (multiple factors to consider)
   - Complex (many variables, deep analysis needed)

Once I know more, I can match you with the perfect framework from our collection of 57 options!
```

## Implementation Notes

### Loading Framework Data

When this skill is invoked:

1. **Load index.json** from `/Users/lijun/Coding/skill_cook/frameworks/index.json`
   - Contains metadata for all 57 frameworks
   - ~500KB, loads in <1 second

2. **Score frameworks** based on user query
   - Extract domain, task, complexity, keywords from query
   - Apply scoring algorithm to all frameworks
   - Sort by score descending

3. **Load framework files** as needed
   - For top 3 matches, read actual markdown files
   - Extract examples and detailed component explanations
   - Files located in `/Users/lijun/Coding/skill_cook/frameworks/`

### Domain Detection Rules

**From user query, detect:**
- **education**: "teach", "learn", "lesson", "curriculum", "student", "assessment"
- **business**: "business", "marketing", "sales", "strategy", "management", "professional"
- **creative**: "creative", "brainstorm", "innovation", "design", "storytelling"
- **technical**: "technical", "code", "development", "ai", "data", "analysis"
- **decision**: "decision", "choice", "evaluate", "select", "choose"
- **problem**: "problem", "solution", "solve", "resolve", "challenge"

### Task Type Detection Rules

**From user query, detect:**
- **prompt_engineering**: "prompt", "ai interaction", "ask", "query"
- **decision_making**: "decide", "choose", "prioritize", "select"
- **problem_solving**: "solve", "fix", "resolve", "troubleshoot"
- **content_creation**: "write", "create", "generate", "content"
- **analysis**: "analyze", "examine", "evaluate", "assess"
- **brainstorming**: "brainstorm", "ideate", "innovate", "idea"

### Complexity Detection Rules

**Simple:**
- Single-step requests
- Short queries (< 50 words)
- No conjunctions like "and", "but", "however"

**Medium:**
- 2-3 step processes
- 50-100 words
- Some conjunctions

**Complex:**
- Multi-step processes
- >100 words
- Many variables or factors mentioned
- Words like "comprehensive", "systematic", "detailed"

## Critical Success Factors

1. **Accurate Domain Classification**: Correctly identifying the user's domain is crucial (30% of score)
2. **Task Type Matching**: Understanding what the user wants to accomplish (25% of score)
3. **Keyword Relevance**: Extracting meaningful keywords from the query (20% of score)
4. **Appropriate Complexity**: Matching framework complexity to task complexity (15% of score)
5. **Practical Examples**: Frameworks with examples get higher scores (10% bonus)

## Troubleshooting

**Problem:** All frameworks score < 60
**Solution:** Ask clarification questions to gather more context

**Problem:** Multiple frameworks tie at top score
**Solution:** Apply tie-breaking rules (examples > flexibility > simplicity > ID)

**Problem:** User asks for specific framework by name
**Solution:** Present that framework directly, but also show similar alternatives

**Problem:** Query is too long/complex
**Solution:** Focus on key themes, extract main domain/task, score accordingly

## References

See `references/` directory for:
- `scoring-algorithm.md`: Detailed scoring logic and weight explanations
- `domain-mappings.md`: Complete keyword classification rules and vocabulary
- `framework-examples.md`: Additional framework responses and interaction samples
