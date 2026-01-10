---
description: Interview about a specification to uncover hidden requirements, edge cases, and tradeoffs
argument-hint: <file-path or description>
---

# Spec Interview

Follow the instructions in `${CLAUDE_PLUGIN_ROOT}/skills/spec-interview/SKILL.md` to conduct this interview.

## Input Handling

Determine the input type from the argument:
- If it looks like a file path (contains `/`, `.md`, `.txt`, or exists as a file), read it as a specification file
- Otherwise, treat it as a description to build a new spec from scratch

## Examples

```
/spec-interview spec.md
/spec-interview ./docs/api-design.md
/spec-interview A CLI tool that syncs local files to S3
/spec-interview User authentication system with OAuth and MFA
```
