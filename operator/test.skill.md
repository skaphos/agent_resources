<!-- SPDX-FileCopyrightText: 2026 Skaphos -->
<!-- SPDX-License-Identifier: MIT -->

<!-- version: 0.1.0 -->
# Kubernetes Operator Test Strategy And Generation

## Purpose
Use this skill when designing or writing tests for Kubernetes operators built in Go.

Apply this skill with `go/policy.skill.md`, `go/workflow.skill.md`, and `go/test.skill.md` for base Go testing standards.

## Test Layers
- pure Go unit tests for helpers, predicates, mapping functions, and condition logic
- focused reconciler tests for branching, retries, and error handling
- `envtest` for API server backed reconciliation behavior
- webhook tests for validation and defaulting
- generation checks for CRDs and manifests when code generation is part of the repo

## Guidance
- Prioritize reconciliation invariants: idempotency, ownership, finalizers, status updates, and event ordering resilience.
- Test status and conditions as part of the contract, not as incidental output.
- Prefer deterministic fake-client tests only for narrow logic; use `envtest` when API-server semantics matter.
- Cover deletion paths, not-found paths, partial creation, and requeue-after-error behavior.
- Treat CRD version changes and webhooks as high-risk areas requiring explicit coverage.
