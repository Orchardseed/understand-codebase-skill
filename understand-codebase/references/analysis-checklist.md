# Analysis Checklist

Use this checklist while inspecting a repository. Keep the final guide aligned with the selected mode.

## 1. Clarification Checklist

Resolve these before writing:

- Language: English by default, or user-requested language.
- Guide mode:
  - Engineer Fast-Start
  - Beginner Full Runtime Code Walkthrough
  - Both
- Composite flow focus:
  - Input data to trace
  - Model/service/backend/workflow to trace
  - Training, inference, evaluation, API serving, data processing, or end-to-end operation

Infer when obvious. Ask one focused question when unclear.

## 2. Top-Level Context

- Read README, docs, examples, notebooks, and comments that explain purpose.
- Treat README/docs as the first source for the project's operating model: what users run, what data they provide, what outputs they expect, and what issues they hit.
- Inspect dependency files such as `package.json`, `pyproject.toml`, `requirements.txt`, `Cargo.toml`, `go.mod`, `pom.xml`, or `environment.yml`.
- Inspect scripts, Makefiles, Dockerfiles, compose files, CI workflows, and task runners.
- Identify generated, vendored, build, cache, and artifact directories so they can be skipped initially.

## 2A. README / Docs Runbook Extraction

Capture from README and user-facing docs when available:

- Project purpose and what it provides
- Install/environment requirements
- Repository layout
- Data/input formats and required columns, keys, fields, shapes, or files
- Preparation or preprocessing steps
- Main commands for training, inference, evaluation, serving, UI, workers, CLIs, or data processing
- Config files, important fields, defaults, and override priority
- Output files, responses, logs, checkpoints, metrics, naming rules, and overwrite behavior
- Post-run utilities and visualization/reporting commands
- Multi-process, GPU, service, database, or external dependency assumptions
- Common issues and debugging advice

Then check important documentation claims against code, configs, tests, or safe runtime commands. Mark each as Confirmed, Runtime verified, Static inference, Unknown, or Mismatch.

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

- Overall goal and expected post-run behavior
- README/docs-derived operating summary
- Install command
- Run command
- Test command
- Command cookbook for common operations
- Debug/log commands and locations
- CLI arguments, config fields, defaults, and override order
- Input validation rules and expected error behavior
- Required configs and environment variables
- Primary entrypoint and high-level flow
- Workflow coverage matrix across major documented flows
- Workflow stage map: consumes, does, produces, failure cases
- Main data contracts and outputs
- Output file/response/log/checkpoint schemas and naming rules
- README/docs claims versus code evidence
- Common issues and debugging map
- Common modification tasks and files
- Risky files and hidden coupling
- External service assumptions
- Commands that were run and commands not run
- Explicit conventions and invariants future edits must preserve

Prefer concise tables and file references.

## 6. Beginner Full Runtime Code Walkthrough Checklist

Use this when the selected mode is Beginner Full Runtime Code Walkthrough.

Trace code in execution order. For each step, capture:

- README/docs-derived project learning route before selecting the runtime path
- Workflow coverage matrix for major flows, such as preprocessing, training, inference, evaluation, visualization, serving, workers, or UI operation
- PLAN-style workflow map before line-level analysis:
- Overall goal and expected behavior
- CLI/config/input/model/output contracts
- Runtime stage map
- Validation/error contracts
- Explicit conventions and invariants
- README/docs claims versus code evidence
- Step number
- Plain-language action
- File and exact line number or tight line range, or closest function/class when exact lines are not reliable
- Lines explained, with one explanation per important line or tight line range
- Code goal completed by those exact lines
- Libraries/classes/functions/methods used
- Input variable/data, source, shape/schema/type, and evidence
- Operations performed by each line or line range
- Output variable/data, destination, shape/schema/type, and evidence
- State changes or side effects
- Next code path, including file/line/function reached next
- Caller/callee relationship for important local calls
- Beginner note

This mode should feel like following a debugger plus a teacher explaining each important line. Avoid replacing the walkthrough with a module catalog, file inventory, or responsibility list.

Use the workflow map to decide which code path to expand first. The line-level walkthrough should explain how the code implements each workflow stage.

Do not shorten the walkthrough just because the generated markdown is long. Use clear navigation and headings, but keep the detail needed for a beginner to follow the code.

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

For Beginner Full Runtime Code Walkthrough mode:

- Prefer exact line numbers from the current repository.
- Use tight line ranges when one line alone does not explain a complete action.
- Cite function/class names when line numbers are unavailable, and mark the evidence as Unknown or Static inference.
- Track external library calls used in the selected path.
- Track local function calls in the order execution reaches them.
- For each important call, record caller line, callee function/class/method, input arguments, return value, and where execution resumes.
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

In Beginner Full Runtime Code Walkthrough mode, emphasize dependencies actually used in the selected runtime path.

## 11. Final Review

Before finishing the guide, check:

- The selected mode is named near the top.
- Startup and entrypoints are explained.
- README/docs were read when present, and their commands, configs, data formats, outputs, and common issues are reflected.
- The guide includes a PLAN-style workflow map: goal, contracts, stages, outputs, validation/errors, and conventions.
- Composite projects include a workflow coverage matrix and state which path is expanded.
- Data sources and outputs are traced.
- Shape/schema claims have evidence labels.
- Engineer Fast-Start mode includes run/test/debug/modify guidance.
- Beginner Full Runtime Code Walkthrough mode connects the workflow map to execution order with exact lines or tight line ranges, line-level explanations, libraries/methods, inputs, outputs, caller/callee transitions, and next code path.
- Important README/docs claims are confirmed, runtime verified, marked as static inference, marked unknown, or flagged as mismatches.
- Important detail was not omitted for brevity.
- Unknowns are explicit.
- No irrelevant personal local paths are included.
