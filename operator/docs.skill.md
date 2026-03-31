<!-- SPDX-FileCopyrightText: 2026 Skaphos -->
<!-- SPDX-License-Identifier: MIT -->

<!-- version: 0.1.0 -->
# Kubernetes Operator Documentation Guidance

## Purpose
Use this skill when documenting Kubernetes operator behavior, CRD contracts, reconciliation semantics, operational procedures, or upgrade guidance.

## Scope
- CRD and API documentation
- controller behavior and ownership documentation
- install, upgrade, and rollback guides
- troubleshooting and operational runbooks
- webhook and status semantics documentation

## Rules
- Document the API as users experience it: required fields, defaults, status, conditions, and lifecycle semantics.
- Explain what the controller owns, what it watches, and what side effects it produces.
- Keep examples grounded in actual CRD fields and real reconciliation behavior.
- Treat generated CRDs and manifests as artifacts to explain, not as the only source of documentation.
