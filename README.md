# LLM Coding Skills

A curated set of skills for LLM-powered coding assistants. Each skill is a structured prompt that gives your AI assistant deep, opinionated guidance for a specific task type — turning a general-purpose LLM into a focused specialist.

Skills are tool-agnostic and work with **Claude Code**, **Codex**, and **OpenCode**.

## Skills Matrix

| Skill | Go | Python | Terraform |
|-------|----|--------|-----------|
| **policy** | Standards layer for Go design, boundaries, errors, context, concurrency, config, observability, security, and review priorities | Standards layer for Python design, boundaries, exceptions, typing, dependency injection, concurrency, config, observability, security, and review priorities | n/a |
| **workflow** | Execution layer for Go work: tool-first discovery, truth hierarchy, verification depth, and task-mode workflow | Execution layer for Python work: tool-first discovery, truth hierarchy, verification depth, and task-mode workflow | n/a |
| **dev** | Thin implementation mode layered on top of Go policy and workflow | Thin implementation mode layered on top of Python policy and workflow | Write, modify, and review HCL with IaC best practices |
| **audit** | Phased 5-stage deep-dive audit with evidence, chunking, and phase gates | Phased 5-stage deep-dive audit adapted for Python codebases and tooling | Phased 5-stage infrastructure audit: resources, state, security, compliance |
| **docs** | Documentation mode for godoc, README, ADR, API, runbook, changelog, and onboarding work | Generate docstrings (PEP 257), Sphinx/mkdocs, ADRs, runbooks, changelogs | Generate module READMEs, terraform-docs, ADRs, runbooks |
| **test** | Test mode for strategy, unit/integration/e2e coverage, fuzzing, benchmarks, and regression work | Design test strategies, write tests (pytest, hypothesis, parametrize, fixtures) | Design test strategies (terraform test, Terratest, OPA/Rego, checkov) |
| **migrate** | Migration mode for Go versions, dependency swaps, framework changes, architecture shifts, and rollback planning | Plan version upgrades, framework migrations (Flask/Django/FastAPI), packaging modernization | Plan version upgrades, state migrations, module refactoring, backend changes |

## Quick Start

### Install

The installer auto-detects which tools you have and installs skills at the user level for each:

```bash
./install.sh
```

### Selective Install

Install for specific tools or languages:

```bash
# Only Claude Code
./install.sh --tool=claude

# Only Claude Code and OpenCode
./install.sh --tool=claude,opencode

# Only Go and Python skills
./install.sh --lang=go,python

# Combine filters
./install.sh --tool=claude --lang=terraform

# Preview without installing
./install.sh --dry-run
```

### Other Commands

```bash
# List detected tools and all available skills
./install.sh --list

# Remove all installed skills
./install.sh --uninstall

# Remove only Codex skills
./install.sh --uninstall --tool=codex
```

## Using Skills

Once installed, skills are invoked differently depending on your tool:

### Claude Code

Skills are installed as custom slash commands in `~/.claude/commands/`:

```
> /go-dev
> /python-audit
> /terraform-test
```

Pair a skill with your task in the same prompt:

```
> /go-dev Implement the new queue consumer in this repo. Follow TDD.
```

### Codex

Skills are installed in `~/.agents/skills/` and invoked with the `$` prefix:

```
$go-dev
$python-audit
$terraform-test
```

Codex will also auto-select skills based on task descriptions when the skill's trigger conditions match.

### OpenCode

Skills are installed as agents in `~/.config/opencode/agents/` and invoked with the `@` prefix:

```
@go-dev
@python-audit
@terraform-test
```

## Skill Details

### Go policy + workflow

The Go stack now uses a layered model:

- **policy** defines what good Go engineering looks like: package boundaries, interfaces, errors, context, concurrency, config, logging, security, shutdown, and review priorities.
- **workflow** defines how Go work should be executed: repository discovery, tool precedence, truth hierarchy, verification depth, task classification, and uncertainty reporting.
- **dev**, **audit**, **docs**, **test**, and **migrate** are task modes layered on top of policy and workflow.

This gives the Go stack a clearer precedence model and reduces duplication between skills.

### Python policy + workflow

The Python stack now uses the same layered model:

- **policy** defines what good Python engineering looks like: module boundaries, protocols and ABCs, exceptions, typing, dependency injection, concurrency, config, logging, security, shutdown, and review priorities.
- **workflow** defines how Python work should be executed: repository discovery, tool precedence, truth hierarchy, verification depth, task classification, and uncertainty reporting.
- **dev**, **audit**, **docs**, **test**, and **migrate** are task modes layered on top of policy and workflow.

This gives the Python stack the same explicit precedence model and reduces duplicated boilerplate across skills.

### dev (Development Guidance)

For Go and Python, `dev` is now a thin implementation mode layered on top of language-specific policy and workflow. For Terraform, `dev` remains the core coding skill.

### audit (Audit Deep Dive)

A structured 5-phase audit protocol for enterprise-grade codebase review:

1. **Phase 1 — Inventory + Entrypoints**: Catalog files, packages, entry points, startup/shutdown behavior, configuration sources
2. **Phase 2 — Accounting**: Index every function/class/resource with CSV artifacts
3. **Phase 3 — Architecture + Boundaries**: Map data flow, identify boundary violations, assess isolation
4. **Phase 4 — Security + Observability**: Prioritized findings (P0/P1/P2) with evidence and concrete fixes
5. **Phase 5 — Synthesis**: Letter grades, prioritized refactor plan, 90-day roadmap

Each phase has strict gate rules — no recommendations before findings, no grades before synthesis.

### docs (Documentation Guidance)

Covers all documentation types: inline docs (godoc/docstrings/variable descriptions), project docs (READMEs, ADRs, runbooks, changelogs), and API docs (OpenAPI, Sphinx, mkdocs, terraform-docs). Enforces language-specific conventions (godoc format, PEP 257, terraform-docs markers) and requires all documentation to be grounded in actual code.

### test (Test Strategy and Generation)

Covers the full testing spectrum for each language:

- **Go**: Table-driven tests, Ginkgo/Gomega BDD, fuzz testing, benchmarks, golden files, httptest, race detection
- **Python**: pytest fixtures/parametrize, hypothesis property-based testing, async testing, mocking patterns, coverage analysis
- **Terraform**: Native terraform test (.tftest.hcl), Terratest, OPA/Rego policy testing, checkov compliance, plan-time assertions

Includes guidance on test philosophy, coverage analysis, fixture design, and common anti-patterns.

### migrate (Migration Planning)

Structured migration planning with impact analysis, risk assessment, phased execution, and rollback strategies:

- **Go**: Version upgrades, dependency swaps, framework migrations, architecture transitions, database migrations
- **Python**: Version upgrades, framework migrations (Flask/Django/FastAPI), sync-to-async transitions, packaging modernization (setup.py to pyproject.toml)
- **Terraform**: Version upgrades, state migrations (moved/import blocks), module refactoring, backend changes, state splitting, tool migrations (Terraform to OpenTofu)

Core rule: never migrate and refactor simultaneously.

## Versioning

All skills are versioned using a `<!-- version: X.Y.Z -->` comment at the top of each file. The installer detects existing installations and reports:

- **Upgrade**: when the source version is newer than the installed version
- **Downgrade**: when the installed version is newer (warns before overwriting)
- **No change**: when versions match (still overwrites to pick up non-version changes)

Check installed versions with `./install.sh --list`.

## Directory Structure

```
skills/
├── go/
│   ├── audit.skill.md
│   ├── dev.skill.md
│   ├── docs.skill.md
│   ├── migrate.skill.md
│   ├── policy.skill.md
│   ├── test.skill.md
│   └── workflow.skill.md
├── python/
│   ├── audit.skill.md
│   ├── dev.skill.md
│   ├── docs.skill.md
│   ├── migrate.skill.md
│   ├── policy.skill.md
│   ├── test.skill.md
│   └── workflow.skill.md
├── terraform/
│   ├── audit.skill.md
│   ├── dev.skill.md
│   ├── docs.skill.md
│   ├── migrate.skill.md
│   └── test.skill.md
├── install.sh
└── README.md
```
