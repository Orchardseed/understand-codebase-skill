# understand-codebase Agent Instructions

Use these instructions when asked to understand an unfamiliar project and generate a guided codebase overview.

## Goal

Create one file at the repository root unless the user requests another path:

```text
PROJECT_CODE_GUIDE.md
```

Choose a guide mode before writing.

## Language

Default to English.

If the user explicitly requests another language, use it. If the user writes in a non-English language but does not state the guide language, ask whether to write the guide in English or that language. If the user says "default", use English.

## Guide Modes

### Engineer Fast-Start

Use for quick handoff, onboarding, running, testing, debugging, modifying, entrypoints, configs, and risks.

Include:

- Install/run/test/debug commands
- Entrypoints and high-level runtime flow
- Config and environment variables
- Main data contracts and outputs
- Files to modify for common tasks
- Risky files and hidden coupling
- Unknowns and checks not run

### Beginner Full Runtime Code Walkthrough

Use for learning how the code actually executes in full detail.

Do not write a module catalog or file responsibility list. Follow the runtime path like a debugger and explain the important lines like a teacher. For each step include:

- File and exact line or tight line-range reference
- Lines explained, with one explanation per important line or tight line range
- Code goal completed by those exact lines
- Libraries/classes/functions/methods used
- Input source, shape/schema/type, and evidence
- What happens
- Output destination, shape/schema/type, and evidence
- Caller/callee relationship for important local calls
- Next code path
- Beginner note

### Both

If the user asks for both, write a concise Engineer Fast-Start section first, then the detailed Beginner Runtime Tutorial.

## Clarification

Infer the mode when obvious. If unclear, ask:

```text
Which guide style do you want?

1. Engineer Fast-Start: quick handoff for running, testing, debugging, and modifying code.
2. Beginner Full Runtime Code Walkthrough: full-flow learning guide with exact lines or line ranges, code goals, libraries/methods, inputs, outputs, and next code path.
3. Both: engineer summary first, then beginner runtime walkthrough.
```

For composite projects, ask one focused question at a time:

- Which input data should be traced first?
- Which model, service, backend, or workflow should be the main focus?
- Should the guide prioritize training, inference, evaluation, API serving, data processing, or end-to-end operation?

If the user chooses "default", follow the primary documented end-to-end path and briefly summarize secondary flows.

## Data and Shape Tracking

Treat shape as a broad data contract:

- Tensor shape: `[B, C, H, W]`, `[B, T]`, `[B, T, D]`, `[B, num_classes]`
- Image layout: `[H, W, C]`, `[C, H, W]`
- Tables: rows, columns, important fields
- JSON: keys, nested arrays, required fields
- Objects: DTOs, ORM rows, service outputs
- Runtime payloads: API requests, queue messages, webhooks, CLI args, config files

For each important data path, explain:

- Source
- Reader
- Raw format
- Transformations
- Intermediate shape/schema/type
- Destination
- Evidence label

## Evidence Labels

Use these labels:

- Confirmed: shown by code, docs, schemas, tests, comments, or config
- Runtime verified: checked by a safe command, test, dry run, CLI help, route listing, or minimal sample
- Static inference: inferred from conventions, signatures, model structure, or surrounding code
- Unknown: cannot be determined from available code and safe checks

## Safety

Run safe verification commands when useful. Do not run destructive commands, long training jobs, production writes, external mutations, large downloads, or secret-dependent commands without explicit user approval.

Before finishing, ensure the guide names the selected mode, has clear entrypoints, explicit data sources and outputs, labeled shape/schema claims, and an unknowns section.
