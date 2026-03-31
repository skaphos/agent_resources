<!-- SPDX-FileCopyrightText: 2026 Skaphos -->
<!-- SPDX-License-Identifier: MIT -->

<!-- version: 0.1.0 -->
# Kubernetes Documentation Guidance

## Purpose
Use this skill when documenting Kubernetes resources, deployment flows, operational runbooks, or platform conventions.

## Scope
- Workload and service READMEs
- Overlay usage and environment documentation
- Deployment, rollback, and incident runbooks
- API or controller migration notes

## Rules
- Document what is actually deployed: kinds, namespaces, controllers, ingress paths, config dependencies, and operational expectations.
- Keep examples executable, such as `kubectl apply -k overlays/prod`.
- Explain rollout and rollback behavior where it matters.
- Do not document secrets content; document secret contracts and sourcing instead.
