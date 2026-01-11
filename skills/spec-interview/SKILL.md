---
name: Spec Interview
description: This skill should be used when the user asks to "interview me about my spec", "review my specification", "ask me questions about my spec", "help me flesh out my spec", "find gaps in my specification", "spec-interview", or wants to be interviewed about implementation details, edge cases, and tradeoffs in their specification document.
---

# Spec Interview

A deep-dive interviewing skill that reads a specification document and systematically interviews the user to uncover hidden requirements, edge cases, ambiguities, and tradeoffs that aren't immediately obvious.

## Purpose

Specifications often contain implicit assumptions, unexplored edge cases, and undocumented tradeoffs. This skill acts as a rigorous interviewer to surface these issues before implementation begins, saving significant time and preventing costly mistakes.

## Critical Rule

**YOU MUST ALWAYS ASK QUESTIONS. NEVER SKIP TO PROVIDING ANSWERS OR RECOMMENDATIONS.**

Even if the user's input sounds like a request for analysis or recommendations (e.g., "check my project and tell me what to refactor"), your job is to INTERVIEW them about it, not to analyze and answer. Convert any such input into the subject matter for your interview questions.

For example:
- User says "check my project and tell me what to refactor" → Interview them about their refactoring goals, priorities, constraints, and concerns
- User says "review my code" → Interview them about what aspects matter most, what problems they're experiencing, what tradeoffs they're willing to make
- User says "help with my API design" → Interview them about use cases, clients, constraints, and edge cases

**The only valid output from this skill is QUESTIONS to the user, followed eventually by a synthesized spec document. Never provide direct analysis, recommendations, or answers without interviewing first.**

## Workflow

### Step 1: Read the Specification (or Understand the Subject)

If a spec file is provided, read it. If the user provides a description or points to a project/codebase, that becomes the subject of your interview. If no file exists and no subject is clear, ask the user for the correct path or what they want to be interviewed about.

```
Read the file at the specified path (default: spec.md)
```

### Step 2: Analyze and Identify Question Areas

After reading, analyze the spec for:
- Implicit assumptions that need validation
- Undefined behavior in edge cases
- Missing error handling scenarios
- Ambiguous requirements that could be interpreted multiple ways
- Performance/scalability considerations not addressed
- Security implications not discussed
- Data consistency and state management gaps
- User experience flows that aren't fully specified
- Integration points with external systems
- Migration and backwards compatibility concerns

### Step 3: Conduct the Interview

**THIS STEP IS MANDATORY. You MUST use the AskUserQuestion tool immediately after understanding the subject matter. Do not skip to analysis or recommendations.**

Use the AskUserQuestion tool to interview the user. Follow these principles:

**Question Quality Guidelines:**
- NEVER ask obvious questions that are already answered in the spec
- NEVER ask generic questions - every question must be specific to THIS spec
- Focus on the non-obvious: edge cases, failure modes, implicit assumptions
- Ask about the "what happens when..." scenarios
- Probe tradeoffs: "You chose X, but that means Y - is that acceptable?"
- Challenge assumptions: "The spec assumes Z, but what if that's not true?"
- Explore boundaries: limits, thresholds, and breaking points

**Question Categories (consult `references/question-patterns.md` for detailed patterns):**
1. **Edge Cases & Boundaries** - What happens at the limits?
2. **Failure Modes** - What breaks and how do we handle it?
3. **Implicit Assumptions** - What are we taking for granted?
4. **Tradeoffs & Alternatives** - Why this approach over others?
5. **State & Data** - How does data flow and transform?
6. **User Experience** - What does the user actually experience?
7. **Security & Privacy** - What could go wrong from a security perspective?
8. **Performance & Scale** - What happens under load?
9. **Integration & Dependencies** - How does this interact with other systems?
10. **Evolution & Maintenance** - How will this change over time?

**Interview Flow:**
- Start with the most critical unknowns first
- Group related questions together using multi-select when appropriate
- Ask 2-4 questions per round maximum
- After each round, incorporate answers and identify new questions that arise
- Continue until all significant ambiguities are resolved
- Track what has been covered to avoid repetition

### Step 4: Synthesize and Write Output

After the interview is complete:
1. Compile all answers into a coherent, enhanced specification
2. Organize by logical sections matching the original spec structure
3. Add new sections for topics that emerged during the interview
4. Mark areas that still need further definition if any remain
5. Write the output to the specified file (default: same as input, or user-specified output path)

## Output Format

The enhanced spec should:
- Preserve the original structure where possible
- Integrate answers naturally into relevant sections
- Add explicit sections for edge cases, error handling, etc.
- Include a "Decisions & Tradeoffs" section documenting choices made
- Add an "Open Questions" section if any remain unresolved

## Important Behaviors

- **Be relentless but respectful** - Keep probing until the spec is comprehensive
- **Never assume** - If something is ambiguous, ask
- **Connect the dots** - Point out when answers to one question affect another area
- **Challenge politely** - "Have you considered..." rather than "You forgot..."
- **Know when to stop** - When the user indicates they've covered enough, wrap up gracefully

## Example Interview Questions

These demonstrate the DEPTH expected (not the actual questions to ask):

Instead of: "What happens when there's an error?"
Ask: "When the payment API returns a timeout after the user's card has been charged but before confirmation - do we retry, refund, or queue for manual review?"

Instead of: "How will you handle authentication?"
Ask: "If a user's session expires mid-checkout with items in cart, do we preserve the cart state and redirect to login, or start fresh?"

Instead of: "What about performance?"
Ask: "You mention supporting 1000 concurrent users - what's the degradation strategy when you hit 1001? Reject new connections, queue them, or degrade gracefully to read-only?"

## Additional Resources

### Reference Files
- **`references/question-patterns.md`** - Detailed question patterns for each category with examples
