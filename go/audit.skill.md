<!-- version: 2.0.0 -->
# Go Audit Mode

## Purpose
Use this skill to run a phased, evidence-based deep audit of a Go codebase.

Apply this skill with:
- `policy.skill.md` for evaluation standards
- `workflow.skill.md` for tool-first execution discipline

This mode exists because audit work has materially different output constraints, evidence rules, and sequencing from normal implementation work.

## When To Use
Use this skill when the user asks for:
- a deep Go repository audit
- phased architecture review
- function or package accounting
- observability or security review as part of a broader Go audit
- evidence-backed grading, modernization, or refactor planning

Do not use this skill for:
- small patch reviews
- narrow bug hunts
- ordinary implementation work

## Required Inputs
The invoking prompt must provide:
- repository path or scope
- exact phase to execute

Recommended inputs:
- focus areas
- exclusions
- depth constraints
- how to treat generated or vendored code

If scope or phase is missing, stop and ask.

## Operating Stance
- Prefer evidence over intuition.
- Describe the system as implemented, not as intended.
- Stay phase-disciplined.
- Treat tests, scripts, CI, infra, and docs as first-class evidence.
- Do not collapse multiple phases into one response.

## Evidence Rules
- Every factual claim must be anchored to a file path and, when applicable, a symbol.
- Mark any non-provable conclusion as `INFERENCE`.
- List inaccessible or unreviewed material under `UNREVIEWED/INACCESSIBLE` with impact notes.
- Do not imply runtime certainty without code, config, test, or runtime evidence.

## Output Contract
- Output only Markdown.
- Machine-readable artifacts must be fenced `csv` or `json`.
- If a hard requirement cannot be met, output exactly:

```text
ERROR: <short reason>
BLOCKED_BY: <what is missing>
```

## Chunking Rules
- Work only on the requested phase.
- Stop at the end of the phase boundary.
- Chunk large artifacts rather than compressing them inaccurately.
- End every response with:

```text
STATE_SNAPSHOT: (max 8 bullets)
- <bullet>

NEXT: <exact next phase name>
```

## Phase Gate Rules
- Phase 1 may inventory and describe, but must not recommend.
- Phase 2 may account and index, but must not recommend or grade.
- Phase 3 may assess architecture and boundary violations, but must not produce detailed remediation plans.
- Phase 4 may produce prioritized findings with fixes, but must not assign overall grades.
- Phase 5 may synthesize, grade, prioritize, and plan.

## Phase Rules

### PHASE 1 - Inventory + Entrypoints
Produce:
- repository inventory grouped by directory
- one-line purpose and importance tag for each directory
- one-line purpose for each file
- key exported symbols for Go files
- entrypoints, startup, shutdown, config, and secret source summary where evidenced
- totals and `UNREVIEWED/INACCESSIBLE`

### PHASE 2 - Function Accounting
Produce exactly:
- `function_index.csv`
- `package_index.csv`

Rules:
- one row per function or method, including `init`, `main`, and tests
- chunk outputs to 500 rows max per file part
- leave caller or callee fields blank when precision is not supportable and note `INFERENCE`

### PHASE 3 - Architecture + Data Boundaries
Using phase 1 and 2 evidence:
- describe architecture as implemented
- map ingress and egress
- identify validation points and missing validation points
- identify leakage between transport, domain, and persistence
- assess transaction boundaries, idempotency, and dependency direction

### PHASE 4 - Observability + Security Audit
Review:
- logging structure and correlation
- metrics, tracing, health checks, shutdown, drain behavior
- trust boundaries, authn/authz, input validation, injection risks, path handling, secret handling

Output findings grouped by `P0`, `P1`, and `P2`, each with:
- file path
- symbol
- evidence
- concrete fix

### PHASE 5 - Synthesis
Produce:
- overall grade `A-F`
- subgrades for code, architecture, observability, security, testing, performance, modularity, docs/DX
- anchored justification
- prioritized refactor recommendations with `P0`, `P1`, and `P2`
- effort sizing `S`, `M`, `L`

## Completion Rule
An audit response is incomplete if it:
- mixes phases
- makes unsupported claims
- omits required artifacts
- grades before synthesis
- recommends fixes before the proper phase

## Invocation Template
Use this skill with a prompt that supplies repository-specific context. Example:

```text
Use Go Audit Mode with Go Engineering Policy and Go Engineering Workflow.
Audit /path/to/repo.
Execute PHASE 3 - Architecture + Data Boundaries.
Focus on package direction, shutdown behavior, and queue consumers.
Summarize generated code instead of expanding it.
```
