---
name: understand-codebase
description: Generate a single beginner-friendly but engineer-useful PROJECT_CODE_GUIDE.md for an unfamiliar codebase. Use when the user asks to understand a project, find entrypoints/config/core classes, explain module execution, trace data sources and outputs, inspect tensor shapes or data contracts, understand training/inference/API/CLI/data-processing flows, identify key loops or pipelines, or create a guided Markdown overview for learning code.
---

# Understand Codebase

Use this skill to turn an unfamiliar repository into one coherent learning guide: `PROJECT_CODE_GUIDE.md`.

Act like a code-reading tutor first and a handoff engineer second. Explain what the project does, how it runs, where data comes from, how data changes shape or schema, which files matter most, and what a newcomer should read in order.

## Output Contract

Generate one Markdown file named `PROJECT_CODE_GUIDE.md` at the repository root unless the user requests another path.

Default the guide language to English. If the user explicitly requests another language, use it. If the user writes in a non-English language but does not state the guide language, ask one short question before writing: "Should I write the guide in English or <detected language>?" If the user answers "default", use English.

Use a beginner-friendly teaching style:

- Explain what each important component does.
- Explain why it matters in this project.
- Identify what to read first, next, later, and what to skip initially.
- Add engineer quick anchors: key files, functions/classes, commands, configs, call chains, and modification risks.

## Workflow

1. Inspect top-level context: README, package metadata, dependency files, config files, scripts, Docker files, notebooks, source directories, and tests.
2. Identify the project type: backend, frontend, CLI, library, ML training, ML inference, data pipeline, worker system, desktop/mobile app, or mixed system.
3. If the project has multiple major flows and the user's target is ambiguous, ask one focused question at a time:
   - Which input data should be traced first?
   - Which model, backend, service, or workflow should be the main focus?
   - Should the guide prioritize training, inference, evaluation, API serving, data processing, or end-to-end operation?
4. If the user says "default" or has no preference, follow the primary documented end-to-end path and briefly summarize secondary flows.
5. Find entrypoints from docs, package scripts, Makefiles, Dockerfiles, main blocks, route registration, CLI definitions, notebooks, or framework conventions.
6. Map directories by importance rather than listing every file.
7. Trace the core runtime flow from entrypoint to output.
8. Trace data sources, transformations, schemas, tensor shapes, and destinations.
9. Identify core modules, classes, functions, loops, pipelines, services, and workflows.
10. Explain major dependencies by their role in this project.
11. Identify tests, debug commands, logs, and safe validation paths.
12. Write `PROJECT_CODE_GUIDE.md`.
13. Clearly label confirmed facts, runtime-verified facts, static inferences, and unknowns.

## Reference Files

Load these references only when needed:

- `references/project-guide-template.md`: Use as the output structure for `PROJECT_CODE_GUIDE.md`.
- `references/analysis-checklist.md`: Use as the inspection checklist while reading a repository.

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

## Writing Rules

Use the template reference unless the project clearly needs a small adaptation.

Keep the guide practical:

- Prefer important files over exhaustive lists.
- Include Mermaid diagrams only when they make flow easier to understand.
- Explain library roles in this project, not generic package descriptions.
- Mark generated, vendored, build, and cache files as "skip initially" unless central.
- Include modification risks where changing a file could affect many paths.

Before finishing, scan `PROJECT_CODE_GUIDE.md` for:

- Missing entrypoint or startup explanation
- Missing data source and output explanation
- Unlabeled guesses
- Overly long file dumps
- Missing recommended reading order
- Personal local paths or machine-specific details that do not belong in the analyzed project
