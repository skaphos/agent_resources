<!-- SPDX-FileCopyrightText: 2026 Skaphos -->
<!-- SPDX-License-Identifier: MIT -->

<!-- version: 0.1.0 -->
# Helm Documentation Guidance

## Purpose
Use this skill when writing or updating Helm chart documentation: chart READMEs, values references, upgrade notes, operator runbooks, and release guidance.

## Scope
- `README.md` for chart purpose, install flow, and examples
- `values.yaml` reference tables and override examples
- Upgrade and rollback notes for breaking values or resource changes
- Runbooks for rendering, linting, packaging, and release troubleshooting

## Rules
- Treat `values.yaml` as a public contract; document keys that users are expected to set.
- Keep examples realistic and minimal.
- Document defaults, required values, and compatibility caveats explicitly.
- Ground every statement in actual chart behavior. Do not invent flags, hooks, or values.

## Minimum Deliverables
- What the chart deploys
- Required values and important optional values
- Example `helm install` or `helm upgrade` commands
- Upgrade considerations for users carrying existing releases
