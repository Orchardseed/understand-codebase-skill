# PROJECT_CODE_GUIDE.md Templates

Use the template that matches the selected guide mode. Translate section titles when the user requests a non-English guide.

## Shared Evidence Legend

Include this near the top of every guide:

```markdown
## Evidence Legend

- Confirmed: explicitly shown in code, docs, schemas, tests, comments, or config.
- Runtime verified: checked by a safe command, test, dry run, route listing, CLI help output, or minimal sample.
- Static inference: inferred from conventions, signatures, model structure, or surrounding code.
- Unknown: cannot be determined from available code and safe checks.
```

## Template A: Engineer Fast-Start

Use this for quick engineering handoff, running, testing, debugging, and modifying.

```markdown
# Project Code Guide

Guide mode: Engineer Fast-Start

## Evidence Legend

- Confirmed:
- Runtime verified:
- Static inference:
- Unknown:

## 1. Project Snapshot

- Purpose:
- Project type:
- Main language/framework:
- Primary entrypoint:
- Primary output:
- Most important directories:

## 2. Runbook

### Install

- Command:
- Evidence:

### Run

- Command:
- What it starts:
- First file reached:
- Config loaded:
- Evidence:

### Test

- Command:
- What it covers:
- Evidence:

### Debug / Logs

- Debug command:
- Log location:
- Common failure points:

## 3. Entrypoints and Runtime Flow

Summarize the main path:

1. Command:
2. Entrypoint file/function:
3. Config initialization:
4. Core service/model/pipeline:
5. Output:

Add a Mermaid flowchart when it improves scanning.

## 4. Configuration and Environment

List required and important configs:

| Name | Source | Used by | Effect | Evidence |
| --- | --- | --- | --- | --- |

## 5. Data Contracts and Shape Summary

Summarize key inputs and outputs:

| Data | Source | Shape/Schema/Type | Destination | Evidence |
| --- | --- | --- | --- | --- |

## 6. Key Files for Modification

| Task | File(s) | What to change | Risk | Evidence |
| --- | --- | --- | --- | --- |

## 7. Core Components

Explain only the components an engineer needs to modify or debug:

- Component:
- Responsibility:
- Called by:
- Depends on:
- Modification risk:

## 8. Tests and Validation Strategy

- Fast tests:
- Integration tests:
- Shape/data checks:
- Manual smoke test:
- Checks not run:

## 9. Main Dependencies and Their Project Roles

| Dependency | Role in this project | Where used | Evidence |
| --- | --- | --- | --- |

## 10. Risks, Unknowns, and Follow-Ups

- Risk:
- Unknown:
- Needs runtime verification:
```

## Template B: Beginner Runtime Tutorial

Use this for step-by-step learning through actual execution. This mode should read like following the program in a debugger.

```markdown
# Project Code Guide

Guide mode: Beginner Runtime Tutorial

## Evidence Legend

- Confirmed:
- Runtime verified:
- Static inference:
- Unknown:

## 1. What This Project Does

Explain the project in plain language:

- What problem it solves
- What kind of program it is
- What the selected runtime flow does
- What concepts a beginner should know first

## 2. Selected Runtime Path

- User-selected focus:
- Default path used:
- Input data being traced:
- Model/service/workflow being traced:
- Start command or entrypoint:
- Expected final output:

## 3. Before the Code Runs

Explain setup that affects execution:

- Important config files:
- Environment variables:
- External files/data:
- Dependencies/libraries that matter in this path:

## 4. Step-by-Step Runtime Walkthrough

Repeat this block for each meaningful execution step.

### Step N: <plain-language action>

Location:

- `<file>:<line>` or `<file>:<start-line>-<end-line>`

Code goal:

- Explain what this code is trying to accomplish.

Libraries, classes, and methods used:

- `<library_or_module>.<method>()`: what it does here
- `<local_function>()`: why this project calls it

Input:

- Name:
- Source:
- Shape/schema/type:
- Example value or keys:
- Evidence:

What happens:

1. First operation
2. Next operation
3. Important branch, loop, transform, validation, model call, or side effect

Output:

- Name:
- Shape/schema/type:
- Destination:
- Evidence:

Next code path:

- Goes to `<file>:<line>` / `<function>` because ...

Beginner note:

- Explain the one concept the reader should understand before continuing.

## 5. Important Loops and Branches

For each important loop/branch:

- Location:
- Why it repeats or branches:
- Input per iteration:
- Output per iteration:
- Stop condition:
- Evidence:

## 6. Data and Shape Timeline

Show the data contract changing over time:

| Step | Variable/Data | Shape/Schema/Type | Changed by | Evidence |
| --- | --- | --- | --- | --- |

Examples:

- Raw image: `[H, W, C]`
- Tensor image: `[C, H, W]`
- Batch: `[B, C, H, W]`
- Token ids: `[B, T]`
- Hidden states: `[B, T, D]`
- HTTP body: `{ user_id, items[], created_at }`

## 7. Libraries and Methods Used in This Runtime Path

Explain only libraries/methods actually used in the walkthrough:

| Library/Method | Step | What it does here | Beginner explanation |
| --- | --- | --- | --- |

## 8. Where to Read Next

Give a learning path:

1. Read `<file>` to understand ...
2. Read `<file>` to understand ...
3. Skip `<file>` initially because ...

## 9. Unknowns and Items That Need Runtime Verification

List:

- Lines not reached statically
- Dynamic dispatch
- Missing sample data
- Unverified shapes
- Commands not run
- External services or credentials needed
```

## Template C: Both

If the user asks for both, write:

1. A concise Engineer Fast-Start section first.
2. A Beginner Runtime Tutorial section second.

Keep the fast-start section short. Put detailed line-by-line explanation in the tutorial section.
