# Analysis Checklist

Use this checklist while inspecting a repository. Keep the final guide aligned with the selected mode.

## 1. Clarification Checklist

Resolve these before writing:

- Language: English by default, or user-requested language.
- Guide mode:
  - Engineer Fast-Start
  - Beginner Runtime Tutorial
  - Both
- Composite flow focus:
  - Input data to trace
  - Model/service/backend/workflow to trace
  - Training, inference, evaluation, API serving, data processing, or end-to-end operation

Infer when obvious. Ask one focused question when unclear.

## 2. Top-Level Context

- Read README, docs, examples, notebooks, and comments that explain purpose.
- Inspect dependency files such as `package.json`, `pyproject.toml`, `requirements.txt`, `Cargo.toml`, `go.mod`, `pom.xml`, or `environment.yml`.
- Inspect scripts, Makefiles, Dockerfiles, compose files, CI workflows, and task runners.
- Identify generated, vendored, build, cache, and artifact directories so they can be skipped initially.

## 3. Project Type

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

## 5. Engineer Fast-Start Checklist

Use this when the selected mode is Engineer Fast-Start.

Capture:

- Install command
- Run command
- Test command
- Debug/log commands and locations
- Required configs and environment variables
- Primary entrypoint and high-level flow
- Main data contracts and outputs
- Common modification tasks and files
- Risky files and hidden coupling
- External service assumptions
- Commands that were run and commands not run

Prefer concise tables and file references.

## 6. Beginner Runtime Tutorial Checklist

Use this when the selected mode is Beginner Runtime Tutorial.

Trace code in execution order. For each step, capture:

- Step number
- Plain-language action
- File and line number, or closest function/class when exact lines are not reliable
- Code goal
- Libraries/classes/functions/methods used
- Input variable/data, source, shape/schema/type, and evidence
- Operations performed
- Output variable/data, destination, shape/schema/type, and evidence
- State changes or side effects
- Next code path
- Beginner note

This mode should feel like following a debugger. Avoid replacing the walkthrough with a module catalog.

## 7. Data and Shape Trace

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

## 8. Shape Verification Opportunities

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

## 9. Line and Method Tracing

For Beginner Runtime Tutorial mode:

- Prefer exact line numbers from the current repository.
- Cite function/class names when line numbers are unavailable.
- Track external library calls used in the selected path.
- Track local function calls in the order execution reaches them.
- Note dynamic dispatch, plugin registries, reflection, callbacks, decorators, or framework magic as uncertainty when needed.

## 10. Dependency Explanation

For each major dependency, explain its role in this project:

- Framework
- Model/training library
- Data processing library
- Validation/schema library
- Database/ORM client
- HTTP/API client
- UI library
- Testing/debugging tool

In Beginner Runtime Tutorial mode, emphasize dependencies actually used in the selected runtime path.

## 11. Final Review

Before finishing the guide, check:

- The selected mode is named near the top.
- Startup and entrypoints are explained.
- Data sources and outputs are traced.
- Shape/schema claims have evidence labels.
- Engineer Fast-Start mode includes run/test/debug/modify guidance.
- Beginner Runtime Tutorial mode follows execution order with line references, libraries/methods, inputs, outputs, and next code path.
- Unknowns are explicit.
- No irrelevant personal local paths are included.
