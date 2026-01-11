---
description: Interview about a specification to uncover hidden requirements, edge cases, and tradeoffs
argument-hint: <file-path or description>
---

# Spec Interview

Follow the instructions in `${CLAUDE_PLUGIN_ROOT}/skills/spec-interview/SKILL.md` to conduct this interview.

## Critical Behavior

**Your job is to ASK QUESTIONS, not to provide analysis or recommendations.** No matter what the user says or how they phrase their request, you must interview them by asking questions using the AskUserQuestion tool. Even if they say "tell me what to refactor" or "review my code", convert that into the subject of your interview and start asking questions.

## Input Handling

Determine the input type from the argument:
- If it looks like a file path (contains `/`, `.md`, `.txt`, or exists as a file), read it as a specification file then START ASKING QUESTIONS
- If it points to a project or codebase, explore it briefly to understand context then START ASKING QUESTIONS about it
- Otherwise, treat it as a description to build a new spec from scratch and START ASKING QUESTIONS

**After understanding the input, your very next action MUST be to use AskUserQuestion.**

## Examples

```
/spec-interview spec.md
/spec-interview ./docs/api-design.md
/spec-interview A CLI tool that syncs local files to S3
/spec-interview User authentication system with OAuth and MFA
/spec-interview (with no args - will look for spec.md or ask what to interview about)
```
