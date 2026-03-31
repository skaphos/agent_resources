<!-- SPDX-FileCopyrightText: 2026 Skaphos -->
<!-- SPDX-License-Identifier: MIT -->

<!-- version: 0.1.0 -->
# Helm Test Strategy And Generation

## Purpose
Use this skill when designing validation and test strategy for Helm charts. Focus on linting, rendering, schema validation, manifest assertions, and release regression coverage.

## Test Layers
- `helm lint` for static chart validation
- `helm template` with representative values for render-time regression checks
- Schema validation for values when `values.schema.json` is present or needed
- Manifest assertions with chart-testing, snapshot tests, or policy checks
- Optional install tests for hooks and live-cluster behavior when static checks are insufficient

## Guidance
- Test the values surface that users actually exercise: defaults, minimum valid config, and one or two realistic environment overrides.
- Prioritize selectors, names, labels, ports, probes, resources, affinity, tolerations, RBAC, and secret wiring.
- Treat CRDs, hooks, and stateful resources as upgrade-risk areas requiring explicit coverage.
- Prefer deterministic rendered-manifest checks before live-cluster tests.

## Completion Criteria
- The changed chart has at least one concrete verification path.
- Breaking values or rendered-manifest changes are called out explicitly.
