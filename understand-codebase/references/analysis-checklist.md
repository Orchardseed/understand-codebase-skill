# Analysis Checklist

Use this checklist while inspecting a repository. Keep the final guide focused on what helps a newcomer learn the project.

## 1. Top-Level Context

- Read README, docs, examples, notebooks, and comments that explain purpose.
- Inspect dependency files such as `package.json`, `pyproject.toml`, `requirements.txt`, `Cargo.toml`, `go.mod`, `pom.xml`, or `environment.yml`.
- Inspect scripts, Makefiles, Dockerfiles, compose files, CI workflows, and task runners.
- Identify generated, vendored, build, cache, and artifact directories so they can be skipped initially.

## 2. Project Type

Classify the project as one or more:

- Web backend
- Frontend
- CLI
- Library
- ML training
- ML inference
- Data processing
- Worker or scheduler
- Desktop or mobile app
- Mixed or composite system

## 3. Composite Project Narrowing

If several flows are plausible, ask one focused question at a time:

- Which input data should be traced first?
- Which model, service, backend, or workflow should be the focus?
- Should the guide prioritize training, inference, evaluation, API serving, data processing, or end-to-end operation?

If the user chooses "default", use the primary documented path and summarize secondary paths.

## 4. Entrypoint Discovery

Look for:

- Package scripts
- `main()` functions or `if __name__ == "__main__"` blocks
- CLI registrations
- Route registration
- Framework bootstraps
- Docker `CMD` and `ENTRYPOINT`
- Makefile targets
- Notebook execution order
- Training or inference scripts
- Worker startup commands

Label each entrypoint as confirmed, runtime verified, static inference, or unknown.

## 5. Runtime Flow

Trace:

- Startup command
- First file reached
- Config loading
- Dependency initialization
- Primary orchestration function
- Core service/model/pipeline call
- Output creation

Prefer one main flow plus short notes for secondary flows.

## 6. Data and Shape Trace

For each important path, capture:

- Source: file, HTTP request, database, queue, external API, CLI args, config, Dataset, or user input
- Reader: file/function/class/route/job
- Raw format: JSON, CSV, image, tensor, text, SQL row, DataFrame, DTO, etc.
- Transformations: parse, validate, clean, tokenize, resize, normalize, batch, reshape, permute, encode, decode
- Intermediate data contract: shape, schema, dtype, keys, class type, table columns
- Destination: model, service, DB write, response, file writer, checkpoint, metrics, UI state

Use evidence labels:

- Confirmed
- Runtime verified
- Static inference
- Unknown

## 7. Shape Verification Opportunities

Safe checks include:

- Run a small test that already exists.
- Run CLI help or dry-run commands.
- Import a parser, dataset, model, or route table.
- Print one sample batch's keys, dtypes, and shapes if sample data exists.
- Inspect tests or fixtures for realistic data examples.

Avoid:

- Long training runs
- Production writes
- Destructive commands
- External mutations
- Large downloads
- Secret-dependent checks without user approval

## 8. Core Code Identification

Find:

- Orchestration modules
- Core classes
- Public APIs
- Service classes
- Model definitions
- Dataset or parser code
- Transform and validation code
- Writers and response builders
- Tests that describe expected behavior

Skip initially:

- Generated code
- Vendored dependencies
- Build outputs
- Cache directories
- Low-level utilities unless they control the main flow

## 9. Dependency Explanation

For each major dependency, explain its role in this project:

- Framework
- Model/training library
- Data processing library
- Validation/schema library
- Database/ORM client
- HTTP/API client
- UI library
- Testing/debugging tool

Do not turn this into a generic package encyclopedia.

## 10. Reading Order

Recommend a sequence:

1. Short purpose doc or package metadata
2. Startup script or entrypoint
3. Config loading
4. Main orchestration module
5. Data loading and preprocessing
6. Core model/service/pipeline
7. Output/writer/response layer
8. Tests that clarify behavior
9. Supporting utilities

Each step should say what the reader should understand before moving on.

## 11. Final Review

Before finishing the guide, check:

- One clear project overview exists.
- Startup and entrypoints are explained.
- A practical reading order exists.
- Data sources and outputs are traced.
- Shape/schema claims have evidence labels.
- Core modules are explained by responsibility.
- Key loops or workflows are explained.
- Dependencies are explained by project role.
- Unknowns are explicit.
- No irrelevant personal local paths are included.
