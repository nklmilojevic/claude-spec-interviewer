---
name: Spec Interview
description: This skill should be used when the user asks to "interview me about my spec", "review my specification", "ask me questions about my spec", "help me flesh out my spec", "find gaps in my specification", "spec-interview", or wants to be interviewed about implementation details, edge cases, and tradeoffs in their specification document.
---

# Spec Interview

A deep-dive interviewing skill that reads a specification document and systematically interviews the user to uncover hidden requirements, edge cases, ambiguities, and tradeoffs that aren't immediately obvious.

## Purpose

Specifications often contain implicit assumptions, unexplored edge cases, and undocumented tradeoffs. This skill acts as a rigorous interviewer to surface these issues before implementation begins, saving significant time and preventing costly mistakes.

## Workflow

### Step 1: Read the Specification

Read the spec file provided by the user. Default path is `spec.md` in the current directory. If the file doesn't exist, ask the user for the correct path.

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
