# understand-codebase

`understand-codebase` is a portable coding-agent skill for learning unfamiliar projects. It guides an agent to inspect a repository and produce one complete `PROJECT_CODE_GUIDE.md`.

The skill now supports two guide modes:

- **Engineer Fast-Start:** for engineers who need to run, test, debug, modify, or quickly onboard to a project.
- **Beginner Full Runtime Code Walkthrough:** for learners who want a full-flow, line-level explanation of the actual execution path, including exact lines or line ranges, code goals, libraries/methods, inputs, outputs, shape/schema, and the next code path.

Both modes use a PLAN-style workflow map before detailed analysis: goal, command/config/input contracts, runtime stages, output contracts, validation/error cases, and explicit conventions. This makes the generated guide useful as both a study path and a maintenance reference.

The guide defaults to English. If the user requests another language, or appears to prefer another language, the agent should ask whether to keep English or switch.

## Repository Layout

```text
understand-codebase/
  SKILL.md
  agents/openai.yaml
  references/
    analysis-checklist.md
    project-guide-template.md
adapters/
  AGENTS-understand-codebase.md
  cursor-understand-codebase.mdc
```

## Install

### Codex

Copy the `understand-codebase/` folder into your Codex skills directory, such as:

```text
~/.codex/skills/understand-codebase/
```

If you use a custom `CODEX_HOME`, place it under:

```text
$CODEX_HOME/skills/understand-codebase/
```

### Claude Code

Copy the `understand-codebase/` folder into a Claude Code skills location:

```text
~/.claude/skills/understand-codebase/
```

For project-only usage, copy it into:

```text
.claude/skills/understand-codebase/
```

### Cursor

For Cursor Project Rules, copy:

```text
adapters/cursor-understand-codebase.mdc
```

to:

```text
.cursor/rules/understand-codebase.mdc
```

For a simpler project-level instruction file, copy:

```text
adapters/AGENTS-understand-codebase.md
```

to your project root as:

```text
AGENTS.md
```

## Usage Examples

Engineer Fast-Start:

```text
Use understand-codebase to create an engineer fast-start guide so I can run tests and modify this project.
```

Beginner Full Runtime Code Walkthrough:

```text
Use understand-codebase to create a beginner full runtime code walkthrough. Explain the actual execution path line by line or line-range by line-range, including code goals, libraries/methods, inputs, outputs, and next code path.
```

Composite project with default path:

```text
Help me understand this inference framework. Default path is fine.
```

Shape-focused:

```text
Generate a beginner-friendly guide for this training project, including input and output shapes.
```

## Output

The skill writes one file by default:

```text
PROJECT_CODE_GUIDE.md
```

It should clearly label what was confirmed from code, what was runtime verified, what was statically inferred, and what remains unknown.
