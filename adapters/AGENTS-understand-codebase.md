# understand-codebase Agent Instructions

Use these instructions when asked to understand an unfamiliar project and generate a guided codebase overview.

## Goal

Create one file at the repository root unless the user requests another path:

```text
PROJECT_CODE_GUIDE.md
```

Write the guide as a beginner-friendly code reading tutorial with engineer quick-start anchors.

## Language

Default to English.

If the user explicitly requests another language, use it. If the user writes in a non-English language but does not state the guide language, ask whether to write the guide in English or that language. If the user says "default", use English.

## Composite Projects

If the project has multiple major flows and the user's goal is ambiguous, ask one focused question at a time:

- Which input data should be traced first?
- Which model, service, backend, or workflow should be the main focus?
- Should the guide prioritize training, inference, evaluation, API serving, data processing, or end-to-end operation?

If the user chooses "default", follow the primary documented end-to-end path and briefly summarize secondary flows.

## Analysis Workflow

1. Inspect README, docs, package metadata, dependency files, config files, scripts, Docker files, notebooks, source directories, and tests.
2. Identify project type: backend, frontend, CLI, library, ML training, ML inference, data pipeline, worker system, or mixed system.
3. Find entrypoints from startup scripts, main blocks, route registration, CLI definitions, Docker commands, Makefiles, notebooks, or framework conventions.
4. Map directories by importance rather than listing every file.
5. Trace the primary runtime flow from entrypoint to output.
6. Trace data sources, transformations, shape/schema changes, and destinations.
7. Identify core modules, classes, functions, loops, services, and workflows.
8. Explain major dependencies by their role in this project.
9. Identify tests, debug commands, logs, and safe validation paths.
10. Write `PROJECT_CODE_GUIDE.md`.

## Required Guide Sections

Use these sections unless the project clearly needs a small adaptation:

```markdown
# Project Code Guide

## 1. Project Overview
## 2. Quick Start, Entrypoints, and Runtime Commands
## 3. Directory Map
## 4. Recommended Reading Order
## 5. Core Runtime Flow
## 6. Data Sources, Data Flow, and Shape Tracking
## 7. Core Modules, Classes, and Functions
## 8. Key Loops, Pipelines, and Workflows
## 9. Configuration, Environment Variables, and Parameters
## 10. Main Dependencies and Their Roles
## 11. Testing, Debugging, and Logging
## 12. Notes for Future Code Changes
## 13. Unknowns and Items That Need Runtime Verification
```

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

Before finishing, ensure the guide has a practical reading order, clear entrypoints, explicit data sources and outputs, labeled shape/schema claims, and an unknowns section.
