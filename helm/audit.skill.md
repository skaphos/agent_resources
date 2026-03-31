<!-- SPDX-FileCopyrightText: 2026 Skaphos -->
<!-- SPDX-License-Identifier: MIT -->

<!-- version: 0.1.0 -->
# Helm Audit Deep Dive

## Purpose
Use this skill for a phased, evidence-based audit of Helm charts and chart repositories. Focus on chart structure, values surface, template safety, release ergonomics, upgrade risk, and operational clarity.

## When To Use
- Deep chart audits
- Release safety reviews
- Values sprawl or helper-template complexity reviews
- Security and operability assessment for Helm-packaged workloads

## Audit Priorities
- Inventory chart boundaries: parent charts, subcharts, dependencies, helpers, hooks, CRDs, and values files.
- Identify unstable selectors, names, labels, immutable field risk, and hook side effects.
- Review values hygiene: duplicate knobs, undocumented keys, weak defaults, and breaking surface changes.
- Review security-sensitive output: RBAC, service accounts, secrets handling, pod security context, and network exposure.
- Review release workflow assumptions: install vs. upgrade behavior, dependency pinning, and rollback feasibility.

## Phase Discipline
- Inventory before recommendations.
- Findings before remediation plans.
- Separate templating correctness from workload correctness; note where a problem belongs.

## Output Expectations
- Anchor claims to chart paths, template names, and value keys.
- Mark uncertain runtime behavior as `INFERENCE`.
- End with the exact next phase or follow-up artifact needed.
