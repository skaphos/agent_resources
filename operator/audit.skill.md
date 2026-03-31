<!-- SPDX-FileCopyrightText: 2026 Skaphos -->
<!-- SPDX-License-Identifier: MIT -->

<!-- version: 0.1.0 -->
# Kubernetes Operator Audit Deep Dive

## Purpose
Use this skill for a phased, evidence-based audit of a Kubernetes operator codebase. This skill overlays Go audit discipline with controller-specific concerns.

## When To Use
- Deep operator audits
- Reconciler correctness and lifecycle reviews
- CRD, webhook, or status model reviews
- Operability and upgrade-safety assessment for controllers

## Audit Priorities
- Inventory APIs, versions, controllers, watches, predicates, webhooks, and generated artifacts.
- Review reconciliation flow for idempotency, ownership, retry behavior, and side-effect control.
- Review status and conditions for truthfulness, freshness, and operator usability.
- Review deletion behavior: finalizers, cleanup ordering, and stuck-resource risk.
- Review operational concerns: leader election, concurrency, rate limiting, metrics, events, and log quality.
- Review upgrade safety: CRD evolution, defaulting, conversion, and backwards compatibility.

## Output Rules
- Anchor claims to types, reconcilers, tests, and generated artifacts.
- Mark uncertain runtime behavior as `INFERENCE`.
- Separate generic Go issues from controller-specific design issues.
