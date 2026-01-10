# Spec Interviewer

A Claude Code plugin that interviews you about your specifications to uncover hidden requirements, edge cases, and tradeoffs before implementation begins.

## Why?

Specifications often contain:
- Implicit assumptions that seem obvious to the author
- Unexplored edge cases that cause bugs later
- Undocumented tradeoffs that lead to rework
- Ambiguous requirements that different readers interpret differently

This plugin acts as a rigorous interviewer, systematically questioning your spec to surface these issues before you write any code.

## Installation

### From Marketplace (Recommended)

1. **Add the marketplace** to Claude Code:

   ```
   /plugin marketplace add nklmilojevic/claude-marketplace
   ```

2. **Install the plugin** from the marketplace:

   ```
   /plugin install spec-interviewer@nkl-plugins
   ```

### Manual Installation

Copy this plugin to your Claude Code plugins directory:

```bash
cp -r spec-interviewer ~/.claude/plugins/
```

Or clone directly:

```bash
git clone <repo-url> ~/.claude/plugins/spec-interviewer
```

## Usage

### With a specification file

```
/spec-interviewer:spec-interview path/to/your/spec.md
```

### With a description

```
/spec-interviewer:spec-interview "Brief description of your feature or system"
```

### Natural language

You can also ask naturally:
- "Interview me about my spec"
- "Review my specification"
- "Help me flesh out my spec"
- "Find gaps in my specification"

The interviewer will read your spec, then ask targeted questions across 10 categories until all ambiguities are resolved.

## Question Categories

The interviewer probes your specification across these areas:

| Category | Focus |
|----------|-------|
| Edge Cases & Boundaries | Numeric limits, null states, timing windows |
| Failure Modes | Partial failures, recovery paths, error handling |
| Implicit Assumptions | User behavior, environment, data assumptions |
| Tradeoffs & Alternatives | Architecture decisions, consistency vs availability |
| State & Data | Transitions, ownership, concurrency, lifecycle |
| User Experience | Interruptions, feedback, accessibility |
| Security & Privacy | Access control, attack vectors, compliance |
| Performance & Scale | Load characteristics, degradation, caching |
| Integration & Dependencies | External services, data exchange, versioning |
| Evolution & Maintenance | Feature flags, technical debt, observability |

## How It Works

1. **Read** - Loads your specification file
2. **Analyze** - Identifies gaps, ambiguities, and areas needing clarification
3. **Interview** - Asks 2-4 targeted questions per round until coverage is complete
4. **Synthesize** - Compiles your answers into an enhanced specification

## Output

After the interview, you receive an enhanced specification that:
- Preserves your original structure
- Integrates interview insights naturally
- Adds a "Decisions & Tradeoffs" section documenting key choices
- Includes an "Open Questions" section for unresolved items

## Project Structure

```
spec-interviewer/
├── .claude-plugin/
│   └── plugin.json           # Plugin manifest
├── skills/
│   └── spec-interview/
│       ├── SKILL.md          # Skill definition and workflow
│       └── references/
│           └── question-patterns.md  # Question pattern reference
└── README.md
```

## License

MIT
