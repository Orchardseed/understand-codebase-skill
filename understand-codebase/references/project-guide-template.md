# PROJECT_CODE_GUIDE.md Template

Use this structure for the generated guide. Translate section titles when the user requests a non-English guide.

```markdown
# Project Code Guide

## Evidence Legend

- Confirmed: explicitly shown in code, docs, schemas, tests, comments, or config.
- Runtime verified: checked by a safe command, test, dry run, route listing, CLI help output, or minimal sample.
- Static inference: inferred from conventions, signatures, model structure, or surrounding code.
- Unknown: cannot be determined from available code and safe checks.

## 1. Project Overview

Explain the project in beginner-friendly language:

- What problem it solves
- Main technology/framework
- Main runtime mode
- Most important concepts to know before reading code

Quick anchors:

- Main language:
- Project type:
- Primary entrypoint:
- Main output:

## 2. Quick Start, Entrypoints, and Runtime Commands

List startup commands found in docs, package scripts, Makefiles, Dockerfiles, CLI definitions, notebooks, or framework conventions.

For each command, explain:

- What it starts
- Which file it reaches first
- Which configs it loads
- Whether the command was runtime verified, statically inferred, or unknown

## 3. Directory Map

Explain important directories by role.

Mark each as:

- Read first
- Read next
- Read later
- Skip initially

## 4. Recommended Reading Order

Give a numbered path through the codebase. For each step:

- File or directory
- Why to read it now
- What question it answers
- What to ignore on first pass

## 5. Core Runtime Flow

Trace the primary execution path from entrypoint to output.

Include a Mermaid flowchart when helpful.

For composite projects, state the chosen primary flow and briefly summarize secondary flows.

## 6. Data Sources, Data Flow, and Shape Tracking

For each important data path:

- Source:
- Reader:
- Raw format:
- Transform steps:
- Intermediate shape/schema/type:
- Final destination:
- Evidence label:

For tensors, prefer forms like:

- Raw image: `[H, W, C]`
- Transform output: `[C, H, W]`
- Batch: `[B, C, H, W]`
- Tokens: `[B, T]`
- Hidden states: `[B, T, D]`
- Logits: `[B, num_classes]` or `[B, T, vocab_size]`

For non-tensor data, describe schema:

- HTTP body: `{ user_id, items[], created_at }`
- Table rows: `[N rows x M columns]`, with important columns
- Service object: `OrderSummaryDTO`
- Database rows: `List[OrderRow]`

## 7. Core Modules, Classes, and Functions

Explain the important files, classes, functions, services, and components.

For each:

- Responsibility
- Who calls it
- What it depends on
- Important inputs and outputs
- Why it matters

## 8. Key Loops, Pipelines, and Workflows

Explain loops and repeated workflows:

- Training loops
- Inference pipelines
- Request handlers
- Worker queues
- Data processing pipelines
- Frontend state/update loops
- CLI command workflows

For each loop:

- What repeats
- What state changes
- Stop condition
- Inputs and outputs per iteration

## 9. Configuration, Environment Variables, and Parameters

Explain:

- Config files
- Environment variables
- CLI flags
- Default values
- Required values
- How config reaches core code
- Differences between dev/test/prod if visible

## 10. Main Dependencies and Their Roles

List important dependencies and explain what each one does in this project.

Avoid generic package descriptions unless needed for beginners.

## 11. Testing, Debugging, and Logging

Explain:

- How tests are organized
- How to run relevant tests
- Useful debug commands
- Where logs are created
- Which tests or commands were runtime verified

## 12. Notes for Future Code Changes

Explain where a developer should modify code for common tasks.

Call out risks:

- Files with broad impact
- Dynamic loading
- Shared configuration
- Hidden coupling
- External service assumptions
- Shape/schema assumptions

## 13. Unknowns and Items That Need Runtime Verification

List anything not fully verified:

- Missing sample data
- Missing credentials
- External services
- Generated files
- Ambiguous entrypoints
- Unverified shapes
- Commands not run
```
