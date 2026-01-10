---
description: Interview about a specification to uncover hidden requirements, edge cases, and tradeoffs
argument-hint: <file-path or description>
---

# Spec Interview

Conduct a systematic interview to uncover hidden requirements, edge cases, ambiguities, and tradeoffs.

## Instructions

1. **Determine the input type**:
   - If the argument looks like a file path (contains `/`, `.md`, `.txt`, or exists as a file), read it as a specification file
   - Otherwise, treat it as a description to build a new spec from scratch

2. **For existing spec files**: Read the file and analyze for gaps

   **For new descriptions**: Use the description as the starting point

3. **Analyze/explore** these areas:
   - Implicit assumptions that need validation
   - Undefined behavior in edge cases
   - Missing error handling scenarios
   - Ambiguous requirements
   - Performance/scalability gaps
   - Security implications
   - Data consistency issues
   - User experience gaps
   - Integration points
   - Migration concerns

4. **Conduct the interview** using the AskUserQuestion tool:
   - Start with the most critical unknowns
   - Ask 2-4 questions per round
   - Focus on non-obvious issues - never ask what's already covered
   - Probe tradeoffs and challenge assumptions
   - Continue until significant ambiguities are resolved

5. **Synthesize the output**:
   - Compile answers into a comprehensive specification
   - Include sections for edge cases, error handling, decisions & tradeoffs
   - For existing files: update in place or write to user-specified path
   - For new specs: ask where to save (default: `spec.md`)

## Question Quality

Instead of: "What happens when there's an error?"
Ask: "When the payment API returns a timeout after the user's card has been charged but before confirmation - do we retry, refund, or queue for manual review?"

Consult `${CLAUDE_PLUGIN_ROOT}/skills/spec-interview/references/question-patterns.md` for detailed question patterns.

## Examples

```
/spec-interview spec.md
/spec-interview ./docs/api-design.md
/spec-interview A CLI tool that syncs local files to S3
/spec-interview User authentication system with OAuth and MFA
```
