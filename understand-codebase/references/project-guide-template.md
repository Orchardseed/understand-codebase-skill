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

Output depth policy: This guide has no artificial length limit. Keep summaries concise, but include all details needed to run, test, debug, modify, and verify the project.

## Evidence Legend

- Confirmed:
- Runtime verified:
- Static inference:
- Unknown:

## 1. Goal and Behavior Contract

- Overall goal:
- Expected behavior after running the main workflow:
- What this guide helps an engineer do:
- Primary success criteria:
- Out of scope or intentionally unsupported behavior:

| Goal | Expected behavior | Evidence |
| --- | --- | --- |

## 2. Project Snapshot

- Project type:
- Main language/framework:
- Primary entrypoint:
- Primary output:
- Most important directories:

## 3. Documentation-Derived Operating Summary

Summarize what the README/docs say before tracing code:

- What the project provides:
- Required environment/dependencies:
- Main user workflows:
- Preprocessing/preparation steps:
- Training/inference/API/CLI/UI/worker flows:
- Post-run utilities:
- Common issues mentioned by docs:
- Documentation files read:

## 4. Workflow Coverage Matrix

List the major documented and discovered workflows. Mark which ones are expanded in this guide.

| Workflow | User command/entrypoint | Input | Output | Expanded here? | Evidence |
| --- | --- | --- | --- | --- | --- |

## 5. Command, Config, and Input Contracts

### Commands

| Command/Argument | Role | Default | Override behavior | Evidence |
| --- | --- | --- | --- | --- |

### Config

| Field | Role | Example/default | Used by | Evidence |
| --- | --- | --- | --- | --- |

### Inputs

| Input | Required shape/schema/type | Validation rule | Failure behavior | Evidence |
| --- | --- | --- | --- | --- |

## 6. Runbook

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

### Command Cookbook

| Task | Command | What it does | Expected output/artifact | When to use | Evidence |
| --- | --- | --- | --- | --- | --- |

## 7. Workflow Stage Map

Summarize the workflow as a stage table before diving into files:

| Stage | Consumes | Does | Produces | Failure cases | Evidence |
| --- | --- | --- | --- | --- | --- |

## 8. Entrypoints and Runtime Flow

Summarize the main path:

1. Command:
2. Entrypoint file/function:
3. Config initialization:
4. Core service/model/pipeline:
5. Output:

Add a Mermaid flowchart when it improves scanning.

## 9. Output Contracts

Explain generated files, responses, logs, checkpoints, metrics, or UI state:

| Output | Location/name | Schema/content | Naming/overwrite rule | Evidence |
| --- | --- | --- | --- | --- |

## 10. Data Contracts and Shape Summary

Summarize key inputs and outputs:

| Data | Source | Shape/Schema/Type | Destination | Evidence |
| --- | --- | --- | --- | --- |

## 11. Key Files for Modification

| Task | File(s) | What to change | Risk | Evidence |
| --- | --- | --- | --- | --- |

## 12. Core Components

Explain only the components an engineer needs to modify or debug:

- Component:
- Responsibility:
- Called by:
- Depends on:
- Modification risk:

## 13. Common Issues and Debugging Map

Convert README/doc issues and code-discovered failure points into actionable debugging notes:

| Symptom | Likely cause | Where to check | Safe command/check | Evidence |
| --- | --- | --- | --- | --- |

## 14. Tests and Validation Strategy

- Fast tests:
- Integration tests:
- Shape/data checks:
- Manual smoke test:
- Checks not run:

## 15. Explicit Conventions and Invariants

List project rules that future edits should preserve:

- CLI/config naming:
- Config override order:
- Output naming:
- GPU/process/model assumptions:
- Backward compatibility assumptions:
- Data contract invariants:

## 16. Documentation Claims Versus Code Evidence

Check important README/docs claims against code, config, tests, or safe runtime checks:

| Claim from docs | Code/config evidence | Status | Notes |
| --- | --- | --- | --- |

Use status values: Confirmed, Runtime verified, Static inference, Unknown, or Mismatch.

## 17. Main Dependencies and Their Project Roles

| Dependency | Role in this project | Where used | Evidence |
| --- | --- | --- | --- |

## 18. Risks, Unknowns, and Follow-Ups

- Risk:
- Unknown:
- Needs runtime verification:
```

## Template B: Beginner Full Runtime Code Walkthrough

Use this for a very detailed new-learner guide through actual execution. This mode should read like following the program in a debugger while also explaining what each important line or line range accomplishes.

```markdown
# Project Code Guide

Guide mode: Beginner Full Runtime Code Walkthrough

Output depth policy: This guide has no artificial length limit. Keep overview sections navigable, but fully expand the selected runtime path, important line ranges, shape/schema transitions, and caller/callee transitions.

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

## 2. Project Learning Route

Use README/docs to give the learner a map of the whole project before focusing on code:

- Documents read:
- What the README/docs say the project provides:
- The usual user journey:
- Preparation or preprocessing steps:
- Main operation flows:
- Post-run or analysis utilities:
- Common issues a learner should know:

### Workflow Coverage Matrix

| Workflow | Purpose | Entry command/file | Input data | Output | Expanded in this guide? | Evidence |
| --- | --- | --- | --- | --- | --- | --- |

## 3. Selected Runtime Path

- User-selected focus:
- Default path used:
- Input data being traced:
- Model/service/workflow being traced:
- Start command or entrypoint:
- Expected final output:

## 4. PLAN-Style Workflow Map

Explain the selected workflow before line-level code analysis.

### Goal and Expected Behavior

| Goal | Expected behavior | Evidence |
| --- | --- | --- |

### Command and Config Contracts

| Command/Config/Input | Role | Example/default | Override or validation rule | Evidence |
| --- | --- | --- | --- | --- |

### Runtime Stage Map

| Stage | Consumes | Code responsibility | Produces | Next stage | Evidence |
| --- | --- | --- | --- | --- | --- |

### Output Contracts

| Output | Location/name | Schema/content | Naming/overwrite rule | Evidence |
| --- | --- | --- | --- | --- |

### Validation and Error Contracts

| Invalid condition | Expected behavior | Where handled | Evidence |
| --- | --- | --- | --- |

### Explicit Conventions

- CLI/config naming:
- Config override order:
- Output naming:
- Model/GPU/process assumptions:
- Data contract invariants:

### Documentation Claims Versus Code Evidence

| Claim from README/docs | Code/config/test evidence | Status | Learner note |
| --- | --- | --- | --- |

Use status values: Confirmed, Runtime verified, Static inference, Unknown, or Mismatch.

## 5. Before the Code Runs

Explain setup that affects execution:

- Important config files:
- Environment variables:
- External files/data:
- Dependencies/libraries that matter in this path:

## 6. Full Runtime Code Walkthrough

Repeat this block for each meaningful execution step. Each step must be tied to exact lines or tight line ranges when possible.

### Step N: <plain-language action>

Code location:

- `<file>:<line>` or `<file>:<start-line>-<end-line>`

Lines explained:

| Lines | Code | What this code accomplishes |
| --- | --- | --- |
| `<file>:<line>` | `<short code excerpt or symbol>` | Explains the concrete work done here |
| `<file>:<start-line>-<end-line>` | `<short code excerpt or symbol>` | Explains the concrete work done by this block |

Code goal:

- Explain the exact goal these lines complete in the runtime path.

Libraries, classes, and methods used:

- `<library_or_module>.<method>()`: what it does here
- `<local_function>()`: why this project calls it
- `<local_class.method>()`: what object state or output it produces

Input:

- Name:
- Source:
- Shape/schema/type:
- Example value or keys:
- Passed into:
- Evidence:

What happens:

1. Explain the first executed line or tight line range.
2. Explain the next executed line or tight line range.
3. Explain important branches, loops, transforms, validations, model calls, or side effects.
4. Explain what values are passed into the next function/method call.

Output:

- Name:
- Shape/schema/type:
- Destination:
- Returned from:
- Evidence:

Next code path:

- Goes to `<file>:<line>` / `<function>` because ...
- If a function returns, state which caller line resumes next.

Beginner note:

- Explain the one concept the reader should understand before continuing.

### Step N+1: <next executed action>

Use another full step block. Do not skip important calls simply because they are in a different file.

## 7. Important Loops and Branches

For each important loop/branch:

- Location:
- Lines explained:
- Why it repeats or branches:
- Input per iteration:
- Output per iteration:
- State changed per iteration:
- Stop condition:
- Next code path after the loop/branch:
- Evidence:

## 8. Data and Shape Timeline

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

## 9. Libraries, Classes, Functions, and Methods Used in This Runtime Path

Explain only libraries/classes/functions/methods actually used in the walkthrough:

| Symbol | Type | Step | Lines | What it does here | Input | Output | Beginner explanation |
| --- | --- | --- | --- | --- | --- | --- | --- |

## 10. Acceptance Checks and Learning Exercises

Use this section like a small study plan:

| Check/exercise | Command or file | What it proves | Evidence/notes |
| --- | --- | --- | --- |

Include safe commands such as `--help`, focused tests, dry-runs, or shape-printing probes when available.

## 11. Where to Read Next

Give a learning path:

1. Read `<file>` to understand ...
2. Read `<file>` to understand ...
3. Skip `<file>` initially because ...

## 12. Unknowns and Items That Need Runtime Verification

List:

- Lines not reached statically
- Dynamic dispatch
- Missing sample data
- Unverified shapes
- Commands not run
- External services or credentials needed
- Any important code path that could not be followed to exact lines
```

## Template C: Both

If the user asks for both, write:

1. A concise Engineer Fast-Start section first.
2. A Beginner Full Runtime Code Walkthrough section second.

Keep the fast-start section short. Put detailed line-by-line explanation in the tutorial section.
