---
name: understand-codebase
description: Generate a single PROJECT_CODE_GUIDE.md for understanding an unfamiliar codebase, with selectable guide modes. Use Engineer Fast-Start mode when the user needs to run, test, debug, modify, or quickly onboard to a project. Use Beginner Full Runtime Code Walkthrough mode when the user wants a very detailed learning guide that follows the actual execution path line by line or line-range by line-range, explaining which code completes what goal, which libraries/classes/functions/methods are used, inputs, outputs, data shapes or schemas, and the next code path. Also use for finding entrypoints/config/core classes, tracing data sources and outputs, understanding training/inference/API/CLI/data-processing flows, identifying loops or pipelines, or creating a guided Markdown overview.
---

# Understand Codebase

Use this skill to turn an unfamiliar repository into one coherent guide: `PROJECT_CODE_GUIDE.md`.

The skill supports two distinct guide modes. Do not blend them into a vague hybrid unless the user asks for both.

## PLAN-Style Workflow Map

Before writing detailed sections, build a workflow map similar to a project implementation plan:

1. State the overall goal and expected behavior.
2. Identify the user-facing commands, config files, inputs, weights/models/services, outputs, and validation checks.
3. Summarize the workflow as stages, with each stage describing what is consumed, what work is done, what is produced, and what can fail.
4. Record explicit conventions, such as preferred CLI names, config override order, output file naming, and assumptions about GPU/process/model behavior.
5. Use this workflow map as the backbone for both guide modes.

This workflow map is especially important for learning-oriented guides because it tells the reader what the code is trying to achieve before the line-level walkthrough begins.

## Clarify Before Writing

Clarify only what is needed. If the user's request already makes the answer clear, proceed.

### 1. Language

Default the guide language to English.

If the user explicitly requests another language, use it. If the user writes in a non-English language but does not state the guide language, ask one short question:

```text
Should I write the guide in English or <detected language>?
```

If the user answers "default", use English.

### 2. Guide Mode

Infer the mode when possible:

- Use **Engineer Fast-Start** when the user says quick start, onboard, handoff, run, test, debug, modify, fix, where to change, entrypoints, configs, or risks.
- Use **Beginner Full Runtime Code Walkthrough** when the user says learn, beginner, full flow, detailed, line by line, step-by-step, explain how code runs, follow execution, what happens next, input/output, shape, or "read code with me".

If unclear, ask:

```text
Which guide style do you want?

1. Engineer Fast-Start: quick handoff for running, testing, debugging, and modifying code.
2. Beginner Full Runtime Code Walkthrough: full-flow learning guide with exact lines or line ranges, code goals, libraries/methods, inputs, outputs, and next code path.
3. Both: engineer summary first, then beginner runtime walkthrough.
```

If the user answers "default", choose Beginner Full Runtime Code Walkthrough for learning-oriented requests and Engineer Fast-Start for maintenance-oriented requests.

### 3. Specific Flow

For composite projects with multiple entrypoints, models, services, or workflows, ask one focused question at a time:

- Which input data should be traced first?
- Which model, backend, service, or workflow should be the main focus?
- Should the guide prioritize training, inference, evaluation, API serving, data processing, or end-to-end operation?

If the user answers "default", follow the primary documented end-to-end path and briefly summarize secondary flows.

## Engineer Fast-Start Mode

Use this mode for experienced engineers who need to operate or modify the project quickly.

Prioritize:

- Overall goal and expected behavior contract
- How to install, configure, run, and test the project
- Entrypoints and startup commands
- CLI/config override rules and important defaults
- Required environment variables and configs
- Core runtime flow at a high level
- Main data contracts and output destinations
- Output file schemas, naming rules, and overwrite behavior
- Input validation and likely error messages
- Key files to modify for common tasks
- Debugging/logging locations
- Acceptance tests and smoke commands
- Explicit project conventions and invariants
- Risky files, hidden coupling, external services, and shape/schema assumptions

Avoid long teaching explanations. Prefer concise tables, command blocks, file references, and practical notes.

## Beginner Full Runtime Code Walkthrough Mode

Use this mode for learning how the code actually executes in detail.

This mode is not a module catalog. Do not mainly list "what each file does" or "what each module is responsible for." Instead, write a full runtime code walkthrough in the order code runs.

Start with a PLAN-style workflow map before the line-level walkthrough:

- Overall goal: what the selected command/workflow is supposed to accomplish.
- Inputs and contracts: CLI args, config fields, files, datasets, models, weights, services, or request payloads.
- Runtime stages: a compact stage table from start command to final output.
- Output contracts: generated files, response schemas, metrics, logs, checkpoints, or UI state.
- Validation/error contracts: what inputs are rejected and where errors should appear.
- Explicit conventions: names, override order, folder layout, GPU/process rules, or other assumptions.

For each walkthrough step, include:

- Step number and plain-language action
- File and exact line or line-range reference when available
- Lines explained: break the step into line-level or small line-range explanations
- Code goal: what these lines are trying to accomplish
- Libraries, classes, functions, and methods used by these lines
- Input data, including shape/schema/type when knowable
- Output data, including shape/schema/type when knowable
- State changes, side effects, files written, network calls, database writes, or model calls
- Next code path: where execution goes next
- Evidence label: Confirmed, Runtime verified, Static inference, or Unknown
- Beginner note: the concept a newcomer should understand before continuing

Use line numbers from the repository whenever possible. If exact line numbers are unstable or dynamic dispatch hides the path, say so and cite the closest function/class/file evidence.

For every important call, explain both sides:

- The caller line: why this code calls the function/class/method.
- The callee line or function: what code runs next.
- The input passed into the call.
- The output returned by the call.
- The next line or file reached after the call returns.

If a file is important but not reached in the selected runtime path, mention it only in "Where to read next"; do not turn the walkthrough into a file inventory.

## General Workflow

1. Inspect top-level context: README, package metadata, dependency files, config files, scripts, Docker files, notebooks, source directories, and tests.
2. Identify project type: backend, frontend, CLI, library, ML training, ML inference, data pipeline, worker system, desktop/mobile app, or mixed system.
3. Resolve language, guide mode, and specific flow using the clarification rules above.
4. Find entrypoints from docs, package scripts, Makefiles, Dockerfiles, main blocks, route registration, CLI definitions, notebooks, or framework conventions.
5. Trace the selected runtime flow from entrypoint to output.
6. Trace data sources, transformations, schemas, tensor shapes, and destinations.
7. Identify core modules, classes, functions, loops, pipelines, services, and workflows relevant to the selected mode.
8. Explain major dependencies by their role in the selected flow.
9. Identify tests, debug commands, logs, and safe validation paths.
10. Write one `PROJECT_CODE_GUIDE.md` using the matching template.
11. Clearly label confirmed facts, runtime-verified facts, static inferences, and unknowns.

## Reference Files

Load these references when needed:

- `references/project-guide-template.md`: Mode-specific output structures for `PROJECT_CODE_GUIDE.md`.
- `references/analysis-checklist.md`: Mode-specific inspection checklist.

## Data and Shape Tracking

Treat "shape" as a broad data contract, not only tensor dimensions.

Trace whichever data forms apply:

- Tensor shapes, such as `[B, C, H, W]`, `[B, T]`, `[B, T, D]`, or `[B, num_classes]`
- Image layouts, such as `[H, W, C]` to `[C, H, W]` to `[B, C, H, W]`
- Tables, including important columns and row meaning
- JSON request/response bodies
- CLI arguments, stdin, config files, and input file paths
- ORM objects, SQL rows, DTOs, service-layer objects, and cache entries
- Queue messages, webhook payloads, cron inputs, and background job payloads

For each important data path, answer:

- Where does the input come from?
- Which file, function, class, route, task, or job reads it?
- What is the raw format?
- What parsing, validation, preprocessing, tokenization, resizing, batching, normalization, or conversion happens?
- What shape, schema, or type exists after each important step?
- What receives the output: model, service, database, response, file writer, metric, checkpoint, UI state, or external API?

If shape information is unclear, write that clearly. Do not invent exact dimensions.

## Evidence Labels

Use these labels in the guide:

- **Confirmed:** Explicitly shown by code, docs, type hints, schemas, tests, comments, or config.
- **Runtime verified:** Checked by a safe command, test, script, dry run, CLI help output, route listing, or minimal sample.
- **Static inference:** Inferred from framework conventions, function signatures, model structure, loss function, or surrounding code.
- **Unknown:** Cannot be determined without missing data, credentials, external services, generated files, sample input, or runtime access.

Put unresolved items in the final "Unknowns and Items That Need Runtime Verification" section.

## Runtime Verification Policy

Prefer safe verification when the project permits it.

Good checks include:

- Run existing tests that do not require external services.
- Run a documented dry-run command.
- Run CLI help or route-list commands.
- Import a parser, route table, dataset, or model in a minimal script.
- Print one sample batch's keys, dtypes, and shapes when sample data is available.

Avoid unsafe execution unless the user explicitly approves:

- Destructive commands
- Long training jobs
- Production database writes
- External service calls that mutate state
- Large downloads
- Commands requiring secrets or credentials

If runtime verification is not possible, rely on static analysis and label the result as static inference or unknown.

## Final Review

Before finishing `PROJECT_CODE_GUIDE.md`, check:

- The selected mode is stated near the top.
- Language choice matches the user request or clarification answer.
- Composite-flow choice is stated if the project has multiple major flows.
- A PLAN-style workflow map appears before detailed mode-specific analysis.
- Data source, input, output, and shape/schema claims have evidence labels.
- Engineer mode includes commands, tests, modification points, and risks.
- Beginner Full Runtime Code Walkthrough mode includes workflow contracts first, then follows actual execution order with exact lines or line ranges, line-level explanations, libraries/methods, inputs, outputs, and next code path.
- Unknowns are explicit.
- No irrelevant personal local paths or machine-specific details are included.
