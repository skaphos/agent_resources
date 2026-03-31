<!-- SPDX-FileCopyrightText: 2026 Skaphos -->
<!-- SPDX-License-Identifier: MIT -->

<!-- version: 0.2.0 -->
# Kubernetes Audit Deep Dive

## Purpose
Use this skill for a phased, evidence-based audit of Kubernetes manifests and platform configuration.

This skill is the audit contract for workload boundaries, security posture, operability, policy conformance, and deployment safety.

## Skill Use
- Load this skill when the user explicitly wants a deep Kubernetes manifest or platform audit.
- Treat this skill as the governing audit contract for the turn or session.
- Keep repository-specific scope, focus areas, and exclusions in the invoking prompt.
- Execute only the requested phase and stop at the phase boundary.

## When To Use
Use this skill for:
- deep manifest audits
- namespace or platform boundary reviews
- security and RBAC reviews as part of a broader workload assessment
- operational readiness reviews for production deployments
- evidence-backed API cleanup or upgrade-planning work

Do not use this skill for:
- ordinary manifest edits
- narrow rollout debugging without broader audit intent
- one-change review without repository-level audit scope

## Required Inputs
The invoking prompt must provide:
- repository path or manifest scope
- exact phase to execute

Recommended inputs:
- namespaces, workloads, or overlays to emphasize
- exclusions
- whether rendered output or source manifests are the source of truth
- previous phase artifacts or `STATE_SNAPSHOT` when continuing

If scope or phase is missing, stop and ask.

## Operating Stance
- Prefer evidence over intuition.
- Describe the platform behavior as implemented, not as intended.
- Stay phase-disciplined.
- Separate configuration defects from missing operational evidence.
- Treat manifests, overlays, policies, RBAC, generated output, tests, and deployment tooling as first-class evidence.

## Evidence Rules
- Every factual claim must be anchored to a file path and resource name and, when applicable, a namespace, kind, or patch target.
- Mark any non-provable conclusion as `INFERENCE`.
- List inaccessible or unreviewed material under `UNREVIEWED/INACCESSIBLE` with impact notes.
- Do not imply cluster-runtime certainty unless it is supported by manifests, rendered output, tests, controller behavior, or docs.

## Output Contract
- Output only Markdown.
- Machine-readable artifacts must be fenced `csv` or `json`.
- If a hard requirement cannot be met, output exactly:

```text
ERROR: <short reason>
BLOCKED_BY: <what is missing>
```

## Chunking And Continuation Rules
- Work only on the requested phase.
- Stop at the end of the phase boundary.
- Chunk large artifacts rather than compressing them inaccurately.
- When a phase is too large for one response, emit the current chunk, preserve artifact part names, and set `NEXT` to the exact remaining step or artifact part.
- If required information is missing, stop and identify exactly what is missing instead of guessing.
- End every response with:

```text
STATE_SNAPSHOT: (max 8 bullets)
- <bullet>

NEXT: <exact next phase name>
```

## General Audit Method
1. Establish accessible manifest scope and obvious exclusions.
2. Build a fast inventory of workloads, services, ingress, config, RBAC, policy objects, overlays, and deployment assets.
3. Read the files relevant to the current phase before making conclusions.
4. Build inventories or rendered evidence before evaluative claims.
5. Preserve phase boundaries strictly.

## Phase Gate Rules
- Phase 1 may inventory and describe, but must not recommend.
- Phase 2 may account and index, but must not recommend or grade.
- Phase 3 may assess workload boundaries, rollout behavior, and API hygiene, but must not produce detailed remediation plans.
- Phase 4 may produce prioritized findings with fixes, but must not assign overall grades.
- Phase 5 may synthesize, grade, prioritize, and plan.

## Phase Rules

### PHASE 1 - Inventory + Resource Surface
Produce:
- repository inventory grouped by namespace, workload family, overlay, or platform area as evidenced
- one-line purpose for each manifest set, patch chain, policy object, and operational asset
- resource inventory covering workloads, services, ingress, config, secrets references, RBAC, policy, and storage objects
- deployment and rendering surface summary: Kustomize, Helm output, raw manifests, generators, validation scripts, or CI hooks where evidenced
- totals and `UNREVIEWED/INACCESSIBLE`

### PHASE 2 - Resource Accounting
Produce exactly:
- `resource_index.csv`
- `workload_index.csv`

Rules:
- include one row per resource object, including RBAC, policy, config, and networking resources
- include one row per workload or controller boundary with ownership and rollout-critical notes
- chunk outputs to 500 rows max per file part
- leave ownership or runtime fields blank when precision is not supportable and note `INFERENCE`

### PHASE 3 - Workload Boundaries + Deployment Safety
Using phase 1 and 2 evidence:
- describe platform architecture as implemented
- map namespace, overlay, service, and controller ownership boundaries
- assess rollout safety: selectors, replica strategy, disruption budgets, probes, autoscaling, storage semantics, and immutable field risk
- assess API hygiene: deprecated versions, patch layering, controller ownership, and drift risk
- identify where operational behavior depends on external or missing evidence

### PHASE 4 - Security + Operability Findings
Review:
- service accounts, RBAC scope, pod security context, container privileges, image sourcing, and network exposure
- logs, metrics hooks, health endpoints, graceful shutdown, and failure isolation where evidenced
- policy conformance and manifest-level guardrails where present

Output findings grouped by `P0`, `P1`, and `P2`, each with:
- file path
- resource name or workload boundary
- evidence
- concrete fix

### PHASE 5 - Synthesis
Produce:
- overall grade `A-F`
- subgrades for boundary design, security, operability, deployment safety, API hygiene, and docs/DX
- anchored justification
- prioritized recommendations with `P0`, `P1`, and `P2`
- effort sizing `S`, `M`, `L`

## Completion Rule
An audit response is incomplete if it:
- mixes phases
- makes unsupported claims
- omits required artifacts
- grades before synthesis
- recommends fixes before the proper phase
- omits the continuation footer

## Invocation Template
Use this skill with a prompt that supplies repository-specific context. Example:

```text
Use Kubernetes Audit Deep Dive.
Audit /path/to/manifests.
Execute PHASE 4 - Security + Operability Findings.
Focus on RBAC scope, rollout safety, and missing health or metrics signals.
Treat rendered manifests as the source of truth when overlays compose them.
```
