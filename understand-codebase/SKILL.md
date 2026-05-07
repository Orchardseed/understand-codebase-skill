---
name: understand-codebase
description: Generate a single PROJECT_CODE_GUIDE.md for understanding an unfamiliar codebase, with selectable guide modes. Use Engineer Fast-Start mode when the user needs a README-style runbook for running, testing, debugging, modifying, or quickly onboarding to a project. Use Beginner Full Runtime Code Walkthrough mode when the user wants a detailed learning guide that first maps the project workflow and then follows the actual execution path line by line or line-range by line-range, explaining which code completes what goal, which libraries/classes/functions/methods are used, inputs, outputs, data shapes or schemas, and the next code path. Also use for finding entrypoints/config/core classes, tracing data sources and outputs, understanding training/inference/API/CLI/data-processing flows, identifying loops or pipelines, or creating a guided Markdown overview.
---

# Understand Codebase

Use this skill to turn an unfamiliar repository into one coherent guide: `PROJECT_CODE_GUIDE.md`.

The skill supports two distinct guide modes. Do not blend them into a vague hybrid unless the user asks for both.

## Output Depth Policy

Do not impose an artificial size limit on the generated `PROJECT_CODE_GUIDE.md`. Make the guide as detailed as the selected mode and project complexity require.

Be concise in summaries, but fully expand sections that are important for understanding, running, debugging, modifying, or learning the code:

- Full runtime walkthrough steps
- Line or tight line-range explanations
- Caller/callee transitions
- Input/output shape, schema, and data provenance
- Config, CLI, output, validation, and error contracts
- Multi-stage project workflows
- README/documentation claims that must be checked against code

If the guide becomes long, improve navigation with a table of contents, clear section headings, and workflow stage links. Do not remove necessary detail just to shorten the file.

## README-Style Runbook Context

Before tracing code, read project-facing documentation when present:

- `README*`
- `docs/`, `examples/`, `notebooks/`, tutorials, quickstarts, and usage guides
- CLI help text, package scripts, Makefiles, Docker files, CI workflows, and config examples

Extract the project's operating model from those docs:

- What the project provides
- Environment and dependency requirements
- Repository layout
- Data/input formats
- Preprocessing or preparation steps
- Training, inference, evaluation, API, CLI, UI, worker, or data-processing commands
- Config fields, defaults, and override order
- Output files, response schemas, logs, checkpoints, metrics, naming, and overwrite behavior
- Common issues, debugging advice, and known limitations

Then compare documentation claims with code evidence. Mark each important claim as confirmed, runtime verified, static inference, or unknown. If docs and code disagree, call that out explicitly.

## PLAN-Style Workflow Map

Before writing detailed sections, build a workflow map similar to a project implementation plan:

1. State the overall goal and expected behavior.
2. Identify the major workflows exposed by the project, such as preprocessing, training, inference, evaluation, visualization, serving, background jobs, or UI operation.
3. Identify the user-facing commands, config files, inputs, weights/models/services, outputs, and validation checks.
4. Summarize each selected workflow as stages, with each stage describing what is consumed, what work is done, what is produced, and what can fail.
5. Record explicit conventions, such as preferred CLI names, config override order, output file naming, and assumptions about GPU/process/model behavior.
6. Use this workflow map as the backbone for both guide modes.

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
- README/docs-derived operating summary
- How to install, configure, run, and test the project
- Workflow coverage matrix across major documented flows
- Command cookbook with copyable commands and what each command proves or produces
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
- Documentation claims versus code evidence
- Risky files, hidden coupling, external services, and shape/schema assumptions

Avoid long teaching explanations. Prefer concise tables, command blocks, file references, and practical notes.

## Beginner Full Runtime Code Walkthrough Mode

Use this mode for learning how the code actually executes in detail.

This mode is not a module catalog. Do not mainly list "what each file does" or "what each module is responsible for." Instead, write a full runtime code walkthrough in the order code runs.

Start with a README-style project learning route and PLAN-style workflow map before the line-level walkthrough:

- Overall goal: what the selected command/workflow is supposed to accomplish.
- Full project workflow map: what major workflows exist and which one is expanded in detail.
- Inputs and contracts: CLI args, config fields, files, datasets, models, weights, services, or request payloads.
- Runtime stages: a compact stage table from start command to final output.
- Output contracts: generated files, response schemas, metrics, logs, checkpoints, or UI state.
- Validation/error contracts: what inputs are rejected and where errors should appear.
- Explicit conventions: names, override order, folder layout, GPU/process rules, or other assumptions.
- Documentation claims versus code evidence: what the README/docs say and whether code confirms it.

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
2. Build a docs-derived runbook map: purpose, commands, workflows, configs, data contracts, outputs, and common issues.
3. Identify project type: backend, frontend, CLI, library, ML training, ML inference, data pipeline, worker system, desktop/mobile app, or mixed system.
4. Resolve language, guide mode, and specific flow using the clarification rules above.
5. Find entrypoints from docs, package scripts, Makefiles, Dockerfiles, main blocks, route registration, CLI definitions, notebooks, or framework conventions.
6. Trace the selected runtime flow from entrypoint to output.
7. Trace data sources, transformations, schemas, tensor shapes, and destinations.
8. Identify core modules, classes, functions, loops, pipelines, services, and workflows relevant to the selected mode.
9. Explain major dependencies by their role in the selected flow.
10. Identify tests, debug commands, logs, and safe validation paths.
11. Compare important README/docs claims with code evidence.
12. Write one `PROJECT_CODE_GUIDE.md` using the matching template, with no artificial length cap.
13. Clearly label confirmed facts, runtime-verified facts, static inferences, and unknowns.

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
- README/docs-derived workflows, commands, configs, outputs, and common issues are reflected when available.
- A PLAN-style workflow map appears before detailed mode-specific analysis.
- Data source, input, output, and shape/schema claims have evidence labels.
- Engineer mode includes commands, tests, modification points, and risks.
- Beginner Full Runtime Code Walkthrough mode includes workflow contracts first, then follows actual execution order with exact lines or line ranges, line-level explanations, libraries/methods, inputs, outputs, and next code path.
- The guide does not omit important detail merely to stay short.
- Important README/docs claims are either confirmed, runtime verified, marked as static inference, marked unknown, or flagged as mismatches.
- Unknowns are explicit.
- No irrelevant personal local paths or machine-specific details are included.
